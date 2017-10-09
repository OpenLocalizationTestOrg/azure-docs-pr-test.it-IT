---
title: aaaAzure IoT Suite e Azure Active Directory | Documenti Microsoft
description: Descrive l'utilizzo di autorizzazioni di Azure Active Directory toomanage Azure IoT Suite.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a>Autorizzazioni nel sito azureiotsuite.com hello

## <a name="what-happens-when-you-sign-in"></a>Cosa accade quando si accede

Hello prima volta che accedi a [azureiotsuite.com][lnk-azureiotsuite], sito hello determina i livelli di autorizzazione hello basato sul hello attualmente selezionato tenant Azure Active Directory (AAD) e Azure sottoscrizione.

1. In primo luogo, elenco toopopulate hello del nome utente tooyour Avanti tenant visualizzato sito hello rileva da Azure cui si appartiene i tenant AAD. Attualmente, sito hello può ricevere solo i token utente per un tenant alla volta. Pertanto, quando si passa tenant usando l'elenco a discesa hello nell'angolo superiore destro di hello, sito hello consente l'accesso i token di hello toothat tenant tooobtain per tenant.

2. Successivamente, il sito hello rileva dalle sottoscrizioni che sono stati associati a hello selezionato tenant di Azure. Vedrai sottoscrizioni disponibili hello quando si crea una nuova soluzione preconfigurata.

3. Infine, sito hello recupera tutte le risorse di hello in sottoscrizioni hello e gruppi di risorse contrassegnate come soluzioni preconfigurate e popola riquadri hello hello home page.

Hello le sezioni seguenti vengono descritti i ruoli di hello che controllano l'accesso toohello preconfigurato soluzioni.

## <a name="aad-roles"></a>Ruoli AAD

ruoli AAD Hello le soluzioni di effettuare il provisioning preconfigurato possibilità hello di controllo e gestire gli utenti in una soluzione preconfigurata.

Per altre informazioni sui ruoli di amministratore in AAD, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory][lnk-aad-admin]. Hello corrente viene descritta la hello **amministratore globale** hello e **utente** ruoli della directory utilizzata da hello preconfigurato soluzioni.

### <a name="global-administrator"></a>Amministratore globale

Per ogni tenant di AAD possono essere presenti più amministratori globali:

* Quando si crea un tenant di AAD, si è amministratore predefinito hello globale del tenant.
* amministratore globale di Hello è possibile eseguire il provisioning di una soluzione preconfigurata e viene assegnato un **Admin** ruolo per l'applicazione hello interno al proprio tenant AAD.
* Se un altro utente in hello stesso tenant di AAD viene creata un'applicazione, ruolo predefinito hello concesso toohello amministratore globale è **ReadOnly**.
* Un amministratore globale può assegnare tooroles gli utenti per applicazioni che utilizzano hello [portale di Azure][lnk-portal].

### <a name="domain-user"></a>Utente di dominio

Per ogni tenant di AAD possono essere presenti molti utenti del dominio:

* Un utente di dominio può eseguire il provisioning di una soluzione preconfigurata tramite hello [azureiotsuite.com] [ lnk-azureiotsuite] sito. Per impostazione predefinita, utente di dominio hello viene concessa hello **Admin** ruolo in hello il provisioning dell'applicazione.
* Un utente di dominio è possibile creare un'applicazione tramite lo script build.cmd hello in hello [azure iot-remoto monitoraggio][lnk-rm-github-repo], [azure-iot--manutenzione predittiva] [ lnk-pm-github-repo], o [azure iot-connessione-factory] [ lnk-cf-github-repo] repository. Tuttavia, ruolo predefinito hello concesso è utente di dominio toohello **ReadOnly**, perché un utente di dominio non dispone di ruoli tooassign di autorizzazione.
* Se un altro utente nel tenant AAD hello viene creata un'applicazione, utente di dominio hello viene assegnato hello **ReadOnly** ruolo per impostazione predefinita per l'applicazione.
* Un utente di dominio non può assegnare ruoli per le applicazioni, quindi non può aggiungere utenti o ruoli per gli utenti di un'applicazione anche se ne è stato effettuato il provisioning.

### <a name="guest-user"></a>Utente guest

Per ogni tenant AAD possono essere presenti molti utenti guest. Gli utenti guest dispongono di un set limitato di diritti nel tenant AAD hello. Di conseguenza, gli utenti guest non è possibile eseguire il provisioning di una soluzione preconfigurata nel tenant AAD hello.

Per ulteriori informazioni su utenti e ruoli in AAD, vedere hello seguenti risorse:

* [Creare utenti in Azure AD][lnk-create-edit-users]
* [Assegnare gli utenti tooapps][lnk-assign-app-roles]

## <a name="azure-subscription-administrator-roles"></a>Ruoli di amministratore della sottoscrizione di Azure

ruoli di amministratore di Azure Hello controllare hello possibilità toomap tenant di tooan AD una sottoscrizione di Azure.

Maggiori informazioni sui ruoli di amministratore Azure hello nell'articolo hello [come tooadd o modificare l'Account amministratore, amministratore del servizio e Azure CO-amministratore][lnk-admin-roles].

## <a name="application-roles"></a>Ruoli applicazione

i ruoli applicazione Hello controllano accesso toodevices nella soluzione preconfigurata.

In un'applicazione su cui è stato eseguito il provisioning sono stati definiti due ruoli e uno implicito:

* **Amministratore:** ha tooadd controllo completo, gestire, rimuovere i dispositivi e modificare le impostazioni.
* **ReadOnly:** è possibile visualizzare i dispositivi, le regole, le azioni, i processi e i dati di telemetria.

È possibile trovare le autorizzazioni di hello assegnato il ruolo di tooeach in hello [RolePermissions.cs] [ lnk-resource-cs] file di origine.

### <a name="changing-application-roles-for-a-user"></a>Modifica dei ruoli applicazione di un utente

È possibile utilizzare hello seguendo procedure toomake un utente in Active Directory un amministratore della soluzione preconfigurata.

È necessario essere un ruolo di toochange AAD amministratore globale per un utente:

1. Passare toohello [portale di Azure][lnk-portal].
2. Selezionare **Azure Active Directory**.
3. Verificare che si utilizzano directory hello che scelto azureiotsuite.com quando è stato effettuato il provisioning della soluzione. Se si dispone di più directory associata alla sottoscrizione, è possibile passare tra loro se si sceglie il nome dell'account in alto a destra di hello del portale hello.
4. Fare clic su **Applicazioni aziendali**, quindi su **Tutte le applicazioni**.
4. Vengono visualizzate **Tutte le applicazioni** con stato **Qualsiasi**. Eseguire quindi una ricerca per un'applicazione con il nome della soluzione preconfigurata.
5. Fare clic su nome hello dell'applicazione hello che corrisponde al nome della soluzione preconfigurata.
6. Fare clic su **Utenti e gruppi**.
7. Selezionare utente hello tooswitch ruoli.
8. Fare clic su **assegnare** e selezionare hello ruolo (ad esempio **Admin**) tooassign toohello utente, fare clic su hello segno di spunta.

## <a name="faq"></a>domande frequenti

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a>Sono un amministratore del servizio e il mapping della directory hello toochange vorrei tra la sottoscrizione e un tenant di Azure ad specifico. Come completare questa attività

1. Passare toohello [portale di Azure classico][lnk-classic-portal], fare clic su **impostazioni** nell'elenco di hello dei servizi sul lato sinistro di hello.
2. Selezionare la sottoscrizione di hello che desideri toochange hello directory mapping.
3. Fare clic su **Modifica directory**.
4. Seleziona hello **Directory** desiderato nell'elenco a discesa hello toouse. Fare clic sulla freccia avanti hello.
5. Confermare il mapping della directory hello e coamministratori interessati. Se si stanno spostando da un'altra directory, vengono rimossi tutti i hello coamministratori dalla directory originale hello.

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a>Un utente/membro di dominio nel tenant AAD hello e ho creato una soluzione preconfigurata. Come gli viene assegnato un ruolo per l'applicazione?

Chiedere a un amministratore globale di toomake è un amministratore globale in hello AAD tenant e quindi assegnare i ruoli toousers. In alternativa, chiedere tooassign un amministratore globale è un ruolo direttamente. Se si desidera tenant AAD toochange hello in che è stata distribuita la soluzione preconfigurata, vedere la domanda successiva hello.

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a>Come passare la soluzione preconfigurata di monitoraggio remoto e l'applicazione assegnati ai tenant AAD hello?

È possibile eseguire una distribuzione cloud da <https://github.com/Azure/azure-iot-remote-monitoring> ed eseguire una ridistribuizione con un tenant AAD appena creato. Poiché sono, per impostazione predefinita, un amministratore globale quando si crea un tenant di AAD, gli utenti tooadd le autorizzazioni e assegnare ruoli agli utenti di toothose.

1. Creare una directory AAD in hello [portale di Azure][lnk-portal].
2. Andare troppo<https://github.com/Azure/azure-iot-remote-monitoring>.
3. Eseguire `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}`. Ad esempio `build.cmd cloud debug myRMSolution`.
4. Quando richiesto, impostare hello **tenantid** toobe tenant appena creato, anziché del tenant precedente.

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a>Voglio toochange amministratore del servizio o coamministratore quando l'accesso con un account organizzativo

Vedere l'articolo del supporto tecnico hello [modifica amministratore del servizio e coamministratore quando l'accesso con un account organizzativo][lnk-service-admins].

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a>Perché viene visualizzato un errore simile al seguente? "L'account non dispone hello delle autorizzazioni appropriate toocreate una soluzione. Rivolgersi all'amministratore account o provare con un account diverso".

Esaminare hello diagramma per linee guida seguenti:

![][img-flowchart]

> [!NOTE]
> Se si continua l'errore hello toosee dopo la convalida si è un amministratore globale nel tenant AAD hello e un coamministratore della sottoscrizione di hello, chiedere all'amministratore di account rimuovere utente hello e riassegnare le autorizzazioni necessarie per questo ordine. Innanzitutto, aggiungere hello utente come amministratore globale e quindi aggiungere l'utente come coamministratore su hello sottoscrizione di Azure. Se i problemi persistono, contattare il tema [Guida e supporto][lnk-help-support].

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a>Perché viene visualizzato questo errore quando si dispone di una sottoscrizione di Azure? "Una sottoscrizione di Azure è necessario toocreate preconfigurato soluzioni. È possibile creare un account di valutazione gratuito in pochi minuti."

Se si è certi di avere una sottoscrizione di Azure, convalidare i mapping per la sottoscrizione del tenant hello e verificare tenant corretto hello sia selezionato nell'elenco a discesa hello. Se è stato convalidato hello desiderato tenant è corretto, seguire hello precedente diagramma e convalidare il mapping di hello della sottoscrizione e questo tenant AAD.

## <a name="next-steps"></a>Passaggi successivi
toocontinue apprendendo IoT Suite, vedere come è possibile [personalizzare una soluzione preconfigurata][lnk-customize].

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
