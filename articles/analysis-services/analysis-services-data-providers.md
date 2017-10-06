---
title: librerie aaaClient necessarie per la connessione di Analysis Services di tooAzure | Documenti Microsoft
description: Descrive le librerie client necessarie per client tooconnect di strumenti e applicazioni Azure Analysis Services
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a>Librerie client per la connessione tooAzure Analysis Services

Le librerie client sono necessari per le applicazioni client e server di servizi tooAnalysis tooconnect strumenti. 

Analysis Services usa tre librerie client. ADOMD.NET e Analysis Services Management Objects (AMO) sono librerie client gestite. provider OLE DB per Analysis Services Hello (MSOLAP DLL) è una libreria client nativa. In genere, in cui sono installati tutti e tre in hello contemporaneamente. Azure Analysis Services richiede versioni più recenti di hello. 

Le applicazioni client di Microsoft, come ad esempio Power BI Desktop ed Excel, installano tutte e tre le librerie client. Tuttavia, a seconda della versione di hello o frequenza degli aggiornamenti, le librerie client potrebbero non essere versioni più recenti di hello richieste da Azure Analysis Services. Hello vale toocustom applicazioni o altre interfacce, ad esempio AsCmd, TOM, ADOMD.NET. Queste applicazioni richiedono l'installazione manuale di librerie hello. le librerie client Hello per l'installazione manuale sono inclusi nel feature pack di SQL Server come pacchetti distribuibili. Tuttavia, le librerie client sono toohello legati versione di SQL Server e hello potrebbero non essere più recente.  

Le librerie client per le connessioni client sono diverse dalle tooconnect necessari i provider di dati da un'origine di dati tooa server Azure Analysis Services. toolearn più sulle connessioni di origine dati, vedere [connessioni origine dati](analysis-services-datasource.md).

## <a name="download-hello-latest-client-libraries"></a>Scaricare le librerie client più recente di hello  
Utilizzare hello seguendo le librerie client se si dispone di un ambiente di produzione e richiedono versioni completamente rilasciate e supportate.

[MSOLAP (amd64)](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a>Passaggi successivi
[Connettersi con Excel](analysis-services-connect-excel.md)    
[Stabilire la connessione con Power BI](analysis-services-connect-pbi.md)
