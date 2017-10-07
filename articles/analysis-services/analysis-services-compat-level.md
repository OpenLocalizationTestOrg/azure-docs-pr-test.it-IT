---
title: "livello di compatibilità aaaData modello in Analysis Services di Azure | Documenti Microsoft"
description: "Informazioni sul livello di compatibilità del modello di dati tabulari."
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
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Livello di compatibilità per i modelli tabulari di Analysis Services

*Livello di compatibilità* fa riferimento toorelease specifici comportamenti nel motore di Analysis Services hello. Livello di compatibilità toohello modifiche in genere coincide con le versioni principali di SQL Server. Queste modifiche vengono inoltre implementate in entrambe le piattaforme analogia toomaintain Azure Analysis Services. Le modifiche del livello di compatibilità influiscono anche sulle funzionalità disponibili nei modelli tabulari. Ad esempio, DirectQuery e i metadati degli oggetti tabulari sono implementazioni diverse in base al livello di compatibilità hello. 

Azure Analysis Services supporta modelli tabulari con livelli di compatibilità 1200 e 1400 di hello.

livello di compatibilità più recente di Hello è 1400. Questo livello corrisponde a SQL Server 2017 Analysis Services. Le funzionalità principali nel livello di compatibilità 1400 hello includono:

*  Nuova infrastruttura per la connettività dati e per l'importazione in modelli tabulari con il supporto delle API TOM e degli script TMSL. Questa nuova funzionalità consente il supporto per origini dati aggiuntive, ad esempio l'archiviazione BLOB di Azure.
*  Funzionalità di trasformazione e mashup dei dati tramite Recupera dati ed espressioni M.
*  Le misure supportano una proprietà Espressione di righe di dettaglio con un'espressione DAX. Questa proprietà consente di strumenti client quali Microsoft Excel toodrill toodetailed dati da un report aggregato. Ad esempio, quando gli utenti di visualizzare le vendite totali per una regione e un mese, è possibile visualizzare dettagli dell'ordine hello associata. 
*  Sicurezza a livello di oggetto per la tabella e colonna i nomi di inoltre toohello dati all'interno di essi.
*  Supporto migliorato per le gerarchie incomplete.
*  Miglioramenti per prestazioni e monitoraggio.
  
## <a name="set-compatibility-level"></a>Impostare il livello di compatibilità 
 Quando si crea un nuovo progetto di modello tabulare in SSDT, è possibile specificare il livello di compatibilità di hello in hello **progettazione di modelli tabulari** finestra di dialogo. 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 Se si seleziona hello **non visualizzare più questo messaggio** opzione, il livello di compatibilità hello specificato come valore predefinito di hello di utilizzare tutti i progetti successivi. È possibile modificare a livello di compatibilità predefinito hello in SSDT in **strumenti** > **opzioni**.  
  
 un progetto di modello tabulare esistente in SSDT, hello set tooupgrade **livello di compatibilità** proprietà nel modello hello **proprietà** finestra. Tenere presente, l'aggiornamento a livello di compatibilità hello è irreversibile.
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>Controllare il livello di compatibilità per un database con modello tabulare in SQL Server Management Studio 
 In SQL Server Management Studio, fare clic sul nome del database hello > **proprietà** > **livello di compatibilità**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Controllare il livello di compatibilità supportato per un server in SQL Server Management Studio  
 In SQL Server Management Studio, fare clic sul nome del server hello > **proprietà** > **livello di compatibilità supportato**.  
  
 Questa proprietà specifica hello massimo livello di compatibilità di un database che verrà eseguiti nel server di hello (escluso preview). Impossibile modificare il livello di compatibilità di Hello è supportato.  

## <a name="next-steps"></a>Passaggi successivi
  [Creare un modello nel portale di Azure](analysis-services-create-model-portal.md)   
  [Gestire Analysis Services](analysis-services-manage.md)  
