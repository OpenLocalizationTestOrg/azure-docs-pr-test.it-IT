---
title: aaaInstall Visual Studio e SSDT per SQL Data Warehouse | Documenti Microsoft
description: Installare Visual Studio e SQL Server Data Tools (SSDT) per Azure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a>Installare Visual Studio e SSDT per SQL Data Warehouse
applicazioni toodevelop per SQL Data Warehouse, è consigliabile utilizzare hello più recente di Visual Studio con la versione più recente hello di SQL Server Data Tools (SSDT).  È supportato anche Visual Studio 2013 Update 5 con SSDT per la compatibilità con le versioni precedenti.  

Utilizzo di Visual Studio con SSDT sarà toouse hello Esplora oggetti di SQL Server toovisually esplorare le tabelle, viste, stored procedure e molti altri oggetti in SQL Data Warehouse, nonché di eseguire query.

> [!NOTE]
> SQL Data Warehouse non supporta ancora i progetti di database di Visual Studio.  Questa funzionalità verrà aggiunta in una versione futura.
> 
> 

## <a name="step-1-install-visual-studio"></a>Passaggio 1: Installare Visual Studio
Seguire questi toodownload collegamenti e installare Visual Studio. Se si dispone già di Visual Studio 2013 o versione successiva, è possibile ignorare tooStep 2, installare SSDT.

1. [Scaricare Visual Studio][].
2. Seguire hello [installazione di Visual Studio] [ Installing Visual Studio] Guida su MSDN e scegliere le configurazioni predefinite di hello.

## <a name="step-2-install-ssdt"></a>Passaggio 2: Installare SSDT
tooinstall SSDT per Visual Studio è sufficiente selezionare un aggiornamento di SSDT da Visual Studio eseguendo la procedura seguente.

1. In Visual Studio fare clic su **Strumenti** / **Estensioni e aggiornamenti** / **Aggiornamenti**
2. Selezionare **Aggiornamenti del prodotto**, quindi cercare **Aggiornamento di Microsoft SQL Server per strumenti di database**

Se non viene trovato un aggiornamento, è necessario installare la versione più recente hello.  tooconfirm SSDT è installato, fare clic su **Guida** / **su Microsoft Visual Studio** e cercare di SQL Server Data Tools nell'elenco di hello.  versione più recente di Hello di SSDT è 14.0.60525.0.  Se hello opzione tooinstall non è disponibile da Visual Studio, in alternativa è possibile visitare lo hello [di Download di SSDT] [ SSDT Download] pagina toodownload e installare SSDT manualmente.

## <a name="next-steps"></a>Passaggi successivi
Ora che si dispone di hello la versione più recente di SSDT, si è pronti troppo[connettersi] [ connect] tooyour SQL Data Warehouse.

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Scaricare Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
