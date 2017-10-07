---
title: la crittografia dei dati nel Data Warehouse di SQL (portale) aaaTransparent | Documenti Microsoft
description: Transparent Data Encryption (TDE) in SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="874fc-103">Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="874fc-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="874fc-104">Proteggere un database in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="874fc-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="874fc-105">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="874fc-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="874fc-106">Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="874fc-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="874fc-107">Introduzione a Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="874fc-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="874fc-108">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="874fc-108">Required Permssions</span></span>
<span data-ttu-id="874fc-109">tooenable Transparent Data Encryption (TDE), è necessario essere un amministratore o un membro del ruolo dbmanager hello.</span><span class="sxs-lookup"><span data-stu-id="874fc-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="874fc-110">Abilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="874fc-110">Enabling Encryption</span></span>
<span data-ttu-id="874fc-111">tooenable TDE per un SQL Data Warehouse, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="874fc-111">tooenable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="874fc-112">Database aperto hello in hello [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="874fc-112">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="874fc-113">Nel pannello database hello, fare clic su hello **impostazioni** pulsante</span><span class="sxs-lookup"><span data-stu-id="874fc-113">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="874fc-114">Seleziona hello **crittografia dati trasparente** opzione![][1]</span><span class="sxs-lookup"><span data-stu-id="874fc-114">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="874fc-115">Seleziona hello **su** impostazione![][2]</span><span class="sxs-lookup"><span data-stu-id="874fc-115">Select hello **On** setting ![][2]</span></span>
5. <span data-ttu-id="874fc-116">Selezionare **Salva**
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="874fc-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="874fc-117">Disabilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="874fc-117">Disabling Encryption</span></span>
<span data-ttu-id="874fc-118">toodisable TDE per un SQL Data Warehouse, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="874fc-118">toodisable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="874fc-119">Database aperto hello in hello [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="874fc-119">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="874fc-120">Nel pannello database hello, fare clic su hello **impostazioni** pulsante</span><span class="sxs-lookup"><span data-stu-id="874fc-120">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="874fc-121">Seleziona hello **crittografia dati trasparente** opzione![][1]</span><span class="sxs-lookup"><span data-stu-id="874fc-121">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="874fc-122">Seleziona hello **Off** impostazione![][4]</span><span class="sxs-lookup"><span data-stu-id="874fc-122">Select hello **Off** setting ![][4]</span></span>
5. <span data-ttu-id="874fc-123">Selezionare **Salva**
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="874fc-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="874fc-124">Viste a gestione dinamica della crittografia</span><span class="sxs-lookup"><span data-stu-id="874fc-124">Encryption DMVs</span></span>
<span data-ttu-id="874fc-125">La crittografia può essere confermata con hello DMV indicate di seguito:</span><span class="sxs-lookup"><span data-stu-id="874fc-125">Encryption can be confirmed with hello following DMVs:</span></span>

* <span data-ttu-id="874fc-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="874fc-126">[sys.databases]</span></span>
* <span data-ttu-id="874fc-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="874fc-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
