---
title: Panoramica di aaaAzure Cloud Shell (anteprima) | Documenti Microsoft
description: Panoramica di hello Shell di Cloud di Azure.
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a>Panoramica di Azure Cloud Shell (anteprima)
Azure Cloud Shell è una shell interattiva accessibile dal browser per la gestione delle risorse di Azure.

![](media/overview-pic.png)

## <a name="features"></a>Funzionalità
### <a name="browser-based-shell-experience"></a>Esperienza di shell basata su browser
Cloud Shell Abilita tooa basate su browser della riga di comando l'esperienza di accesso compilato con le attività di gestione di Azure presente. Sfruttare toowork Shell Cloud illimitata da un computer locale in modo che solo i cloud hello può fornire.

### <a name="pre-configured-azure-workstation"></a>Workstation Azure preconfigurata
In Cloud Shell sono preinstallati i più diffusi strumenti da riga di comando e il supporto per linguaggi per poter lavorare più velocemente.

[Visualizzazione hello completo di strumenti elenco per Shell di Cloud di Azure.](features.md#tools)

### <a name="automatic-authentication"></a>Autenticazione automatica
Shell cloud in modo sicuro autentica automaticamente in ogni sessione per le risorse tooyour accesso immediato tramite hello CLI di Azure 2.0.

### <a name="connect-your-azure-file-storage"></a>Connettersi ad Archiviazione file di Azure
Cloud Shell macchine sono temporanee e pertanto richiedono un toobe di condivisione file di Azure montata come `clouddrive` toopersist $Home directory.
Primo avvio della Shell Cloud richiede toocreate che un gruppo di risorse, account di archiviazione e della condivisione file per conto dell'utente. Questo passaggio è occasionale e verrà automaticamente collegato per tutte le sessioni. 

#### <a name="create-new-storage"></a>Creare una nuova risorsa di archiviazione
![](media/basic-storage.png)

Viene creato per conto dell'utente un account di archiviazione con ridondanza locale, ovvero LRS, con una condivisione file di Azure contenente un'immagine del disco da 5 GB. condivisione di file Hello collega come `clouddrive` per file condividono l'interazione con l'immagine del disco hello viene utilizzato toosync e mantenere la directory $Home. Vengono applicati i normali costi di archiviazione.

Verranno create tre risorse per conto dell'utente:
1. Gruppo di risorse denominato: `cloud-shell-storage-<region>`
2. Account di archiviazione denominato: `cs<uniqueGuid>`
3. Condivisione file denominata: `cs-<user>-<domain>-com-uniqueGuid`

> [!Note]
> Tutti i file della directory $Home, come le chiavi SSH, vengono mantenuti nell'immagine del disco utente archiviato nella condivisione file montata. Applicare le procedure consigliate quando si salvano i file nella directory $Home e nella condivisione file montata.

#### <a name="use-existing-resources"></a>Usare le risorse esistenti
![](media/advanced-storage.png)

Un'opzione avanzata viene inoltre fornita per consentire di tooassociate esistente risorse tooCloud Shell. Quando verrà visualizzata con richiesta di installazione di hello archiviazione, fare clic su "Show advanced settings" tooselect ulteriori opzioni. I menu a discesa vengono filtrati per le aree Cloud Shell assegnate e gli account di archiviazione ridondanti a livello locale o globale.

[Altre informazioni sull'archiviazione di Cloud Shell, l'aggiornamento delle condivisioni file e il caricamento e download di file.] (persisting-shell-storage.md)

## <a name="concepts"></a>Concetti
* Cloud Shell viene eseguito in un computer temporaneo disponibile per ogni sessione e per ogni utente
* Il timeout di Cloud Shell si verifica dopo 20 minuti senza attività interattiva
* Cloud Shell è accessibile solo con una condivisione di file collegata
* A Cloud Shell viene assegnato un computer per ogni account utente
* Vengono impostate le autorizzazioni per un normale utente Linux

[Altre informazioni su tutte le funzionalità Cloud Shell.](features.md)

## <a name="examples"></a>esempi
* Creare o modificare gli script tooautomate gestione di Azure
* Gestire le risorse tramite il portale di Azure e l'interfaccia della riga di comando di Azure 2.0 contemporaneamente
* Effettuare il test drive dell'interfaccia della riga di comando di Azure 2.0

[Provare questi esempi in avvio rapido di hello Cloud Shell.](quickstart.md)

## <a name="pricing"></a>Prezzi
macchina Hello Shell Cloud di hosting è disponibile, con un prerequisito di un file di Azure montato condividere toopersist $Home directory. Vengono applicati i normali costi di archiviazione.

## <a name="supported-browsers"></a>Browser supportati
Cloud Shell è consigliato per Chrome, Microsoft Edge e Safari. Sebbene Shell Cloud è supportata per Chrome, Firefox, Safari, Internet Explorer e bordo, Cloud Shell è le impostazioni del browser toospecific soggetto.

## <a name="troubleshooting"></a>Risoluzione dei problemi
1. Quando si utilizza una sottoscrizione di Azure Active Directory, non è possibile creare Archiviazione scadenza tooError: DisallowedOperation 400. tooresolve, utilizzare una sottoscrizione di Azure in grado di creare le risorse di archiviazione. Le sottoscrizioni di Active Directory è toocreate non in grado di risorse di Azure.

Per le limitazioni note specifiche, vedere le [limitazioni di Cloud Shell](limitations.md).
