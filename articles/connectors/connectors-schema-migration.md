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
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-logic-apps-to-schema-version-2015-08-01-preview"></a><span data-ttu-id="cd8e5-104">Come eseguire la migrazione di app per la logica alla versione dello schema 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="cd8e5-104">How to migrate logic apps to schema version 2015-08-01-preview</span></span>
<span data-ttu-id="cd8e5-105">Per spostare le app per la logica esistenti nel nuovo schema, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="cd8e5-105">To move your existing logic apps to the new schema, do the following:</span></span>  

1. <span data-ttu-id="cd8e5-106">Aprire l'app per la logica nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd8e5-106">Open your logic app in the Azure portal</span></span>  
2. <span data-ttu-id="cd8e5-107">Fare clic su Aggiorna schema:</span><span class="sxs-lookup"><span data-stu-id="cd8e5-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="cd8e5-108">![Icona API][step1] </span><span class="sxs-lookup"><span data-stu-id="cd8e5-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="cd8e5-109">Viene visualizzata la pagina Aggiorna schema, con un collegamento a un documento che fornisce dettagli sui miglioramenti disponibili nel nuovo schema: ![Icona API][step2]</span><span class="sxs-lookup"><span data-stu-id="cd8e5-109">The Update Schema page displays and provides a link to a document that provide details on the improvements in the new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="cd8e5-110">Quando si seleziona **Aggiorna schema**, vengono eseguiti automaticamente i passaggi della migrazione e viene generato l'output del codice.</span><span class="sxs-lookup"><span data-stu-id="cd8e5-110">When you select **Update Schema**, we automatically run the migration steps and provide the code output for you.</span></span> <span data-ttu-id="cd8e5-111">È possibile usare questi elementi per aggiornare la definizione. Assicurarsi, tuttavia, di seguire le procedure di codifica consigliate, ad esempio quelle indicate nella **sezione seguente**.</span><span class="sxs-lookup"><span data-stu-id="cd8e5-111">You can use this to update your definition, however, ensure you follow good coding practices such as those outlined in the **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-to-the-latest-schema-version"></a><span data-ttu-id="cd8e5-112">Procedure consigliate durante la migrazione di app per la logica alla versione più recente dello schema</span><span class="sxs-lookup"><span data-stu-id="cd8e5-112">Best practices when migrating your Logic apps to the latest schema version:</span></span>
* <span data-ttu-id="cd8e5-113">Copiare lo script di cui è stata eseguita la migrazione in una nuova app per la logica. Non sovrascrivere l'app precedente fino a quando non è stato completato il test ed è stato confermato il corretto funzionamento dell'app di cui è stata eseguita la migrazione.</span><span class="sxs-lookup"><span data-stu-id="cd8e5-113">Copy the migrated script to a new Logic App - don't overwrite the old one until you've completed your testing and confirmed the migrated app works as expected.</span></span>
* <span data-ttu-id="cd8e5-114">Testare l'app per la logica **prima** di passare alla fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="cd8e5-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="cd8e5-115">Al termine della migrazione, avviare l'aggiornamento delle app per la logica per usare le [API gestite](apis-list.md), quando è possibile.</span><span class="sxs-lookup"><span data-stu-id="cd8e5-115">After migration completes, start updating your Logic apps to use the [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="cd8e5-116">Ad esempio, si può iniziare a usare Dropbox 2 anziché Dropbox 1.</span><span class="sxs-lookup"><span data-stu-id="cd8e5-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="cd8e5-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd8e5-117">What's next</span></span>
* [<span data-ttu-id="cd8e5-118">Informazioni su come eseguire manualmente la migrazione delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="cd8e5-118">Learn how to manually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






