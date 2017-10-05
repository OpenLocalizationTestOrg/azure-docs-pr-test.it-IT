---
title: Eseguire l'autenticazione con un registro contenitori di Azure | Microsoft Docs
description: "Come accedere a un registro contenitori di Azure usando un'entità servizio di Azure Active Directory o un account amministratore"
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
ms.openlocfilehash: aa2a6bf3d7d9ec22020036851fc0f2bca37e31bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>Eseguire l'autenticazione con un registro contenitori Docker privato
Per usare le immagini contenitore nel registro contenitori di Azure, accedere usando il comando `docker login`. È possibile accedere usando un'**[entità servizio di Azure Active Directory](../active-directory/active-directory-application-objects.md)** o un **account amministratore** specifico del registro. In questo articolo vengono fornite maggiori informazioni su tali identità.



## <a name="service-principal"></a>Entità servizio

È possibile [assegnare un'entità servizio](container-registry-get-started-azure-cli.md#assign-a-service-principal) nel registro e usarla per eseguire l'autenticazione Docker di base. È consigliabile usare un'entità servizio per la maggior parte degli scenari. Fornire l'ID app e la password dell'entità servizio per il comando `docker login`, come illustrato nell'esempio seguente:

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Dopo aver effettuato l'accesso, Docker memorizza nella cache le credenziali, così da non doversi ricordare l'ID app.

> [!TIP]
> Se lo si desidera, è possibile rigenerare la password di un'entità servizio eseguendo il comando `az ad sp reset-credentials`.
>


Le entità servizio consentono l'[accesso basato su ruoli](../active-directory/role-based-access-control-configure.md) a un registro. I ruoli disponibili sono:
  * Lettore (solo accesso pull).
  * Collaboratore (accesso pull e push).
  * Proprietario (accesso pull e push e facoltà di assegnare ruoli ad altri utenti).

L'accesso anonimo non è disponibile nei registri contenitori di Azure. Per le immagini pubbliche è possibile utilizzare [Docker Hub](https://docs.docker.com/docker-hub/).

È possibile assegnare più entità di servizio a un registro, così da poter definire l'accesso per utenti o applicazioni differenti. Le entità servizio abilitano anche la connettività "headless" a un registro negli scenari DevOps o per sviluppatori, come gli esempi seguenti:

  * Distribuzioni di contenitori da un registro ai sistemi di orchestrazione, tra cui DC/OS, Docker Swarm e Kubernetes. È anche possibile eseguire il pull dei registri contenitori a servizi di Azure correlati, come [Servizio contenitore](../container-service/index.yml), [Servizio App](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/) e altri.

  * Soluzioni di distribuzione e integrazione continua (ad esempio Visual Studio Team Services o Jenkins) che creano immagini contenitore e le inviano a un registro.





## <a name="admin-account"></a>Account amministratore
Per ogni registro che si crea viene creato automaticamente un account amministratore. Per impostazione predefinita l'account è disabilitato, ma è possibile abilitarlo e gestirne le credenziali, ad esempio tramite il [portale](container-registry-get-started-portal.md#manage-registry-settings) o con i [comandi dell'interfaccia della riga di comando di Azure 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials). Ogni account amministratore dispone di due password, ognuna rigenerabile. Le due password consentono di mantenere le connessioni al registro usando una password mentre si rigenera l'altra. Se l'account è abilitato, è possibile passare il nome utente e la password al comando `docker login` per l'autenticazione di base per accedere al registro. Ad esempio:

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> L'account amministratore è pensato per l'accesso di un singolo utente al registro, principalmente per fare dei test. Non è consigliabile condividere le credenziali dell'account amministratore con altri utenti. Tutti gli utenti vengono visualizzati come un singolo utente nel registro. La modifica o la disattivazione di questo account disabilita l'accesso al registro da parte di tutti gli utenti che usano quelle credenziali.
>


### <a name="next-steps"></a>Passaggi successivi
* [Eseguire il push della prima immagine con l'interfaccia della riga di comando di Docker](container-registry-get-started-docker-cli.md).
* Per altre informazioni sull'autenticazione nell'anteprima del registro contenitori, vedere il [post di blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).
