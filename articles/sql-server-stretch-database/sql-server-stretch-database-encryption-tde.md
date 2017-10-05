---
title: Abilitare Transparent Data Encryption per Estensione database - Azure | Documentazione Microsoft
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
ms.openlocfilehash: ceb355d2ba872ed5d3886c6dc82ca75b1854db0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="3e022-103">Abilitare Transparent Data Encryption (TDE) per Estensione database su Azure</span><span class="sxs-lookup"><span data-stu-id="3e022-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e022-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3e022-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="3e022-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="3e022-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="3e022-106">La funzionalità Transparent Data Encryption (TDE) consente di proteggersi da attività dannose eseguendo in tempo reale la crittografia e la decrittografia dei database, dei backup associati e dei file di log delle transazioni inattivi, senza dover apportare modifiche all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e022-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="3e022-107">TDE esegue la crittografia dell'archiviazione di un intero database usando una chiave simmetrica detta "chiave di crittografia del database".</span><span class="sxs-lookup"><span data-stu-id="3e022-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="3e022-108">La chiave di crittografia del database è protetta da un certificato server incorporato.</span><span class="sxs-lookup"><span data-stu-id="3e022-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="3e022-109">Il certificato server incorporato è univoco per ogni server Azure.</span><span class="sxs-lookup"><span data-stu-id="3e022-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="3e022-110">Microsoft ruota automaticamente questi certificati almeno ogni 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="3e022-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="3e022-111">Per una descrizione generale della funzionalità TDE, vedere [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="3e022-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="3e022-112">Abilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="3e022-112">Enabling Encryption</span></span>
<span data-ttu-id="3e022-113">Per abilitare la funzionalità TDE per un database di Azure che archivia i dati migrati da un database SQL Server con Estensione abilitata, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3e022-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="3e022-114">Aprire il database nel [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="3e022-114">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="3e022-115">Nel pannello del database fare clic sul pulsante **Impostazioni**</span><span class="sxs-lookup"><span data-stu-id="3e022-115">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="3e022-116">Selezionare l'opzione **Transparent data encryption**![][1]</span><span class="sxs-lookup"><span data-stu-id="3e022-116">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="3e022-117">Selezionare **Attiva** e quindi selezionare **Salva**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="3e022-117">Select the **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="3e022-118">Disabilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="3e022-118">Disabling Encryption</span></span>
<span data-ttu-id="3e022-119">Per disabilitare TDE per un database di Azure che archivia i dati migrati da un database SQL Server con Estensione abilitata, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3e022-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="3e022-120">Aprire il database nel [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="3e022-120">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="3e022-121">Nel pannello del database fare clic sul pulsante **Impostazioni**</span><span class="sxs-lookup"><span data-stu-id="3e022-121">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="3e022-122">Selezionare l'opzione **Transparent data encryption**</span><span class="sxs-lookup"><span data-stu-id="3e022-122">Select the **Transparent data encryption** option</span></span>
4. <span data-ttu-id="3e022-123">Selezionare **Disattiva** e quindi selezionare **Salva**</span><span class="sxs-lookup"><span data-stu-id="3e022-123">Select the **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
<span data-ttu-id="3e022-124">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="3e022-124">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
