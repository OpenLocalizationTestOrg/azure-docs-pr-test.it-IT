---
title: Risoluzione dei problemi relativi allo strumento Importazione/Esportazione di Azure | Documentazione Microsoft
description: Informazioni su alcuni problemi comuni rilevati durante l'uso dello strumento Importazione/Esportazione di Azure e su come gestirli.
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
ms.openlocfilehash: 7bfda602dbc0ea47828a7c9243b8b9b09ec78432
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-the-azure-importexport-tool"></a><span data-ttu-id="de874-103">Risoluzione dei problemi relativi allo strumento di importazione/esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="de874-103">Troubleshooting the Azure Import/Export Tool</span></span>
<span data-ttu-id="de874-104">Lo strumento Importazione/Esportazione di Microsoft Azure restituisce messaggi di errore in caso di problemi.</span><span class="sxs-lookup"><span data-stu-id="de874-104">The Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="de874-105">Questo argomento elenca alcuni problemi comuni in cui possono incorrere gli utenti.</span><span class="sxs-lookup"><span data-stu-id="de874-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="de874-106">Cosa fare se una sessione di copia non viene completata correttamente?</span><span class="sxs-lookup"><span data-stu-id="de874-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="de874-107">Quando una sessione di copia non viene completata correttamente, sono disponibili due opzioni.</span><span class="sxs-lookup"><span data-stu-id="de874-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="de874-108">Se l'errore non è irreversibile, ad esempio se la condivisione di rete è stata offline per un breve periodo e ora è tornata online, è possibile riprendere la sessione di copia.</span><span class="sxs-lookup"><span data-stu-id="de874-108">If the error is retryable, for example if the network share was offline for a short period and now is back online, you can resume the copy session.</span></span> <span data-ttu-id="de874-109">Se l'errore è irreversibile, ad esempio se è stata specificata una directory del file di origine errata nei parametri della riga di comando, è necessario interrompere la sessione di copia.</span><span class="sxs-lookup"><span data-stu-id="de874-109">If the error is not retryable, for example if you specified the wrong source file directory in the command line parameters, you need to abort the copy session.</span></span> <span data-ttu-id="de874-110">Vedere [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione) per altre informazioni su come riprendere e interrompere le sessioni di copia.</span><span class="sxs-lookup"><span data-stu-id="de874-110">See [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="de874-111">Non è possibile riprendere o interrompere una sessione di copia.</span><span class="sxs-lookup"><span data-stu-id="de874-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="de874-112">Se la sessione di copia è la prima sessione di copia per un'unità, dovrebbe essere visualizzato un messaggio di errore che indica che "la prima sessione di copia non può essere ripresa o interrotta".</span><span class="sxs-lookup"><span data-stu-id="de874-112">If the copy session is the first copy session for a drive, then the error message should state: "The first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="de874-113">In questo caso, è possibile eliminare il file journal precedente e rieseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="de874-113">In this case, you can delete the old journal file and rerun the command.</span></span>  
  
 <span data-ttu-id="de874-114">Se una sessione di copia non è la prima per un'unità, può essere sempre ripresa o interrotta.</span><span class="sxs-lookup"><span data-stu-id="de874-114">If a copy session is not the first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-the-journal-file-can-i-still-create-the-job"></a><span data-ttu-id="de874-115">È possibile creare il processo anche se il file journal è andato perso?</span><span class="sxs-lookup"><span data-stu-id="de874-115">I lost the journal file, can I still create the job?</span></span>  
 <span data-ttu-id="de874-116">Il file journal per un'unità contiene le informazioni complete sulla copia dei dati in questa unità, è necessario per aggiungere altri file all'unità e verrà usato per creare un processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="de874-116">The journal file for a drive contains the complete information of copying data to this drive, and it is needed to add more files to the drive and will be used to create an import job.</span></span> <span data-ttu-id="de874-117">Se il file journal è andato perso, sarà necessario ripetere tutte le sessioni di copia per l'unità.</span><span class="sxs-lookup"><span data-stu-id="de874-117">If the journal file is lost, you will have to redo all the copy sessions for the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="de874-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="de874-118">Next steps</span></span>
 
* [<span data-ttu-id="de874-119">Configurazione dello strumento Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="de874-119">Setting up the azure import/export tool</span></span>](../storage-import-export-tool-setup-v1.md)   
* <span data-ttu-id="de874-120">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="de874-120">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import-v1.md)</span></span>   
* <span data-ttu-id="de874-121">[Reviewing job status with copy log files](../storage-import-export-tool-reviewing-job-status-v1.md) (Revisione dello stato dei processi con i file di log di copia)</span><span class="sxs-lookup"><span data-stu-id="de874-121">[Reviewing job status with copy log files](../storage-import-export-tool-reviewing-job-status-v1.md)</span></span>   
* [<span data-ttu-id="de874-122">Riparazione di un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="de874-122">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* <span data-ttu-id="de874-123">[Repairing an export job](../storage-import-export-tool-repairing-an-export-job-v1.md) (Riparazione di un processo di esportazione)</span><span class="sxs-lookup"><span data-stu-id="de874-123">[Repairing an export job](../storage-import-export-tool-repairing-an-export-job-v1.md)</span></span>
