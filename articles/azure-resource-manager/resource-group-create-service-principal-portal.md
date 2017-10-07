---
title: "identità aaaCreate per app nel portale di Azure | Documenti Microsoft"
description: "Viene descritto come toocreate una nuova applicazione Azure Active Directory e il servizio dell'entità che può essere usato con il controllo di accesso basato sui ruoli hello in Gestione risorse di Azure toomanage accedere tooresources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a>Utilizzare portale toocreate un'applicazione Azure Active Directory e dell'entità servizio che possono accedere alle risorse

Quando si dispone di un'applicazione che richiede tooaccess o modifica le risorse, è necessario configurare un'applicazione Azure Active Directory (AD) e assegnare tooit autorizzazioni hello necessario. Questo approccio è preferibile toorunning hello app con le proprie credenziali perché:

* È possibile assegnare le autorizzazioni di identità app toohello che sono diverse dalle proprie autorizzazioni. In genere, queste autorizzazioni sono limitate tooexactly quali app hello deve toodo.
* Non si dispone delle credenziali dell'applicazione hello toochange se Modifica responsabilità dell'utente. 
* Quando si esegue uno script automatico, è possibile utilizzare l'autenticazione tooautomate un certificato.

Questo argomento viene illustrato come tooperform quelli passaggi tramite il portale di hello. Si concentra in un'applicazione single-tenant in cui un'applicazione hello è previsto toorun all'interno del sola organizzazione. Le applicazioni con un tenant singolo si usano in genere per applicazioni line-of-business eseguite all'interno dell'organizzazione.
 
## <a name="required-permissions"></a>Autorizzazioni necessarie
toocomplete in questo argomento, è necessario disporre di un'applicazione tooregister di autorizzazioni sufficienti con tenant di Azure AD e assegnare ruoli di tooa applicazione hello nella sottoscrizione di Azure. Verifichiamo che tu sia che è hello delle corrette autorizzazioni tooperform questi passaggi.

### <a name="check-azure-active-directory-permissions"></a>Controllare le autorizzazioni di Azure Active Directory
1. Accedi tooyour Account Azure tramite hello [portale di Azure](https://portal.azure.com).
2. Selezionare **Azure Active Directory**.

     ![Selezionare Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. In Azure Active Directory selezionare **Impostazioni utente**.

     ![Selezionare Impostazioni utente](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. Controllare hello **registrazioni di App** impostazione. Se impostato troppo**Sì**, gli utenti non amministratori possono registrare le app di Active Directory. Questa impostazione indica che qualsiasi utente nel tenant di Azure AD hello può registrare un'app. È possibile procedere troppo[autorizzazioni della sottoscrizione Azure controllare](#check-azure-subscription-permissions).

     ![Visualizzare le registrazioni dell'app](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. Se le registrazioni di app hello impostazione è troppo**n**, solo gli utenti amministratori possono registrare le app. È necessario toocheck se l'account è un amministratore per il tenant di Azure AD hello. Selezionare **Panoramica** e **Trova un utente** da Attività rapide.

     ![Trova un utente](./media/resource-group-create-service-principal-portal/find-user.png)
6. Cercare il proprio account e selezionarlo.

     ![Cercare un utente](./media/resource-group-create-service-principal-portal/show-user.png)
7. Per il proprio account selezionare **Ruolo della directory**. 

     ![Ruolo della directory](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. Visualizzare il proprio ruolo della directory assegnato in Azure AD. Se l'account viene assegnato il ruolo di utente toohello, ma impostazioni di registrazione dell'app (da hello passaggi precedenti) hello sono limitato tooadmin utenti, chiedere tooeither l'amministratore assegna si tooan ruolo di amministratore o tooenable utenti tooregister app.

     ![Visualizzare il ruolo](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a>Controllare le autorizzazioni di sottoscrizione di Azure
Nella sottoscrizione di Azure, è necessario che l'account `Microsoft.Authorization/*/Write` tooassign un ruolo di tooa AD app di accedere. Questa azione viene concesso tramite hello [proprietario](../active-directory/role-based-access-built-in-roles.md#owner) ruolo o [amministratore di accesso utente](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) ruolo. Se l'account viene assegnata toohello **collaboratore** ruolo, non si dispone dell'autorizzazione appropriata. Si riceverà un errore durante il tentativo di ruolo tooa principale del servizio tooassign hello. 

toocheck le autorizzazioni della sottoscrizione:

1. Se non già desiderata al proprio account Azure AD da hello passaggi precedenti, selezionare **Azure Active Directory** hello nel riquadro di sinistra.

2. Trovare il proprio account Azure AD. Selezionare **Panoramica** e **Trova un utente** da Attività rapide.

     ![Trova un utente](./media/resource-group-create-service-principal-portal/find-user.png)
2. Cercare il proprio account e selezionarlo.

     ![Cercare un utente](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. Selezionare **Risorse di Azure**.

     ![Selezionare le risorse](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. Consente di visualizzare i ruoli assegnati e determinare se si dispone delle autorizzazioni appropriate tooassign un ruolo di tooa AD app. In caso contrario, chiedere il tooadd amministratore sottoscrizione si tooUser accesso ruolo di amministratore. Hello seguente immagine, hello utente è assegnato toohello ruolo di proprietario per le sottoscrizioni di due, il che significa che l'utente disponga delle autorizzazioni adeguate. 

     ![Visualizzare le autorizzazioni](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a>Creare un'applicazione Azure Active Directory
1. Accedi tooyour Account Azure tramite hello [portale di Azure](https://portal.azure.com).
2. Selezionare **Azure Active Directory**.

     ![Selezionare Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. Selezionare **Registrazioni per l'app**.   

     ![Selezionare Registrazioni per l'app](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. Selezionare **Aggiungi**.

     ![Aggiungere l'app](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. Fornire un nome e l'URL per un'applicazione hello. Selezionare l'opzione **app Web / API** o **nativo** per il tipo di hello dell'applicazione si desidera toocreate. Dopo aver impostato i valori hello, selezionare **crea**.

     ![assegnare un nome all'applicazione](./media/resource-group-create-service-principal-portal/create-app.png)

L'applicazione è stata creata.

## <a name="get-application-id-and-authentication-key"></a>Ottenere l'ID applicazione e la chiave di autenticazione
Durante l'accesso a livello di codice, è necessario hello ID per l'applicazione e una chiave di autenticazione. tooget tali valori, utilizzare hello alla procedura seguente:

1. Da **Registrazioni dell'app** in Azure Active Directory selezionare l'applicazione.

     ![Selezionare l'applicazione](./media/resource-group-create-service-principal-portal/select-app.png)
2. Hello copia **ID applicazione** e archiviarlo nel codice dell'applicazione. le applicazioni in hello Hello [applicazioni di esempio](#sample-applications) sezione valore toothis hello client id di riferimento.

     ![ID CLIENT](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. Selezionare una chiave di autenticazione, toogenerate **chiavi**.

     ![Selezionare Chiavi](./media/resource-group-create-service-principal-portal/select-keys.png)
4. Fornire una descrizione della chiave hello e una durata per la chiave di hello. Al termine scegliere **Salva**.

     ![Salvare la chiave](./media/resource-group-create-service-principal-portal/save-key.png)

     Dopo aver salvato chiave hello, viene visualizzato il valore di hello della chiave di hello. Copiare questo valore perché non si è in grado di tooretrieve chiave di hello in un secondo momento. Fornire valore chiave hello con toolog ID applicazione di hello in come un'applicazione hello. Archiviare il valore di chiave hello in cui l'applicazione può recuperare.

     ![chiave salvata](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a>Ottenere l'ID tenant
Durante l'accesso a livello di codice, è necessario l'ID tenant hello toopass con la richiesta di autenticazione. 

1. ID tenant tooget hello selezionare **proprietà** per tenant di Azure AD. 

     ![selezionare le proprietà di Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. Hello copia **ID Directory**. Questo valore è l'ID tenant.

     ![tenant id](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a>Assegnare l'applicazione toorole
tooaccess risorse nella sottoscrizione, è necessario assegnare ruoli di tooa applicazione hello. Decidere quale ruolo rappresenta hello delle autorizzazioni necessarie per un'applicazione hello. toolearn sui ruoli disponibile hello, vedere [RBAC: compilato nei ruoli](../active-directory/role-based-access-built-in-roles.md).

È possibile impostare l'ambito hello a livello di hello di sottoscrizione hello, gruppo di risorse o la risorsa. Le autorizzazioni sono ereditate toolower livelli di ambito. Ad esempio, l'aggiunta di un ruolo di lettore toohello applicazione per un gruppo di risorse che significa che può leggere il gruppo di risorse hello e tutte le risorse che contiene.

1. Passa al livello toohello dell'ambito desiderato per un'applicazione hello tooassign. Ad esempio, di selezionare un ruolo nell'ambito di sottoscrizione hello di tooassign **sottoscrizioni**. In alternativa è possibile selezionare una risorsa o un gruppo di risorse.

     ![selezionare la sottoscrizione](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. Selezionare la sottoscrizione specifica (gruppo di risorse o risorsa) tooassign hello applicazione hello per.

     ![selezionare la sottoscrizione per l'assegnazione](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. Selezionare **Controllo di accesso (IAM)**.

     ![selezionare accesso](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. Selezionare **Aggiungi**.

     ![selezionare aggiungi](./media/resource-group-create-service-principal-portal/select-add.png)
6. Selezionare il ruolo di hello desiderato tooassign toohello applicazione. Hello immagine seguente viene illustrato hello **lettore** ruolo.

     ![selezionare il ruolo](./media/resource-group-create-service-principal-portal/select-role.png)

8. Cercare l'applicazione e selezionarla.

     ![Cercare l'app](./media/resource-group-create-service-principal-portal/search-app.png)
9. Selezionare **OK** toofinish l'assegnazione di ruolo hello. Viene visualizzata l'applicazione nell'elenco di hello di utenti con ruolo tooa per tale ambito.

## <a name="log-in-as-hello-application"></a>Accedere come un'applicazione hello

L'applicazione è ora configurata in Azure Active Directory. È necessario un ID e toouse chiave per l'accesso come un'applicazione hello. un'applicazione Hello viene assegnata il ruolo tooa che fornisce alcune azioni che è possibile eseguire. Per informazioni su come un'applicazione hello tramite diverse piattaforme, vedere:

* [PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [Interfaccia della riga di comando di Azure](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [REST](/rest/api/#create-the-request)
* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a>Passaggi successivi
* tooset backup di un'applicazione multi-tenant, vedere [tooauthorization di Guida per gli sviluppatori con API di gestione risorse di Azure hello](resource-manager-api-authentication.md).
* toolearn sull'impostazione di criteri di sicurezza, vedere [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).  
* Per un elenco di azioni disponibili che possono essere concesse o negate toousers, vedere [operazioni di Provider di risorse di Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).
