---
title: utilizzando la cache Redis aaaManaging hello Esplora Azure per IntelliJ | Documenti Microsoft
description: Informazioni su come toomanage il redis di Azure vengono memorizzati nella cache tramite Esplora Azure hello per IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: 76ba37a2a35c26d0045e17003181108992eb957d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-intellij"></a>Gestione delle cache Redis di hello Azure Explorer IntelliJ

Esplora Azure, che fa parte di hello Azure Toolkit per IntelliJ, fornisce agli sviluppatori Java con una soluzione da usare per la gestione di redis cache nel loro account Azure all'interno di hello IntelliJ IDE Hello.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a>Creare una Cache Redis tramite IntelliJ

Hello seguendo i passaggi illustrati hello passaggi toocreate una cache redis tramite hello Azure Explorer.

1. Accedi tooyour account Azure utilizzando i passaggi di hello hello [Sign In istruzioni per hello Azure Toolkit per IntelliJ] articolo.

1. In hello **Esplora Azure** finestra degli strumenti, espandere hello **Azure** nodo, fare doppio clic su **cache Redis**, quindi fare clic su **Create Cache Redis**.

   ![Creare un menu di Cache Redis][CR01]

1. Quando hello **nuova Cache Redis** viene visualizzata la finestra di dialogo, specificare hello le opzioni seguenti:

   ![Finestra di dialogo Crea nuova Cache Redis][CR02]

   a. **Nome DNS**: Specifica il sottodominio DNS hello per cache redis nuovo hello, che vengono anteposti troppo ". redis.cache.windows .net", ad esempio: *wingtiptoys.redis.cache.windows.net*.

   b. **Sottoscrizione**: specifica sottoscrizione di Azure da toouse per cache redis nuovo hello hello.

   c. **Gruppo di risorse**: Specifica il gruppo di risorse hello per la cache redis, occorre toochoose di hello le opzioni seguenti:
      * **Crea nuovo**: Specifica che si desidera toocreate un nuovo gruppo di risorse.
      * **Usa esistente**: specifica che sarà possibile scegliere in un elenco i gruppi di risorse associati all'account di Azure.

   d. **Percorso**: Specifica il percorso di hello in cui viene creata la cache redis; ad esempio, *Stati Uniti occidentali*.

   e. **Livello di prezzo**: Specifica il livello di prezzo utilizza la cache redis; questa impostazione determina il numero di hello di connessioni client. (Per altre informazioni, vedere [Prezzi di Cache Redis].)

   f. **Porta non SSL**: specifica se la Cache Redis consente le connessioni non SSL. Per impostazione predefinita, sono consentite solo le connessioni SSL.

1. Dopo aver specificato tutte le impostazioni della Cache Redis, fare clic su **OK**.

Dopo aver creata la cache redis, verrà visualizzato in Esplora Azure hello.

   ![Cache Redis in Azure Explorer][CR03]

> [!NOTE]
>
> Per ulteriori informazioni sulla configurazione di Azure redis le impostazioni della cache, vedere [come tooconfigure Cache Redis di Azure].
>

## <a name="display-hello-properties-for-your-redis-cache-in-intellij"></a>Visualizzare le proprietà di hello per le Cache Redis in IntelliJ

1. Esplora Azure hello destro la cache redis e fare clic su **visualizzare le proprietà**.

   ![Azure Esplora menu toodisplay proprietà di contesto per una cache redis][SP01]

1. Hello Azure Explorer consente di visualizzare proprietà di hello per la cache redis.

   ![Proprietà della Cache Redis][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a>Eliminare la Cache Redis tramite IntelliJ

1. Esplora Azure hello destro la cache redis e fare clic su **eliminare**.

   ![Esplora contesto menu toodelete una cache redis di Azure][DE01]

1. Fare clic su **Sì** quando richiesto toodelete la cache redis.

   ![Eliminare il prompt della Cache Redis][DE02]

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Per ulteriori informazioni sulle cache redis di Azure, le impostazioni di configurazione e sui prezzi, vedere hello seguenti collegamenti:

* [Cache Redis di Azure]
* [Documentazione di Cache Redis]
* [Prezzi di Cache Redis]
* [come tooconfigure Cache Redis di Azure]

<!-- URL List -->

[Prezzi di Cache Redis]: https://azure.microsoft.com/pricing/details/cache/
[Cache Redis di Azure]: https://azure.microsoft.com/services/cache/
[Documentazione di Cache Redis]: ./redis-cache/index.md
[come tooconfigure Cache Redis di Azure]: ./redis-cache/cache-configure.md
[Sign In istruzioni per hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
