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
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="2d178-103">Esempio 2 – applicazioni tooprotect una rete Perimetrale con un Firewall e NSGs</span><span class="sxs-lookup"><span data-stu-id="2d178-103">Example 2 – Build a DMZ tooprotect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="2d178-104">[Restituire la pagina sicurezza limite Best Practices toohello][HOME]</span><span class="sxs-lookup"><span data-stu-id="2d178-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="2d178-105">Questo esempio illustra come creare una rete perimetrale con un firewall, quattro server Windows e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="2d178-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="2d178-106">Ogni tooprovide comandi rilevanti hello in modo dettagliato anche una comprensione più approfondita di ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="2d178-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="2d178-107">È inoltre disponibile un Scenario di traffico sezione tooprovide un'analisi approfondita dettagliate come traffico procede attraverso i livelli di difesa hello hello rete Perimetrale.</span><span class="sxs-lookup"><span data-stu-id="2d178-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="2d178-108">Infine, nella sezione dei riferimenti hello è codice completo hello e istruzione toobuild questo ambiente tootest e sperimentare vari scenari.</span><span class="sxs-lookup"><span data-stu-id="2d178-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="2d178-109">![Rete Perimetrale in ingresso con NVA e gruppo][1]</span><span class="sxs-lookup"><span data-stu-id="2d178-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="2d178-110">Descrizione dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="2d178-110">Environment Description</span></span>
<span data-ttu-id="2d178-111">In questo esempio è associata una sottoscrizione che contiene la seguente sintassi hello:</span><span class="sxs-lookup"><span data-stu-id="2d178-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="2d178-112">Due servizi cloud, "FrontEnd001" e "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="2d178-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="2d178-113">Una rete virtuale, "CorpNetwork", con due subnet: "FrontEnd" e "BackEnd"</span><span class="sxs-lookup"><span data-stu-id="2d178-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="2d178-114">Un unico gruppo di sicurezza di rete che viene applicato tooboth subnet</span><span class="sxs-lookup"><span data-stu-id="2d178-114">A single Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="2d178-115">Un accessorio virtuale di rete, in questo esempio un Firewall, NextGen Barracuda connesso subnet front-end toohello</span><span class="sxs-lookup"><span data-stu-id="2d178-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected toohello Frontend subnet</span></span>
* <span data-ttu-id="2d178-116">Un server Windows che rappresenta un server Web applicazioni ("IIS01").</span><span class="sxs-lookup"><span data-stu-id="2d178-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="2d178-117">Due server Windows che rappresentano server back-end applicazioni ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="2d178-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="2d178-118">Un server Windows che rappresenta un server DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="2d178-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="2d178-119">Sebbene questo esempio viene utilizzato un NextGen Firewall Barracuda, molti dei diversi dispositivi virtuali di rete può essere usati per questo esempio hello.</span><span class="sxs-lookup"><span data-stu-id="2d178-119">Although this example uses a Barracuda NextGen Firewall, many of hello different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="2d178-120">Nella sezione dei riferimenti hello sotto è uno script di PowerShell che compilerà la maggior parte dell'ambiente hello descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2d178-120">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="2d178-121">Macchine virtuali hello di compilazione e le reti virtuali, anche se vengono eseguite dallo script di esempio hello, non sono descritti in dettaglio in questo documento.</span><span class="sxs-lookup"><span data-stu-id="2d178-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="2d178-122">ambiente di hello toobuild:</span><span class="sxs-lookup"><span data-stu-id="2d178-122">toobuild hello environment:</span></span>

1. <span data-ttu-id="2d178-123">Salvare file xml configurazione rete hello inclusi nella sezione dei riferimenti hello (aggiornata con i nomi, la posizione e scenario hello dato toomatch di indirizzi IP)</span><span class="sxs-lookup"><span data-stu-id="2d178-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="2d178-124">Le variabili utente di aggiornamento hello nello script di hello script toomatch hello ambiente hello è toobe eseguite (sottoscrizioni, nomi di servizio e così via)</span><span class="sxs-lookup"><span data-stu-id="2d178-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="2d178-125">Eseguire script hello in PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d178-125">Execute hello script in PowerShell</span></span>

<span data-ttu-id="2d178-126">**Nota**: area hello indicato nell'hello script di PowerShell deve corrispondere area hello indicato nel file xml di configurazione rete hello.</span><span class="sxs-lookup"><span data-stu-id="2d178-126">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="2d178-127">Una volta hello script viene eseguito correttamente può essere prelevato hello post-script come segue:</span><span class="sxs-lookup"><span data-stu-id="2d178-127">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="2d178-128">Impostare le regole firewall hello, questa attività viene descritta in hello sezione seguente: le regole del Firewall.</span><span class="sxs-lookup"><span data-stu-id="2d178-128">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="2d178-129">Facoltativamente, nella sezione dei riferimenti hello sono due script tooset hello web server e il server di app con un tooallow di applicazione web semplice test con questa configurazione di rete Perimetrale.</span><span class="sxs-lookup"><span data-stu-id="2d178-129">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="2d178-130">la sezione successiva di Hello spiega la maggior parte delle hello script istruzioni relativo tooNetwork gruppi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2d178-130">hello next section explains most of hello scripts statements relative tooNetwork Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="2d178-131">Gruppi di sicurezza di rete (NGS)</span><span class="sxs-lookup"><span data-stu-id="2d178-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="2d178-132">Per questo esempio viene creato un gruppo di sicurezza di rete, in cui vengono poi caricate sei regole.</span><span class="sxs-lookup"><span data-stu-id="2d178-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="2d178-133">In genere, si deve creare regole "Consenti" specifiche prima e quindi hello ultima più generico "Deny" regole.</span><span class="sxs-lookup"><span data-stu-id="2d178-133">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="2d178-134">Hello assegnata la priorità determina quali regole vengono valutate per prime.</span><span class="sxs-lookup"><span data-stu-id="2d178-134">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="2d178-135">Una volta traffico trovato tooapply tooa specifica regola, non vengono valutate altre regole.</span><span class="sxs-lookup"><span data-stu-id="2d178-135">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="2d178-136">Possono essere applicate regole di gruppo in hello nella direzione in ingresso o in uscita (dalla prospettiva di hello della subnet hello).</span><span class="sxs-lookup"><span data-stu-id="2d178-136">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="2d178-137">In modo dichiarativo, hello segue le regole è compilato per il traffico in ingresso:</span><span class="sxs-lookup"><span data-stu-id="2d178-137">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="2d178-138">Il traffico DNS interno (porta 53) è consentito.</span><span class="sxs-lookup"><span data-stu-id="2d178-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="2d178-139">È consentito il traffico RDP (porta 3389) da hello Internet tooany VM</span><span class="sxs-lookup"><span data-stu-id="2d178-139">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="2d178-140">È consentito il traffico HTTP (porta 80) da hello Internet toohello NVA (firewall)</span><span class="sxs-lookup"><span data-stu-id="2d178-140">HTTP traffic (port 80) from hello Internet toohello NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="2d178-141">È consentito qualsiasi tipo di traffico (tutte le porte) da IIS01 tooAppVM1</span><span class="sxs-lookup"><span data-stu-id="2d178-141">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="2d178-142">Qualsiasi tipo di traffico (tutte le porte) da hello Internet toohello viene negato l'intera rete virtuale (entrambi subnet)</span><span class="sxs-lookup"><span data-stu-id="2d178-142">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="2d178-143">Qualsiasi tipo di traffico (tutte le porte) dalla subnet di back-end toohello subnet front-end hello negato</span><span class="sxs-lookup"><span data-stu-id="2d178-143">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="2d178-144">Con queste subnet associata tooeach regole, se una richiesta HTTP in ingresso dal server web toohello Internet hello entrambi regole 3 (Consenti) e 5 (Nega) verrà applicata, ma poiché la regola 3 ha una priorità più alta solo esso viene applicato e regola 5 sarebbe non entrano in gioco.</span><span class="sxs-lookup"><span data-stu-id="2d178-144">With these rules bound tooeach subnet, if a HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="2d178-145">In questo modo la richiesta HTTP hello sia possibile usare toohello firewall.</span><span class="sxs-lookup"><span data-stu-id="2d178-145">Thus hello HTTP request would be allowed toohello firewall.</span></span> <span data-ttu-id="2d178-146">Se il traffico stesso cercava server DNS01 di hello tooreach, regola 5 (Nega) sarebbe hello prima tooapply hello il traffico e non sarebbe consentito toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="2d178-146">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="2d178-147">Regola 6 (Nega) blocchi hello subnet front-end dalla conversazione toohello subnet di back-end (ad eccezione di traffico consentito nelle regole 1 e 4), consente di proteggere rete back-end hello nel caso in cui un'utente malintenzionato compromette hello applicazione web sul front-end hello autore dell'attacco hello avrebbe accesso limitato toohello back-end "protetto" rete (solo tooresources esposte nel server AppVM01 hello).</span><span class="sxs-lookup"><span data-stu-id="2d178-147">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="2d178-148">Una regola in uscita predefinito che consente il traffico in uscita toohello internet.</span><span class="sxs-lookup"><span data-stu-id="2d178-148">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="2d178-149">Per questo esempio si consente il traffico in uscita e non si modificano le regole in uscita.</span><span class="sxs-lookup"><span data-stu-id="2d178-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="2d178-150">toolock verso il basso il traffico in entrambe le direzioni, Routing definito dall'utente è obbligatorio, questo viene esaminato in un esempio di diversi che è possibile trovare in hello [documento limite di sicurezza principale][HOME].</span><span class="sxs-lookup"><span data-stu-id="2d178-150">toolock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in hello [main security boundary document][HOME].</span></span>

<span data-ttu-id="2d178-151">Hello sopra descritto NSG le regole sono molto simili toohello NSG in [esempio 1: creare una rete Perimetrale semplice con NSGs][Example1].</span><span class="sxs-lookup"><span data-stu-id="2d178-151">hello above discussed NSG rules are very similar toohello NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="2d178-152">Esaminare hello NSG descrizione in tale documento per ogni regola di gruppo e gli attributi di un'analisi approfondita.</span><span class="sxs-lookup"><span data-stu-id="2d178-152">Please review hello NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="2d178-153">Regole del firewall</span><span class="sxs-lookup"><span data-stu-id="2d178-153">Firewall Rules</span></span>
<span data-ttu-id="2d178-154">Un client di gestione sarà necessario toobe installato su un firewall di hello toomanage PC e creare configurazioni di hello necessarie.</span><span class="sxs-lookup"><span data-stu-id="2d178-154">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="2d178-155">Vedere fornitore documentazione fornita dal firewall (o altri NVA) hello in modo toomanage hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2d178-155">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="2d178-156">resto Hello di questa sezione descrivono la configurazione hello di firewall hello stesso, tramite il client Gestione fornitori hello (ossia, non hello portale di Azure o PowerShell).</span><span class="sxs-lookup"><span data-stu-id="2d178-156">hello remainder of this section will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="2d178-157">Istruzioni per il download di client e connessione toohello Barracuda utilizzato in questo esempio sono disponibili qui: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="2d178-157">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="2d178-158">Regole di inoltro sul firewall hello, saranno necessario toobe creato.</span><span class="sxs-lookup"><span data-stu-id="2d178-158">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="2d178-159">Poiché in questo esempio viene distribuito solo il traffico in entrata toohello firewall internet, quindi toohello web server, è necessario solo un inoltro regola NAT.</span><span class="sxs-lookup"><span data-stu-id="2d178-159">Since this example only routes internet traffic in-bound toohello firewall and then toohello web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="2d178-160">In hello Barracuda NextGen Firewall utilizzato in hello in questo esempio regola sarebbe un NAT di destinazione della regola toopass ("ora legale NAT") il traffico.</span><span class="sxs-lookup"><span data-stu-id="2d178-160">On hello Barracuda NextGen Firewall used in this example hello rule would be a Destination NAT rule (“Dst NAT”) toopass this traffic.</span></span>

<span data-ttu-id="2d178-161">seguente hello toocreate regola (o verificare le regole predefinite esistente), a partire dal dashboard di hello Barracuda NG amministratore client, passare scheda Configurazione toohello, hello configurazione operativa sezione selezionare il set di regole.</span><span class="sxs-lookup"><span data-stu-id="2d178-161">toocreate hello following rule (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="2d178-162">Chiamata di una griglia, "Main regole" mostrerà hello regole attive e disattivate il firewall hello esistente.</span><span class="sxs-lookup"><span data-stu-id="2d178-162">A grid called, “Main Rules” will show hello existing active and deactivated rules on hello firewall.</span></span> <span data-ttu-id="2d178-163">In hello angolo superiore destro di questa griglia è una piccola verde "+" fare clic su questo toocreate una nuova regola (Nota: il firewall può essere "bloccato" per le modifiche, se viene visualizzato un pulsante contrassegnato come "Blocco" e toocreate Impossibile o modificare le regole, fare clic su questo pulsante troppo "sbloccare" hello set di regole e consentire la modifica).</span><span class="sxs-lookup"><span data-stu-id="2d178-163">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello ruleset and allow editing).</span></span> <span data-ttu-id="2d178-164">Se si desidera tooedit una regola esistente, selezionare la regola, fare doppio clic su e scegliere Modifica regola.</span><span class="sxs-lookup"><span data-stu-id="2d178-164">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="2d178-165">Creare una nuova regola e specificare un nome, ad esempio "WebTraffic".</span><span class="sxs-lookup"><span data-stu-id="2d178-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="2d178-166">icona della regola NAT destinazione Hello è simile al seguente: ![icona NAT di destinazione][2]</span><span class="sxs-lookup"><span data-stu-id="2d178-166">hello Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="2d178-167">regola di Hello stessa avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2d178-167">hello rule itself would look something like this:</span></span>

<span data-ttu-id="2d178-168">![Regola del firewall][3]</span><span class="sxs-lookup"><span data-stu-id="2d178-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="2d178-169">Qui qualsiasi indirizzo in ingresso che riscontri hello Firewall tooreach HTTP (porta 80 o 443 per HTTPS) durante il tentativo verrà inviato hello interfaccia "IP locale DHCP1" e toohello reindirizzato il Server Web con indirizzo IP del 10.0.1.5 hello del Firewall.</span><span class="sxs-lookup"><span data-stu-id="2d178-169">Here any inbound address that hits hello Firewall trying tooreach HTTP (port 80 or 443 for HTTPS) will be sent out hello Firewall’s “DHCP1 Local IP” interface and redirected toohello Web Server with hello IP Address of 10.0.1.5.</span></span> <span data-ttu-id="2d178-170">Poiché hello traffico in ingresso sulla porta 80 e server web di toohello corso sulla porta 80 è necessario apportare alcuna modifica porta.</span><span class="sxs-lookup"><span data-stu-id="2d178-170">Since hello traffic is coming in on port 80 and going toohello web server on port 80 no port change was needed.</span></span> <span data-ttu-id="2d178-171">Tuttavia, hello elenco destinazione avrebbe potuto essere 10.0.1.5:8080 se il Server Web resta in attesa su una porta 8080 in questo modo la traduzione hello in ingresso porta 80 in hello firewall tooinbound porta 8080 hello web server.</span><span class="sxs-lookup"><span data-stu-id="2d178-171">However, hello Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating hello inbound port 80 on hello firewall tooinbound port 8080 on hello web server.</span></span>

<span data-ttu-id="2d178-172">Un metodo di connessione devono anche essere indicato, per hello regola di destinazione da Internet, hello "SNAT dinamici" è più appropriato.</span><span class="sxs-lookup"><span data-stu-id="2d178-172">A Connection Method should also be signified, for hello Destination Rule from hello Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="2d178-173">Anche se è stata creata una sola regola, è importante impostarne la priorità correttamente.</span><span class="sxs-lookup"><span data-stu-id="2d178-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="2d178-174">Se nella griglia hello di tutte le regole firewall hello che è la nuova regola nella parte inferiore di hello (sotto regola "BLOCKALL" hello) non verrà mai entrano in gioco.</span><span class="sxs-lookup"><span data-stu-id="2d178-174">If in hello grid of all rules on hello firewall this new rule is on hello bottom (below hello "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="2d178-175">Verificare la regola hello appena creato per il traffico web sia superiore regola BLOCKALL hello.</span><span class="sxs-lookup"><span data-stu-id="2d178-175">Ensure hello newly created rule for web traffic is above hello BLOCKALL rule.</span></span>

<span data-ttu-id="2d178-176">Dopo aver creata la regola hello, deve essere inserito toohello firewall e quindi attivato, se ciò non avviene regola hello modifica non avrà alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="2d178-176">Once hello rule is created, it must be pushed toohello firewall and then activated, if this is not done hello rule change will not take effect.</span></span> <span data-ttu-id="2d178-177">il processo di attivazione e push Hello è descritto nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="2d178-177">hello push and activation process is described in hello next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="2d178-178">Attivazione delle regole</span><span class="sxs-lookup"><span data-stu-id="2d178-178">Rule Activation</span></span>
<span data-ttu-id="2d178-179">Con hello ruleset modificato tooadd questa regola, hello ruleset deve essere caricato toohello firewall e attivato.</span><span class="sxs-lookup"><span data-stu-id="2d178-179">With hello ruleset modified tooadd this rule, hello ruleset must be uploaded toohello firewall and activated.</span></span>

<span data-ttu-id="2d178-180">![Attivazione delle regole firewall][4]</span><span class="sxs-lookup"><span data-stu-id="2d178-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="2d178-181">Nell'angolo superiore destra hello del client di gestione di hello sono un cluster di pulsanti.</span><span class="sxs-lookup"><span data-stu-id="2d178-181">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="2d178-182">Fare clic su hello "inviare modifiche" pulsante toosend hello modificato regole toohello firewall, quindi fare clic sul pulsante "Attiva" hello.</span><span class="sxs-lookup"><span data-stu-id="2d178-182">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="2d178-183">Con l'attivazione del set di regole firewall hello hello è stata completata la compilazione di ambiente di esempio.</span><span class="sxs-lookup"><span data-stu-id="2d178-183">With hello activation of hello firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="2d178-184">Facoltativamente, gli script di compilazione post hello in hello sezione può essere riferimenti esegue tooadd un'applicazione toothis ambiente tootest hello scenari di traffico seguenti.</span><span class="sxs-lookup"><span data-stu-id="2d178-184">Optionally, hello post build scripts in hello References section can be run tooadd an application toothis environment tootest hello below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d178-185">È toorealize critico che non verrà raggiunto di direttamente server web hello.</span><span class="sxs-lookup"><span data-stu-id="2d178-185">It is critical toorealize that you will not hit hello web server directly.</span></span> <span data-ttu-id="2d178-186">Quando un browser richiede una pagina HTTP da FrontEnd001.CloudApp.Net, passa di endpoint (porta 80) HTTP hello questo firewall toohello traffico non hello web server.</span><span class="sxs-lookup"><span data-stu-id="2d178-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, hello HTTP endpoint (port 80) passes this traffic toohello firewall not hello web server.</span></span> <span data-ttu-id="2d178-187">Hello firewall, quindi in base a regole toohello creato in precedenza, NAT che richiedono toohello Server Web.</span><span class="sxs-lookup"><span data-stu-id="2d178-187">hello firewall then, according toohello rule created above, NATs that request toohello Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="2d178-188">Scenari di traffico</span><span class="sxs-lookup"><span data-stu-id="2d178-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-tooweb-server-through-firewall"></a><span data-ttu-id="2d178-189">(Consentito) TooWeb Web Server con Firewall</span><span class="sxs-lookup"><span data-stu-id="2d178-189">(Allowed) Web tooWeb Server through Firewall</span></span>
1. <span data-ttu-id="2d178-190">L'utente Internet richiede una pagina HTTP a FrontEnd001.CloudApp.Net (servizio cloud per Internet).</span><span class="sxs-lookup"><span data-stu-id="2d178-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="2d178-191">Traffico passa del servizio cloud tramite endpoint aperto sull'interfaccia locale di toofirewall la porta 80 in 10.0.1.4:80</span><span class="sxs-lookup"><span data-stu-id="2d178-191">Cloud service passes traffic through open endpoint on port 80 toofirewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="2d178-192">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="2d178-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2d178-193">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="2d178-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="2d178-194">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="2d178-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="2d178-195">Applicare NSG regola 3 (tooFirewall Internet), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="2d178-195">NSG Rule 3 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="2d178-196">Traffico raggiunge l'indirizzo IP interno del firewall hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="2d178-196">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="2d178-197">Regola di inoltro di firewall vedere questa operazione è traffico sulla porta 80, lo reindirizza il server web toohello IIS01</span><span class="sxs-lookup"><span data-stu-id="2d178-197">Firewall forwarding rule see this is port 80 traffic, redirects it toohello web server IIS01</span></span>
6. <span data-ttu-id="2d178-198">Iis01 è in ascolto per il traffico web, riceve la richiesta e avvia l'elaborazione richiesta hello</span><span class="sxs-lookup"><span data-stu-id="2d178-198">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
7. <span data-ttu-id="2d178-199">Iis01 richiede SQL Server hello su AppVM01 per informazioni</span><span class="sxs-lookup"><span data-stu-id="2d178-199">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="2d178-200">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="2d178-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="2d178-201">subnet di back-end Hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="2d178-201">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2d178-202">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="2d178-202">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="2d178-203">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="2d178-203">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="2d178-204">GRUPPO regola 3 (tooFirewall Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="2d178-204">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="2d178-205">Applicare la regola gruppo 4 (IIS01 tooAppVM01), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="2d178-205">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="2d178-206">AppVM01 riceve hello Query SQL e risponde</span><span class="sxs-lookup"><span data-stu-id="2d178-206">AppVM01 receives hello SQL Query and responds</span></span>
11. <span data-ttu-id="2d178-207">Poiché esistono non è consentito alcun regole in uscita su hello risposta hello subnet di back-end</span><span class="sxs-lookup"><span data-stu-id="2d178-207">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
12. <span data-ttu-id="2d178-208">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="2d178-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="2d178-209">Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile</span><span class="sxs-lookup"><span data-stu-id="2d178-209">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="2d178-210">regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="2d178-210">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
13. <span data-ttu-id="2d178-211">server IIS Hello riceve risposta SQL hello e completa di risposta HTTP hello e invia toohello richiedente</span><span class="sxs-lookup"><span data-stu-id="2d178-211">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
14. <span data-ttu-id="2d178-212">Poiché si tratta di una sessione NAT dal firewall hello, destinazione risposta hello è (inizialmente) per hello Firewall</span><span class="sxs-lookup"><span data-stu-id="2d178-212">Since this is a NAT session from hello firewall, hello response destination (initially) is for hello Firewall</span></span>
15. <span data-ttu-id="2d178-213">firewall Hello riceve hello risposta dal Server Web hello e inoltra toohello indietro utente Internet</span><span class="sxs-lookup"><span data-stu-id="2d178-213">hello firewall receives hello response from hello Web Server and forwards back toohello Internet User</span></span>
16. <span data-ttu-id="2d178-214">Poiché esistono non è consentito alcun regole in uscita su hello risposta hello di subnet front-end e hello utente Internet riceve hello web pagina richiesta.</span><span class="sxs-lookup"><span data-stu-id="2d178-214">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="2d178-215">(Consentito) TooBackend RDP</span><span class="sxs-lookup"><span data-stu-id="2d178-215">(Allowed) RDP tooBackend</span></span>
1. <span data-ttu-id="2d178-216">Amministratore del server su internet richiede tooAppVM01 sessione RDP in BackEnd001.CloudApp.Net:xxxxx dove xxxxx è il numero di porta hello assegnato in modo casuale per RDP tooAppVM01 (porta hello assegnato è reperibile nel portale di Azure hello o tramite PowerShell)</span><span class="sxs-lookup"><span data-stu-id="2d178-216">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="2d178-217">Poiché hello che firewall è in ascolto solo hello indirizzo FrontEnd001.CloudApp.Net, non è coinvolta con questo flusso di traffico</span><span class="sxs-lookup"><span data-stu-id="2d178-217">Since hello Firewall is only listening on hello FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="2d178-218">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="2d178-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2d178-219">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="2d178-219">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="2d178-220">Regola gruppo di sicurezza di rete 2 (RDP) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="2d178-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="2d178-221">Senza regole in uscita, sono applicabili le regole predefinite e il traffico restituito è consentito.</span><span class="sxs-lookup"><span data-stu-id="2d178-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="2d178-222">La sessione RDP è abilitata.</span><span class="sxs-lookup"><span data-stu-id="2d178-222">RDP session is enabled</span></span>
6. <span data-ttu-id="2d178-223">AppVM01 richiede il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="2d178-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="2d178-224">(Consentito) Ricerca DNS del server Web sul server DNS</span><span class="sxs-lookup"><span data-stu-id="2d178-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="2d178-225">Web Server, IIS01, necessita di un feed di dati in www.data.gov, ma è necessario tooresolve hello indirizzo.</span><span class="sxs-lookup"><span data-stu-id="2d178-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="2d178-226">Hello configurazione di rete per gli elenchi di rete virtuale hello DNS01 (10.0.2.4 nella subnet back-end hello) come server DNS primario hello, IIS01 invia hello DNS richiesta tooDNS01</span><span class="sxs-lookup"><span data-stu-id="2d178-226">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="2d178-227">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="2d178-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="2d178-228">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="2d178-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2d178-229">Regola gruppo di sicurezza di rete 1 (DNS) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="2d178-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="2d178-230">Server DNS riceve una richiesta di hello</span><span class="sxs-lookup"><span data-stu-id="2d178-230">DNS server receives hello request</span></span>
6. <span data-ttu-id="2d178-231">Server DNS non dispone di indirizzo hello memorizzati nella cache e richiede un server radice DNS su hello internet</span><span class="sxs-lookup"><span data-stu-id="2d178-231">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="2d178-232">Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="2d178-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="2d178-233">Server DNS Internet risponde, poiché questa sessione è stata avviata internamente, la risposta hello è consentita</span><span class="sxs-lookup"><span data-stu-id="2d178-233">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="2d178-234">Server DNS memorizza nella cache la risposta hello e risponde toohello richiesta iniziale indietro tooIIS01</span><span class="sxs-lookup"><span data-stu-id="2d178-234">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="2d178-235">Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="2d178-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="2d178-236">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="2d178-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="2d178-237">Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile</span><span class="sxs-lookup"><span data-stu-id="2d178-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="2d178-238">regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito</span><span class="sxs-lookup"><span data-stu-id="2d178-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="2d178-239">Iis01 riceve risposta hello da DNS01</span><span class="sxs-lookup"><span data-stu-id="2d178-239">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="2d178-240">(Consentito) Il server Web richiede l'accesso a un file su AppVM01</span><span class="sxs-lookup"><span data-stu-id="2d178-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="2d178-241">IIS01 richiede un file su AppVM01.</span><span class="sxs-lookup"><span data-stu-id="2d178-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="2d178-242">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="2d178-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="2d178-243">subnet di back-end Hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="2d178-243">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2d178-244">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="2d178-244">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="2d178-245">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="2d178-245">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="2d178-246">GRUPPO regola 3 (tooFirewall Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="2d178-246">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="2d178-247">Applicare la regola gruppo 4 (IIS01 tooAppVM01), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="2d178-247">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="2d178-248">AppVM01 riceve la richiesta di hello e risponde con il file (presupponendo che l'accesso è autorizzato)</span><span class="sxs-lookup"><span data-stu-id="2d178-248">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="2d178-249">Poiché esistono non è consentito alcun regole in uscita su hello risposta hello subnet di back-end</span><span class="sxs-lookup"><span data-stu-id="2d178-249">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
6. <span data-ttu-id="2d178-250">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="2d178-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2d178-251">Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile</span><span class="sxs-lookup"><span data-stu-id="2d178-251">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="2d178-252">regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="2d178-252">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="2d178-253">server IIS Hello riceve file hello</span><span class="sxs-lookup"><span data-stu-id="2d178-253">hello IIS server receives hello file</span></span>

#### <a name="denied-web-direct-tooweb-server"></a><span data-ttu-id="2d178-254">(Negato) TooWeb diretto Web Server</span><span class="sxs-lookup"><span data-stu-id="2d178-254">(Denied) Web direct tooWeb Server</span></span>
<span data-ttu-id="2d178-255">Poiché hello Server Web, IIS01 e hello Firewall sono in hello nello stesso servizio Cloud condividono hello stesso indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="2d178-255">Since hello Web Server, IIS01, and hello Firewall are in hello same Cloud Service they share hello same public facing IP address.</span></span> <span data-ttu-id="2d178-256">In questo modo sarebbe possibile indirizzare tutto il traffico HTTP toohello firewall.</span><span class="sxs-lookup"><span data-stu-id="2d178-256">Thus any HTTP traffic would be directed toohello firewall.</span></span> <span data-ttu-id="2d178-257">Mentre la richiesta hello viene fornita correttamente, non è possibile associarla direttamente toohello Server Web, viene passato, come previsto, tramite hello del Firewall prima di tutto.</span><span class="sxs-lookup"><span data-stu-id="2d178-257">While hello request would be successfully served, it cannot go directly toohello Web Server, it passed, as designed, through hello Firewall first.</span></span> <span data-ttu-id="2d178-258">Vedere hello primo Scenario in questa sezione per il flusso del traffico hello.</span><span class="sxs-lookup"><span data-stu-id="2d178-258">See hello first Scenario in this section for hello traffic flow.</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="2d178-259">(Negato) TooBackend Web Server</span><span class="sxs-lookup"><span data-stu-id="2d178-259">(Denied) Web tooBackend Server</span></span>
1. <span data-ttu-id="2d178-260">Utente Internet tenta di un file in AppVM01 tramite hello servizio BackEnd001.CloudApp.Net tooaccess</span><span class="sxs-lookup"><span data-stu-id="2d178-260">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="2d178-261">Poiché non sono presenti endpoint aperto per la condivisione file, questo non raggiungerebbe hello servizio Cloud e non raggiunga il server di hello</span><span class="sxs-lookup"><span data-stu-id="2d178-261">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="2d178-262">Se gli endpoint hello erano aperti per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico</span><span class="sxs-lookup"><span data-stu-id="2d178-262">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="2d178-263">(Negato) Ricerca DNS Web sul server DNS</span><span class="sxs-lookup"><span data-stu-id="2d178-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="2d178-264">Utente Internet tenta un record DNS interno nella DNS01 tramite hello servizio BackEnd001.CloudApp.Net toolookup</span><span class="sxs-lookup"><span data-stu-id="2d178-264">Internet user tries toolookup an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="2d178-265">Poiché non sono presenti endpoint aperto per DNS, questo non raggiungerebbe hello servizio Cloud e non raggiunga il server di hello</span><span class="sxs-lookup"><span data-stu-id="2d178-265">Since there are no endpoints open for DNS, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="2d178-266">Se gli endpoint hello erano aperti per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico (Nota: la regola 1 (DNS) potrebbero non applicarsi per due motivi, primo indirizzo di origine hello è hello internet, questa regola si applica solo a toohello anche rete locale virtuale come hello di origine si tratta di una regola di assenso, non potrebbe negare il traffico mai)</span><span class="sxs-lookup"><span data-stu-id="2d178-266">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="2d178-267">(Negato) Accesso tooSQL Web tramite Firewall</span><span class="sxs-lookup"><span data-stu-id="2d178-267">(Denied) Web tooSQL access through Firewall</span></span>
1. <span data-ttu-id="2d178-268">L'utente Internet richiede dati SQL a FrontEnd001.CloudApp.Net (servizio cloud per Internet).</span><span class="sxs-lookup"><span data-stu-id="2d178-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="2d178-269">Poiché non sono presenti endpoint aperto per SQL, questo non raggiungerebbe hello servizio Cloud e non raggiunga firewall hello</span><span class="sxs-lookup"><span data-stu-id="2d178-269">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="2d178-270">Se gli endpoint sono stati aperti per qualche motivo, subnet front-end hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="2d178-270">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2d178-271">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="2d178-271">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="2d178-272">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="2d178-272">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="2d178-273">Applicare la regola gruppo 2 (tooFirewall Internet), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="2d178-273">NSG Rule 2 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="2d178-274">Traffico raggiunge l'indirizzo IP interno del firewall hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="2d178-274">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="2d178-275">Firewall non dispone di alcuna regola di inoltro per SQL ed Elimina hello traffico</span><span class="sxs-lookup"><span data-stu-id="2d178-275">Firewall has no forwarding rules for SQL and drops hello traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="2d178-276">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="2d178-276">Conclusion</span></span>
<span data-ttu-id="2d178-277">Questo è un modo relativamente semplice di protezione delle applicazioni con un firewall e l'isolamento di subnet di back-end hello dal traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="2d178-277">This is a relatively straight forward way of protecting your application with a firewall and isolating hello back end subnet from inbound traffic.</span></span>

<span data-ttu-id="2d178-278">Altri esempi e una panoramica dei limiti di sicurezza della rete sono disponibili [qui][HOME].</span><span class="sxs-lookup"><span data-stu-id="2d178-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="2d178-279">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="2d178-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="2d178-280">Script principale e configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="2d178-280">Main Script and Network Config</span></span>
<span data-ttu-id="2d178-281">Salvare uno Script completo di hello in un file di script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d178-281">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="2d178-282">Salvare hello configurazione di rete in un file denominato "NetworkConf2.xml".</span><span class="sxs-lookup"><span data-stu-id="2d178-282">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="2d178-283">Modificare le variabili definite dall'utente di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="2d178-283">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="2d178-284">Eseguire script hello, quindi seguire istruzioni di programma di installazione di un regola Firewall di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="2d178-284">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="2d178-285">Script completo</span><span class="sxs-lookup"><span data-stu-id="2d178-285">Full Script</span></span>
<span data-ttu-id="2d178-286">Questo script verrà, in base alle variabili definite dall'utente hello:</span><span class="sxs-lookup"><span data-stu-id="2d178-286">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="2d178-287">Connettersi tooan sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="2d178-287">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="2d178-288">Creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2d178-288">Create a new storage account</span></span>
3. <span data-ttu-id="2d178-289">Creare una nuova rete virtuale e due subnet, come definito nel file di configurazione di rete hello</span><span class="sxs-lookup"><span data-stu-id="2d178-289">Create a new VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="2d178-290">Creare 4 macchine virtuali di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="2d178-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="2d178-291">Configurare il gruppo di sicurezza di rete eseguendo queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="2d178-291">Configure NSG including:</span></span>
   * <span data-ttu-id="2d178-292">Creazione di un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="2d178-292">Creating a NSG</span></span>
   * <span data-ttu-id="2d178-293">Inserimento delle regole.</span><span class="sxs-lookup"><span data-stu-id="2d178-293">Populating it with rules</span></span>
   * <span data-ttu-id="2d178-294">Subnet appropriata toohello associazione hello NSG</span><span class="sxs-lookup"><span data-stu-id="2d178-294">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="2d178-295">Questo script di PowerShell deve essere eseguito localmente in un server o un PC connesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="2d178-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d178-296">Quando si esegue lo script, in PowerShell potrebbero venire visualizzati avvisi o altri messaggi informativi.</span><span class="sxs-lookup"><span data-stu-id="2d178-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="2d178-297">Solo i messaggi di errore formattati in rosso possono indicare un problema.</span><span class="sxs-lookup"><span data-stu-id="2d178-297">Only error messages in red are cause for concern.</span></span>
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


#### <a name="network-config-file"></a><span data-ttu-id="2d178-298">File di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="2d178-298">Network Config File</span></span>
<span data-ttu-id="2d178-299">Salvare il file xml con posizione aggiornata e aggiungere hello collegamento toothis file toohello $NetworkConfigFile variabile nello script hello precedente.</span><span class="sxs-lookup"><span data-stu-id="2d178-299">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="2d178-300">Script di applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="2d178-300">Sample Application Scripts</span></span>
<span data-ttu-id="2d178-301">Se si desidera tooinstall un'applicazione di esempio per questo e altri esempi di rete Perimetrale, ne è stato fornito al collegamento hello: [Script dell'applicazione di esempio][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="2d178-301">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Rete perimetrale in ingresso con gruppo di sicurezza di rete"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Icona di Destination NAT"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Regola del firewall"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Attivazione delle regole firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
