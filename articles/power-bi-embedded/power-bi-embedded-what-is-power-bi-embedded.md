---
title: "Cos'è Microsoft Power BI Embedded?"
description: "Power BI Embedded consente di integrare report di Power BI in applicazioni Web o applicazioni mobili ed elimina la necessità di compilare soluzioni personalizzate."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 03649b72-b7d7-40ca-b077-12356d72d4f3
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/20/2017
ms.author: asaxton
ms.openlocfilehash: 0b5f7a2c3fd16ac32b0bc382616ca6600d378bb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>Cos'è Microsoft Power BI Embedded?
**Power BI Embedded**consente di integrare i report di Power BI direttamente nelle applicazioni Web o per dispositivi mobili.

![](media/powerbi-embedded-whats-is/what-is.png)

Power BI Embedded è un **servizio di Azure** che consente ai fornitori di software indipendente e agli sviluppatori di app di sfruttare i vantaggi dell'esperienza dati di Power BI nelle proprie applicazioni. Gli sviluppatori creano applicazioni, ognuna delle quali ha utenti e set di funzionalità specifici. Queste app possono inoltre contenere alcuni elementi dati predefiniti, ad esempio grafici e report che ora possono essere supportati da Microsoft Power BI Embedded. Per usare l'app non è necessario avere un account Power BI. È possibile continuare ad accedere all'applicazione come in precedenza, nonché visualizzare i report di Power BI e interagire con questi senza dover richiedere licenze aggiuntive.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Licenza di Microsoft Power BI Embedded
Nel modello di utilizzo di **Microsoft Power BI Embedded** l'utente finale non è il responsabile della gestione delle licenze di Power BI.  Le **sessioni** sono in realtà acquistate dallo sviluppatore dell'app che impiega gli oggetti visivi e sono addebitate alla sottoscrizione che comprende tali risorse. Altre informazioni sono disponibili nella [pagine dei prezzi](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Modello concettuale di Microsoft Power BI Embedded

![](media/powerbi-embedded-whats-is/model.png)

Come per qualsiasi altro servizio di Azure, il provisioning delle risorse di Power BI Embedded avviene tramite le [API di Azure Resource Manager](https://msdn.microsoft.com/library/mt712306.aspx). In questo caso la risorsa di cui si effettua il provisioning è una **Raccolta di aree di lavoro di Power BI**.

## <a name="workspace-collection"></a>Raccolta di aree di lavoro
La **Raccolta di aree di lavoro** è il contenitore di Azure di primo livello per le risorse che contengono da zero a più **aree di lavoro**.  La **Raccolta di** **aree di lavoro** ha tutte le proprietà standard di Azure e gli elementi seguenti:

* **Chiavi di accesso**: chiavi usate per chiamare in modo sicuro le API di Power BI, descritte in una sezione successiva.
* **Utenti**: utenti di Azure Active Directory (AAD) con diritti di amministratore per gestire la raccolta di aree di lavoro di Power BI tramite il portale di Azure o l'API di Azure Resource Manager.
* **Area**: nell'ambito del provisioning di una **accolta di aree di lavoro** è possibile selezionare un'area in cui effettuare il provisioning. Per altre informazioni, vedere [Aree di Azure](https://azure.microsoft.com/regions/).

## <a name="workspace"></a>Area di lavoro
Un'**area di lavoro** è un contenitore di contenuto Power BI che può includere set di dati e report. L' **Area di lavoro** è vuota quando viene creata. Si crea il contenuto con Power BI Desktop e si distribuisce il file PBIX nell'area di lavoro a livello di codice con l'[API di importazione di Power BI](https://msdn.microsoft.com/library/mt711504.aspx). Invece di usare Power BI Desktop, è anche possibile creare il set di dati a livello di codice e quindi creare report nell'applicazione.

## <a name="using-workspace-collections-and-workspaces"></a>Uso delle raccolte di aree di lavoro e delle aree di lavoro
Le **raccolte di aree di lavoro** e le **aree di lavoro** sono contenitori di contenuto usate e organizzate nel modo più efficiente perché si adattino alla progettazione dell'applicazione che si sta compilando. I modi per organizzare il contenuto all'interno di questi elementi possono essere molteplici. È possibile scegliere di inserire tutto il contenuto all'interno di un'area di lavoro e di usare successivamente i token delle app per suddividere ulteriormente il contenuto tra i clienti. È possibile anche decidere di inserire tutti i clienti in aree di lavoro distinte in modo che rimangano separati. In alternativa è possibile organizzare gli utenti per area anziché per cliente. Questa progettazione flessibile consente di scegliere il modo migliore per organizzare il contenuto.

## <a name="cached-datasets"></a>Set di dati memorizzati nella cache
È possibile usare set di dati memorizzati nella cache.  Non è tuttavia possibile aggiornare i dati memorizzati nella cache dopo averli caricati in **Microsoft Power BI Embedded**. Un set di dati memorizzato nella cache indica che si sono importati i dati in Power BI Desktop anziché usare DirectQuery.

## <a name="authentication-and-authorization-with-app-tokens"></a>Autenticazione e autorizzazione con token delle app
**Microsoft Power BI Embedded** incarica l'applicazione dell'utente affinché esegua tutte le operazioni necessarie per l'autenticazione e l'autorizzazione utente. Non è necessario che gli utenti finali siano clienti di Azure Active Directory.  Sarà invece l'applicazione ad autorizzare il rendering di un report di Power BI in **Microsoft Power BI Embedded** usando **token di autenticazione dell'applicazione**.  I **token dell'app** vengono creati nel momento in cui l'app intende eseguire il rendering di un report.

![](media/powerbi-embedded-whats-is/app-tokens.png)

I**token di autenticazione dell'applicazione (token dell'app)** vengono usati per eseguire l'autenticazione in **Microsoft Power BI Embedded**.  Esistono tre tipi di **token dell'app**:

1. Token di provisioning: si usano per il provisioning di una nuova **area di lavoro** in una **raccolta di aree di lavoro**
2. Token di sviluppo: si usano per chiamare direttamente le **API REST di Power BI**
3. Token d'incorporamento: sono usati quando si eseguono chiamate per il rendering di un report nell'iframe incorporato

Questi token si usano nelle varie fasi di interazione con **Microsoft Power BI Embedded**.  I token sono progettati in modo che sia possibile delegare le autorizzazioni dalla propria app a Power BI. Per altre informazioni, vedere [Flusso dei token delle app](power-bi-embedded-app-token-flow.md).

## <a name="create-or-edit-reports-within-your-application"></a>Creare o modificare report nell'applicazione

È ora possibile modificare report esistenti o creare nuovi report direttamente nell'applicazione senza dover usare Power BI Desktop. A tale scopo è necessario che nell'area di lavoro sia presente un set di dati.

## <a name="see-also"></a>Vedere anche

[Scenari comuni di Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Introduzione a Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Esempio introduttivo](power-bi-embedded-get-started-sample.md)  
[Incorporare un report](power-bi-embedded-embed-report.md)  
[Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Esempio di incorporamento con JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Repository Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Repository Git PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
Altre domande? [Contattare la community di Power BI](http://community.powerbi.com/)
