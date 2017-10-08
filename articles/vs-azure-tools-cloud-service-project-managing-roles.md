---
title: i ruoli aaaManaging in Azure cloud services con Visual Studio | Documenti Microsoft
description: Informazioni su come tooadd e rimuovere i ruoli in Azure cloud services con Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Gestione dei ruoli nei servizi cloud di Azure con Visual Studio
Dopo aver creato il servizio cloud di Azure, è possibile aggiungere nuovi ruoli tooit o rimuovere quelli esistenti. È inoltre possibile importare un progetto esistente e convertirlo tooa ruolo. Ad esempio, è possibile importare un'applicazione Web ASP.NET e specificarla come ruolo Web.

## <a name="adding-a-role-tooan-azure-cloud-service"></a>Aggiunta di un servizio cloud di Azure di tooan ruolo
Hello alla procedura seguente illustra l'aggiunta di un web o lavoro ruolo tooan Azure progetto servizio cloud in Visual Studio.

1. Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.

1. In **Esplora**, espandere il nodo di progetto hello

1. Pulsante destro del mouse hello **ruoli** menu di scelta rapida nodo toodisplay hello. Selezionare il menu di scelta rapida hello **Aggiungi**, quindi selezionare un ruolo web esistente o un ruolo di lavoro dalla soluzione corrente hello o creare un progetto di ruolo web o di lavoro. È inoltre possibile selezionare un progetto appropriato, ad esempio un progetto di applicazione Web ASP.NET, e associarlo a un progetto di ruolo.

    ![Opzioni di menu tooadd un progetto di servizio di ruolo tooan cloud di Azure](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Rimuovere un ruolo da un servizio cloud di Azure
Hello seguente procedura consente di rimuovere un ruolo web o di lavoro da un progetto di servizio cloud di Azure in Visual Studio.

1. Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.

1. In **Esplora**, espandere il nodo di progetto hello

1. Espandere hello **ruoli** nodo.

1. Nodo di hello rapida desiderato tooremove e, selezionare il menu di scelta rapida hello **rimuovere**. 

    ![Opzioni di menu tooadd tooan un ruolo del servizio cloud di Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a>Nuova aggiunta di un progetto di servizio di ruolo tooan cloud di Azure
Rimuovere un ruolo dal progetto di servizio cloud, ma in seguito si decide tooadd nuovo ruolo di hello toohello progetto, solo dichiarazione del ruolo hello e gli attributi di base, ad esempio informazioni di diagnostica e di endpoint, vengono aggiunti. Nessun risorse o riferimenti aggiuntivi vengono aggiunti toohello `ServiceDefinition.csdef` file o toohello `ServiceConfiguration.cscfg` file. Se si desiderano tooadd queste informazioni, è necessario toomanually aggiungerlo nuovamente a questi file.

Ad esempio, è possibile rimuovere un ruolo del servizio web e successivamente si decide di eseguire il backup di questo ruolo tooadd nella soluzione. Se si esegue questa operazione, si verificherà un errore. tooprevent questo errore, si dispone di hello tooadd `<LocalResources>` elemento mostrato nel seguente hello XML nuovamente in hello `ServiceDefinition.csdef` file. Utilizza il nome del ruolo di servizio web hello aggiunto al progetto hello come parte dell'attributo nome hello per hello hello  **<LocalStorage>**  elemento. In questo esempio, è il nome di hello del ruolo del servizio web hello **WCFServiceWebRole1**.

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a>Passaggi successivi
- [Configurare i ruoli di hello per un servizio cloud di Azure con Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md)
