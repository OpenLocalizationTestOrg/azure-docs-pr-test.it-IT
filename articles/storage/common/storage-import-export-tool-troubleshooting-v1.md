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
# <a name="troubleshooting-hello-azure-importexport-tool"></a>Risoluzione dei problemi hello strumento di importazione/esportazione di Azure
Se si verificano problemi, Hello dello strumento di importazione/esportazione di Microsoft Azure restituisce messaggi di errore. Questo argomento elenca alcuni problemi comuni in cui possono incorrere gli utenti.  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>Cosa fare se una sessione di copia non viene completata correttamente?  
 Quando una sessione di copia non viene completata correttamente, sono disponibili due opzioni.  
  
 Se l'errore hello è irreversibile, ad esempio, se la condivisione di rete hello era offline per un breve periodo e adesso è online, è possibile riprendere la sessione di copia hello. Se l'errore hello non è irreversibile, ad esempio se si specifica directory del file di origine errato hello nei parametri della riga di comando hello, è necessario tooabort sessione di copia hello. Vedere [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione) per altre informazioni su come riprendere e interrompere le sessioni di copia.  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>Non è possibile riprendere o interrompere una sessione di copia.  
 Se la sessione di copia hello hello prima sessione di copia per un'unità, il messaggio di errore hello deve indicare: "hello prima sessione di copia non può essere ripreso o interrotta." In questo caso, è possibile eliminare il file journal precedente hello e rieseguire il comando di hello.  
  
 Se una sessione di copia non è hello primo per un'unità, può sempre essere ripresa o interrotta.  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a>Ho perso file journal hello, è possibile creare il processo di hello?  
 il file journal Hello per un'unità contiene informazioni complete di hello di copia di unità di dati toothis, e viene tooadd necessari ulteriori unità toohello per i file e sarà toocreate utilizzato un processo di importazione. Se il file journal hello viene perduto, sarà necessario tooredo tutte le sessioni di copia hello per unità hello.  
  
## <a name="next-steps"></a>Passaggi successivi
 
* [Impostazione dello strumento di importazione/esportazione di azure hello](../storage-import-export-tool-setup-v1.md)   
* [Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)   
* [Reviewing job status with copy log files](../storage-import-export-tool-reviewing-job-status-v1.md) (Revisione dello stato dei processi con i file di log di copia)   
* [Riparazione di un processo di importazione](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Repairing an export job](../storage-import-export-tool-repairing-an-export-job-v1.md) (Riparazione di un processo di esportazione)
