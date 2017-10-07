---
title: aaaHow tooconfigure un'applicazione Proxy dell'applicazione | Documenti Microsoft
description: Informazioni su come toocreate un Configura applicazione Proxy dell'applicazione in pochi semplici passaggi
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a>Come tooconfigure un'applicazione Proxy dell'applicazione

Questo articolo è utile toounderstand tooconfigure un'applicazione Proxy dell'applicazione all'interno di Azure AD tooexpose il toohello applicazioni on-premise di cloud.

## <a name="recommended-documents"></a>Documenti consigliati 

toolearn sulla creazione di un'applicazione Proxy dell'applicazione tramite il portale di amministrazione, hello e le configurazioni iniziali hello seguire hello [pubblicare applicazioni mediante il Proxy di applicazione AD Azure](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Per informazioni dettagliate sulla configurazione dei connettori, vedere [abilitare i Proxy di applicazione nel portale di Azure hello](active-directory-application-proxy-enable.md).

Per informazioni sul caricamento di certificati e sull'uso di domini personalizzati, vedere [Utilizzo di domini personalizzati nel proxy dell'applicazione di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).

## <a name="create-hello-applicationsetting-hello-urls"></a>Creare hello/impostazione dell'applicazione hello URL

Se si segue hello passaggi hello [pubblicare applicazioni mediante il Proxy di applicazione AD Azure](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentazione e sono il recupero di un errore durante la creazione di un'applicazione hello, vedere i dettagli dell'errore hello per le informazioni e i suggerimenti su come applicazione hello toofix. La maggior parte dei messaggi di errore include una correzione suggerita. gli errori comuni tooavoid, verificare che:

-   Si è un amministratore con autorizzazioni toocreate un'applicazione Proxy dell'applicazione

-   URL interno Hello è univoco

-   URL esterno Hello è univoco

-   Hello gli URL avvio con http o https e terminare con una "/"

-   Hello URL deve essere un nome di dominio, non un indirizzo IP

messaggio di errore Hello riporterà nell'angolo superiore destro di hello quando si crea un'applicazione hello. È anche possibile selezionare i messaggi di errore di hello notifica icona toosee hello.

   ![Prompt di notifica](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>Configurare connettori/gruppi di connettori

Se si riscontrano difficoltà di configurazione dell'applicazione a causa di avviso sui connettori di hello e gruppi di connettori, vedere le istruzioni sull'abilitazione di Proxy dell'applicazione per informazioni dettagliate su come i connettori toodownload. Se si desidera toolearn informazioni sui connettori, vedere hello [documentazione connettori](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).

Se i connettori sono inattivi, ciò significa che sono servizio hello tooreach non è possibile. Si tratta spesso perché tutte le porte hello necessario non sono aperte. toosee un elenco delle porte necessarie, vedere sezione Prerequisiti hello hello attivare la documentazione di Proxy dell'applicazione.

## <a name="upload-certificates-for-custom-domains"></a>Caricare certificati per domini personalizzati

Domini personalizzati consentono di dominio di hello toospecify dell'URL esterno. toouse domini personalizzati, è necessario il certificato di hello tooupload per quel dominio. Per informazioni sull'uso di certificati e domini personalizzati, vedere [Utilizzo di domini personalizzati nel proxy dell'applicazione di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains). 

Se si rilevano problemi di caricamento del certificato, cercare i messaggi di errore hello nel portale di hello per le informazioni aggiuntive sul problema hello con certificato hello. Problemi comuni relativi ai certificati:

-   Certificato scaduto

-   Certificato autofirmato

-   La chiave privata di hello mancante nel certificato

visualizzazione messaggi di errore Hello in hello angolo superiore destro quando si tenta di certificato hello tooupload. È anche possibile selezionare i messaggi di errore di hello notifica icona toosee hello.

   ![Prompt di notifica](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>Passaggi successivi
[Pubblicare applicazioni mediante il proxy di applicazione AD Azure](application-proxy-publish-azure-portal.md)
