---
title: toocreate aaaUse CLI 2.0 un'app di Azure AD e configurarlo tooaccess API di servizi multimediali di Azure | Documenti Microsoft
description: Questo argomento viene illustrato come toocreate toouse CLI 2.0 un'app di Azure AD e configurarlo tooaccess API di servizi multimediali di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a>Utilizzare toocreate CLI 2.0 un'app di Azure ad e configurarlo tooaccess API di servizi multimediali di Azure

Questo argomento viene illustrato come toocreate toouse CLI 2.0 un'applicazione Azure Active Directory (Azure AD) e tooaccess dell'entità servizio servizi multimediali di Azure le risorse. 

## <a name="prerequisites"></a>Prerequisiti

- Un account Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di prova gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Account di Servizi multimediali. Per ulteriori informazioni, vedere [creare un account di servizi multimediali di Azure tramite il portale di Azure hello](media-services-portal-create-account.md).

## <a name="use-hello-azure-cloud-shell"></a>Utilizzare hello Shell di Cloud di Azure

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Avviare hello Shell Cloud dal riquadro di spostamento superiore hello del portale hello.

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

Per altre informazioni, vedere [Panoramica di Azure Cloud Shell](../cloud-shell/overview.md).

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a>Creare un'app di Azure AD e configurare account di accesso toohello multimediali con 2.0 CLI
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

ad esempio:

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

In questo esempio hello **ambito** è il percorso completo della risorsa hello per i supporti hello account di servizi. Tuttavia, hello **ambito** può essere qualsiasi livello.

Ad esempio, potrebbe essere uno dei seguenti livelli di hello:
 
* Hello **sottoscrizione** livello.
* Hello **gruppo di risorse** livello.
* Hello **risorse** livello (ad esempio, un account di supporto).

Per altre informazioni, vedere [Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)

Vedere anche [Manage Role-Based il controllo di accesso con l'interfaccia della riga di comando di Azure hello](../active-directory/role-based-access-control-manage-access-azure-cli.md). 

## <a name="next-steps"></a>Passaggi successivi

Introduzione a [caricamento file account tooyour](media-services-portal-upload-files.md).
