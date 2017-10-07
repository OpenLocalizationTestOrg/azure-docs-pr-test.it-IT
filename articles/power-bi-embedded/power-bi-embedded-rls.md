---
title: sicurezza a livello di aaaRow con Power BI Embedded
description: Informazioni dettagliate sulla sicurezza a livello di riga con Power BI Embedded
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a>Sicurezza a livello di riga con Power BI Embedded

Sicurezza a livello di riga (RLS) può essere utilizzato toorestrict utente accesso tooparticular dati all'interno di un report o un set di dati, consentendo di più utenti diversi toouse hello stesso report durante tutti vedere dati diversi. Power BI Embedded supporta ora i set di dati configurati con la sicurezza a livello di riga.

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

In ordine tootake sfruttare di riga, è importante che comprendere i concetti principali tre; Gli utenti, ruoli e regole. Ecco informazioni più approfondite su ogni concetto:

**Gli utenti** : questi sono gli utenti finali effettivo hello la visualizzazione dei report. In Power BI Embedded, gli utenti vengono identificati dalle proprietà username hello in un Token di App.

**Ruoli** – tooroles appartengono gli utenti. Un ruolo è un contenitore di regole e può essere denominato ad esempio "Responsabile vendite" o "Rappresentante". In Power BI Embedded, gli utenti vengano identificati dalla proprietà ruoli hello in un Token di App.

**Regole** : ruoli dispongono di regole e le regole sono filtri effettivo hello che verranno applicati toobe toohello dati. È ad esempio possibile usare un filtro semplice come "Paese = USA" o un filtro più dinamico.

### <a name="example"></a>Esempio

Per rest hello di questo articolo, verrà suggerito un esempio di creazione di riga e quindi che l'utilizzo all'interno di un'applicazione incorporata. Questo esempio utilizza hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) file PBIX.

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

L'esempio di analisi delle vendite al dettaglio Mostra le vendite per tutti gli archivi di hello in una catena di distribuzione specifico. Senza di riga, indipendentemente da quale district manager accede e visualizzazioni hello report, verranno visualizzate hello stessi dati. I dirigenti ha determinato che ogni direttore dovrebbe visualizzare solo hello vendite per gli archivi di hello che gestiscono e toodo questa, sarà possibile utilizzare di riga.

La sicurezza a livello di riga viene creata in Power BI Desktop. Quando vengono aperti hello set di dati e report, è possibile passare schema hello toosee della vista toodiagram:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

Ecco alcuni aspetti toonotice con questo schema:

* Tutte le misure, ad esempio **Total Sales**, vengono archiviati in hello **Sales** tabella dei fatti.
* Sono presenti altre quattro tabelle relative alle dimensioni correlate, ovvero **Elemento**, **Tempo**, **Negozio** e **Distretto**.
* le frecce di Hello sulle linee di relazione hello indicano che modo i filtri possono avvenire da una tabella tooanother. Ad esempio, se viene applicato un filtro a **ora [Date]**, nello schema corrente hello sarebbe filtrare solo verso il basso valori hello **Sales** tabella. Altre tabelle non sarebbero interessate da questo filtro poiché tutti frecce hello hello relazione righe toohello punto vendita nella tabella e non da subito.
* Hello **District** tabella indica che per ciascun gestore hello:
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

In base a questo schema, se si applica un filtro toohello **direttore** colonna nella tabella District hello e se tale filtro corrisponde a utente hello visualizzazione report hello, tale filtro filtrerà anche verso il basso hello **archivio**e **Sales** tabelle tooonly visualizzare i dati per quel particolare district manager.

Ecco come:

1. Nella scheda modellazione hello, fare clic su **gestione ruoli**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. Creare un nuovo ruolo denominato **Manager**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. In hello **District** tabella immettere l'espressione DAX seguente hello: **[direttore] = username)**  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. le regole hello toomake che siano lavorando, hello **modellazione** scheda, fare clic su **Visualizza come ruoli**e quindi immettere hello seguenti:  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   Hello report verranno visualizzati dati come se hai eseguito l'accesso come **Andrew Ma**.

L'applicazione hello filtro, il modo di hello abbiamo fatto in questo caso, verrà filtrano tutti i record di hello **District**, **archivio**, e **Sales** tabelle. Tuttavia, a causa della direzione del filtro hello per le relazioni tra hello **Sales** e **ora**, **Sales** e **elemento**e **Elemento** e **ora** tabelle non verranno filtrate verso il basso.

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

Che può essere accettabile per questo requisito, tuttavia, se non si Gestioni toosee elementi per cui non dispongono di tutte le vendite, è stato possibile accendere bidirezionale filtro incrociato per hello relazioni e flusso hello filtro di sicurezza in entrambe le direzioni. Questa operazione può essere eseguita mediante la modifica della relazione hello tra **Sales** e **elemento**, come segue:

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

A questo punto, i filtri possono inoltre passare da hello Sales tabella toohello **elemento** tabella:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> Se si utilizza la modalità DirectQuery per i dati, è necessario tooenable bidirezionale-tra filtro selezionando queste due opzioni:

1. **File** -> **Opzioni e impostazioni** -> **Funzionalità di anteprima** -> **Abilita il filtro incrociato in entrambe le direzioni per DirectQuery**.
2. **File** -> **Opzioni e impostazioni** -> **DirectQuery** -> **Consenti misure senza limitazioni in modalità DirectQuery**.

informazioni sul filtro incrociato bidirezionale, hello download toolearn [filtro incrociato bidirezionale in Power BI Desktop e di SQL Server Analysis Services 2016](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) white paper.

Questo conclude tutto il lavoro hello necessarie toobe eseguita in Power BI Desktop, ma non esiste uno più elemento di lavoro che deve toomake toobe eseguita hello e regole di lavoro è stato definito in Power BI Embedded. Gli utenti vengono autenticati e autorizzati dall'applicazione e i token App sono utilizzati toogrant utente accesso tooa Power BI Embedded report specificato. Power BI Embedded non ha informazioni specifiche sull'identità dell'utente. Per toowork di riga, è necessario toopass un contesto aggiuntivo come parte del token di app:

* **nome utente** (facoltativo): usato con una riga è una stringa che può essere usata toohelp identificare utente hello quando l'applicazione delle regole di riga. Vedere l'articolo relativo all'uso della sicurezza a livello di riga con Power BI Embedded.
* **ruoli** : una stringa contenente hello ruoli tooselect quando l'applicazione delle regole di sicurezza a livello di riga. Se si passa più di un ruolo, è consigliabile passarli come matrice di stringhe.

Per creare token hello, utilizzare hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) metodo. Se proprietà username hello è presente, è inoltre necessario passare almeno un valore nei ruoli.

Ad esempio, è possibile modificare hello EmbedSample. La riga 55 di DashboardController può essere aggiornata da

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

to

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

token app completo Hello avrà un aspetto simile al seguente:

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

A questo punto, con tutte le parti di hello insieme, quando un utente accede a tooview l'applicazione di questo report, essi verrà solo essere toosee in grado di hello dati che sono consentiti toosee, come definito per i livelli di sicurezza a livello di riga.

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a>Vedere anche

[Sicurezza a livello di riga con Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Esempio di incorporamento con JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Altre domande? [Provare a hello Community di Power BI](http://community.powerbi.com/)

