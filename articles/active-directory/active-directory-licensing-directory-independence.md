---
title: aaaCharacteristics di Azure Active Directory del tenant intercaction | Documenti Microsoft
description: Gestire i tenant di Azure Active Directory considerando i tenant come risorse completamente indipendenti
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a>Informazioni sull'interazione di più tenant di Azure Active Directory

In Azure Active Directory (Azure AD), ogni tenant è una risorsa totalmente indipendente: hello di un peer logicamente indipendente da altri tenant gestiti. Tra i tenant non esiste alcuna relazione padre-figlio. Questa indipendenza tra i tenant include l'indipendenza delle risorse, l'indipendenza amministrativa e l'indipendenza della sincronizzazione.

## <a name="resource-independence"></a>Indipendenza delle risorse.
* Se si crea o si elimina una risorsa in un unico tenant, ha alcun impatto sulle risorse in un altro tenant, con l'eccezione parziale di hello di utenti esterni. 
* Se si usa uno dei nomi di dominio con un tenant, questo non potrà essere usato con altri tenant.

## <a name="administrative-independence"></a>Indipendenza amministrativa
Se un utente non amministratore del tenant "Contoso" crea un tenant di test denominato "Test", si verifica quanto segue:

* Per impostazione predefinita, gli utenti hello crea un tenant viene aggiunto come utente esterno di tale nuovo tenant e il ruolo di amministratore globale hello assegnato nel tenant.
* gli amministratori di Hello del tenant 'Contoso' non possono tootenant di privilegi amministrativi diretti 'Test', a meno che un amministratore di "Test" vengono loro concessi specificamente questi privilegi. Tuttavia, gli amministratori di 'Contoso' possono controllare accesso tootenant 'Test' Se si ha il controllo account utente di hello creato 'Test'.
* Se si installazione un ruolo di amministratore per un utente in un unico tenant, modifica hello non non interessano hello i ruoli di amministratore che hello utente dispone di un altro tenant.

## <a name="synchronization-independence"></a>Indipendenza della sincronizzazione
È possibile configurare ogni Azure Active Directory del tenant in modo indipendente tooget sincronizzare i dati da una singola istanza di uno:

* strumento di Hello Azure AD Connect, toosynchronize dati con una singola foresta di Active Directory.
* Hello tenant Azure Active Connector per Forefront Identity Manager, toosynchronize dati con uno o più in locale gli insiemi di strutture e/o le origini dati diverse da Azure AD.

## <a name="add-an-azure-ad-tenant"></a>Aggiungere un tenant di Azure AD
un tenant di Azure AD nel portale di Azure hello tooadd Accedi troppo[hello Azure portal](https://portal.azure.com) con un account di amministratore globale di Azure AD e, a sinistra di hello, selezionare **New**.

> [!NOTE]
> A differenza di altre risorse di Azure, i tenant non sono risorse figlio di una sottoscrizione di Azure. Se la sottoscrizione di Azure viene annullata o è scaduta, è comunque possibile accedere ai dati di tenant usando Azure PowerShell, hello API Graph di Azure o centro di amministrazione di hello Office 365. È anche possibile associare un'altra sottoscrizione tenant hello.
>

## <a name="next-steps"></a>Passaggi successivi
Per un'ampia panoramica dei problemi relativi alle licenze di Azure AD e le procedure consigliate, vedere [Informazioni sulle licenze dei tenant di Azure Active Directory](active-directory-licensing-whatis-azure-portal.md)
