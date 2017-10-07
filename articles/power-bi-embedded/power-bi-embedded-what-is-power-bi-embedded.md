---
title: "aaaWhat è Microsoft Power BI Embedded?"
description: "Power BI Embedded consente toointegrate report di Power BI nel web o applicazioni per dispositivi mobili è necessario toobuild di soluzioni personalizzate."
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
ms.openlocfilehash: 0353938b6cdd9bb58b123b250f45f76b8cc7abe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>Cos'è Microsoft Power BI Embedded?
**Power BI Embedded**consente di integrare i report di Power BI direttamente nelle applicazioni Web o per dispositivi mobili.

![](media/powerbi-embedded-whats-is/what-is.png)

Power BI Embedded è un **servizio Azure** che consente agli ISV e sviluppatori di app toosurface dati di Power BI si verifica all'interno delle applicazioni. Gli sviluppatori creano applicazioni, ognuna delle quali ha utenti e set di funzionalità specifici. Tali App possono anche verificarsi toohave alcuni elementi di dati incorporato, ad esempio grafici e report che ora possono essere spenti per Microsoft Power BI Embedded. Non è necessario un toouse account Power BI l'app. È possibile continuare toosign nell'applicazione tooyour come prima e consente di visualizzare e interagire con l'esperienza di Power BI reporting hello senza eventuali licenze aggiuntive.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Licenza di Microsoft Power BI Embedded
In hello **Microsoft Power BI Embedded** il modello di utilizzo, gestione delle licenze per Power BI non è una responsabilità hello dell'utente finale di hello.  In alternativa, **sessioni** vengono acquistati dallo sviluppatore hello dell'applicazione hello che utilizza gli oggetti visivi hello e vengono addebitati toohello sottoscrizione che possiede tali risorse. Informazioni aggiuntive possono trovarsi in hello [pagina dei prezzi](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Modello concettuale di Microsoft Power BI Embedded

![](media/powerbi-embedded-whats-is/model.png)

Come qualsiasi altro servizio in Azure, le risorse di Power BI Embedded vengono effettuato il provisioning tramite hello [le API di gestione risorse di Azure](https://msdn.microsoft.com/library/mt712306.aspx). In questo caso, le risorse hello che viene effettuato il provisioning sono una **raccolta dell'area di lavoro di Power BI**.

## <a name="workspace-collection"></a>Raccolta di aree di lavoro
Oggetto **dell'area di lavoro raccolta** è hello Azure contenitore di livello superiore per le risorse che contiene 0 o più **aree di lavoro**.  Oggetto **dell'area di lavoro** **raccolta** dispone di tutte le proprietà di Azure standard hello, nonché seguente hello:

* **Le chiavi di accesso** : le chiavi usate quando si chiama in modo sicuro hello API Power BI (descritto in una sezione successiva).
* **Gli utenti** : gli utenti di Azure Active Directory (AAD) che hanno toomanage diritti di amministratore hello raccolta dell'area di lavoro di Power BI tramite il portale di Azure hello o API di gestione risorse di Azure.
* **Area** , come parte di provisioning di un **dell'area di lavoro raccolta**, è possibile selezionare un toobe area eseguito il provisioning in. Per altre informazioni, vedere [Aree di Azure](https://azure.microsoft.com/regions/).

## <a name="workspace"></a>Area di lavoro
Un'**area di lavoro** è un contenitore di contenuto Power BI che può includere set di dati e report. L' **Area di lavoro** è vuota quando viene creata. Verrà creazione di contenuto con Power BI Desktop e verrà distribuito a livello di codice hello PBIX nell'area di lavoro utilizzando hello [API Power BI Importa](https://msdn.microsoft.com/library/mt711504.aspx). Invece di usare Power BI Desktop, è anche possibile creare il set di dati a livello di codice e quindi creare report nell'applicazione.

## <a name="using-workspace-collections-and-workspaces"></a>Uso delle raccolte di aree di lavoro e delle aree di lavoro
**Area di lavoro raccolte** e **aree di lavoro** sono contenitori di contenuto che vengono utilizzati e organizzati in una soluzione migliore adatta progettazione hello dell'applicazione hello si sta compilando. Saranno presenti molti modi diversi, che è possibile disporre il contenuto di hello al loro interno. È possibile scegliere tooput tutto il contenuto all'interno di un'area di lavoro e versioni successive utilizzare app token toofurther suddividere contenuto hello tra i clienti. È possibile anche scegliere tooput tutti i clienti nelle aree di lavoro separati in modo che alcuni prevede la separazione tra di essi. In alternativa, è possibile scegliere gli utenti tooorganize dall'area anziché dal cliente. Questa progettazione flessibile consente toochoose hello migliore modo tooorganize contenuto.

## <a name="cached-datasets"></a>Set di dati memorizzati nella cache
È possibile usare set di dati memorizzati nella cache.  Non è tuttavia possibile aggiornare i dati memorizzati nella cache dopo averli caricati in **Microsoft Power BI Embedded**. Un set di dati memorizzati nella cache indica che sono stati importati i dati di hello in Power BI Desktop anziché tramite DirectQuery.

## <a name="authentication-and-authorization-with-app-tokens"></a>Autenticazione e autorizzazione con token delle app
**Microsoft Power BI Embedded** rinvia tooyour applicazione tooperform tutti hello necessaria l'autenticazione e autorizzazione. Non è necessario che gli utenti finali siano clienti di Azure Active Directory.  Al contrario, l'applicazione esprime troppo**Microsoft Power BI Embedded** autorizzazione toorender un report di Power BI usando **i token di autenticazione applicazione (App token)**.  Questi **App token** vengono creati in base alle esigenze quando l'app desidera toorender un report.

![](media/powerbi-embedded-whats-is/app-tokens.png)

**I token di autenticazione applicazione (App token)** sono tooauthenticate usato contro **Microsoft Power BI Embedded**.  Esistono tre tipi di **token dell'app**:

1. Token di provisioning: si usano per il provisioning di una nuova **area di lavoro** in una **raccolta di aree di lavoro**
2. Token sviluppo - utilizzato durante la chiamata direttamente toohello **API REST di Power BI**
3. Token - utilizzati quando si effettua chiamate toorender l'incorporamento di un report in hello incorporato iframe

Questi token vengono utilizzati per hello diverse fasi delle proprie interazioni con **Microsoft Power BI Embedded**.  token Hello sono progettati in modo che è possibile delegare le autorizzazioni dal tooPower app BI. Per altre informazioni, vedere [Flusso dei token delle app](power-bi-embedded-app-token-flow.md).

## <a name="create-or-edit-reports-within-your-application"></a>Creare o modificare report nell'applicazione

È possibile modificare esiste report o creare nuovi report direttamente nell'applicazione senza dovere toouse Power BI Desktop. A tale scopo è necessario che nell'area di lavoro sia presente un set di dati.

## <a name="see-also"></a>Vedere anche

[Scenari comuni di Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Introduzione a Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Esempio introduttivo](power-bi-embedded-get-started-sample.md)  
[Incorporare un report](power-bi-embedded-embed-report.md)  
[Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Esempio di incorporamento con JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Repository Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Repository Git PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
Altre domande? [Provare a hello Community di Power BI](http://community.powerbi.com/)
