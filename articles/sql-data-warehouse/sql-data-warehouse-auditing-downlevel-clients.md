---
title: 'SQL Data Warehouse: supporto client di livello inferiore per controllo dati | Microsoft Docs'
description: Informazioni sul supporto di client di livello inferiore di SQL Data Warehouse per il controllo dati
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: a7ea6141285a0098339f1e071af2592dd4535c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="377ea-103">SQL Data Warehouse - Supporto client di livello inferiore per controllo e maschera dati dinamica</span><span class="sxs-lookup"><span data-stu-id="377ea-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="377ea-104">[Controllo](sql-data-warehouse-auditing-overview.md) funziona con i client SQL che supportano il reindirizzamento TDS.</span><span class="sxs-lookup"><span data-stu-id="377ea-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="377ea-105">Qualsiasi client che implementa TDS 7.4 deve supportare anche il reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="377ea-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="377ea-106">Rappresentano un'eccezione JDBC 4.0, in cui non è del tutto supportata la funzionalità di reindirizzamento, e Tedious per Node.JS, in cui non è implementato il reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="377ea-106">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="377ea-107">Per i "client di livello inferiore", ad esempio quelli che supportano la versione 7.3 di TDS e inferiori, il nome di dominio completo del server nella stringa di connessione deve essere modificato:</span><span class="sxs-lookup"><span data-stu-id="377ea-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span></span>

<span data-ttu-id="377ea-108">Nome di dominio completo del server originale nella stringa di connessione: <*server name*>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="377ea-108">Original server FQDN in the connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="377ea-109">Nome di dominio completo del server modificato nella stringa di connessione: <*server name*>.database.**secure**.windows.net</span><span class="sxs-lookup"><span data-stu-id="377ea-109">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="377ea-110">Un elenco parziale di "client di livello inferiore" include:</span><span class="sxs-lookup"><span data-stu-id="377ea-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="377ea-111">.NET 4.0 e versioni precedenti,</span><span class="sxs-lookup"><span data-stu-id="377ea-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="377ea-112">ODBC 10.0 e versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="377ea-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="377ea-113">JDBC (mentre JDBC supporta TDS 7.4, la funzionalità di reindirizzamento TDS non è del tutto supportata)</span><span class="sxs-lookup"><span data-stu-id="377ea-113">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="377ea-114">Tedious (per Node.JS)</span><span class="sxs-lookup"><span data-stu-id="377ea-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="377ea-115">**Nota:** la modifica del nome di dominio completo del server citata in precedenza può risultare utile per applicare un criterio di controllo a livello di server SQL senza la necessità di una procedura di configurazione in ogni database (attenuazione temporanea).</span><span class="sxs-lookup"><span data-stu-id="377ea-115">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

