---
title: Guida alla risoluzione dei problemi di DNS aaaAzure | Documenti Microsoft
description: "La modalità di problemi comuni di tootroubleshoot con DNS di Azure"
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
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="9ca93-103">Guida alla risoluzione dei problemi di DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="9ca93-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="9ca93-104">Questa pagina fornisce informazioni sulla risoluzione dei problemi comuni di DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca93-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="9ca93-105">Se questi passaggi non consentono di risolvere il problema, è anche possibile eseguire una ricerca o inserire una domanda nel [forum di supporto della community su MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="9ca93-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="9ca93-106">In alternativa, aprire una richiesta di Supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca93-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="9ca93-107">Non è possibile creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="9ca93-107">I can't create a DNS zone</span></span>

<span data-ttu-id="9ca93-108">problemi comuni tooresolve, provare a uno o più hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9ca93-108">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="9ca93-109">Hello revisione che DNS di Azure di controllo Registra motivo dell'errore toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="9ca93-109">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="9ca93-110">Ogni nome di zona DNS deve essere univoco all'interno del relativo gruppo di risorse,</span><span class="sxs-lookup"><span data-stu-id="9ca93-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="9ca93-111">Ovvero, due zone DNS con hello stesso nome non può condividere un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9ca93-111">That is, two DNS zones with hello same name cannot share a resource group.</span></span> <span data-ttu-id="9ca93-112">Provare a usare un nome di zona o un gruppo di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="9ca93-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="9ca93-113">Potrebbe essere visualizzato un errore "È stato raggiunto o superato hello il numero massimo di zone nella sottoscrizione {id sottoscrizione}."</span><span class="sxs-lookup"><span data-stu-id="9ca93-113">You may see an error "You have reached or exceeded hello maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="9ca93-114">Utilizzare un'altra sottoscrizione di Azure, eliminare alcune aree oppure contattare il supporto tecnico di Azure tooraise il limite della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9ca93-114">Either use a different Azure subscription, delete some zones, or contact Azure Support tooraise your subscription limit.</span></span>
4.  <span data-ttu-id="9ca93-115">Potrebbe essere visualizzato un errore "zona hello '{nome zona}' non è disponibile."</span><span class="sxs-lookup"><span data-stu-id="9ca93-115">You may see an error "hello zone '{zone name}' is not available."</span></span> <span data-ttu-id="9ca93-116">Questo errore indica che il DNS di Azure è stato Impossibile tooallocate server dei nomi per la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="9ca93-116">This error means that Azure DNS was unable tooallocate name servers for this DNS zone.</span></span> <span data-ttu-id="9ca93-117">Provare a usare un nome di zona diverso.</span><span class="sxs-lookup"><span data-stu-id="9ca93-117">Try using a different zone name.</span></span> <span data-ttu-id="9ca93-118">In alternativa, se si è proprietario del nome di dominio di hello, contattare il supporto tecnico di Azure, che può allocare server dei nomi per l'utente.</span><span class="sxs-lookup"><span data-stu-id="9ca93-118">Alternatively, if you are hello domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="9ca93-119">**Documenti consigliati**</span><span class="sxs-lookup"><span data-stu-id="9ca93-119">**Recommended documents**</span></span>

<span data-ttu-id="9ca93-120">[Zone e record DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="9ca93-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="9ca93-121">
[Creare una zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9ca93-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="9ca93-122">Non è possibile creare un record DNS</span><span class="sxs-lookup"><span data-stu-id="9ca93-122">I can't create a DNS record</span></span>

<span data-ttu-id="9ca93-123">problemi comuni tooresolve, provare a uno o più hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9ca93-123">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="9ca93-124">Hello revisione che DNS di Azure di controllo Registra motivo dell'errore toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="9ca93-124">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="9ca93-125">Set di record hello esiste già?</span><span class="sxs-lookup"><span data-stu-id="9ca93-125">Does hello record set exist already?</span></span>  <span data-ttu-id="9ca93-126">DNS di Azure gestisce i record di utilizzo di record *imposta*, che sono raccolta hello dei record di hello stesso nome e hello stesso tipo.</span><span class="sxs-lookup"><span data-stu-id="9ca93-126">Azure DNS manages records using record *sets*, which are hello collection of records of hello same name and hello same type.</span></span> <span data-ttu-id="9ca93-127">Se un record con hello stesso nome e tipo già esistente, quindi tooadd un altro record di questo tipo è consigliabile modificare hello record esistente.</span><span class="sxs-lookup"><span data-stu-id="9ca93-127">If a record with hello same name and type already exists, then tooadd another such record you should edit hello existing record set.</span></span>
3.  <span data-ttu-id="9ca93-128">Si sta cercando toocreate un record al vertice di zona DNS hello (Buongiorno 'root' della zona hello)?</span><span class="sxs-lookup"><span data-stu-id="9ca93-128">Are you trying toocreate a record at hello DNS zone apex (hello ‘root’ of hello zone)?</span></span> <span data-ttu-id="9ca93-129">In caso affermativo, hello convenzione DNS toouse hello ' @' carattere come nome del record di hello.</span><span class="sxs-lookup"><span data-stu-id="9ca93-129">If so, hello DNS convention is toouse hello ‘@’ character as hello record name.</span></span> <span data-ttu-id="9ca93-130">Si noti inoltre che standard DNS hello non consentono i record CNAME al vertice zona hello.</span><span class="sxs-lookup"><span data-stu-id="9ca93-130">Also note that hello DNS standards do not permit CNAME records at hello zone apex.</span></span>
4.  <span data-ttu-id="9ca93-131">Si è verificato un conflitto CNAME?</span><span class="sxs-lookup"><span data-stu-id="9ca93-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="9ca93-132">standard DNS Hello non consentono un record CNAME con hello stesso nome di un record di qualsiasi altro tipo.</span><span class="sxs-lookup"><span data-stu-id="9ca93-132">hello DNS standards do not allow a CNAME record with hello same name as a record of any other type.</span></span> <span data-ttu-id="9ca93-133">Se si dispone di un CNAME esistente, la creazione di un record con hello stesso nome di un tipo diverso ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="9ca93-133">If you have an existing CNAME, creating a record with hello same name of a different type fails.</span></span>  <span data-ttu-id="9ca93-134">Analogamente, la creazione di un record CNAME, ha esito negativo se hello nome corrisponde a un record esistente di un tipo diverso.</span><span class="sxs-lookup"><span data-stu-id="9ca93-134">Likewise, creating a CNAME fails if hello name matches an existing record of a different type.</span></span> <span data-ttu-id="9ca93-135">Rimuovere il conflitto hello rimuovendo hello altri record o scegliere un nome di un record diverso.</span><span class="sxs-lookup"><span data-stu-id="9ca93-135">Remove hello conflict by removing hello other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="9ca93-136">È stato raggiunto limite hello numero hello di set di record consentiti in una zona DNS di? Imposta il numero corrente di Hello del record e hello numero massimo di set di record viene visualizzato nel portale di Azure in hello 'proprietà' per la zona hello hello.</span><span class="sxs-lookup"><span data-stu-id="9ca93-136">Have you reached hello limit on hello number of record sets permitted in a DNS zone? hello current number of record sets and hello maximum number of record sets are shown in hello Azure portal, under hello 'Properties' for hello zone.</span></span> <span data-ttu-id="9ca93-137">Se si hanno raggiunto questo limite, quindi eliminare alcuni set di record o contatta tooraise supporto tecnico di Azure il limite del set di record per la zona, quindi riprovare.</span><span class="sxs-lookup"><span data-stu-id="9ca93-137">If you have reached this limit, then either delete some record sets or contact Azure Support tooraise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="9ca93-138">**Documenti consigliati**</span><span class="sxs-lookup"><span data-stu-id="9ca93-138">**Recommended documents**</span></span>

<span data-ttu-id="9ca93-139">[Zone e record DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="9ca93-139">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="9ca93-140">
[Creare una zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9ca93-140">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="9ca93-141">Non riesco a risolvere un record DNS</span><span class="sxs-lookup"><span data-stu-id="9ca93-141">I can't resolve my DNS record</span></span>

<span data-ttu-id="9ca93-142">La risoluzione dei nomi DNS è un processo articolato in più passaggi che può non riuscire per vari motivi.</span><span class="sxs-lookup"><span data-stu-id="9ca93-142">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="9ca93-143">Hello passaggi seguenti consentono di analizzare perché la risoluzione DNS non riesce per un record DNS in una zona ospitata nel sistema DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca93-143">hello following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="9ca93-144">Verificare che i record DNS hello siano stati configurati correttamente nel sistema DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca93-144">Confirm that hello DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="9ca93-145">Esaminare i record DNS hello in hello portale di Azure, verifica che nome zona hello e nome del record di tipo di record siano corretti.</span><span class="sxs-lookup"><span data-stu-id="9ca93-145">Review hello DNS records in hello Azure portal, checking that hello zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="9ca93-146">Verificare che i record DNS hello risolvere correttamente nel server dei nomi DNS di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9ca93-146">Confirm that hello DNS records resolve correctly on hello Azure DNS name servers.</span></span>
    - <span data-ttu-id="9ca93-147">Se si apportano le query DNS dal computer locale, è possibile ottenere risultati memorizzati nella cache che non riflettono lo stato corrente di hello hello server dei nomi.</span><span class="sxs-lookup"><span data-stu-id="9ca93-147">If you make DNS queries from your local PC, you may see cached results that don’t reflect hello current state of hello name servers.</span></span>  <span data-ttu-id="9ca93-148">Inoltre, alle reti aziendali utilizzano server proxy DNS, che impedire le query DNS indirizzate toospecific server dei nomi.</span><span class="sxs-lookup"><span data-stu-id="9ca93-148">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed toospecific name servers.</span></span>  <span data-ttu-id="9ca93-149">tooavoid questi problemi, utilizzare un servizio risoluzione dei nomi basato sul web, ad esempio [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="9ca93-149">tooavoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="9ca93-150">Essere toospecify che server dei nomi corretto hello per la zona DNS, come illustrato nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9ca93-150">Be sure toospecify hello correct name servers for your DNS zone, as shown in hello Azure portal.</span></span>
    - <span data-ttu-id="9ca93-151">Verificare che il nome DNS hello sia corretto (si dispone di nome completo di hello toospecify, inclusi nome della zona hello) e tipo di record hello sia corretto</span><span class="sxs-lookup"><span data-stu-id="9ca93-151">Check that hello DNS name is correct (you have toospecify hello fully qualified name, including hello zone name) and hello record type is correct</span></span>
3.  <span data-ttu-id="9ca93-152">Verificare il nome di dominio DNS hello è stata correttamente [delega server dei nomi DNS di Azure toohello](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="9ca93-152">Confirm that hello DNS domain name has been correctly [delegated toohello Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="9ca93-153">Esistono [molti siti Web di terze parti da cui è possibile eseguire la convalida della delega DNS](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="9ca93-153">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="9ca93-154">Questo test è un *zona* test di delega, deve essere immesso solo nome della zona DNS hello e non hello record nome completo.</span><span class="sxs-lookup"><span data-stu-id="9ca93-154">This test is a *zone* delegation test, so you should only enter hello DNS zone name and not hello fully qualified record name.</span></span>
4.  <span data-ttu-id="9ca93-155">Dopo aver completato hello precedente, il record DNS debba ora risolto correttamente.</span><span class="sxs-lookup"><span data-stu-id="9ca93-155">Having completed hello above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="9ca93-156">tooverify, è possibile usare nuovamente [digwebinterface](http://digwebinterface.com), questa volta utilizzando le impostazioni di hello predefinite nome server.</span><span class="sxs-lookup"><span data-stu-id="9ca93-156">tooverify, you can again use [digwebinterface](http://digwebinterface.com), this time using hello default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="9ca93-157">**Documenti consigliati**</span><span class="sxs-lookup"><span data-stu-id="9ca93-157">**Recommended documents**</span></span>

[<span data-ttu-id="9ca93-158">Delegato tooAzure un dominio DNS</span><span class="sxs-lookup"><span data-stu-id="9ca93-158">Delegate a domain tooAzure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="9ca93-159">Come specificare hello 'service' e 'protocollo' per un record SRV?</span><span class="sxs-lookup"><span data-stu-id="9ca93-159">How do I specify hello ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="9ca93-160">DNS di Azure gestisce i record DNS come set di record: hello raccolta di record con hello stesso nome e hello stesso tipo.</span><span class="sxs-lookup"><span data-stu-id="9ca93-160">Azure DNS manages DNS records as record sets—hello collection of records with hello same name and hello same type.</span></span> <span data-ttu-id="9ca93-161">Per un set di record SRV, servizio"hello" e "protocollo" necessario toobe specificato come parte del nome di set di record di hello.</span><span class="sxs-lookup"><span data-stu-id="9ca93-161">For an SRV record set, hello 'service' and 'protocol' need toobe specified as part of hello record set name.</span></span> <span data-ttu-id="9ca93-162">Hello SRV ('priority', 'peso', 'porta' e 'target') sono specificati altri parametri separatamente per ciascun record nel set di record di hello.</span><span class="sxs-lookup"><span data-stu-id="9ca93-162">hello other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in hello record set.</span></span>

<span data-ttu-id="9ca93-163">Nomi di record SRV di esempio ("sip" indica il nome del servizio, "tcp" il protocollo):</span><span class="sxs-lookup"><span data-stu-id="9ca93-163">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="9ca93-164">\_SIP. \_tcp (Crea un set al vertice zona hello di record)</span><span class="sxs-lookup"><span data-stu-id="9ca93-164">\_sip.\_tcp (creates a record set at hello zone apex)</span></span>
- <span data-ttu-id="9ca93-165">\_sip.\_tcp.sipservice (crea un set di record denominato "sipservice")</span><span class="sxs-lookup"><span data-stu-id="9ca93-165">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="9ca93-166">**Documenti consigliati**</span><span class="sxs-lookup"><span data-stu-id="9ca93-166">**Recommended documents**</span></span>

<span data-ttu-id="9ca93-167">[Zone e record DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="9ca93-167">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="9ca93-168">
[Creare set di record DNS e i record utilizzando hello portale di Azure](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="9ca93-168">
[Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="9ca93-169">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record) (Tipo di record SRV (Wikipedia))</span><span class="sxs-lookup"><span data-stu-id="9ca93-169">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="9ca93-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9ca93-170">Next steps</span></span>

* <span data-ttu-id="9ca93-171">Informazioni sulle [zone e sui record di DNS di Azure](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="9ca93-171">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="9ca93-172">toostart tramite DNS di Azure, informazioni su come troppo[creare una zona DNS](dns-getstarted-create-dnszone-portal.md) e [creare record DNS](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9ca93-172">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="9ca93-173">toomigrate una zona DNS esistente, informazioni su come troppo[importare ed esportare un file di zona DNS](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="9ca93-173">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>

