---
title: aaaHow toosecure accesso tooAzure catalogo dati | Documenti Microsoft
description: In questo articolo viene illustrato come toosecure catalogo dati e i dati aziendali.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a>Modalità di accesso di asset di dati e di catalogo toodata toosecure
> [!IMPORTANT]
> Questa funzionalità è disponibile solo nell'edizione standard di hello di Azure Data Catalog.

Azure Data Catalog consente toospecify chi può accedere al catalogo dati hello e quali operazioni (registrare, annotare, diventare proprietario) possono eseguire sui metadati nel catalogo di hello. 

## <a name="catalog-users-and-permissions"></a>Utenti e autorizzazioni del catalogo
toogive un utente o un hello gruppo accedere catalogo dati tooa e impostare le autorizzazioni:

1. In hello [home page del catalogo dati](http://www.azuredatacatalog.com), fare clic su **impostazioni** sulla barra degli strumenti hello.

    ![Catalogo dati - Impostazioni](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. Nella pagina delle impostazioni di hello, espandere hello **utenti catalogo** sezione.
    ![Utenti del catalogo - Aggiungi](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)
3. Fare clic su **Aggiungi**.
4. Immettere hello completo **nome utente** o nome di hello **gruppo di sicurezza** in Azure Active Directory (AAD) associata a catalogo hello hello. Se si aggiungono più utenti o gruppi usare la virgola (',') come separatore.
    ![Utenti del catalogo - Utenti o gruppi](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)
5. Premere **invio** o **scheda** dalla casella di testo hello. 
6.  Verificare che tutte le autorizzazioni (**Annota**, **registrare**, e **Take Ownership**) assegnati toothese utenti o gruppi per impostazione predefinita. Vale a dire hello utente o gruppo può [registrare asset di dati]( data-catalog-how-to-register.md), [annotare asset di dati]( data-catalog-how-to-annotate.md), e [diventare proprietario dell'asset di dati]( data-catalog-how-to-manage.md). 
    ![Utenti del catalogo - Autorizzazioni predefinite](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)
7.  toogive un utente o gruppo solo hello leggere catalogo toohello di accesso, cancellare hello **annotare** opzione per l'utente o gruppo. Quando si esegue questa operazione, hello utente o gruppo non è possibile annotare asset di dati nel catalogo di hello ma possono visualizzarli. 
8.  toodeny un utente o gruppo tramite la registrazione di asset di dati, cancellare hello **registrare** opzione per l'utente o gruppo.
9.  un utente di assunzione di proprietà di un asset di dati crittografato hello toodeny **assumere la proprietà** opzione per l'utente o gruppo. 
10. Fare clic su un utente/gruppo di utenti del catalogo, toodelete **x** per hello utente/gruppo nella parte inferiore di hello dell'elenco di hello. 
    ![Utenti del catalogo - Elimina utente](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)

    > [!IMPORTANT]
    > Si consiglia di aggiungere direttamente utenti toocatalog gruppi di sicurezza anziché l'aggiunta di utenti e assegnare le autorizzazioni. Quindi, aggiungere gruppi di sicurezza toohello gli utenti che corrispondono ai loro catalogo toohello diritti di accesso e i relativi ruoli.

## <a name="special-considerations"></a>Considerazioni speciali

- le autorizzazioni di Hello assegnate toosecurity gruppi sono additive. Si supponga ad esempio che un utente appartenga a due gruppi. Un gruppo ha l'autorizzazione di annotazione e l'altro gruppo non ha tale autorizzazione. L'utente avrà dell'autorizzazione di annotazione. 
- assegnare le autorizzazioni di Hello in modo esplicito hello di override utente tooa le autorizzazioni assegnate toogroups toowhich hello utente appartiene. Nell'esempio precedente hello, ad esempio, aggiunte in modo esplicito gli utenti di toocatalog utente hello e non si assegnano autorizzazioni annotare. utente Hello non è possibile annotare asset di dati, anche se l'utente di hello è un membro di un gruppo che dispone di annotare le autorizzazioni.

## <a name="next-steps"></a>Passaggi successivi
- [Introduzione ad Azure Data Catalog](data-catalog-get-started.md)

