---
title: aaaShare Azure dashboard del portale tramite RBAC | Documenti Microsoft
description: Questo articolo spiega come tooshare un dashboard in hello portale di Azure usando il controllo di accesso basato sui ruoli.
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: b12f9f8582596ee14aa8bfdfb4772cc139e3bf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a>Condividere i dashboard di Azure tramite il Controllo degli accessi in base al ruolo
Dopo aver configurato un dashboard, è possibile pubblicarlo e condividerlo con altri utenti nell'organizzazione. Consentire ad altri utenti tooview dashboard mediante Azure [Role-Based Access Control](../active-directory/role-based-access-control-configure.md). Assegnare un utente o gruppo di ruolo tooa utenti, e tale ruolo definisce se tali utenti di visualizzare o modificare dashboard pubblicati hello. 

Tutti i dashboard pubblicati vengono implementati come risorse di Azure, di conseguenza costituiscono elementi gestibili all'interno della sottoscrizione e sono contenuti in un gruppo di risorse.  Dal punto di vista del controllo di accesso, i dashboard non sono diversi da altre risorse, ad esempio una macchina virtuale o un account di archiviazione.

> [!TIP]
> Singoli riquadri nei dashboard hello imporre i propri requisiti di controllo di accesso in base alle risorse di hello che vengano visualizzate.  Pertanto, è possibile progettare un dashboard condiviso su vasta scala, proteggendo al contempo i dati di hello nei singoli riquadri.
> 
> 

## <a name="understanding-access-control-for-dashboards"></a>Informazioni sul controllo di accesso per i dashboard
Con Role-Based Access controllo (RBAC), è possibile assegnare gli utenti tooroles tre diversi livelli di ambito:

* sottoscrizione
* gruppo di risorse
* resource

Hello assegnate vengono ereditate dalla sottoscrizione di risorse toohello verso il basso. dashboard pubblicati Hello è una risorsa. Pertanto, potrebbe essere già tooroles gli utenti assegnati per la sottoscrizione di hello che funzionano anche per dashboard pubblicati hello. 

Di seguito è fornito un esempio.  Si supponga di avere una sottoscrizione di Azure e vari membri del team assegnati ruoli hello del **proprietario**, **collaboratore**, o **lettore** per sottoscrizione hello. Gli utenti che sono proprietari o i collaboratori sono in grado di toolist, visualizzare, creare, modificare o eliminare i dashboard in sottoscrizione hello.  Gli utenti che sono i visualizzatori sono in grado di toolist e visualizzare i dashboard, ma non è possibile modificarli o eliminarli.  Gli utenti con accesso in lettura sono in grado di toomake le modifiche locali tooa pubblicato dashboard (ad esempio, quando un problema di risoluzione dei problemi), ma non è possibile toopublish tali server back-toohello modifiche.  Avranno hello opzione toomake una copia privata di dashboard hello per se stessi

Tuttavia, è possibile assegnare anche autorizzazioni toohello gruppo contenente più dashboard o tooan singolo dashboard. Ad esempio, si potrebbe decidere che un gruppo di utenti deve disporre di autorizzazioni limitate in sottoscrizione hello ma maggiore particolare dashboard tooa accesso. Assegnare il ruolo di tali tooa gli utenti per i dashboard. 

## <a name="publish-dashboard"></a>Pubblicare dashboard
Si supponga di che aver completato la configurazione di un dashboard che si desidera tooshare con un gruppo di utenti nella sottoscrizione. passaggi Hello riportati di seguito illustrano un gruppo personalizzato denominato gestioni di archiviazione, ma è possibile denominare il gruppo di qualsiasi modo desiderato. Per informazioni sulla creazione di un gruppo di Active Directory e aggiunta di utenti toothat gruppo, vedere [la gestione dei gruppi in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

1. Nel dashboard di hello, selezionare **condivisione**.
   
     ![Selezionare Condividi](./media/azure-portal-dashboard-share-access/select-share.png)
2. Prima di assegnare l'accesso, è necessario pubblicare dashboard hello. Per impostazione predefinita, il dashboard di hello sarà pubblicato tooa gruppo di risorse denominato **dashboard**. Selezionare **Pubblica**.
   
     ![Pubblica](./media/azure-portal-dashboard-share-access/publish.png)

Il dashboard viene pubblicato. Se le autorizzazioni di hello ereditate dalla sottoscrizione hello sono adatti, non è necessario toodo.. Gli altri utenti dell'organizzazione verranno in grado di tooaccess e modificare il dashboard di hello in base al proprio ruolo di livello di sottoscrizione. Tuttavia, per questa esercitazione, si assegnare un gruppo del ruolo di tooa gli utenti per i dashboard.

## <a name="assign-access-tooa-dashboard"></a>Assegnare l'accesso tooa dashboard
1. Dopo la pubblicazione dashboard hello, selezionare **Gestisci utenti**.
   
     ![gestione utenti](./media/azure-portal-dashboard-share-access/manage-users.png)
2. Verrà visualizzato un elenco di utenti esistenti già stati assegnati a un ruolo per questo dashboard. L'elenco di utenti esistenti sarà diverso da immagine hello riportata di seguito. È probabile che le assegnazioni di hello vengono ereditate dalla sottoscrizione hello. tooadd un nuovo utente o gruppo, selezionare **Aggiungi**.
   
     ![Aggiungi utente](./media/azure-portal-dashboard-share-access/existing-users.png)
3. Selezionare il ruolo hello che rappresenta le autorizzazioni di hello toogrant desiderato. Per questo esempio selezionare **Collaboratore**.
   
     ![selezionare il ruolo](./media/azure-portal-dashboard-share-access/select-role.png)
4. Selezionare utente hello o un gruppo che si desidera tooassign toohello ruolo. Se non è possibile visualizzare hello utente o un gruppo che si sta cercando nell'elenco di hello, utilizzare la casella di ricerca hello. L'elenco dei gruppi disponibili dipenderanno gruppi hello creati in Active Directory.
   
     ![Seleziona utente](./media/azure-portal-dashboard-share-access/select-user.png) 
5. Al termine dell'operazione di aggiunta di utenti o gruppi, scegliere **OK**. 
6. nuova assegnazione Hello viene aggiunto toohello elenco di utenti. Si noti che il relativo **Accesso** è elencato come **Assegnato** anziché **Ereditato**.
   
     ![Ruoli assegnati](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a>Passaggi successivi
* Per un elenco di ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).
* toolearn sulla gestione delle risorse, vedere [le risorse di gestione di Azure tramite il portale](resource-group-portal.md).

