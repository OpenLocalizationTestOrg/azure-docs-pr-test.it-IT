---
title: controllo di accesso, ruoli e aaaResources in Azure Application Insights | Documenti Microsoft
description: Proprietari, collaboratori e lettori di informazioni dell'organizzazione.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a>Risorse, ruoli e controllo di accesso in Application Insights
È possibile controllare chi ha letto e aggiornare i dati di accesso tooyour in Azure [Application Insights][start], utilizzando [controllo di accesso basato sui ruoli in Microsoft Azure](../active-directory/role-based-access-control-configure.md).

> [!IMPORTANT]
> Assegnare l'accesso toousers in hello **gruppo di risorse o sottoscrizione** toowhich appartiene la risorsa di applicazione - non nella risorsa hello stessa. Assegnare hello **collaboratore di componenti di Application Insights** ruolo. In questo modo uniform controllo di accesso tooweb test e gli avvisi con la risorsa di applicazione. [Altre informazioni](#access)
> 
> 

## <a name="resources-groups-and-subscriptions"></a>Risorse, gruppi e sottoscrizioni
Innanzitutto prendere nota di alcune definizioni:

* **Risorse** : un'istanza di un servizio di Microsoft Azure. La risorsa di Application Insights consente di raccogliere, analizza e visualizza i dati di telemetria hello inviati dall'applicazione.  Altri tipi di risorse di Azure includono app Web, database e macchine virtuali.
  
    Aprire le risorse, toosee hello [portale Azure][portal], accedere e fare clic su tutte le risorse. toofind una risorsa, tipo di parte del nome nel campo filtro hello.
  
    ![Elenco di risorse di Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* [**Gruppo di risorse** ] [ group] -tutte le risorse appartiene tooone gruppo. Un gruppo è un modo toomanage relative risorse, in particolare per il controllo di accesso. Ad esempio, in una risorsa del gruppo, è possibile inserire un'App Web, un'app di Application Insights risorse toomonitor hello e una tookeep risorse di archiviazione dati esportati.

    ![Scegliere Sfoglia, gruppi di risorse e quindi scegliere un gruppo](./media/app-insights-resources-roles-access-control/11-group.png)

* [**Sottoscrizione** ](https://manage.windowsazure.com) -toouse Application Insights o altre risorse di Azure, accedi tooan sottoscrizione di Azure. Ogni gruppo di risorse appartiene tooone sottoscrizione di Azure, in cui si sceglie il pacchetto di prezzi e, se si tratta di una sottoscrizione di organizzazione, scegliere i membri di hello e le relative autorizzazioni di accesso.
* [**Account Microsoft** ] [ account] -hello nome utente e password utilizzare toosign tooMicrosoft Azure sottoscrizioni, XBox Live, Outlook.com e altri servizi Microsoft.

## <a name="access"></a>Controllare l'accesso nel gruppo di risorse hello
È importante toounderstand in risorsa toohello aggiunta creato per l'applicazione, sono presenti inoltre di separare risorse nascoste per gli avvisi e i test web. Sono collegato toohello stesso [gruppo di risorse](#resource-group) dell'applicazione. È anche possibile che siano stati inseriti altri servizi di Azure in tale posizione, ad esempio siti Web o risorsa di archiviazione.

![Risorse in Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

risorse di toothese accesso toocontrol che è pertanto consigliabile:

* Controllare l'accesso a hello **gruppo di risorse o sottoscrizione** livello.
* Assegnare hello **collaboratore di componenti di Application Insights** toousers ruolo. In questo modo i test web tooedit, avvisi e le risorse di Application Insights, senza fornire accesso tooany altri servizi nel gruppo di hello.

## <a name="tooprovide-access-tooanother-user"></a>tooprovide accesso tooanother utente
È necessario disporre di sottoscrizione toohello diritti di proprietario o il gruppo di risorse hello.

Hello utente deve disporre di un [Account Microsoft][account], o accesso tootheir [Account aziendale di Microsoft](../active-directory/sign-up-organization.md). È possibile fornire accesso tooindividuals e toouser gruppi definiti in Azure Active Directory.

#### <a name="navigate-toohello-resource-group"></a>Passare il gruppo di risorse toohello
Aggiungere hello utente non esiste.

![Nel pannello della risorsa dell'applicazione, aprire Essentials, aprire il gruppo di risorse hello e vi selezionare impostazioni o gli utenti. Fare clic su Aggiungi.](./media/app-insights-resources-roles-access-control/01-add-user.png)

Oppure è possibile passare ad un livello e aggiungere hello utente toohello sottoscrizione.

#### <a name="select-a-role"></a>Selezionare un ruolo
![Selezionare un ruolo per hello nuovo utente](./media/app-insights-resources-roles-access-control/03-role.png)

| Ruolo | Nel gruppo di risorse hello |
| --- | --- |
| Proprietario |È possibile modificare qualsiasi oggetto, incluso l'accesso utente |
| Collaboratore |È possibile modificare qualsiasi oggetto, incluse tutte le risorse |
| collaboratore componente di Application Insights  |Può modificare risorse, test Web e avvisi di Application Insights |
| Reader |È possibile visualizzare qualsiasi oggetto ma non apportare alcuna modifica |

'Modifica' include la creazione, l'eliminazione e l'aggiornamento:

* Risorse
* Test Web
* Avvisi
* Esportazione continua

#### <a name="select-hello-user"></a>Selezionare utente hello

Se non è utente hello desiderato nella directory di hello, è possibile invitare tutti gli utenti con un account Microsoft.
Se si usano servizi come Outlook.com, OneDrive, Windows Phone o XBox Live, hanno un account Microsoft.

## <a name="related-content"></a>Contenuti correlati

* [Controllo di accesso basato sui ruoli in Microsoft Azure](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
