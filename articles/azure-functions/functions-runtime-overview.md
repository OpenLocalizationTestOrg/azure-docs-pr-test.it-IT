---
title: Cenni preliminari sul Runtime di funzioni aaaAzure | Documenti Microsoft
description: Panoramica di hello anteprima di Azure funzioni di Runtime
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a>Panoramica di Runtime di Funzioni di Azure

Hello Azure funzioni di Runtime fornisce un nuovo modo per si tootake vantaggio della semplicità hello e la flessibilità di hello Azure funzioni di programmazione del modello locale. Basato su hello stesso aprire radici di origine come funzioni di Azure, Azure funzioni di Runtime è quasi identica per lo sviluppo esperienza come servizio cloud hello tooprovide di distribuiti in locale.

![Anteprima del runtime di Funzioni di Azure - Portale][1]

Hello Azure funzioni Runtime fornisce un modo per si tooexperience le funzioni di Azure prima del commit toohello cloud. In questo modo, risorse di codice hello che compili quindi è possibile portare toohello cloud quando esegue la migrazione.  runtime Hello apre anche nuove opzioni per l'utente, ad esempio l'utilizzo di potenza di calcolo riserva hello dei processi batch toorun computer locale durante la notte. È anche possibile utilizzare i dispositivi all'interno dell'organizzazione tooconditionally trasmissione dati tooother sistemi, sia in locale e nel cloud hello.

Hello Azure funzioni di Runtime è costituito da due parti:
* Il ruolo di gestione del runtime di Funzioni di Azure
* Il ruolo di lavoro del runtime di Funzioni di Azure

## <a name="azure-functions-management-role"></a>Il ruolo di gestione di Funzioni di Azure

Ruolo di gestione di Azure funzioni Hello fornisce un host per la gestione di hello di funzioni locali. Questo ruolo esegue hello seguenti attività:

* Hosting del portale di gestione di Azure funzioni, hello è hello hello stesso viene visualizzato in hello [portale di Azure](https://portal.azure.com). Questo consente di sviluppare le funzioni in hello stesso modo come si farebbe in hello portale di Azure.
* La distribuzione di funzioni tra più ruoli di lavoro di Funzioni.
* La garanzia di un endpoint di pubblicazione in modo che sia possibile pubblicare direttamente le funzioni da Microsoft Visual Studio.

## <a name="azure-functions-worker-role"></a>Ruolo di lavoro di Funzioni di Azure

i ruoli di lavoro funzioni Hello Azure vengono distribuiti nei contenitori di Windows e si tratta in cui viene eseguito il codice della funzione.  È possibile distribuire più ruoli di lavoro in tutta l'organizzazione e i clienti possono quindi sfruttare potenza di calcolo di riserva.

## <a name="minimum-requirements"></a>Requisiti minimi

tooget introduttiva hello Azure funzioni di Runtime è necessario disporre di un computer con **Windows Server 2016 o Windows 10 creatori Update** con accesso tooa **SQL Server** istanza.

## <a name="next-steps"></a>Passaggi successivi

Installare hello [anteprima di Azure funzioni Runtime](https://aka.ms/azafr)

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
