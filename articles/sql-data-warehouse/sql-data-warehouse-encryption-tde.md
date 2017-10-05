---
title: Transparent Data Encryption in SQL Data Warehouse (Portale) | Documentazione Microsoft
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
ms.openlocfilehash: b1db3bdfdfb54bda325c9b971cfcb4dd5efa333a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="b7fb1-103">Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b7fb1-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b7fb1-104">Proteggere un database in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b7fb1-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="b7fb1-105">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="b7fb1-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="b7fb1-106">Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b7fb1-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="b7fb1-107">Introduzione a Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="b7fb1-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="b7fb1-108">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="b7fb1-108">Required Permssions</span></span>
<span data-ttu-id="b7fb1-109">Per abilitare Transparent Data Encryption (TDE), è necessario essere un amministratore o un membro del ruolo dbmanager.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="b7fb1-110">Abilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="b7fb1-110">Enabling Encryption</span></span>
<span data-ttu-id="b7fb1-111">Per abilitare TDE per un SQL Data Warehouse, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b7fb1-111">To enable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="b7fb1-112">Aprire il database nel [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b7fb1-112">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="b7fb1-113">Nel pannello del database fare clic sul pulsante **Impostazioni**</span><span class="sxs-lookup"><span data-stu-id="b7fb1-113">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="b7fb1-114">Selezionare l'opzione **Transparent data encryption**![][1]</span><span class="sxs-lookup"><span data-stu-id="b7fb1-114">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="b7fb1-115">Selezionare l'impostazione **Attiva** ![][2]</span><span class="sxs-lookup"><span data-stu-id="b7fb1-115">Select the **On** setting ![][2]</span></span>
5. <span data-ttu-id="b7fb1-116">Selezionare **Salva**
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="b7fb1-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="b7fb1-117">Disabilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="b7fb1-117">Disabling Encryption</span></span>
<span data-ttu-id="b7fb1-118">Per disabilitare TDE per un SQL Data Warehouse, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b7fb1-118">To disable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="b7fb1-119">Aprire il database nel [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b7fb1-119">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="b7fb1-120">Nel pannello del database fare clic sul pulsante **Impostazioni**</span><span class="sxs-lookup"><span data-stu-id="b7fb1-120">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="b7fb1-121">Selezionare l'opzione **Transparent data encryption**![][1]</span><span class="sxs-lookup"><span data-stu-id="b7fb1-121">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="b7fb1-122">Selezionare l'impostazione **Disattiva** ![][4]</span><span class="sxs-lookup"><span data-stu-id="b7fb1-122">Select the **Off** setting ![][4]</span></span>
5. <span data-ttu-id="b7fb1-123">Selezionare **Salva**
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="b7fb1-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="b7fb1-124">Viste a gestione dinamica della crittografia</span><span class="sxs-lookup"><span data-stu-id="b7fb1-124">Encryption DMVs</span></span>
<span data-ttu-id="b7fb1-125">La crittografia può essere confermata con le seguenti viste a gestione dinamica:</span><span class="sxs-lookup"><span data-stu-id="b7fb1-125">Encryption can be confirmed with the following DMVs:</span></span>

* <span data-ttu-id="b7fb1-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="b7fb1-126">[sys.databases]</span></span>
* <span data-ttu-id="b7fb1-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="b7fb1-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
<span data-ttu-id="b7fb1-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span><span class="sxs-lookup"><span data-stu-id="b7fb1-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span></span>
<span data-ttu-id="b7fb1-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span><span class="sxs-lookup"><span data-stu-id="b7fb1-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
