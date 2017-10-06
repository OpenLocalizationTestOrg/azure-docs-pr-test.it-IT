---
title: hello aaaTroubleshooting strumento di importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su alcuni dei problemi comuni di hello visualizzati quando si utilizza lo strumento di importazione/esportazione di Azure hello e come toohandle li.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a><span data-ttu-id="0cb09-103">Risoluzione dei problemi hello strumento di importazione/esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0cb09-103">Troubleshooting hello Azure Import/Export Tool</span></span>
<span data-ttu-id="0cb09-104">Se si verificano problemi, Hello dello strumento di importazione/esportazione di Microsoft Azure restituisce messaggi di errore.</span><span class="sxs-lookup"><span data-stu-id="0cb09-104">hello Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="0cb09-105">Questo argomento elenca alcuni problemi comuni in cui possono incorrere gli utenti.</span><span class="sxs-lookup"><span data-stu-id="0cb09-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="0cb09-106">Cosa fare se una sessione di copia non viene completata correttamente?</span><span class="sxs-lookup"><span data-stu-id="0cb09-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="0cb09-107">Quando una sessione di copia non viene completata correttamente, sono disponibili due opzioni.</span><span class="sxs-lookup"><span data-stu-id="0cb09-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="0cb09-108">Se l'errore hello è irreversibile, ad esempio, se la condivisione di rete hello era offline per un breve periodo e adesso è online, è possibile riprendere la sessione di copia hello.</span><span class="sxs-lookup"><span data-stu-id="0cb09-108">If hello error is retryable, for example if hello network share was offline for a short period and now is back online, you can resume hello copy session.</span></span> <span data-ttu-id="0cb09-109">Se l'errore hello non è irreversibile, ad esempio se si specifica directory del file di origine errato hello nei parametri della riga di comando hello, è necessario tooabort sessione di copia hello.</span><span class="sxs-lookup"><span data-stu-id="0cb09-109">If hello error is not retryable, for example if you specified hello wrong source file directory in hello command line parameters, you need tooabort hello copy session.</span></span> <span data-ttu-id="0cb09-110">Vedere [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione) per altre informazioni su come riprendere e interrompere le sessioni di copia.</span><span class="sxs-lookup"><span data-stu-id="0cb09-110">See [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="0cb09-111">Non è possibile riprendere o interrompere una sessione di copia.</span><span class="sxs-lookup"><span data-stu-id="0cb09-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="0cb09-112">Se la sessione di copia hello hello prima sessione di copia per un'unità, il messaggio di errore hello deve indicare: "hello prima sessione di copia non può essere ripreso o interrotta."</span><span class="sxs-lookup"><span data-stu-id="0cb09-112">If hello copy session is hello first copy session for a drive, then hello error message should state: "hello first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="0cb09-113">In questo caso, è possibile eliminare il file journal precedente hello e rieseguire il comando di hello.</span><span class="sxs-lookup"><span data-stu-id="0cb09-113">In this case, you can delete hello old journal file and rerun hello command.</span></span>  
  
 <span data-ttu-id="0cb09-114">Se una sessione di copia non è hello primo per un'unità, può sempre essere ripresa o interrotta.</span><span class="sxs-lookup"><span data-stu-id="0cb09-114">If a copy session is not hello first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a><span data-ttu-id="0cb09-115">Ho perso file journal hello, è possibile creare il processo di hello?</span><span class="sxs-lookup"><span data-stu-id="0cb09-115">I lost hello journal file, can I still create hello job?</span></span>  
 <span data-ttu-id="0cb09-116">il file journal Hello per un'unità contiene informazioni complete di hello di copia di unità di dati toothis, e viene tooadd necessari ulteriori unità toohello per i file e sarà toocreate utilizzato un processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="0cb09-116">hello journal file for a drive contains hello complete information of copying data toothis drive, and it is needed tooadd more files toohello drive and will be used toocreate an import job.</span></span> <span data-ttu-id="0cb09-117">Se il file journal hello viene perduto, sarà necessario tooredo tutte le sessioni di copia hello per unità hello.</span><span class="sxs-lookup"><span data-stu-id="0cb09-117">If hello journal file is lost, you will have tooredo all hello copy sessions for hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="0cb09-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0cb09-118">Next steps</span></span>
 
* [<span data-ttu-id="0cb09-119">Impostazione dello strumento di importazione/esportazione di azure hello</span><span class="sxs-lookup"><span data-stu-id="0cb09-119">Setting up hello azure import/export tool</span></span>](../storage-import-export-tool-setup-v1.md)   
* <span data-ttu-id="0cb09-120">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="0cb09-120">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import-v1.md)</span></span>   
* <span data-ttu-id="0cb09-121">[Reviewing job status with copy log files](../storage-import-export-tool-reviewing-job-status-v1.md) (Revisione dello stato dei processi con i file di log di copia)</span><span class="sxs-lookup"><span data-stu-id="0cb09-121">[Reviewing job status with copy log files](../storage-import-export-tool-reviewing-job-status-v1.md)</span></span>   
* [<span data-ttu-id="0cb09-122">Riparazione di un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="0cb09-122">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* <span data-ttu-id="0cb09-123">[Repairing an export job](../storage-import-export-tool-repairing-an-export-job-v1.md) (Riparazione di un processo di esportazione)</span><span class="sxs-lookup"><span data-stu-id="0cb09-123">[Repairing an export job](../storage-import-export-tool-repairing-an-export-job-v1.md)</span></span>
