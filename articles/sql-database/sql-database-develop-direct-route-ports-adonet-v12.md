---
title: Porte superiori a 1433 per il database SQL | Documentazione Microsoft
description: Le connessioni client da ADO.NET al database SQL di Azure talvolta ignorano il proxy e interagiscono direttamente con il database. Le porte diverse da 1433 diventano importanti.
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: d47ee8c794d1e231507dae6bb4aa88bf19ce6418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="e2125-104">Porte successive alla 1433 per ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="e2125-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="e2125-105">In questo argomento viene descritto il comportamento di connessione del database SQL di Azure per i client che utilizzano ADO.NET 4.5 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e2125-105">This topic describes the Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e2125-106">Per informazioni sull'architettura di connettività, vedere [Architettura della connettività del database SQL di Azure](sql-database-connectivity-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="e2125-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="e2125-107">Esterno rispetto all'interno</span><span class="sxs-lookup"><span data-stu-id="e2125-107">Outside vs inside</span></span>
<span data-ttu-id="e2125-108">Per le connessioni al database SQL di Azure, è necessario prima chiedere se il programma client viene eseguito *all'esterno* o *all'interno* del limite del cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2125-108">For connections to Azure SQL Database, we must first ask whether your client program runs *outside* or *inside* the Azure cloud boundary.</span></span> <span data-ttu-id="e2125-109">Nelle sottosezioni vengono illustrati due scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="e2125-109">The subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="e2125-110">*Esterno:* il client è in esecuzione nel computer desktop</span><span class="sxs-lookup"><span data-stu-id="e2125-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="e2125-111">La porta 1433 è l'unica porta da aprire nel computer desktop che ospita l'applicazione client del database SQL.</span><span class="sxs-lookup"><span data-stu-id="e2125-111">Port 1433 is the only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="e2125-112">*All'interno:* il client è in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="e2125-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="e2125-113">Quando il client viene eseguito all'interno del limite del cloud di Azure, viene utilizzato ciò che possiamo definire un *percorso diretto* per interagire con il server del database SQL.</span><span class="sxs-lookup"><span data-stu-id="e2125-113">When your client runs inside the Azure cloud boundary, it uses what we can call a *direct route* to interact with the SQL Database server.</span></span> <span data-ttu-id="e2125-114">Una volta stabilita una connessione, ulteriori interazioni tra il client e il database non coinvolgono alcun proxy middleware.</span><span class="sxs-lookup"><span data-stu-id="e2125-114">After a connection is established, further interactions between the client and database involve no middleware proxy.</span></span>

<span data-ttu-id="e2125-115">La sequenza è la seguente:</span><span class="sxs-lookup"><span data-stu-id="e2125-115">The sequence is as follows:</span></span>

1. <span data-ttu-id="e2125-116">ADO.NET 4.5 (o versione successiva) avvia una breve interazione con il cloud di Azure e riceve un numero di porta identificato in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="e2125-116">ADO.NET 4.5 (or later) initiates a brief interaction with the Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="e2125-117">Il numero di porta identificato in modo dinamico è compreso nell'intervallo tra 11000-11999 o 14000-14999.</span><span class="sxs-lookup"><span data-stu-id="e2125-117">The dynamically identified port number is in the range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="e2125-118">ADO.NET quindi si connette direttamente al server del database SQL, senza alcun middleware intermedio.</span><span class="sxs-lookup"><span data-stu-id="e2125-118">ADO.NET then connects to the SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="e2125-119">Le query vengono inviate direttamente al database e i risultati vengono restituiti direttamente al client.</span><span class="sxs-lookup"><span data-stu-id="e2125-119">Queries are sent directly to the database, and results are returned directly to the client.</span></span>

<span data-ttu-id="e2125-120">Assicurarsi che l'intervallo di porte 11000-11999 e 14000-14999 nel computer client di Azure venga reso disponibile per le interazioni del client ADO.NET 4.5 con il database SQL.</span><span class="sxs-lookup"><span data-stu-id="e2125-120">Ensure that the port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="e2125-121">In particolare, le porte nell'intervallo devono essere libere da eventuali altri blocchi in uscita.</span><span class="sxs-lookup"><span data-stu-id="e2125-121">In particular, ports in the range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="e2125-122">Nella macchina virtuale di Azure, il **Windows Firewall con sicurezza avanzata** controlla le impostazioni della porta.</span><span class="sxs-lookup"><span data-stu-id="e2125-122">On your Azure VM, the **Windows Firewall with Advanced Security** controls the port settings.</span></span>
  
  * <span data-ttu-id="e2125-123">È possibile usare l'[interfaccia utente del firewall](http://msdn.microsoft.com/library/cc646023.aspx) per aggiungere una regola per cui si specifica il protocollo**TCP** con un intervallo di porte con la sintassi **11000-11999**.</span><span class="sxs-lookup"><span data-stu-id="e2125-123">You can use the [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) to add a rule for which you specify the **TCP** protocol along with a port range with the syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="e2125-124">Chiarimenti sulla versione</span><span class="sxs-lookup"><span data-stu-id="e2125-124">Version clarifications</span></span>
<span data-ttu-id="e2125-125">In questa sezione vengono spiegati i moniker che fanno riferimento a versioni precedenti del prodotto.</span><span class="sxs-lookup"><span data-stu-id="e2125-125">This section clarifies the monikers that refer to product versions.</span></span> <span data-ttu-id="e2125-126">Sono inoltre indicate alcune associazioni di versioni tra prodotti.</span><span class="sxs-lookup"><span data-stu-id="e2125-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="e2125-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="e2125-127">ADO.NET</span></span>
* <span data-ttu-id="e2125-128">ADO.NET 4.0 supporta il protocollo TDS 7.3, ma non 7.4.</span><span class="sxs-lookup"><span data-stu-id="e2125-128">ADO.NET 4.0 supports the TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="e2125-129">ADO.NET 4.5 e versioni successive supportano il protocollo TDS 7.4.</span><span class="sxs-lookup"><span data-stu-id="e2125-129">ADO.NET 4.5 and later supports the TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="e2125-130">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="e2125-130">Related links</span></span>
* <span data-ttu-id="e2125-131">ADO.NET 4.6 è stato rilasciato il 20 luglio 2015.</span><span class="sxs-lookup"><span data-stu-id="e2125-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="e2125-132">È disponibile un annuncio di blog del team .NET [qui](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2125-132">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="e2125-133">ADO.NET 4.5 è stato rilasciato il 15 agosto 2012.</span><span class="sxs-lookup"><span data-stu-id="e2125-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="e2125-134">È disponibile un annuncio di blog del team .NET [qui](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2125-134">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="e2125-135">È disponibile un post di blog su ADO.NET 4.5.1 [qui](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2125-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="e2125-136">Elenco versioni del protocollo TDS</span><span class="sxs-lookup"><span data-stu-id="e2125-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="e2125-137">Panoramica dello sviluppo di database SQL</span><span class="sxs-lookup"><span data-stu-id="e2125-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="e2125-138">Firewall del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="e2125-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="e2125-139">Procedura: configurare le impostazioni del firewall su Database SQL</span><span class="sxs-lookup"><span data-stu-id="e2125-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

