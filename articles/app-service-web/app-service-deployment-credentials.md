---
title: le credenziali di distribuzione di servizio App aaaAzure | Documenti Microsoft
description: Informazioni su come toouse hello le credenziali di distribuzione di servizio App di Azure.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a>Configurazione delle credenziali per la distribuzione del Servizio app di Azure
Il [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) supporta due tipi di credenziali per la [distribuzione di GIT locale](app-service-deploy-local-git.md) e la [distribuzione FTP/S](app-service-deploy-ftp.md). Questi non sono hello stesso come credenziali di Azure Active Directory.

* **Le credenziali a livello di utente**: un insieme di credenziali per l'intero account Azure di hello. Può essere utilizzato toodeploy tooApp servizio per qualsiasi app, in tutte le sottoscrizioni, hello account Azure dispone di autorizzazione tooaccess. Si tratta di set di credenziali predefinito hello configurate in **servizi App** > **&lt;nome_app >** > **lecredenzialididistribuzione**. Questo è anche hello set predefinito che viene esposto in portale hello GUI (ad esempio hello **Panoramica** e **proprietà** della tua app [pannello della risorsa](../azure-resource-manager/resource-group-portal.md#manage-resources)).

    > [!NOTE]
    > Quando si delegano tooAzure di accedere alle risorse tramite basato sui ruoli accesso controllo (RBAC) o le autorizzazioni di co-amministratore, ogni utente di Azure che riceve l'accesso tooan app può utilizzare proprie credenziali a livello di utente personali fino a quando non viene revocato l'accesso. Queste credenziali di distribuzione non devono essere condivise con altri utenti di Azure.
    >
    >

* **Credenziali a livello di applicazione**: un insieme di credenziali per ogni applicazione. Può essere utilizzato toodeploy toothat app solo. le credenziali di Hello per ogni app viene generato automaticamente al momento della creazione di app ed è disponibile dell'applicazione hello profilo di pubblicazione. Non è possibile configurare manualmente le credenziali di hello, ma è possibile reimpostarle per un'app in qualsiasi momento.

    > [!NOTE]
    > In ordine toogive un utente l'accesso le credenziali toothese tramite basato sui ruoli accesso controllo (RBAC), è necessario toomake li collaboratore o versione successiva hello App Web. I lettori non sono consentiti toopublish e pertanto non è possibile accedere a tali credenziali.
    >
    >

## <a name="userscope"></a>Impostare e reimpostare le credenziali a livello di utente

È possibile configurare le credenziali a livello di utente nel [pannello risorse](../azure-resource-manager/resource-group-portal.md#manage-resources) di ogni app. Indipendentemente dal fatto che nella quale app configurare queste credenziali, viene applicato tooall App e per tutte le sottoscrizioni di Azure dell'account. 

tooconfigure le credenziali a livello di utente:

1. In hello [portale di Azure](https://portal.azure.com), fare clic su servizio App >  **&lt;any_app >** > **le credenziali di distribuzione**.

    > [!NOTE]
    > Nel portale di hello, è necessario disporre di almeno un'app prima di poter accedere pannello credenziali di distribuzione hello. Tuttavia, con hello [CLI di Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), è possibile configurare le credenziali a livello di utente senza un'app esistente.

2. Configurare il nome di utente hello e una password e quindi fare clic su **salvare**.

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

Dopo aver impostato le credenziali di distribuzione, è possibile trovare hello *Git* nome utente di distribuzione dell'app **Panoramica**,

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

oltre a un nome utente per la distribuzione *FTP* nelle **Proprietà** dell'app.

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> Azure non mostra la password di distribuzione a livello di utente. Se si dimentica la password di hello, non possono essere recuperati. Tuttavia, è possibile reimpostare le credenziali seguendo i passaggi di hello in questa sezione.
>
>  

## <a name="appscope"></a>Ottenere e reimpostare le credenziali a livello di utente
Per ogni applicazione nel servizio App, le credenziali a livello di applicazione vengono archiviate in hello XML profilo di pubblicazione.

credenziali a livello di applicazione hello tooget:

1. In hello [portale di Azure](https://portal.azure.com), fare clic su servizio App >  **&lt;any_app >** > **Panoramica**.

2. Fare clic su **...More** (...Altro) > **Recupera profilo di pubblicazione** per avviare il download di un file .PublishSettings.

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. Aprire hello. Trovare hello e file PublishSettings `<publishProfile>` tag con attributo hello `publishMethod="FTP"`. Quindi, ottenere i relativi attributi `userName` e `password`.
Si tratta di credenziali a livello di applicazione hello.

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    Credenziali a livello di utente toohello analoghe, nome utente di distribuzione FTP hello è nel formato di hello delle `<app_name>\<username>`, e nome utente di distribuzione Git hello è semplicemente `<username>` senza hello precedente `<app_name>\`.

credenziali a livello di applicazione hello tooreset:

1. In hello [portale di Azure](https://portal.azure.com), fare clic su servizio App >  **&lt;any_app >** > **Panoramica**.

2. Fare clic su **...More** (...Altro) > **Reimposta profilo di pubblicazione**. Fare clic su **Sì** tooconfirm hello Reimposta.

    l'azione reset Hello invalida qualsiasi scaricati in precedenza. File PublishSettings.

## <a name="next-steps"></a>Passaggi successivi

Scoprire come toouse toodeploy queste credenziali l'app da [Git locale](app-service-deploy-local-git.md) o tramite [FTP/S](app-service-deploy-ftp.md).
