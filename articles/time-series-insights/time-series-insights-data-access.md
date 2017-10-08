---
title: i criteri di accesso aaaData in Azure ora serie Insights | Documenti Microsoft
description: "In questa esercitazione, è illustrato toomanage criteri di accesso ai dati in fase di Insights di serie"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a>Concedere l'ambiente di data access tooa Insights serie ora tramite il portale di Azure

Gli ambienti Time Series Insights hanno due tipologie indipendenti di criteri di accesso:

* Criteri di accesso di gestione
* Criteri di accesso ai dati

Entrambi criteri concedono alle entità di sicurezza di Azure Active Directory (utenti e app) varie autorizzazioni per un determinato ambiente. salve le entità (utenti e applicazioni) devono appartenere toohello active directory (o "Tenant di Azure") associato alla sottoscrizione hello contenente ambiente hello.

I criteri di accesso Gestione concedono configurazione toohello correlate le autorizzazioni dell'ambiente di hello, ad esempio
*   Creazione e l'eliminazione dell'ambiente di hello, origini eventi, fare riferimento a set di dati, e
*   Gestione dei criteri di accesso ai dati hello.

Criteri di accesso ai dati concedono le autorizzazioni di query di data tooissue, modificano i dati di riferimento nell'ambiente di hello e condividono le query salvate e alle prospettive associate ambiente hello.

due tipi di Hello di criteri consentono una netta separazione tra la gestione dell'ambiente hello toohello di accesso e accedere ai dati toohello hello ambiente. Ad esempio, è possibile toosetup un ambiente tale proprietario hello/creatore dell'ambiente hello viene rimosso dall'accesso ai dati hello. Oltre a utenti e servizi che sono consentiti dati tooread hello ambiente non può essere concessa alcuna configurazione di accesso toohello dell'ambiente hello.

## <a name="grant-data-access"></a>Concedere l'accesso ai dati
Hello passaggi seguenti viene illustrato come accedere a dati toogrant per un'entità utente:

1.  Accedi toohello [portale di Azure](https://portal.azure.com).
2.  Fare clic su "Tutte le risorse" nel menu hello sul lato sinistro di hello di hello portale di Azure.
3.  Selezionare l'ambiente Time Series Insights.

  ![Gestire l'origine ora serie Insights hello - ambiente](media/data-access/getstarted-grant-data-access1.png)

4.  Selezionare "Accesso al piano dati" e fare clic su "Aggiungi".

  ![Gestire l'origine ora serie Insights hello - Aggiungi](media/data-access/getstarted-grant-data-access2.png)

5.  Fare clic su "Seleziona utente".
6.  Ricerca e selezionare l'utente tramite posta elettronica hello.
7.  Fare clic su "Seleziona" nel pannello "Selezionare l'utente".

  ![Gestire l'origine ora serie Insights hello - selezionare l'utente](media/data-access/getstarted-grant-data-access3.png)

8.  Fare clic su "Seleziona ruolo".
9.  Se si desidera che i dati di riferimento tooallow utente toochange condividere query salvate e prospettive con altri utenti dell'ambiente di hello, selezionare "Collaboratore". In caso contrario, selezionare i dati di query di "Lettura" tooallow utente nell'ambiente di hello e salvare query (non condivisa) personali nell'ambiente di hello.
10. Nel pannello "Selezionare il ruolo" hello, fare clic su "Ok".

  ![Gestire origine ora serie Insights hello - selezione ruolo](media/data-access/getstarted-grant-data-access4.png)

11. Nel pannello "Selezionare il ruolo utente" hello, fare clic su "Ok".
12. Dovrebbe essere visualizzato:

  ![Gestire l'origine ora serie Insights hello - risultati](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a>Passaggi successivi

* [Creare un'origine evento](time-series-insights-add-event-source.md)
* [Invio di eventi](time-series-insights-send-events.md) origine evento toohello
* Visualizzare l'ambiente nel [portale di Time Series Insights](https://insights.timeseries.azure.com)
