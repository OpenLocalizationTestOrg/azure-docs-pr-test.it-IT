---
title: aaaPorts oltre 1433 per il Database SQL | Documenti Microsoft
description: Le connessioni client da ADO.NET tooAzure Database SQL a volte ignorare il proxy di hello e interagiscono direttamente con il database di hello. Le porte diverse da 1433 diventano importanti.
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
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="6aeae-104">Porte successive alla 1433 per ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="6aeae-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="6aeae-105">Questo argomento descrive il comportamento di connessione di hello Database SQL di Azure per i client che usano ADO.NET 4.5 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="6aeae-105">This topic describes hello Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6aeae-106">Per informazioni sull'architettura di connettività, vedere [Architettura della connettività del database SQL di Azure](sql-database-connectivity-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="6aeae-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="6aeae-107">Esterno rispetto all'interno</span><span class="sxs-lookup"><span data-stu-id="6aeae-107">Outside vs inside</span></span>
<span data-ttu-id="6aeae-108">Per le connessioni tooAzure Database SQL, è necessario innanzitutto chiedere se viene eseguito il programma client *esterno* o *all'interno di* limiti di hello cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="6aeae-108">For connections tooAzure SQL Database, we must first ask whether your client program runs *outside* or *inside* hello Azure cloud boundary.</span></span> <span data-ttu-id="6aeae-109">nelle sottosezioni Hello illustrano due scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="6aeae-109">hello subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="6aeae-110">*Esterno:* il client è in esecuzione nel computer desktop</span><span class="sxs-lookup"><span data-stu-id="6aeae-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="6aeae-111">La porta 1433 è hello solo la porta che deve essere aperta nel computer desktop che ospita l'applicazione client di Database SQL.</span><span class="sxs-lookup"><span data-stu-id="6aeae-111">Port 1433 is hello only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="6aeae-112">*All'interno:* il client è in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="6aeae-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="6aeae-113">Quando il client viene eseguita all'interno dei confini di hello cloud di Azure, viene utilizzato è possibile chiamare un *route diretta* toointeract con il server di Database SQL di hello.</span><span class="sxs-lookup"><span data-stu-id="6aeae-113">When your client runs inside hello Azure cloud boundary, it uses what we can call a *direct route* toointeract with hello SQL Database server.</span></span> <span data-ttu-id="6aeae-114">Dopo aver stabilita una connessione, altre interazioni tra client hello e database non implicano alcun proxy middleware.</span><span class="sxs-lookup"><span data-stu-id="6aeae-114">After a connection is established, further interactions between hello client and database involve no middleware proxy.</span></span>

<span data-ttu-id="6aeae-115">sequenza di Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="6aeae-115">hello sequence is as follows:</span></span>

1. <span data-ttu-id="6aeae-116">ADO.NET 4.5 (o versioni successive) avvia una breve interazione con hello cloud di Azure e riceve un numero di porta identificato in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="6aeae-116">ADO.NET 4.5 (or later) initiates a brief interaction with hello Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="6aeae-117">numero di porta Hello identificato in modo dinamico è compreso nell'intervallo di hello di 11000 11999 o 14000 14999.</span><span class="sxs-lookup"><span data-stu-id="6aeae-117">hello dynamically identified port number is in hello range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="6aeae-118">ADO.NET si connette quindi il server di Database SQL toohello direttamente, con nessuna middleware tra.</span><span class="sxs-lookup"><span data-stu-id="6aeae-118">ADO.NET then connects toohello SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="6aeae-119">Le query vengono inviate direttamente toohello database e i risultati vengono restituiti toohello client direttamente.</span><span class="sxs-lookup"><span data-stu-id="6aeae-119">Queries are sent directly toohello database, and results are returned directly toohello client.</span></span>

<span data-ttu-id="6aeae-120">Verificare che tale porta hello intervalli di 11000 11999 e 14000-14999 nel computer client di Azure rimangono disponibili per le interazioni client ADO.NET 4.5 con il Database SQL.</span><span class="sxs-lookup"><span data-stu-id="6aeae-120">Ensure that hello port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="6aeae-121">In particolare, le porte nell'intervallo di hello devono rimanere libere da eventuali altri blocchi in uscita.</span><span class="sxs-lookup"><span data-stu-id="6aeae-121">In particular, ports in hello range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="6aeae-122">Nella macchina virtuale di Azure, hello **Windows Firewall con sicurezza avanzata** controlli hello impostazioni della porta.</span><span class="sxs-lookup"><span data-stu-id="6aeae-122">On your Azure VM, hello **Windows Firewall with Advanced Security** controls hello port settings.</span></span>
  
  * <span data-ttu-id="6aeae-123">È possibile utilizzare hello [interfaccia utente del firewall](http://msdn.microsoft.com/library/cc646023.aspx) tooadd una regola per cui si specifica hello **TCP** come protocollo insieme a un intervallo di porte con sintassi hello **11000 11999**.</span><span class="sxs-lookup"><span data-stu-id="6aeae-123">You can use hello [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a rule for which you specify hello **TCP** protocol along with a port range with hello syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="6aeae-124">Chiarimenti sulla versione</span><span class="sxs-lookup"><span data-stu-id="6aeae-124">Version clarifications</span></span>
<span data-ttu-id="6aeae-125">In questa sezione illustra i moniker hello che fanno riferimento le versioni tooproduct.</span><span class="sxs-lookup"><span data-stu-id="6aeae-125">This section clarifies hello monikers that refer tooproduct versions.</span></span> <span data-ttu-id="6aeae-126">Sono inoltre indicate alcune associazioni di versioni tra prodotti.</span><span class="sxs-lookup"><span data-stu-id="6aeae-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="6aeae-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="6aeae-127">ADO.NET</span></span>
* <span data-ttu-id="6aeae-128">ADO.NET 4.0 supporta il protocollo TDS 7.3 hello, ma non 7.4.</span><span class="sxs-lookup"><span data-stu-id="6aeae-128">ADO.NET 4.0 supports hello TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="6aeae-129">ADO.NET 4.5 e versioni successive supporta il protocollo TDS 7.4 hello.</span><span class="sxs-lookup"><span data-stu-id="6aeae-129">ADO.NET 4.5 and later supports hello TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="6aeae-130">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="6aeae-130">Related links</span></span>
* <span data-ttu-id="6aeae-131">ADO.NET 4.6 è stato rilasciato il 20 luglio 2015.</span><span class="sxs-lookup"><span data-stu-id="6aeae-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="6aeae-132">È disponibile un annuncio sul blog del team di .NET hello [qui](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="6aeae-132">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="6aeae-133">ADO.NET 4.5 è stato rilasciato il 15 agosto 2012.</span><span class="sxs-lookup"><span data-stu-id="6aeae-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="6aeae-134">È disponibile un annuncio sul blog del team di .NET hello [qui](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="6aeae-134">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="6aeae-135">È disponibile un post di blog su ADO.NET 4.5.1 [qui](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="6aeae-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="6aeae-136">Elenco versioni del protocollo TDS</span><span class="sxs-lookup"><span data-stu-id="6aeae-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="6aeae-137">Panoramica dello sviluppo di database SQL</span><span class="sxs-lookup"><span data-stu-id="6aeae-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="6aeae-138">Firewall del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="6aeae-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="6aeae-139">Procedura: configurare le impostazioni del firewall su Database SQL</span><span class="sxs-lookup"><span data-stu-id="6aeae-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

