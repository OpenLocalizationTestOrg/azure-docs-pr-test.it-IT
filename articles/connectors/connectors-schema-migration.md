---
title: aaaHow toomigrate logica App tooschema versione 2015-08-01-preview | Documenti Microsoft
description: "È possibile migrare facilmente la versione di schema più recente logica App toohello. seguendo questa procedura."
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a>Come toomigrate logica App tooschema versione 2015-08-01-preview
toomove logica App toohello nuovo schema esistente, hello seguenti:  

1. Apri l'app logica in hello portale di Azure  
2. Fare clic su Aggiorna schema:
   
   ![Icona API][step1]   
   pagina Aggiorna Schema Hello Visualizza e fornisce un collegamento tooa documento che forniscono informazioni dettagliate sui miglioramenti di hello nel nuovo schema hello: ![icona API][step2]

> [!NOTE]
> Quando si seleziona **Aggiorna Schema**, è di eseguire automaticamente i passaggi della migrazione hello e fornire output di hello codice per l'utente. È possibile utilizzare questo tooupdate la propria definizione, tuttavia, attenersi alle procedure di codifica ottimale, ad esempio quelli descritti nella hello **consigliate** sezione riportata di seguito.
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a>Procedure consigliate per la migrazione la versione di schema più recente logica App toohello:
* Script di migrazione hello copia tooa nuova logica di App - non sovrascrivere hello precedente uno finché non vengono completati l'app migrato hello confermata e test funziona come previsto.
* Testare l'app per la logica **prima** di passare alla fase di produzione.
* Al termine della migrazione, avviare l'aggiornamento del hello di logica App toouse [API gestite](apis-list.md) laddove possibile. Ad esempio, si può iniziare a usare Dropbox 2 anziché Dropbox 1.

## <a name="whats-next"></a>Passaggi successivi
* [Informazioni su come toomanually migrare le app di logica](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






