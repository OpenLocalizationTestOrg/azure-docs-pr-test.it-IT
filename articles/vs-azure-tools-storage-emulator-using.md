---
title: aaaConfiguring e utilizzando hello emulatore di archiviazione con Visual Studio | Documenti Microsoft
description: Configurazione e l'utilizzo di hello emulatore di archiviazione con Visual Studio
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: c8e7996f-6027-4762-806e-614b93131867
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/17/2017
ms.author: kraigb
ms.openlocfilehash: d590f21146c86bcb7bfa6b6164b92c6df5938d5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-hello-storage-emulator-with-visual-studio"></a>Configurazione e l'utilizzo di hello emulatore di archiviazione con Visual Studio
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Panoramica
ambiente di sviluppo di Hello Azure SDK include l'emulatore di archiviazione hello, un'utilità che simula hello Blob, coda e tabella di servizi di archiviazione disponibili in Azure nel computer di sviluppo locale. Se si compila un servizio cloud che utilizza servizi di archiviazione Azure hello o scrive un'applicazione esterna che chiama hello servizi di archiviazione, è possibile testare il codice in locale nell'emulatore di archiviazione hello. Hello Azure Tools per Microsoft Visual Studio consente di integrare gestione dell'emulatore di archiviazione hello Visual Studio. Strumenti di Azure Hello inizializzare database dell'emulatore di archiviazione hello al primo utilizzo, avvia hello servizio dell'emulatore di archiviazione quando si esegue o il debug del codice da Visual Studio e fornisce i dati di accesso in sola lettura toohello archiviazione emulatore tramite hello Azure Storage Explorer.

Per informazioni dettagliate sull'emulatore di archiviazione hello, inclusi i requisiti di sistema e istruzioni di configurazione personalizzata, vedere [hello Usa emulatore di archiviazione di Azure per sviluppo e test](storage/common/storage-use-emulator.md).

> [!NOTE]
> Esistono alcune differenze nelle funzionalità tra simulazione dell'emulatore di archiviazione hello e servizi di archiviazione di Azure hello. Vedere [differenze tra hello emulatore di archiviazione e servizi di archiviazione Azure](storage/common/storage-use-emulator.md) nella documentazione di Azure SDK per informazioni sulle differenze specifiche hello hello.
> 
> 

## <a name="configuring-a-connection-string-for-hello-storage-emulator"></a>Configurazione di una stringa di connessione per l'emulatore di archiviazione hello
emulatore di archiviazione hello tooaccess dal codice all'interno di un ruolo, è opportuno tooconfigure una connessione di stringa dell'emulatore di archiviazione che punti toohello e che può essere successivamente modificati toopoint tooan account di archiviazione di Azure. Una stringa di connessione è in grado di leggere il ruolo all'account di archiviazione di runtime tooconnect tooa un'impostazione di configurazione. Per ulteriori informazioni su come toocreate le stringhe di connessione, vedere [hello configurazione applicazione Azure](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage).

> [!NOTE]
> È possibile ripristinare un account di emulatore di archiviazione toohello riferimento dal codice utilizzando hello **DevelopmentStorageAccount** proprietà. Questo approccio funziona correttamente se si desidera tooaccess hello emulatore di archiviazione dal codice, ma se si prevede di toopublish tooAzure l'applicazione, sarà anche necessario toocreate un tooaccess di stringa di connessione l'account di archiviazione di Azure e modificare il codice toouse che stringa di connessione prima della pubblicazione. Se si passa tra l'account dell'emulatore di archiviazione hello e un account di archiviazione di Azure frequentemente, una stringa di connessione semplificherà questo processo.
> 
> 

## <a name="initializing-and-running-hello-storage-emulator"></a>Inizializzazione ed esecuzione dell'emulatore di archiviazione hello
È possibile specificare che, quando si esegue o eseguire il debug del servizio in Visual Studio, Visual Studio avvia automaticamente emulatore di archiviazione hello. In Esplora soluzioni, aprire il menu di scelta rapida hello per le **Azure** progetto e scegliere **proprietà**. In hello **sviluppo** scheda hello **Avvia emulatore di archiviazione di Azure** scegliere **True** (se non è già impostato un valore toothat).

Hello prima fase di esecuzione o il debug del servizio da Visual Studio, emulatore di archiviazione hello avvia un processo di inizializzazione. Questo processo riserva le porte locali per l'emulatore di archiviazione hello e crea i database dell'emulatore di archiviazione hello. Al termine del processo, questo processo non è necessario toorun nuovamente a meno che non viene eliminato i database dell'emulatore di archiviazione hello.

> [!NOTE]
> A partire dalla versione di giugno 2012 hello di hello Azure Tools, emulatore di archiviazione hello viene eseguito, per impostazione predefinita, in SQL Express LocalDB. Nelle versioni precedenti di strumenti di Azure hello, emulatore di archiviazione hello viene eseguito su un'istanza predefinita di SQL Express 2005 o 2008, che deve essere installato prima di installare hello Azure SDK. È inoltre possibile eseguire l'emulatore di archiviazione hello in un'istanza denominata di SQL Express o un oggetto denominato o l'istanza predefinita di Microsoft SQL Server. Se è necessario tooconfigure hello archiviazione emulatore toorun rispetto a un'istanza diversa istanza predefinita di hello, vedere [hello Usa emulatore di archiviazione di Azure per sviluppo e test](storage/common/storage-use-emulator.md).
> 
> 

emulatore di archiviazione Hello fornisce uno stato di hello tooview dell'interfaccia utente dei servizi di archiviazione locale hello e toostart, arrestare e reimpostarli. Dopo aver avviato il servizio dell'emulatore di archiviazione hello, è possibile visualizzare l'interfaccia utente di hello o Avvia o Arresta servizio hello facendo clic sull'icona di area di notifica hello per hello emulatore di Microsoft Azure nella barra delle applicazioni Windows hello.

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>Visualizzazione dei dati dell'emulatore di archiviazione in Esplora Server
nodo di archiviazione di Azure Hello in Esplora Server consente tooview dati e modifica delle impostazioni per il blob e dati della tabella negli account di archiviazione, tra cui hello emulatore di archiviazione. Per altre informazioni, vedere [Gestire le risorse di archiviazione BLOB di Azure con Storage Explorer (anteprima)](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).

