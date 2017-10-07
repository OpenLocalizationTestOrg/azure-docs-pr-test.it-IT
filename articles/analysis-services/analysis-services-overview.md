---
title: "aaaWhat è Azure Analysis Services | Documenti Microsoft"
description: Ottenere una visione hello di Analysis Services in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 83d7a29c-57ae-4aa0-8327-72dd8f00247d
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: 48830a86f47a8ddc7770e6c44dd56c29927fe582
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-analysis-services"></a>Informazioni su Azure Analysis Services
![Azure Analysis Services](./media/analysis-services-overview/aas-overview-aas-icon.png)

Azure Analysis Services fornisce i dati di livello aziendale nel cloud hello di modellazione. È una piattaforma distribuita come servizio (PaaS) completamente gestita, integrata con i servizi della piattaforma dati di Azure. 

Analysis Services consente di eseguire il mashup e di combinare dati da più origini, definire metriche e proteggere i dati in un singolo modello semantico di dati attendibile. modello di dati Hello fornisce un modo più semplice e veloce per il toobrowse utenti enormi quantità di dati con applicazioni client quali Power BI, Excel, Reporting Services, le applicazioni di terze parti e personalizzate.

![Origini dati](./media/analysis-services-overview/aas-overview-data-sources.png)

Estrarre [questo video](https://sec.ch9.ms/ch9/d6dd/a1cda46b-ef03-4cea-8f11-68da23c5d6dd/AzureASoverview_high.mp4) toolearn adattamento Azure Analysis Services con Microsoft del complessivo funzionalità di Business Intelligence e come è possibile trarre vantaggio da ottenere i modelli di data in cloud hello.

## <a name="built-on-sql-server-analysis-services"></a>Compilare in SQL Server Analysis Services
Azure Analysis Services è compatibile con molte funzionalità avanzate già disponibili in SQL Server Analysis Services Enterprise Edition. Azure Analysis Services supporta i modelli tabulari a 1200 e 1400 di hello [livelli di compatibilità](analysis-services-compat-level.md). Sono supportate anche partizioni, sicurezza a livello di riga, relazioni bidirezionali e traduzioni. Le modalità In-Memory e DirectQuery consentono query velocissime su set di dati complessi e di grandi dimensioni.

I modelli tabulari offrono uno sviluppo rapido e sono altamente personalizzabili. Per gli sviluppatori, i modelli tabulari includono gli oggetti del modello di hello modello a oggetti tabulare (TOM) toodescribe. TOM viene esposto in JSON tramite hello [Tabular Model Scripting Language (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) hello AMO DDL tramite hello e [Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) dello spazio dei nomi.

## <a name="better-with-azure"></a>Ottimizzato per Azure
Azure Analysis Services si integra con molti servizi di Azure permette toobuild sofisticate soluzioni analitica. Integrazione con [Azure Active Directory](../active-directory/active-directory-whatis.md) fornisce i dati critici tooyour accesso sicuro basato sui ruoli. Integrazione con [Data Factory di Azure](../data-factory/data-factory-introduction.md) pipeline includendo un'attività che carica i dati nel modello di hello. È possibile usare [Automazione di Azure](../automation/automation-intro.md) e [Funzioni di Azure](../azure-functions/functions-overview.md) per un'orchestrazione semplice di modelli tramite codice personalizzato.

## <a name="get-up-and-running-quickly"></a>Operazioni iniziali rapide
Nel portale di Azure è possibile [creare un server](analysis-services-create-server.md) in pochi minuti. Con i [modelli](../azure-resource-manager/resource-manager-create-first-template.md) di Azure Resource Manager e PowerShell è possibile effettuare il provisioning dei server tramite un modello dichiarativo. Con un singolo modello si possono distribuire più servizi e altri componenti di Azure, ad esempio gli account di archiviazione e Funzioni di Azure. 

Dopo avere creato un server, è possibile creare un modello tabulare direttamente nel portale di Azure. Con nuova hello (anteprima) [funzionalità della finestra di progettazione Web](analysis-services-create-model-portal.md), è possibile connettersi a Database SQL di Azure, origine dati Azure SQL Data Warehouse, tooan o importare un file con estensione pbix di Power BI Desktop. Le relazioni tra tabelle vengono create automaticamente e, è possibile creare misure o modificare il file model.bim hello in formato json corretto dal browser.

## <a name="scale-tooyour-needs"></a>Scala tooyour esigenze
Azure Analysis Services è disponibile nei livelli Developer, Basic e Standard. All'interno di ogni livello, i costi di piano in base tooprocessing power QPUs e memoria le dimensioni variano. Quando si crea un server, si seleziona un piano entro un livello. È possibile modificare i piani di o verso il basso all'interno di hello stesso livello o aggiornamento tooa livello superiore, ma è possibile effettuare il downgrade da un livello più basso tooa di livello superiore.

È possibile aumentare o ridurre le prestazioni o sospendere il server. Utilizzare hello portale di Azure o il controllo totale al volo tramite PowerShell. Si paga solo per le risorse utilizzate. toolearn ulteriori informazioni sui diversi piani hello e livelli e utilizzare hello calcolatrice toodetermine hello destra piano tariffario per l'utente, vedere [dei prezzi di Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="keep-your-data-close"></a>Mantenere i dati nelle vicinanze
Il server Analysis Services Azure può essere creato in seguito hello [aree di Azure](https://azure.microsoft.com/regions/):

| Americhe | Europa | Asia/Pacifico |
|----------|--------|--------------|
|  Brasile meridionale<br> Canada centrale<br> Stati Uniti orientali 2<br> Stati Uniti centro-settentrionali<br> Stati Uniti centro-meridionali<br> Stati Uniti centro-occidentali<br> Stati Uniti occidentali | Europa settentrionale<br> Regno Unito meridionale<br> Europa occidentale |   Australia sudorientale<br> Giappone orientale<br> Asia sudorientale<br> India occidentale  |

Nuove aree vengono aggiunti tutti gli orari di hello, in modo da questo elenco potrebbe essere incompleto. Scegliere una località in cui creare il server nel portale di Azure oppure usando i modelli di Azure Resource Manager. hello tooget prestazioni ottimali, scegliere un percorso più vicino al più grande utenti. È possibile assicurare la [disponibilità elevata](analysis-services-bcdr.md) distribuendo i modelli in server ridondanti in più aree.

## <a name="migrate-your-existing-tabular-models"></a>Eseguire la migrazione dei modelli tabulari esistenti
Se si dispone già di soluzioni di modelli di SQL Server Analysis Services locale esistente, è possibile migrare tooAzure Analysis Services senza modifiche significative. toomigrate, è possibile utilizzare SSDT toodeploy server tooyour modello. In alternativa, in SSMS è possibile usare il backup e ripristino o TMSL.

Se si dispone di origini dati locali, è necessario tooinstall e configurare un [gateway dati locale](analysis-services-gateway.md). Se si dispone di ruoli e i membri del ruolo già configurati, eseguire la migrazione dei ruoli, ma sono presenti membri del ruolo tooreadd utilizzando SQL Server Management Studio o PowerShell.

## <a name="connect-toopopular-data-sources"></a>Connettere le origini dati toopopular
Azure Analysis Services supporta [connessione origini toodata](analysis-services-datasource.md) locale all'interno dell'organizzazione e nel cloud hello. È possibile combinare i dati provenienti dall'ambiente locale e dalle origini dati cloud per una soluzione ibrida. 

Nuovi modelli tabulari di 1400 funzione hello moderna recupera dati in SSDT, basato sul linguaggio di query formula hello M. Con dati, più la trasformazione dei dati e funzionalità mashup e toocreate possibilità hello e modificare le query di linguaggio delle formule M avanzate. Ad esempio, con i modelli tabulari 1400 è possibile eseguire la modellazione sui file di dati nell'archivio BLOB di Azure.

## <a name="use-hello-tools-you-already-know"></a>Utilizzare gli strumenti di hello che si conosce già

![Strumenti di sviluppo di Business Intelligence](./media/analysis-services-overview/aas-overview-dev-tools.png)

#### <a name="sql-server-data-tools-ssdt-for-visual-studio"></a>SQL Server Data Tools (SSDT) per Visual Studio
Sviluppare e distribuire i modelli con hello libero [SQL Server Data Tools (SSDT) per Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx). SSDT include modelli di progetto di Analysis Services che consentono di iniziare subito a lavorare. SSDT include ora hello moderna recupera dati datasource query mashup funzionalità e per i modelli tabulari 1400. Se si ha familiarità con i dati in Power BI Desktop ed Excel 2016, si conosce già quanto sia facile toocreate altamente personalizzati query origine dati.

#### <a name="sql-server-management-studio"></a>SQL Server Management Studio
Gestire i server e i database modello usando [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx) Connettere i server tooyour nel cloud hello. Eseguire gli script TMSL direttamente dalla finestra di query XMLA hello e automatizzare le attività tramite script TMSL. Le nuove funzionalità sono disponibili rapidamente, perché SSMS viene aggiornato ogni mese.

#### <a name="powershell"></a>PowerShell
Attività di gestione risorse di server come la creazione di server, la sospensione o ripresa delle operazioni del server o modifica del livello di servizio hello (livello) utilizzare i cmdlet di gestione risorse di Azure (Azure Resource Manager). Altre attività per la gestione di database, ad esempio aggiungendo o rimuovendo i membri del ruolo, l'elaborazione o l'esecuzione di script TMSL utilizzare i cmdlet nel modulo SqlServer hello. I moduli di Azure Resource Manager e SQL Server sono disponibili in hello [PowerShell gallery](https://www.powershellgallery.com/).


## <a name="your-data-is-secure"></a>I dati sono protetti
![Visualizzazioni di dati](./media/analysis-services-overview/aas-overview-secure.png)

#### <a name="authentication"></a>Autenticazione
L'autenticazione utente per Azure Analysis Services viene gestita da [Azure Active Directory (AAD)](../active-directory/active-directory-whatis.md). Durante il tentativo di un'identità dell'account dell'organizzazione con database di access toohello toolog nel database di Azure Analysis Services tooan, utilizzare gli utenti tentano tooaccess. Queste identità utente devono essere membri del valore predefinito di hello Azure Active Directory per la sottoscrizione di hello in cui risiede il server di Azure Analysis Services hello. vedere, più toolearn [l'autenticazione e le autorizzazioni utente](analysis-services-manage-users.md).

#### <a name="data-security"></a>Sicurezza dei dati
Azure Analysis Services utilizza archiviazione toopersist di archiviazione Blob di Azure e i metadati per i database di Analysis Services. I file di dati nel BLOB vengono crittografati mediante crittografia sul lato server di BLOB di Azure. Quando si usa la modalità di query diretta, vengono archiviati solo i metadati. accesso ai dati effettivi Hello sono eseguito dall'origine dati hello in fase di query.

#### <a name="on-premises-data-sources"></a>Origini dati locali
Accesso sicuro toodata che risiedono in locale nell'organizzazione viene ottenuta mediante l'installazione e configurazione di un [gateway dati locale](analysis-services-gateway.md). Gateway offrono accesso toodata per Query diretta e le modalità in memoria. Quando un modello di Azure Analysis Services si connette tooan origine di dati locale, insieme alle credenziali crittografato hello per l'origine dati locale di hello viene creata una query. il servizio cloud gateway Hello analizza query hello e inserisce tooan richiesta hello Azure Service Bus. gateway locale Hello esegue il polling hello Azure Service Bus per le richieste in sospeso. gateway Hello quindi ottiene hello query, decrittografa le credenziali di hello e si connette toohello di origine dati per l'esecuzione. risultati Hello vengono quindi inviati dall'origine dati di hello, eseguire il gateway toohello e quindi in toohello Azure Analysis Services il database.

Azure Analysis Services è disciplinato dalle hello [condizioni per i servizi Online Microsoft](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) hello e [informativa sulla Privacy di servizi Online Microsoft](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).
toolearn più sulla sicurezza di Azure, vedere hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/Security/AzureSecurity).

## <a name="supports-hello-latest-client-tools"></a>Supporta gli strumenti client più recenti di hello
![Visualizzazioni di dati](./media/analysis-services-overview/aas-overview-clients.png)

Gli strumenti moderni per l'esplorazione e la visualizzazione dei dati, come Power BI, Excel e strumenti di terze parti, forniscono agli utenti informazioni dettagliate a interattività elevata e visivamente accattivanti nei dati del modello.

I client usano MSOLAP, AMO o ADOMD [librerie client](analysis-services-data-providers.md) tooconnect tooAnalysis server di servizi. Le applicazioni client di Microsoft, come ad esempio Power BI Desktop ed Excel, installano tutte e tre le librerie client. Ma tenere presente, a seconda della versione di hello o frequenza degli aggiornamenti, le librerie client potrebbero non essere versioni più recenti di hello richieste da Azure Analysis Services. Hello vale toocustom applicazioni o altre interfacce, ad esempio AsCmd, TOM, ADOMD.NET. Queste applicazioni richiedono in genere l'installazione manuale di librerie hello come parte di un pacchetto.


## <a name="get-help"></a>Ottenere aiuto

#### <a name="documentation"></a>Documentazione
Azure Analysis Services è toomanage e tooset semplice backup. È possibile trovare tutte le informazioni di hello necessari toocreate e gestire i servizi server qui. Quando si crea un server di tooyour toodeploy modello dei dati, è molto hello stesso come nel caso di creazione di un modello di dati si distribuisce server on-premise tooan. È disponibile una ricca libreria concettuale, procedurale e di esercitazioni e articoli di riferimento in [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services).

#### <a name="videos"></a>Video
In [Azure Analysis Services su Channel 9](https://channel9.msdn.com/series/Azure-Analysis-Services) sono disponibili alcuni video utili.

#### <a name="blogs"></a>Blog
Per rimanere sempre aggiornati È sempre possibile ottenere informazioni più recenti di hello in hello [blog del team di Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/) e [blog di Azure](https://azure.microsoft.com/blog/).

#### <a name="community"></a>Community
Analysis Services è costituito da una vivace community di utenti. Creare un join conversazione hello in [forum di Azure Analysis Services](https://aka.ms/azureanalysisservicesforum).

## <a name="feedback"></a>Commenti e suggerimenti
In caso di suggerimenti o richieste di funzionalità, Essere tooleave che i commenti su [Azure Analysis Services Feedback](https://aka.ms/azureanalysisservicesfeedback).

Dispone di suggerimenti sulla documentazione hello? È possibile aggiungere commenti utilizzando Livefyre in hello parte inferiore di ogni articolo.

## <a name="next-steps"></a>Passaggi successivi
Ora che si conoscono ulteriori informazioni su Azure Analysis Services, è ora tooget avviato. Informazioni su come troppo[creare un server](analysis-services-create-server.md) in Azure. Quando il server è pronto, eseguire hello [esercitazione Adventure Works](tutorials/aas-adventure-works-tutorial.md) toolearn come toocreate un modello tabulare completamente funzionale e distribuirlo tooyour server.
