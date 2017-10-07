---
title: aaaSave ricerche e pin asset di dati in Azure Data Catalog | Documenti Microsoft
description: "Come tooarticle evidenziazione funzionalità in Azure Data Catalog per il salvataggio delle origini dati e gli asset di dati per un uso successivo."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a>Salvare le ricerche e aggiungere gli asset di dati in Azure Data Catalog
## <a name="introduction"></a>Introduzione
Azure Data Catalog fornisce le funzionalità per l'individuazione delle origini dati. Rapidamente, è possibile cercare e filtrare le origini dati del catalogo toolocate hello e comprendere lo scopo previsto, rendendo più semplice toofind hello destra dei dati per il processo di hello in questione.

Ma cosa accade se è necessario tooregularly funzionano con hello stesso dati? E cosa accade se altri utenti contribuiscono regolarmente il toohello knowledge stesse origini dati nel catalogo di hello? In queste situazioni, verificato il problema toorepeatedly hello stesso ricerche possono risultare inefficiente. In questi casi possono essere d'aiuto gli asset delle ricerche salvate e dei dati aggiunti.

## <a name="saved-searches"></a>Ricerche salvate
Una ricerca salvata di Data Catalog è una definizione di ricerca riutilizzabile per singolo utente. È possibile definire una ricerca, inclusi termini di ricerca, tag e altri filtri e quindi salvarli. È possibile eseguire nuovamente la definizione di ricerca salvata hello tooreturn successive tutte le risorse di dati corrispondenti ai criteri di ricerca.

### <a name="create-a-saved-search"></a>Creare una ricerca salvata
toocreate una ricerca salvata, hello seguenti:
1. Nel portale di Azure Data Catalog, hello hello **ricerca corrente** finestra, fare clic su **salvare**. 

    ![Collegamento Salva nelle impostazioni di Ricerca corrente](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. Immettere i criteri di ricerca hello che desidera tooreuse e quindi fare clic su **salvare**.

    ![Nome della ricerca salvato nelle impostazioni di Ricerca corrente](./media/data-catalog-how-to-save-pin/02-name.png)

3. Quando richiesto, immettere un nome per la ricerca salvata hello. Scegliere un nome significativo e che descrive l'asset di dati hello che verranno restituiti dalla ricerca hello.

### <a name="manage-saved-searches"></a>Gestire le ricerche salvate
Dopo aver salvato le ricerche di uno o più, un **ricerche salvate** opzione viene visualizzata di sotto di hello **ricerca corrente** casella. Quando viene espanso l'elenco di hello, vengono visualizzate tutte le ricerche salvate.

 ![Elenco di ricerche salvate](./media/data-catalog-how-to-save-pin/03-list.png)

Eseguire una delle seguenti hello:

* tooexecute una ricerca, selezionare una ricerca salvata nell'elenco di hello.

* tooview un elenco di opzioni di gestione per una ricerca salvata, fare clic su hello il nome successivo toohello ricerca sulla freccia verso il basso.

    ![Opzioni per la gestione delle ricerche salvate](./media/data-catalog-how-to-save-pin/04-managing.png)

* Selezionare un nuovo nome per la ricerca salvata hello tooenter **rinominare**. definizione di ricerca Hello non viene modificata.

* ricerca di tooremove hello salvato dall'elenco, selezionare **eliminare**, quindi confermare l'eliminazione di hello.

* ricerca di hello salvato toomark come ricerca predefinito, selezionare **Salva come predefinito**. Se si esegue una ricerca di "vuota" dalla home page di hello Azure Data Catalog, viene eseguita la ricerca del valore predefinito. Inoltre, hello ricerca che è contrassegnato come ricerca predefinita hello viene visualizzato nella parte superiore di hello di hello **ricerche salvate** elenco.

### <a name="organizational-saved-searches"></a>Ricerche salvate dall'organizzazione
Tutti gli utenti dell'organizzazione possono salvare le ricerche per usarle a livello personale. Gli amministratori del catalogo dati è inoltre possono salvare le ricerche per tutti gli utenti all'interno dell'organizzazione hello. Quando gli amministratori di salvino una ricerca, essi vengono presentati con un **condivisione all'interno della società hello** opzione. Se si seleziona questo hello condivisioni opzione salvato cercare tutti gli utenti nell'organizzazione hello.

 ![Ricerche salvate dall'organizzazione](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a>Risorse di dati aggiunte
Con le ricerche salvate, è possibile salvare e usare di nuovo le definizioni di ricerca. Asset di dati Hello restituite da ricerche hello potrebbe cambiare nel tempo come contenuto di hello di modifica di catalogo hello. Quando si aggiunge l'asset di dati, è possibile identificare in modo esplicito dati specifici asset toomake li tooaccess più semplice senza la necessità di toouse una ricerca.

L'aggiunta di un asset di dati è molto semplice. elenco di tooadd hello dati asset tooyour bloccato, sufficiente fare clic su hello **pin** icona. icona Hello viene visualizzata nell'angolo hello di hello asset riquadro nella visualizzazione affiancata hello e nella colonna più a sinistra di hello nella visualizzazione elenco hello nel portale di Azure Data Catalog hello.

![icona della puntina Hello asset di dati](./media/data-catalog-how-to-save-pin/05-pinning.png)

Anche la rimozione di un asset di dati è molto semplice. Fare semplicemente clic hello **sbloccare** impostazione hello tootoggle di icona per la risorsa selezionata hello.

![icona Sblocca asset di dati Hello](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a>Hello sezione risorse personali
Hello catalogo dati home page del portale include un **asset My** sezione che visualizza l'attività dell'utente corrente toohello di interesse. Questa sezione include sia le risorse aggiunte che le ricerche salvate.

![sezione delle risorse personali nella home page di hello Hello](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a>Riepilogo
Azure Data Catalog offre funzionalità che rendono più semplice toodiscover hello le origini dati che è necessario, pertanto tutti i membri dell'organizzazione possono ridurre il tempo per dati e più tempo di utilizzo. Le ricerche salvate e gli asset di dati aggiunti si basano su queste funzionalità di base, in modo che gli utenti possano identificare con facilità le origini dati con cui lavorano ripetutamente.
