---
title: App Estensioni - Azure AD B2C | Microsoft Docs
description: Ripristino hello b2c-estensioni-app
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a>Azure AD B2C: app Estensioni

Quando viene creata una directory di Azure Active Directory B2C, un'app denominata `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` viene automaticamente creato all'interno di hello nuova directory. Questa app, cui viene fatto riferimento tooas hello **b2c-estensioni-app**, è visibile in *registrazioni di App*. Viene utilizzato da hello Azure Active Directory B2C servizio toostore informazioni gli utenti e gli attributi personalizzati. Se l'applicazione hello viene eliminato, Azure AD B2C non funzionerà correttamente e ne sarà interessato nell'ambiente di produzione.

> [!IMPORTANT]
> Non eliminare hello b2c-estensioni-app, a meno che non si intende eliminare tooimmediately tenant. Se l'applicazione hello rimane eliminati per più di 30 giorni, le informazioni utente andranno persi definitivamente.

## <a name="verifying-that-hello-extensions-app-is-present"></a>Verifica per determinare se è presente tale app estensioni hello

tooverify che hello b2c-estensioni-app è presente:

1. All'interno del tenant di Azure Active Directory B2C, fare clic su **più servizi** nel menu di navigazione a sinistra di hello.
1. Cercare e aprire **Registrazioni per l'app**.
1. Cercare un'app che inizia con **b2c-extensions-app**

## <a name="recover-hello-extensions-app"></a>Ripristinare hello estensioni app

Se è stato eliminato accidentalmente hello b2c-estensioni-app, è necessario toorecover di 30 giorni è. È possibile ripristinare l'applicazione hello utilizzando hello API Graph:

1. Sfoglia troppo[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).
1. Accedere come amministratore globale per la directory di Azure Active Directory B2C hello da app hello eliminato toorestore per toohello sito.
1. Inviare una richiesta HTTP GET per URL hello `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` con api-version = 1.6. Verificare che tooreplace `{tenantName}` con il nome del tenant. Questa operazione elencherà tutte le applicazioni hello che sono state eliminate all'interno di hello negli ultimi 30 giorni.
1. Trovare un'applicazione hello hello elenco in cui il nome di hello inizia con 'b2c-estensione-app' e copiare il relativo `objectid` valore della proprietà.
1. Emettere un POST HTTP con URL hello `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`. Sostituire hello `{OBJECTID}` parte dell'URL hello con hello `objectid` dal passaggio precedente hello. 

È ora possibile troppo[vedere app hello ripristinato](#verifying-that-the-extensions-app-is-present) in hello portale di Azure.

> [!NOTE]
> Un'applicazione può essere ripristinata solo se è stato eliminato all'interno di hello ultimi 30 giorni. Se sono trascorsi più di 30 giorni, i dati andranno persi definitivamente. Per ottenere assistenza, inviare un ticket al supporto tecnico.
