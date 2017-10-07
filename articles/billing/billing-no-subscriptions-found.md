---
title: le sottoscrizioni aaaNo errore quando tenta toosign nel portale di tooAzure o centro account Azure | Documenti Microsoft
description: Fornisce una soluzione di hello per un problema in cui le sottoscrizioni non rilevato l'errore si verifica quando accede al portale tooAzure o centro account Azure.
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>Errore Non sono state trovate sottoscrizioni nel portale di Azure o nel Centro account di Azure
Si potrebbe ricevere un messaggio di errore "Non è stata trovata alcuna sottoscrizione" quando si tenta di toosign in toohello [portale di Azure](https://portal.azure.com/) o hello [centro account Azure](https://account.windowsazure.com/Subscriptions). Questo articolo offre una soluzione al problema.

## <a name="symptom"></a>Sintomo

Quando si tenta di toosign in toohello [portale di Azure](https://portal.azure.com/) o hello [centro account Azure](https://account.windowsazure.com/Subscriptions), viene visualizzato hello seguente messaggio di errore: "Non è stata trovata alcuna sottoscrizione".

## <a name="cause"></a>Causa

Questo problema si verifica se l'account non ha autorizzazioni sufficienti. 

## <a name="solution"></a>Soluzione

Assicurarsi di accedere come amministratore di hello corretto. Un amministratore di Account può accedere solo hello Account Center. Gli amministratori del servizio (SA) e coamministratore (CA) hanno toohello solo dell'autorizzazione di accesso portale di Azure o hello portale di Azure classico.

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a>Scenario 1: Messaggio di errore viene generato in hello [portale di Azure](https://portal.azure.com)

toofix questo problema:

* Verificare che tale hello directory Azure è selezionata, fare clic su account in alto a destra hello corretto.

  ![Directory selezionare hello hello in alto a destra di hello portale di Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* Se hello Azure right directory è selezionata, ma viene visualizzato il messaggio di errore hello, [l'account aggiunto come proprietario](billing-add-change-azure-subscription-administrator.md).

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>Scenario 2: Messaggio di errore viene generato in hello [centro account Azure](https://account.windowsazure.com/Subscriptions)

Controllare se l'account hello utilizzato è hello amministratore dell'Account. tooverify che hello amministratore dell'Account, eseguire la procedura seguente:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, selezionare **sottoscrizione**.
3. Selezionare hello sottoscrizione che desidera toocheck e quindi selezionare **impostazioni**.
4. Selezionare **Proprietà**. amministratore dell'account di sottoscrizione hello Hello viene visualizzato in hello **amministratore dell'Account** casella.

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se è ancora necessario della Guida, [contattare il supporto tecnico](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget risolta il problema. 
