---
title: Configurazione e uso dell'emulatore di archiviazione con Visual Studio | Documentazione Microsoft
description: Configurazione e uso dell'emulatore di archiviazione con Visual Studio
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
ms.openlocfilehash: f4cd8ccc3b186cf2b4178b7d8a98d8928c705cbc
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="configuring-and-using-the-storage-emulator-with-visual-studio"></a>Configurazione e uso dell'emulatore di archiviazione con Visual Studio
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Panoramica
L'ambiente di sviluppo di Azure SDK include l'emulatore di archiviazione, ovvero un'utilità che simula i servizi BLOB, di coda e di tabella disponibili in Azure nel computer di sviluppo locale. Se si sta compilando un servizio cloud che usa i servizi di archiviazione di Azure o si sta scrivendo una qualsiasi applicazione esterna che chiama i servizi di archiviazione, è possibile testare il codice in locale in relazione all'emulatore di archiviazione. Gli strumenti di Azure per Microsoft Visual Studio integrano la gestione dell'emulatore di archiviazione in Visual Studio. Gli strumenti di Azure inizializzano il database dell'emulatore di archiviazione al primo uso, avviano il servizio dell'emulatore di archiviazione quando si esegue o si sottopone a debug il codice da Visual Studio e forniscono l'accesso di sola lettura ai dati dell'emulatore di archiviazione in Esplora archivi Azure.

Per informazioni dettagliate sull'emulatore di archiviazione, inclusi i requisiti di sistema e le istruzioni per la configurazione personalizzata, vedere [Usare l'emulatore di archiviazione di Azure per sviluppo e test](storage/common/storage-use-emulator.md).

> [!NOTE]
> Le funzionalità della simulazione dell'emulatore di archiviazione e dei servizi di archiviazione di Azure presentano alcune differenze. Per informazioni sulle differenze specifiche, vedere [Differenze tra l'emulatore di archiviazione e i servizi di archiviazione di Azure](storage/common/storage-use-emulator.md) nella documentazione di Azure SDK.
> 
> 

## <a name="configuring-a-connection-string-for-the-storage-emulator"></a>Configurazione di una stringa di connessione per l'emulatore di archiviazione
Per accedere all'emulatore di archiviazione dal codice in esecuzione in un ruolo, è consigliabile configurare una stringa di connessione che punti all'emulatore di archiviazione e che successivamente potrà essere modificata in modo da puntare a un account di archiviazione di Azure. Una stringa di connessione è un'impostazione di configurazione che può essere letta dal ruolo in fase di runtime per connettersi a un account di archiviazione. Per altre informazioni sulla creazione di stringhe di connessione, vedere [Configurazione dell'applicazione Azure con Visual Studio](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage).

> [!NOTE]
> È possibile restituire un riferimento all'account dell'emulatore di archiviazione dal codice con la proprietà **DevelopmentStorageAccount**. Questo approccio produce i risultati desiderati quando si vuole accedere all'emulatore di archiviazione dal codice. Se invece si prevede di distribuire l'applicazione in Azure, sarà necessario creare una stringa di connessione per accedere all'account di archiviazione di Azure e modificare il codice al fine di usare tale stringa di connessione prima di effettuare la pubblicazione. Se si passa frequentemente dall'account dell'emulatore di archiviazione a un account di archiviazione di Azure, una stringa di connessione semplificherà questo processo.
> 
> 

## <a name="initializing-and-running-the-storage-emulator"></a>Inizializzazione ed esecuzione dell'emulatore di archiviazione
È possibile specificare che quando si esegue o si sottopone a debug il servizio in Visual Studio, quest'ultimo avvii automaticamente l'emulatore di archiviazione. In Esplora soluzioni aprire il menu di scelta rapida per il progetto **Azure** e scegliere **Proprietà**. Nella scheda **Sviluppo** nell'elenco **Avvia l'emulatore di archiviazione di Azure** scegliere **True**, se questo valore non è già impostato.

In occasione della prima esecuzione o del primo debug del servizio da Visual Studio, l'emulatore di archiviazione avvia un processo di inizializzazione. Questo processo riserva le porte locali per l'emulatore di archiviazione e crea il relativo database. Una volta completato, questo processo non deve più essere eseguito a meno che non venga eliminato il database dell'emulatore di archiviazione.

> [!NOTE]
> A partire dalla versione di giugno 2012 di Strumenti di Azure, l'emulatore di archiviazione viene eseguito per impostazione predefinita in SQL Express LocalDB. Nelle versioni precedenti di Strumenti di Azure, l'emulatore di archiviazione viene eseguito su un'istanza predefinita di SQL Express 2005 o 2008 che deve essere installata prima di Azure SDK. L'emulatore di archiviazione può essere eseguito anche su un'istanza denominata di SQL Express o su un'istanza denominata o predefinita di Microsoft SQL Server. Se è necessario configurare l'emulatore di archiviazione per l'esecuzione con un'istanza diversa da quella predefinita, vedere [Usare l'emulatore di archiviazione di Azure per sviluppo e test](storage/common/storage-use-emulator.md).
> 
> 

L'emulatore di archiviazione fornisce un'interfaccia utente per visualizzare lo stato dei servizi di archiviazione locale, nonché per avviarli, arrestarli e reimpostarli. Una volta avviato il servizio dell'emulatore di archiviazione, è possibile visualizzare l'interfaccia utente oppure avviare o arrestare il servizio facendo clic con il pulsante destro del mouse sull'icona dell'area di notifica relativa a Emulatore di Microsoft Azure sulla barra delle applicazioni di Windows.

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>Visualizzazione dei dati dell'emulatore di archiviazione in Esplora Server
Il nodo Archiviazione di Azure in Esplora Server consente di visualizzare i dati e modificare le impostazioni per i dati di BLOB e tabelle negli account di archiviazione, incluso l'emulatore di archiviazione. Per altre informazioni, vedere [Gestire le risorse di archiviazione BLOB di Azure con Storage Explorer (anteprima)](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).

