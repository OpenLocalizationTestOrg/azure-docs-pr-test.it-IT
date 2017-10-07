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
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Abilitare Transparent Data Encryption (TDE) per Estensione database su Azure
> [!div class="op_single_selector"]
> * [Portale di Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Transparent Data Encryption (TDE) contribuisce alla protezione dalle minacce di hello di attività dannose eseguendo la crittografia in tempo reale e la decrittografia del database hello, i backup associati e i file di log delle transazioni a riposo senza richiedere modifiche toohello applicazione.

Transparent Data Encryption crittografa l'archivio di hello di un intero database utilizzando una chiave di crittografia simmetrica hello chiamata chiave database. chiave di crittografia del database Hello è protetto da un certificato server predefinito. certificato server predefinito Hello è univoco per ogni server di Azure. Microsoft ruota automaticamente questi certificati almeno ogni 90 giorni. Per una descrizione generale della funzionalità TDE, vedere [Transparent Data Encryption (TDE)].

## <a name="enabling-encryption"></a>Abilitazione della crittografia
tooenable TDE per un database di Azure a cui è archiviati i dati migrati da un database di SQL Server abilitata per l'estensione, hello hello seguenti operazioni:

1. Database aperto hello in hello [portale di Azure](https://portal.azure.com)
2. Nel pannello database hello, fare clic su hello **impostazioni** pulsante
3. Seleziona hello **crittografia dati trasparente** opzione![][1]
4. Seleziona hello **su** impostazione e quindi selezionare **salvare**
   ![][2]

## <a name="disabling-encryption"></a>Disabilitazione della crittografia
toodisable TDE per un database di Azure a cui è archiviati i dati migrati da un database di SQL Server abilitata per l'estensione, hello hello seguenti operazioni:

1. Database aperto hello in hello [portale di Azure](https://portal.azure.com)
2. Nel pannello database hello, fare clic su hello **impostazioni** pulsante
3. Seleziona hello **crittografia dati trasparente** opzione
4. Seleziona hello **Off** impostazione e quindi selezionare **salvare**

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
