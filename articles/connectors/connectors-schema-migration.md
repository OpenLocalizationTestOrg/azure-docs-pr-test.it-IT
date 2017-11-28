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
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a><span data-ttu-id="345dd-104">Come toomigrate logica App tooschema versione 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="345dd-104">How toomigrate logic apps tooschema version 2015-08-01-preview</span></span>
<span data-ttu-id="345dd-105">toomove logica App toohello nuovo schema esistente, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="345dd-105">toomove your existing logic apps toohello new schema, do hello following:</span></span>  

1. <span data-ttu-id="345dd-106">Apri l'app logica in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="345dd-106">Open your logic app in hello Azure portal</span></span>  
2. <span data-ttu-id="345dd-107">Fare clic su Aggiorna schema:</span><span class="sxs-lookup"><span data-stu-id="345dd-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="345dd-108">![Icona API][step1] </span><span class="sxs-lookup"><span data-stu-id="345dd-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="345dd-109">pagina Aggiorna Schema Hello Visualizza e fornisce un collegamento tooa documento che forniscono informazioni dettagliate sui miglioramenti di hello nel nuovo schema hello: ![icona API][step2]</span><span class="sxs-lookup"><span data-stu-id="345dd-109">hello Update Schema page displays and provides a link tooa document that provide details on hello improvements in hello new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="345dd-110">Quando si seleziona **Aggiorna Schema**, è di eseguire automaticamente i passaggi della migrazione hello e fornire output di hello codice per l'utente.</span><span class="sxs-lookup"><span data-stu-id="345dd-110">When you select **Update Schema**, we automatically run hello migration steps and provide hello code output for you.</span></span> <span data-ttu-id="345dd-111">È possibile utilizzare questo tooupdate la propria definizione, tuttavia, attenersi alle procedure di codifica ottimale, ad esempio quelli descritti nella hello **consigliate** sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="345dd-111">You can use this tooupdate your definition, however, ensure you follow good coding practices such as those outlined in hello **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a><span data-ttu-id="345dd-112">Procedure consigliate per la migrazione la versione di schema più recente logica App toohello:</span><span class="sxs-lookup"><span data-stu-id="345dd-112">Best practices when migrating your Logic apps toohello latest schema version:</span></span>
* <span data-ttu-id="345dd-113">Script di migrazione hello copia tooa nuova logica di App - non sovrascrivere hello precedente uno finché non vengono completati l'app migrato hello confermata e test funziona come previsto.</span><span class="sxs-lookup"><span data-stu-id="345dd-113">Copy hello migrated script tooa new Logic App - don't overwrite hello old one until you've completed your testing and confirmed hello migrated app works as expected.</span></span>
* <span data-ttu-id="345dd-114">Testare l'app per la logica **prima** di passare alla fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="345dd-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="345dd-115">Al termine della migrazione, avviare l'aggiornamento del hello di logica App toouse [API gestite](apis-list.md) laddove possibile.</span><span class="sxs-lookup"><span data-stu-id="345dd-115">After migration completes, start updating your Logic apps toouse hello [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="345dd-116">Ad esempio, si può iniziare a usare Dropbox 2 anziché Dropbox 1.</span><span class="sxs-lookup"><span data-stu-id="345dd-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="345dd-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="345dd-117">What's next</span></span>
* [<span data-ttu-id="345dd-118">Informazioni su come toomanually migrare le app di logica</span><span class="sxs-lookup"><span data-stu-id="345dd-118">Learn how toomanually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






