---
title: aaaDesign il database SQL di Azure prima - c# | Documenti Microsoft
description: Informazioni su toodesign di un database SQL di Azure e connettersi tooit con un programma c# tramite ADO.NET.
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a>Progettare un database SQL di Azure e connettersi con C&#x23; e ADO.NET

Database SQL di Azure è un relazionale database-come a un servizio (DBaaS) in hello Cloud Microsoft ("Azure"). In questa esercitazione, è illustrato come toouse hello portale di Azure e ADO.NET con Visual Studio per: 

> [!div class="checklist"]
> * Creare un database in hello portale di Azure
> * Impostare una regola firewall di livello server nel portale di Azure hello
> * La connessione a database toohello con ADO.NET e Visual Studio
> * Creare tabelle con ADO.NET
> * Inserire, aggiornare ed eliminare dati con ADO.NET 
> * Eseguire query sui dati con ADO.NET

Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.

## <a name="prerequisites"></a>Prerequisiti

Un'installazione di [Visual Studio Community 2017, Visual Studio Professional 2017 o Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato attività di base del database, ad esempio creare un database e tabelle, caricare e query sui dati e hello database tooa precedente punto di ripristino temporizzato. Si è appreso come:
> [!div class="checklist"]
> * Creare un database
> * Configurare una regola del firewall
> * La connessione a database toohello con [c# e Visual Studio](sql-database-connect-query-dotnet-visual-studio.md)
> * Creare tabelle
> * Inserire, aggiornare ed eliminare i dati
> * Eseguire query sui dati

Spostare toohello toolearn esercitazione successiva sulla migrazione dei dati.

> [!div class="nextstepaction"]
>[Eseguire la migrazione del tooAzure di database di SQL Server Database SQL](sql-database-migrate-your-sql-server-database.md)

