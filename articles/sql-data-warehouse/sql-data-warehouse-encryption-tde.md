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
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a>Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Proteggere un database in SQL Data Warehouse](sql-data-warehouse-overview-manage-security.md)
> * [Autenticazione](sql-data-warehouse-authentication.md)
> * [Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse](sql-data-warehouse-encryption-tde.md)
> * [Introduzione a Transparent Data Encryption (TDE)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Autorizzazioni necessarie
tooenable Transparent Data Encryption (TDE), è necessario essere un amministratore o un membro del ruolo dbmanager hello.

## <a name="enabling-encryption"></a>Abilitazione della crittografia
tooenable TDE per un SQL Data Warehouse, procedura hello riportata di seguito:

1. Database aperto hello in hello [portale di Azure](https://portal.azure.com)
2. Nel pannello database hello, fare clic su hello **impostazioni** pulsante
3. Seleziona hello **crittografia dati trasparente** opzione![][1]
4. Seleziona hello **su** impostazione![][2]
5. Selezionare **Salva**
   ![][3]  

## <a name="disabling-encryption"></a>Disabilitazione della crittografia
toodisable TDE per un SQL Data Warehouse, procedura hello riportata di seguito:

1. Database aperto hello in hello [portale di Azure](https://portal.azure.com)
2. Nel pannello database hello, fare clic su hello **impostazioni** pulsante
3. Seleziona hello **crittografia dati trasparente** opzione![][1]
4. Seleziona hello **Off** impostazione![][4]
5. Selezionare **Salva**
   ![][5]  

## <a name="encryption-dmvs"></a>Viste a gestione dinamica della crittografia
La crittografia può essere confermata con hello DMV indicate di seguito:

* [sys.databases]
* [sys.dm_pdw_nodes_database_encryption_keys]

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
