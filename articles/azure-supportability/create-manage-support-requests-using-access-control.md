---
title: toocontrol di controllo di accesso basato sui ruoli (RBAC) aaaAzure toocreate diritti di accesso e gestire le richieste di assistenza | Documenti Microsoft
description: Azure toocontrol di controllo di accesso basato sui ruoli (RBAC) toocreate diritti di accesso e gestire le richieste di assistenza
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a>Azure toocontrol di controllo di accesso basato sui ruoli (RBAC) toocreate diritti di accesso e gestire le richieste di assistenza

Il [Controllo degli accessi in base al ruolo di Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) consente una gestione specifica degli accessi per Azure.
Supporta la creazione della richiesta nel portale di Azure hello [portal.azure.com](https://portal.azure.com), utilizza toodefine di modello RBAC di Azure, che è possibile creare e gestire le richieste di assistenza.
Assegnando hello appropriato RBAC ruolo toousers, gruppi e applicazioni in un determinato ambito, può essere una sottoscrizione, gruppo di risorse o una risorsa è concesso l'accesso.

Esaminiamo un esempio: come un proprietario del gruppo di risorse con le autorizzazioni di lettura nell'ambito di hello sottoscrizione, è possibile gestire tutte le risorse di hello nel gruppo di risorse hello, ad esempio siti Web, macchine virtuali e subnet.
Tuttavia, quando si tenta una richiesta di supporto per la risorsa di macchina virtuale hello toocreate, si verifica il seguente errore hello

![Errore relativo alla sottoscrizione](./media/create-manage-support-requests-using-access-control/subscription-error.png)

Nella gestione delle richieste di supporto, è necessario scrivere autorizzazione o un ruolo che dispone di hello azione Microsoft.Support/* toocreate toobe di ambito sottoscrizione hello in grado di supportare e gestire le richieste di assistenza.

Hello articolo seguente viene illustrato come utilizzare toocreate di controllo di accesso basato sui ruoli (RBAC) personalizzato di Azure e gestire le richieste di supporto di hello portale di Azure.

## <a name="getting-started"></a>Introduzione

Utilizzando l'esempio hello precedente, sarà in grado di toocreate una richiesta di supporto per la risorsa se sono stati è stato assegnato un ruolo personalizzato RBAC sottoscrizione hello dal proprietario della sottoscrizione hello.
[Ruoli RBAC personalizzati](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) può essere creata usando Azure PowerShell, l'interfaccia della riga di comando (CLI) di Azure e hello API REST.

proprietà di azioni Hello di un ruolo personalizzato specifica hello Azure operazioni toowhich hello ruolo concede l'accesso.
toocreate un ruolo personalizzato per la gestione delle richieste di supporto, hello al ruolo deve essere azione hello Microsoft.Support/*

Di seguito è riportato un esempio di un ruolo personalizzato, è possibile utilizzare toocreate e gestire le richieste di supporto.
È stato denominato in questo ruolo "Collaboratore di richiesta di supporto" e si riferisce toohello ruolo personalizzato in questo articolo.

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

Seguire i passaggi di hello illustrati in [questo video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn come toocreate un ruolo personalizzato per la sottoscrizione.

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a>Creare e gestire le richieste di assistenza in hello portale di Azure

Esaminiamo un esempio: si è proprietari di hello di sottoscrizione "Visual Studio MSDN sottoscrizione."
Joe è il peer che è un toosome proprietario risorsa hello di gruppi di risorse nella sottoscrizione e che disponga di sottoscrizione toohello autorizzazione di lettura.
Si desidera toogive accesso tooyour peer, Gianni, hello possibilità toocreate e gestire i ticket di supporto per le risorse di hello in questa sottoscrizione.

1. primo passaggio Hello è toogo toohello sottoscrizione e in "Impostazioni" viene visualizzato un elenco di utenti. Fare clic su utente hello Joe che dispone dell'accesso in lettura per hello sottoscrizione e si assegna un nuovo toohim di ruolo personalizzata.

    ![Aggiungi ruolo](./media/create-manage-support-requests-using-access-control/add-role.png)

2. Nel Pannello di "Utenti" hello, fare clic su "Aggiungi". Selezionare il ruolo personalizzato hello "Collaboratore di richiesta di supporto" hello elenco dei ruoli

    ![Aggiungere il ruolo di collaboratore di supporto](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. Dopo aver selezionato il nome del ruolo hello, fare clic su "Aggiungi utenti" e immettere le credenziali di posta elettronica hello Joe. Fare clic su "Seleziona"

    ![Aggiungi utenti](./media/create-manage-support-requests-using-access-control/add-users.png)

4. Fare clic su "Ok" tooproceed

    ![Aggiungere un accesso](./media/create-manage-support-requests-using-access-control/add-access.png)

5. È ora possibile visualizzare utente hello con il ruolo personalizzato appena aggiunto "Supporto richiesta Collaboratore" nella sottoscrizione hello per cui si è proprietari di hello hello

    ![Utente aggiunto](./media/create-manage-support-requests-using-access-control/user-added.png)

    Quando si connette Joe portale hello, vede hello toowhich di sottoscrizione che è stato aggiunto.

7. Joe fa clic su "Nuova richiesta di supporto" pannello "Guida in linea e supporto di" hello e può creare richieste di supporto per "Visual Studio Ultimate con MSDN"

    ![Nuova richiesta di supporto](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. Fare clic su "Tutte le richieste di supporto" Joe possibile visualizzare l'elenco di hello delle richieste di supporto creato per questa sottoscrizione ![Case visualizzazione dettagli](./media/create-manage-support-requests-using-access-control/case-details-view.png)

## <a name="remove-support-request-access-in-hello-azure-portal"></a>Rimuovere il supporto richiedere l'accesso in hello portale di Azure

Come è possibile toogrant accesso tooa utente toocreate e gestire le richieste di supporto, è possibili tooremove accesso utente hello.
tooremove hello toocreate possibilità gestire le richieste di supporto, toohello sottoscrizione, fare clic su "Impostazioni" e fare clic utente hello (in questo caso, Joe).
Fare doppio clic su nome ruolo hello, "Collaboratore di richiesta di supporto" e fare clic su "Rimuovi"

![Rimuovere l'accesso alle richiesta di supporto](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

Quando Joe registra nel portale toohello e tenta di toocreate una richiesta di supporto, egli rileva il seguente errore hello

![Errore di sottoscrizione 2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

Quando Joe fa clic su "Tutte le richieste di supporto", non sarà visibile nessuna richiesta di supporto

![Visualizzazione dettagli del caso 2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
