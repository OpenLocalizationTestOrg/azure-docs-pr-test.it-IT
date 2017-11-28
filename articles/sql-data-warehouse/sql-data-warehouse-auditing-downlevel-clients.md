---
title: i client di Data Warehouse aaaSQL supportano per il controllo dati | Documenti Microsoft
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
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="88432-103">SQL Data Warehouse - Supporto client di livello inferiore per controllo e maschera dati dinamica</span><span class="sxs-lookup"><span data-stu-id="88432-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="88432-104">[Controllo](sql-data-warehouse-auditing-overview.md) funziona con i client SQL che supportano il reindirizzamento TDS.</span><span class="sxs-lookup"><span data-stu-id="88432-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="88432-105">Qualsiasi client che implementa TDS 7.4 deve supportare anche il reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="88432-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="88432-106">Eccezioni toothis includono JDBC 4.0 non è supportato completamente le funzionalità di reindirizzamento di hello e Tedious per Node.JS in cui non è stato implementato il reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="88432-106">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="88432-107">Per "I client legacy", vale a dire che supporta TDS versione 7.3 e hello seguito - nome FQDN del server nella stringa di connessione hello deve essere modificati:</span><span class="sxs-lookup"><span data-stu-id="88432-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="88432-108">FQDN server originale nella stringa di connessione hello: <*nome server*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="88432-108">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="88432-109">FQDN server modificato nella stringa di connessione hello: <*nome server*> database. **protezione**. windows.net</span><span class="sxs-lookup"><span data-stu-id="88432-109">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="88432-110">Un elenco parziale di "client di livello inferiore" include:</span><span class="sxs-lookup"><span data-stu-id="88432-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="88432-111">.NET 4.0 e versioni precedenti,</span><span class="sxs-lookup"><span data-stu-id="88432-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="88432-112">ODBC 10.0 e versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="88432-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="88432-113">JDBC (mentre JDBC supporta TDS 7.4, hello funzionalità di reindirizzamento TDS non è completamente supportata)</span><span class="sxs-lookup"><span data-stu-id="88432-113">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="88432-114">Tedious (per Node.JS)</span><span class="sxs-lookup"><span data-stu-id="88432-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="88432-115">**Nota:** hello sopra Modifica nome FDQN di server può essere utile anche per applicare un criterio di controllo a livello di Server SQL senza la necessità di una configurazione passaggio in ogni database (attenuazione temporaneo).</span><span class="sxs-lookup"><span data-stu-id="88432-115">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

