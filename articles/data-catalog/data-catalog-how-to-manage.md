---
title: aaaManage asset di dati in Azure Data Catalog | Documenti Microsoft
description: "articolo Hello evidenzia come toocontrol visibilità e la proprietà di asset di dati registrata in Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a>Gestire gli asset di dati in Azure Data Catalog
## <a name="introduction"></a>Introduzione
Azure Data Catalog è progettato per l'individuazione dell'origine dati, in modo che è possibile individuare facilmente e comprendere le origini dati hello è necessario analysis tooperform e prendere decisioni. Queste funzionalità di individuazione verificare l'impatto maggiore sul hello quando gli utenti di trovare e comprendere più ampia gamma di hello delle origini dati disponibili. Con questi elementi presenti, il comportamento predefinito hello del catalogo dati è per tutti i dati registrati origini toobe visibile tooand individuabili tutti gli utenti del catalogo.

Catalogo dati non consentono di accedere ai dati toohello stesso. Accesso ai dati è controllato dal proprietario hello dell'origine dati hello. Con il catalogo dati, è possibile individuare le origini dati e visualizzare i metadati hello origini toohello correlati che vengono registrate nel catalogo di hello.

Potrebbero esserci delle situazioni, tuttavia, in cui devono essere solo origini dati utenti toospecific visibili, o toomembers di gruppi specifici. In questi scenari, gli utenti possono diventare proprietari di asset di dati registrati all'interno del catalogo hello e quindi controllare la visibilità di hello degli asset hello che sono proprietari.

> [!NOTE]
> funzionalità di Hello descritto in questo articolo è disponibile solo nell'edizione Standard di Azure Data Catalog hello. Hello edizione gratuita non fornisce funzionalità per la proprietà e per limitare la visibilità di asset di dati.
>
>

## <a name="manage-ownership-of-data-assets"></a>Gestire la proprietà degli asset di dati
Per impostazione predefinita, gli asset di dati registrati in Data Catalog sono senza proprietario. Qualsiasi utente con il catalogo di hello tooaccess di autorizzazione può individuare e annotare queste risorse. Gli utenti possono diventare proprietari di asset di dati senza proprietario e quindi limitare la visibilità di hello degli asset hello che sono proprietari.

Quando un asset di dati nel catalogo dati è di proprietà, solo gli utenti autorizzati dai proprietari hello possono individuare asset hello e visualizzarne i metadati e solo i proprietari di hello possono eliminare asset hello dal catalogo hello.

> [!NOTE]
> Proprietà nel catalogo dati interessa solo i metadati di hello archiviati nel catalogo di hello. La proprietà non conferisce tutte le autorizzazioni per l'origine dati sottostante hello.
>
>

### <a name="take-ownership"></a>Diventare proprietario
Gli utenti possono diventare proprietari di asset di dati selezionando hello **Take Ownership** opzione nel portale di hello catalogo dati. Autorizzazioni speciali non sono necessari tootake proprietà di un asset di dati senza proprietario. Qualsiasi utente può diventare proprietario di un asset di dati senza proprietario.

### <a name="add-owners-and-co-owners"></a>Aggiungere proprietari e comproprietari
Se un asset di dati ha già un proprietario, gli altri utenti non possono semplicemente diventare proprietari. Devono essere aggiunti come comproprietari da un proprietario esistente. Qualsiasi proprietario può aggiungere altri utenti o gruppi di sicurezza come comproprietari.

> [!NOTE]
> Si è un migliore toohave practice almeno due utenti come proprietari per qualsiasi proprietà dell'asset di dati.
>
>

### <a name="remove-owners"></a>Rimuovere i proprietari
Qualsiasi proprietario di asset può rimuovere i relativi comproprietari.

Un proprietario asset rimuove aggiungersi come proprietario non è più possibile gestire asset hello. Se esistono altri CO-proprietari proprietario dell'asset hello rimuove aggiungersi come proprietario, asset hello Ripristina tooan senza proprietario dello stato.

## <a name="control-visibility"></a>Controllare la visibilità
Proprietari di asset di dati è possono controllare la visibilità di hello degli asset di dati hello che sono proprietari. visibilità toorestrict come valore predefinito di hello, in cui tutti i Data Catalog, gli utenti possono individuare e visualizzare hello asset di dati, proprietario dell'asset hello può attivare o hello visibilità impostazione **Everyone** troppo**proprietari e utenti** nelle proprietà hello asset hello. I proprietari possono quindi aggiungere utenti e gruppi di sicurezza specifici.

> [!NOTE]
> Quando possibile, devono essere assegnate le autorizzazioni di proprietà e la visibilità di asset, toosecurity gruppi e non agli utenti di tooindividual.
>
>

## <a name="catalog-administrators"></a>Amministratori del catalogo
Gli amministratori del catalogo dati sono implicitamente comproprietari di tutte le risorse nel catalogo di hello. Proprietari della risorsa non è possibile rimuovere la visibilità da parte degli amministratori e gli amministratori possono gestire proprietà e la visibilità per tutti gli asset di dati nel catalogo di hello.

## <a name="summary"></a>Riepilogo
Hello catalogo dati crowdsourcing modello toometadata e dati di individuazione consente a tutti i toocontribute gli utenti del catalogo e individuare. Hello edizione Standard di catalogo dati è progettato per la gestione e la proprietà visibilità hello toolimit e l'uso di asset di dati specifico.
