---
title: Transparent Data Encryption per estensione Database - Azure aaaEnable | Documenti Microsoft
description: Abilitare Transparent Data Encryption (TDE) per Estensione database di SQL Server su Azure
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="ed487-103">Abilitare Transparent Data Encryption (TDE) per Estensione database su Azure</span><span class="sxs-lookup"><span data-stu-id="ed487-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed487-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ed487-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="ed487-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="ed487-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="ed487-106">Transparent Data Encryption (TDE) contribuisce alla protezione dalle minacce di hello di attività dannose eseguendo la crittografia in tempo reale e la decrittografia del database hello, i backup associati e i file di log delle transazioni a riposo senza richiedere modifiche toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="ed487-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="ed487-107">Transparent Data Encryption crittografa l'archivio di hello di un intero database utilizzando una chiave di crittografia simmetrica hello chiamata chiave database.</span><span class="sxs-lookup"><span data-stu-id="ed487-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="ed487-108">chiave di crittografia del database Hello è protetto da un certificato server predefinito.</span><span class="sxs-lookup"><span data-stu-id="ed487-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="ed487-109">certificato server predefinito Hello è univoco per ogni server di Azure.</span><span class="sxs-lookup"><span data-stu-id="ed487-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="ed487-110">Microsoft ruota automaticamente questi certificati almeno ogni 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="ed487-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="ed487-111">Per una descrizione generale della funzionalità TDE, vedere [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="ed487-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="ed487-112">Abilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="ed487-112">Enabling Encryption</span></span>
<span data-ttu-id="ed487-113">tooenable TDE per un database di Azure a cui è archiviati i dati migrati da un database di SQL Server abilitata per l'estensione, hello hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="ed487-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="ed487-114">Database aperto hello in hello [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ed487-114">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="ed487-115">Nel pannello database hello, fare clic su hello **impostazioni** pulsante</span><span class="sxs-lookup"><span data-stu-id="ed487-115">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="ed487-116">Seleziona hello **crittografia dati trasparente** opzione![][1]</span><span class="sxs-lookup"><span data-stu-id="ed487-116">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="ed487-117">Seleziona hello **su** impostazione e quindi selezionare **salvare**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="ed487-117">Select hello **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="ed487-118">Disabilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="ed487-118">Disabling Encryption</span></span>
<span data-ttu-id="ed487-119">toodisable TDE per un database di Azure a cui è archiviati i dati migrati da un database di SQL Server abilitata per l'estensione, hello hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="ed487-119">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="ed487-120">Database aperto hello in hello [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ed487-120">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="ed487-121">Nel pannello database hello, fare clic su hello **impostazioni** pulsante</span><span class="sxs-lookup"><span data-stu-id="ed487-121">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="ed487-122">Seleziona hello **crittografia dati trasparente** opzione</span><span class="sxs-lookup"><span data-stu-id="ed487-122">Select hello **Transparent data encryption** option</span></span>
4. <span data-ttu-id="ed487-123">Seleziona hello **Off** impostazione e quindi selezionare **salvare**</span><span class="sxs-lookup"><span data-stu-id="ed487-123">Select hello **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
