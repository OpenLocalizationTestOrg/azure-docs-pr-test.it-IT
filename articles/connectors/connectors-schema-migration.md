---
title: Come eseguire la migrazione di app per la logica alla versione dello schema 2015-08-01-preview | Documentazione Microsoft
description: "È possibile eseguire facilmente la migrazione di app per la logica alla versione più recente dello schema, seguendo questa procedura."
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
ms.openlocfilehash: a5a73a9f124e5339b61dbc49021444a208a471f0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-migrate-logic-apps-to-schema-version-2015-08-01-preview"></a>Come eseguire la migrazione di app per la logica alla versione dello schema 2015-08-01-preview
Per spostare le app per la logica esistenti nel nuovo schema, seguire questa procedura:  

1. Aprire l'app per la logica nel portale di Azure.  
2. Fare clic su Aggiorna schema:
   
   ![Icona API][step1]   
   Viene visualizzata la pagina Aggiorna schema, con un collegamento a un documento che fornisce dettagli sui miglioramenti disponibili nel nuovo schema: ![Icona API][step2]

> [!NOTE]
> Quando si seleziona **Aggiorna schema**, vengono eseguiti automaticamente i passaggi della migrazione e viene generato l'output del codice. È possibile usare questi elementi per aggiornare la definizione. Assicurarsi, tuttavia, di seguire le procedure di codifica consigliate, ad esempio quelle indicate nella **sezione seguente**.
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-to-the-latest-schema-version"></a>Procedure consigliate durante la migrazione di app per la logica alla versione più recente dello schema
* Copiare lo script di cui è stata eseguita la migrazione in una nuova app per la logica. Non sovrascrivere l'app precedente fino a quando non è stato completato il test ed è stato confermato il corretto funzionamento dell'app di cui è stata eseguita la migrazione.
* Testare l'app per la logica **prima** di passare alla fase di produzione.
* Al termine della migrazione, avviare l'aggiornamento delle app per la logica per usare le [API gestite](apis-list.md), quando è possibile. Ad esempio, si può iniziare a usare Dropbox 2 anziché Dropbox 1.

## <a name="whats-next"></a>Passaggi successivi
* [Informazioni su come eseguire manualmente la migrazione delle app per la logica](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






