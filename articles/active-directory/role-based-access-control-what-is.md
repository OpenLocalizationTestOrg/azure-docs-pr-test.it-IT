---
title: aaaManage accesso e autorizzazioni con RBAC - RBAC Azure | Documenti Microsoft
description: Introduzione a Gestione accesso con controllo di accesso basato sui ruoli di Azure in hello portale di Azure. Utilizzare le autorizzazioni tooassign assegnazioni di ruolo nel servizio directory.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8f8aadeb-45c9-4d0e-af87-f1f79373e039
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 1c133b2b57b49d85f0e12a318c7997478e095fb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-role-based-access-control-in-hello-azure-portal"></a>Introduzione a controllo di accesso basato sui ruoli nel portale di Azure hello
Le aziende sicurezza è consigliabile concentrarsi sul dando dipendenti hello conoscere esattamente le autorizzazioni che necessarie. Numero eccessivo di autorizzazioni possono esporre un tooattackers account. Un numero di autorizzazioni insufficiente ostacola l'efficienza del lavoro dei dipendenti. Il Controllo degli accessi in base al ruolo di Azure (RBAC) aiuta a risolvere questo problema offrendo la gestione specifica degli accessi per Azure.

Usa tale controllo, è possibile separare i compiti all'interno del team e concedere solo quantità di hello di accesso toousers necessarie tooperform i processi. Invece di concedere a tutti autorizzazioni senza restrizioni per la sottoscrizione o le risorse di Azure, è possibile consentire solo determinate azioni. Ad esempio, un dipendente di usare RBAC toolet gestire macchine virtuali in una sottoscrizione, mentre un altro può gestire SQL database all'interno di hello stessa sottoscrizione.

## <a name="basics-of-access-management-in-azure"></a>Nozioni fondamentali della gestione degli accessi in Azure
Ogni sottoscrizione di Azure è associata a una directory di Azure Active Directory (AD). Gli utenti, gruppi e applicazioni da tale directory possono gestire le risorse nella sottoscrizione di Azure hello. Assegnare i diritti di accesso utilizzando hello portale di Azure, gli strumenti da riga di comando di Azure e le API di gestione di Azure.

Concedere l'accesso tramite l'assegnazione di hello appropriato RBAC ruolo toousers, gruppi e applicazioni in un determinato ambito. ambito Hello un'assegnazione di ruolo può essere una sottoscrizione, un gruppo di risorse o una singola risorsa. Un ruolo assegnato a un ambito padre concede l'accesso anche elementi figlio toohello in esso contenuti. Ad esempio, un utente con gruppo di risorse tooa di accesso è possibile gestire tutte le risorse di hello che contiene, ad esempio siti Web, macchine virtuali e subnet.

![Diagramma della relazione tra gli elementi di Azure Active Directory](./media/role-based-access-control-what-is/rbac_aad.png)

ruolo RBAC Hello assegnato determina quali risorse hello utente, gruppo o applicazione è possibile gestire in tale ambito.

## <a name="built-in-roles"></a>Ruoli predefiniti
Azure RBAC presenta tre ruoli di base che si applicano a tipi di risorse tooall:

* **Proprietario** dispone di accesso completo tooall risorse hello toodelegate destra accesso tooothers inclusi.
* **Collaboratore** possono creare e gestire tutti i tipi di risorse di Azure, ma non è possibile concedere l'accesso tooothers.
* **Lettore** può visualizzare le risorse di Azure esistenti.

rest Hello dei ruoli RBAC hello in Azure consente la gestione delle risorse di Azure specifiche. Ad esempio, hello ruolo Collaboratore di macchina virtuale consente toocreate utente hello e gestire macchine virtuali. Non viene loro rete virtuale di accesso toohello o subnet hello hello macchina virtuale si connette a. 

[Ruoli predefiniti RBAC](role-based-access-built-in-roles.md) elenchi hello ruoli disponibili in Azure. Specifica le operazioni di hello e che ogni ruolo incorporato e concede toousers ambito. Se si cerca toodefine dei ruoli personalizzati per un maggiore controllo, vedere come toobuild [ruoli personalizzati in Azure RBAC](role-based-access-control-custom-roles.md).

## <a name="resource-hierarchy-and-access-inheritance"></a>Gerarchia delle risorse ed ereditarietà dell'accesso
* Ogni **sottoscrizione** in Azure appartiene tooonly una directory. Ogni directory può avere più di una sottoscrizione.
* Ogni **gruppo di risorse** appartiene tooonly una sottoscrizione.
* Ogni **risorse** appartiene tooonly un gruppo di risorse.

L'accesso che si concede all'ambito padre viene ereditato dall'ambito figlio. ad esempio:

* Assegnare il gruppo hello Reader ruolo tooan Azure AD nell'ambito di sottoscrizione hello. membri di Hello di tale gruppo possono visualizzare tutte le risorse e del gruppo di risorse nella sottoscrizione hello.
* Assegnare l'applicazione tooan ruolo di collaboratore hello nell'ambito del gruppo di risorse hello. È possibile gestire le risorse di tutti i tipi in tale gruppo di risorse, ma non altri gruppi di risorse nella sottoscrizione hello.

## <a name="azure-rbac-vs-classic-subscription-administrators"></a>Controllo degli accessi in base al ruolo di Azure e Amministratore sottoscrizione classico
Gli amministratori delle sottoscrizioni classico e co-amministratori hanno accesso completo toohello sottoscrizione di Azure. Essi possono gestire le risorse utilizzando hello [portale di Azure](https://portal.azure.com) con le API di gestione risorse di Azure o hello [portale di Azure classico](https://manage.windowsazure.com) e il modello di distribuzione classico di Azure. Nel modello RBAC hello, degli amministratori classici ruolo hello proprietario ambito della sottoscrizione hello.

Solo hello portale di Azure e il nuovo supporto per le API di gestione risorse di Azure Azure RBAC hello. Utenti e applicazioni che vengono assegnate ruoli RBAC non è possibile utilizzare il portale di gestione classico hello e il modello di distribuzione classica Azure hello.

## <a name="authorization-for-management-vs-data-operations"></a>Autorizzazioni per le operazioni di gestione e per le operazioni sui dati
RBAC Azure solo hello di supporta le operazioni di gestione risorse di Azure in hello portale di Azure e le API di gestione risorse di Azure. Non tutte le operazioni a livello di dati svolte sulle risorse di Azure possono essere autorizzate tramite RBAC. Ad esempio, è possibile autorizzare un utente toomanage gli account di archiviazione, ma non toohello BLOB o tabelle all'interno di un Account di archiviazione. Analogamente, un database SQL può essere gestito, ma non hello tabelle all'interno di esso.

## <a name="next-steps"></a>Passaggi successivi
* Introduzione a [basata sui ruoli di controllo di accesso nel portale di Azure hello](role-based-access-control-configure.md).
* Vedere hello [ruoli predefiniti RBAC](role-based-access-built-in-roles.md)
* Definire i [ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](role-based-access-control-custom-roles.md)
