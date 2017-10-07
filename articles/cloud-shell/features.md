---
title: "funzionalità della Shell di Cloud (anteprima) aaaAzure | Documenti Microsoft"
description: "Panoramica delle funzionalità di Azure Cloud Shell"
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a>Funzionalità e strumenti per Azure Cloud Shell
Shell Cloud Azure è un toomanage esperienza di shell basata su browser e sviluppare le risorse di Azure.

Cloud Shell offre un browser accessibile, preconfigurato esperienza di shell per la gestione delle risorse di Azure senza il sovraccarico di hello di installazione, il controllo delle versioni e gestire un computer manualmente.

Cloud Shell esegue il provisioning delle macchine sulla base delle richieste e di conseguenza lo stato della macchina non viene mantenuto tra le sessioni. Poiché Cloud Shell è pensato per le sessioni interattive, le shell vengono terminate automaticamente dopo 20 minuti di inattività della shell stessa.

## <a name="bash-in-cloud-shell"></a>Bash in Cloud Shell
### <a name="tools"></a>Strumenti
|Categoria   |Nome   |
|---|---|
|Interprete shell di Linux|Bash<br> sh               |
|Strumenti di Azure            |[Interfaccia della riga di comando di Azure 2.0](https://github.com/Azure/azure-cli) e [1.0](https://github.com/Azure/azure-xplat-cli)<br> [AzCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Batch Shipyard](https://github.com/Azure/batch-shipyard)     |
|Editor di testo           |vim<br> nano<br> emacs       |
|Controllo del codice sorgente         |git                    |
|Strumenti di compilazione            |make<br> maven<br> npm<br> pip         |
|Contenitori             |[Interfaccia della riga di comando Docker](https://github.com/docker/cli)/[Computer Docker](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Bozza](https://github.com/Azure/draft)<br> [Interfaccia della riga di comando DC/OS](https://github.com/dcos/dcos-cli)         |
|Database              |Client MySQL<br> Client PostgreSql<br> [Utilità sqlcmd](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli) |
|Altre                  |Client iPython<br> [Interfaccia della riga di comando Cloud Foundry](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a>Supporto per le lingue
|Lingua   |Versione   |
|---|---|
|.NET       |1.01       |
|Go         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|Python     |2.7 e 3.5 (impostazione predefinita)|

## <a name="secure-automatic-authentication"></a>Autenticazione automatica sicura
Shell cloud in modo sicuro e automaticamente autentica account di accesso per hello CLI di Azure 2.0.

## <a name="azure-files-persistence"></a>Persistenza di File di Azure
Poiché Cloud Shell viene allocato su base richiesta usando un computer temporaneo, i file esterni a $Home e lo stato del computer non sono mantenuti tra le sessioni.
file toopersist tra le sessioni, si interromperanno Shell Cloud tramite l'aggiunta di un file di Azure condividono primo avvio.
Al termine, Cloud Shell assocerà automaticamente lo spazio di archiviazione per tutte le sessioni future.

[Ulteriori informazioni sul collegamento di condivisioni di file di Azure tooCloud Shell.](persisting-shell-storage.md)

## <a name="next-steps"></a>Passaggi successivi
[Avvio rapido di Cloud Shell](quickstart.md) <br>
[Informazioni sull'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/) <br>