---
title: Guida alla risoluzione dei problemi di DNS di Azure | Documentazione Microsoft
description: Informazioni su come risolvere i problemi comuni di DNS di Azure
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 1d9bb681a864bdc3e5a2f9c9a531d9566b16ada4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="5d68c-103">Guida alla risoluzione dei problemi di DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="5d68c-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="5d68c-104">Questa pagina fornisce informazioni sulla risoluzione dei problemi comuni di DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d68c-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="5d68c-105">Se questi passaggi non consentono di risolvere il problema, è anche possibile eseguire una ricerca o inserire una domanda nel [forum di supporto della community su MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="5d68c-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="5d68c-106">In alternativa, aprire una richiesta di Supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d68c-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="5d68c-107">Non è possibile creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="5d68c-107">I can't create a DNS zone</span></span>

<span data-ttu-id="5d68c-108">Per risolvere i problemi comuni, provare le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d68c-108">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="5d68c-109">Esaminare i log di controllo di DNS di Azure per determinare le cause dell'errore.</span><span class="sxs-lookup"><span data-stu-id="5d68c-109">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="5d68c-110">Ogni nome di zona DNS deve essere univoco all'interno del relativo gruppo di risorse,</span><span class="sxs-lookup"><span data-stu-id="5d68c-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="5d68c-111">ovvero due zone DNS con lo stesso nome non possono condividere uno stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5d68c-111">That is, two DNS zones with the same name cannot share a resource group.</span></span> <span data-ttu-id="5d68c-112">Provare a usare un nome di zona o un gruppo di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="5d68c-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="5d68c-113">Potrebbe essere visualizzato l'errore "È stato raggiunto o superato il numero massimo di zone nella sottoscrizione {ID sottoscrizione}."</span><span class="sxs-lookup"><span data-stu-id="5d68c-113">You may see an error "You have reached or exceeded the maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="5d68c-114">Usare una sottoscrizione di Azure diversa, eliminare alcune zone o contattare il supporto tecnico di Azure per aumentare il limite della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5d68c-114">Either use a different Azure subscription, delete some zones, or contact Azure Support to raise your subscription limit.</span></span>
4.  <span data-ttu-id="5d68c-115">Se viene visualizzato l'errore "La zona '{nome zona}' non è disponibile.",</span><span class="sxs-lookup"><span data-stu-id="5d68c-115">You may see an error "The zone '{zone name}' is not available."</span></span> <span data-ttu-id="5d68c-116">significa che il servizio DNS di Azure non è riuscito ad allocare i server dei nomi per questa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="5d68c-116">This error means that Azure DNS was unable to allocate name servers for this DNS zone.</span></span> <span data-ttu-id="5d68c-117">Provare a usare un nome di zona diverso.</span><span class="sxs-lookup"><span data-stu-id="5d68c-117">Try using a different zone name.</span></span> <span data-ttu-id="5d68c-118">In alternativa, se si è il proprietario del nome di dominio, contattare il supporto tecnico di Azure, che può allocare i server dei nomi per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="5d68c-118">Alternatively, if you are the domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="5d68c-119">**Documenti consigliati**</span><span class="sxs-lookup"><span data-stu-id="5d68c-119">**Recommended documents**</span></span>

<span data-ttu-id="5d68c-120">[Zone e record DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="5d68c-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="5d68c-121">
[Creare una zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5d68c-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="5d68c-122">Non è possibile creare un record DNS</span><span class="sxs-lookup"><span data-stu-id="5d68c-122">I can't create a DNS record</span></span>

<span data-ttu-id="5d68c-123">Per risolvere i problemi comuni, provare le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d68c-123">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="5d68c-124">Esaminare i log di controllo di DNS di Azure per determinare le cause dell'errore.</span><span class="sxs-lookup"><span data-stu-id="5d68c-124">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="5d68c-125">Il set di record esiste già?</span><span class="sxs-lookup"><span data-stu-id="5d68c-125">Does the record set exist already?</span></span>  <span data-ttu-id="5d68c-126">Il servizio DNS di Azure gestisce i record usando *set* di record, ovvero una raccolta di record dello stesso nome e dello stesso tipo.</span><span class="sxs-lookup"><span data-stu-id="5d68c-126">Azure DNS manages records using record *sets*, which are the collection of records of the same name and the same type.</span></span> <span data-ttu-id="5d68c-127">Se esiste già un record con lo stesso nome e dello stesso tipo, per aggiungere un altro record identico è consigliabile modificare il set di record esistente.</span><span class="sxs-lookup"><span data-stu-id="5d68c-127">If a record with the same name and type already exists, then to add another such record you should edit the existing record set.</span></span>
3.  <span data-ttu-id="5d68c-128">Si sta tentando di creare un record al vertice della zona DNS (la "radice" della zona)?</span><span class="sxs-lookup"><span data-stu-id="5d68c-128">Are you trying to create a record at the DNS zone apex (the ‘root’ of the zone)?</span></span> <span data-ttu-id="5d68c-129">In questo caso, la convenzione DNS è quella di usare il carattere "@" come nome del record.</span><span class="sxs-lookup"><span data-stu-id="5d68c-129">If so, the DNS convention is to use the ‘@’ character as the record name.</span></span> <span data-ttu-id="5d68c-130">Tenere presente inoltre che gli standard DNS non consentono record CNAME al vertice della zona.</span><span class="sxs-lookup"><span data-stu-id="5d68c-130">Also note that the DNS standards do not permit CNAME records at the zone apex.</span></span>
4.  <span data-ttu-id="5d68c-131">Si è verificato un conflitto CNAME?</span><span class="sxs-lookup"><span data-stu-id="5d68c-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="5d68c-132">Gli standard DNS non consentono un record CNAME con lo stesso nome di un record di un altro tipo.</span><span class="sxs-lookup"><span data-stu-id="5d68c-132">The DNS standards do not allow a CNAME record with the same name as a record of any other type.</span></span> <span data-ttu-id="5d68c-133">Se si ha già un record CNAME, la creazione di un record con lo stesso nome e di tipo diverso avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="5d68c-133">If you have an existing CNAME, creating a record with the same name of a different type fails.</span></span>  <span data-ttu-id="5d68c-134">Analogamente, la creazione di un record CNAME avrà esito negativo se il nome corrisponde a un record esistente di tipo diverso.</span><span class="sxs-lookup"><span data-stu-id="5d68c-134">Likewise, creating a CNAME fails if the name matches an existing record of a different type.</span></span> <span data-ttu-id="5d68c-135">Per eliminare il conflitto, rimuovere l'altro record o scegliere un nome di record diverso.</span><span class="sxs-lookup"><span data-stu-id="5d68c-135">Remove the conflict by removing the other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="5d68c-136">È stato raggiunto il limite relativo al numero di set di record consentiti in una zona DNS?</span><span class="sxs-lookup"><span data-stu-id="5d68c-136">Have you reached the limit on the number of record sets permitted in a DNS zone?</span></span> <span data-ttu-id="5d68c-137">Il numero corrente di set di record e il numero massimo di set di record vengono visualizzati nel portale di Azure, nella sezione delle proprietà relative alla zona.</span><span class="sxs-lookup"><span data-stu-id="5d68c-137">The current number of record sets and the maximum number of record sets are shown in the Azure portal, under the 'Properties' for the zone.</span></span> <span data-ttu-id="5d68c-138">Se è stato raggiunto il limite, eliminare alcuni set di record oppure contattare il supporto tecnico di Azure per innalzare il numero massimo di set di record per la zona e riprovare.</span><span class="sxs-lookup"><span data-stu-id="5d68c-138">If you have reached this limit, then either delete some record sets or contact Azure Support to raise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="5d68c-139">**Documenti consigliati**</span><span class="sxs-lookup"><span data-stu-id="5d68c-139">**Recommended documents**</span></span>

<span data-ttu-id="5d68c-140">[Zone e record DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="5d68c-140">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="5d68c-141">
[Creare una zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5d68c-141">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="5d68c-142">Non riesco a risolvere un record DNS</span><span class="sxs-lookup"><span data-stu-id="5d68c-142">I can't resolve my DNS record</span></span>

<span data-ttu-id="5d68c-143">La risoluzione dei nomi DNS è un processo articolato in più passaggi che può non riuscire per vari motivi.</span><span class="sxs-lookup"><span data-stu-id="5d68c-143">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="5d68c-144">La procedura seguente consente di capire il motivo per cui non è possibile eseguire la risoluzione DNS per un record DNS in una zona ospitata nel servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d68c-144">The following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="5d68c-145">Verificare che i record DNS siano stati configurati correttamente nel servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d68c-145">Confirm that the DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="5d68c-146">Esaminare i record DNS nel portale di Azure, controllando che il nome della zona, il nome del record e il tipo di record siano corretti.</span><span class="sxs-lookup"><span data-stu-id="5d68c-146">Review the DNS records in the Azure portal, checking that the zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="5d68c-147">Verificare che i record DNS vengano risolti correttamente nei server dei nomi DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d68c-147">Confirm that the DNS records resolve correctly on the Azure DNS name servers.</span></span>
    - <span data-ttu-id="5d68c-148">Se si eseguono query DNS dal proprio computer locale, è possibile che vengano visualizzati risultati memorizzati nella cache che non riflettono lo stato corrente dei server dei nomi.</span><span class="sxs-lookup"><span data-stu-id="5d68c-148">If you make DNS queries from your local PC, you may see cached results that don’t reflect the current state of the name servers.</span></span>  <span data-ttu-id="5d68c-149">Nelle reti aziendali, inoltre, sono spesso presenti server proxy DNS che impediscono alle query DNS di essere reindirizzate a specifici server dei nomi.</span><span class="sxs-lookup"><span data-stu-id="5d68c-149">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed to specific name servers.</span></span>  <span data-ttu-id="5d68c-150">Per evitare questi problemi, è possibile usare un servizio di risoluzione dei nomi basato sul Web come [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="5d68c-150">To avoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="5d68c-151">Assicurarsi di specificare i server dei nomi corretti per la propria zona DNS, così come sono riportati nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d68c-151">Be sure to specify the correct name servers for your DNS zone, as shown in the Azure portal.</span></span>
    - <span data-ttu-id="5d68c-152">Verificare che siano corretti sia il nome DNS (è necessario specificare il nome completo, incluso il nome della zona) sia il tipo di record.</span><span class="sxs-lookup"><span data-stu-id="5d68c-152">Check that the DNS name is correct (you have to specify the fully qualified name, including the zone name) and the record type is correct</span></span>
3.  <span data-ttu-id="5d68c-153">Assicurarsi che il nome di dominio DNS sia stato correttamente [delegato ai server dei nomi DNS di Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="5d68c-153">Confirm that the DNS domain name has been correctly [delegated to the Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="5d68c-154">Esistono [molti siti Web di terze parti da cui è possibile eseguire la convalida della delega DNS](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="5d68c-154">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="5d68c-155">Trattandosi di un test della delega per la *zona*, è sufficiente specificare il nome della zona DNS, non il nome completo del record.</span><span class="sxs-lookup"><span data-stu-id="5d68c-155">This test is a *zone* delegation test, so you should only enter the DNS zone name and not the fully qualified record name.</span></span>
4.  <span data-ttu-id="5d68c-156">Dopo aver completato la procedura appena descritta dovrebbe essere possibile risolvere correttamente il record DNS.</span><span class="sxs-lookup"><span data-stu-id="5d68c-156">Having completed the above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="5d68c-157">Per verificarlo, è possibile usare nuovamente il servizio [digwebinterface](http://digwebinterface.com), questa volta specificando le impostazioni predefinite dei server dei nomi.</span><span class="sxs-lookup"><span data-stu-id="5d68c-157">To verify, you can again use [digwebinterface](http://digwebinterface.com), this time using the default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="5d68c-158">**Documenti consigliati**</span><span class="sxs-lookup"><span data-stu-id="5d68c-158">**Recommended documents**</span></span>

[<span data-ttu-id="5d68c-159">Delegare un dominio al servizio DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="5d68c-159">Delegate a domain to Azure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-the-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="5d68c-160">Come posso specificare il "servizio" e il "protocollo" per un record SRV?</span><span class="sxs-lookup"><span data-stu-id="5d68c-160">How do I specify the ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="5d68c-161">Il servizio DNS di Azure gestisce i record come set di record, ovvero come una raccolta di record dello stesso nome e dello stesso tipo.</span><span class="sxs-lookup"><span data-stu-id="5d68c-161">Azure DNS manages DNS records as record sets—the collection of records with the same name and the same type.</span></span> <span data-ttu-id="5d68c-162">Per un set di record SRV, il "servizio" e il "protocollo" devono essere specificati come parte del nome del set di record.</span><span class="sxs-lookup"><span data-stu-id="5d68c-162">For an SRV record set, the 'service' and 'protocol' need to be specified as part of the record set name.</span></span> <span data-ttu-id="5d68c-163">Gli altri parametri SRV ("priorità", "peso", "porta" e "destinazione") vengono specificati separatamente per ogni record del set di record.</span><span class="sxs-lookup"><span data-stu-id="5d68c-163">The other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in the record set.</span></span>

<span data-ttu-id="5d68c-164">Nomi di record SRV di esempio ("sip" indica il nome del servizio, "tcp" il protocollo):</span><span class="sxs-lookup"><span data-stu-id="5d68c-164">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="5d68c-165">\_sip.\_tcp (crea un set di record all'apice della zona)</span><span class="sxs-lookup"><span data-stu-id="5d68c-165">\_sip.\_tcp (creates a record set at the zone apex)</span></span>
- <span data-ttu-id="5d68c-166">\_sip.\_tcp.sipservice (crea un set di record denominato "sipservice")</span><span class="sxs-lookup"><span data-stu-id="5d68c-166">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="5d68c-167">**Documenti consigliati**</span><span class="sxs-lookup"><span data-stu-id="5d68c-167">**Recommended documents**</span></span>

<span data-ttu-id="5d68c-168">[Zone e record DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="5d68c-168">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="5d68c-169">
[Creare set di record e record DNS mediante il portale di Azure](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="5d68c-169">
[Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="5d68c-170">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record) (Tipo di record SRV (Wikipedia))</span><span class="sxs-lookup"><span data-stu-id="5d68c-170">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="5d68c-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d68c-171">Next steps</span></span>

* <span data-ttu-id="5d68c-172">Informazioni sulle [zone e sui record di DNS di Azure](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="5d68c-172">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="5d68c-173">Per iniziare a usare DNS di Azure, è necessario sapere come [creare una zona DNS](dns-getstarted-create-dnszone-portal.md) e come [creare record DNS](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5d68c-173">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="5d68c-174">Per eseguire la migrazione di una zona DNS esistente, è necessario saper [importare ed esportare un file di zona DNS](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="5d68c-174">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span></span>

