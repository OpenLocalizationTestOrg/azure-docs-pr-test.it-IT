---
title: aaaAuthenticate con un registro di sistema del contenitore di Azure | Documenti Microsoft
description: Come toolog nel Registro di sistema di contenitore di Azure tooan usando Azure Active Directory service principale o un account amministratore
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>Eseguire l'autenticazione con un registro contenitori Docker privato
toowork con immagini contenitore nel Registro di sistema contenitore di Azure, si accede tramite hello `docker login` comando. È possibile accedere usando un'**[entità servizio di Azure Active Directory](../active-directory/active-directory-application-objects.md)** o un **account amministratore** specifico del registro. In questo articolo vengono fornite maggiori informazioni su tali identità.



## <a name="service-principal"></a>Entità servizio

È possibile [assegnare un'entità servizio](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour Registro di sistema e utilizzarlo per l'autenticazione di base Docker. È consigliabile usare un'entità servizio per la maggior parte degli scenari. Fornire l'ID app hello e la password di hello servizio principale toohello `docker login` comando, come illustrato nell'esempio seguente hello:

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Una volta effettuato l'accesso, Docker memorizza nella cache le credenziali di hello, pertanto non è necessario l'ID dell'app tooremember hello.

> [!TIP]
> Se si desidera, è possibile rigenerare la password di hello di un'entità servizio eseguendo hello `az ad sp reset-credentials` comando.
>


Consentono l'entità servizio [accesso basato sui ruoli](../active-directory/role-based-access-control-configure.md) tooa Registro di sistema. I ruoli disponibili sono:
  * Lettore (solo accesso pull).
  * Collaboratore (accesso pull e push).
  * Proprietario (pull, push e assegnare ruoli tooother utenti).

L'accesso anonimo non è disponibile nei registri contenitori di Azure. Per le immagini pubbliche è possibile utilizzare [Docker Hub](https://docs.docker.com/docker-hub/).

È possibile assegnare più entità di servizio tooa del Registro di sistema, che consente di accedere a toodefine per diversi utenti o applicazioni. Le entità servizio abilitare anche "headless" connettività tooa nel Registro di sistema per sviluppatori o DevOps scenari, ad esempio hello seguono esempi:

  * Distribuzioni di contenitori da sistemi di tooorchestration un registro di sistema inclusi controller di dominio/OS, Docker Swarm e Kubernetes. È possibile anche effettuare il pull toorelated registri contenitore Servizi di Azure, ad esempio [servizio contenitore](../container-service/index.yml), [servizio App](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/)e altri.

  * Continua integrazione e distribuzione di soluzioni (ad esempio Visual Studio Team Services o Jenkins) che compilano le immagini contenitore e inviarli tooa Registro di sistema.





## <a name="admin-account"></a>Account amministratore
Per ogni registro che si crea viene creato automaticamente un account amministratore. Per impostazione predefinita account hello è disabilitata, ma è possibile abilitare e gestire le credenziali di hello, ad esempio tramite hello [portale](container-registry-get-started-portal.md#manage-registry-settings) o tramite hello [comandi CLI di Azure 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials). Ogni account amministratore dispone di due password, ognuna rigenerabile. due password Hello consentono del Registro di sistema di toomaintain connessioni toohello utilizzando una password mentre si rigenera hello altre password. Se hello account è abilitato, è possibile passare il nome di utente hello ed entrambi toohello password `docker login` comando del Registro di sistema di autenticazione di base toohello. ad esempio:

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> account amministratore Hello è progettato per un singolo utente tooaccess hello del Registro di sistema, principalmente per scopi di test. Non è consigliabile credenziali dell'account amministratore hello tooshare tra altri utenti. Tutti gli utenti vengono visualizzati come un registro di sistema toohello utente singolo. La modifica o la disattivazione di questo account Disabilita accesso Registro di sistema per tutti gli utenti che utilizzano le credenziali di hello.
>


### <a name="next-steps"></a>Passaggi successivi
* [La prima immagine usando Docker CLI hello push](container-registry-get-started-docker-cli.md).
* Per ulteriori informazioni sull'autenticazione in anteprima di hello contenitore del Registro di sistema, vedere hello [post di blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).
