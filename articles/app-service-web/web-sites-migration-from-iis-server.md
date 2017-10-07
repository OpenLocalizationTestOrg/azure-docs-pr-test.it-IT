---
title: aaaMigrate un tooAzure di app web enterprise servizio App
description: Viene illustrato come tooquickly Web App Migration Assistant toouse migrazione tooAzure di siti Web IIS esistente App del servizio Web App
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: 
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 7d66c5b799f0eefe85cbd9ba596ee0a05167f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-enterprise-web-app-tooazure-app-service"></a>Eseguire la migrazione di un tooAzure di app web enterprise servizio App
È possibile migrare facilmente i siti Web esistenti eseguite in Internet Information Service (IIS) 6 o versione successiva troppo[App del servizio Web App](http://go.microsoft.com/fwlink/?LinkId=529714). 

> [!IMPORTANT]
> Il supporto per Windows Server 2003 è terminato il 14 luglio 2015. Se attualmente si trovano i siti Web in un server IIS in Windows Server 2003, Web App è basso rischio, a basso costo e a basso attrito tookeep ai siti Web online e App migrazione pubblicazione guidata sul Web consente di automatizzare il processo di migrazione hello di. 
> 
> 

[Web App Migration Assistant](https://www.movemetothecloud.net/) possibile analizzare l'installazione del server IIS, identificare quali siti possono essere migrati tooApp servizio evidenziare tutti gli elementi che non è possibile eseguire la migrazione o non sono supportati nella piattaforma hello e quindi eseguire la migrazione di siti Web e tooAzure database associati.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a>Elementi verificati durante l'analisi della compatibilità ##
Migration Assistant Hello crea un tooidentify report conformità le potenziali cause problema o problemi di blocco che potrebbero impedire correttamente una migrazione da on-premise IIS tooAzure App del servizio Web App. Alcune delle toobe elementi chiave hello comunicata sono:

* Associazioni delle porte: App Web supporta solo la porta 80 per il traffico HTTP e la porta 443 per quello HTTPS. Diverse configurazioni di porta verranno ignorate e il traffico verrà indirizzato too80 o 443. 
* Autenticazione: App Web supporta l'autenticazione anonima per impostazione predefinita e l'autenticazione basata su form laddove specificato da un'applicazione. L'autenticazione di Windows può essere usata eseguendo l'integrazione solo con Azure Active Directory e ADFS. Tutte le altre forme di autenticazione, come ad esempio l'autenticazione di base, al momento non sono supportate. 
* Global Assembly Cache (GAC): hello Global Assembly Cache non è supportata nelle App Web. Se l'applicazione fa riferimento ad assembly che si distribuisce in genere toohello Global Assembly Cache, è necessario cartella bin dell'applicazione toohello toodeploy nelle App Web. 
* Modalità di compatibilità IIS5: non supportata in App Web. 
* Pool di applicazioni – nelle App Web, ogni sito e le relative applicazioni figlio eseguiti in hello stesso pool di applicazioni. Se il sito ha più applicazioni figlio che utilizzano più pool di applicazioni, consolidare tooa singolo pool di applicazioni con le stesse impostazioni o eseguire la migrazione di ogni app web separato tooa di applicazione.
* Componenti COM, App Web non consente la registrazione di hello di componenti COM su piattaforma hello. Se le applicazioni o siti Web di avvalersi di tutti i componenti COM, è necessario riscriverle nel codice gestito e distribuirle con l'applicazione o sito Web di hello.
* Estensioni ISAPI, l'App Web può supportare utilizzo hello di estensioni ISAPI. È necessario seguente hello toodo:
  
  * distribuire le DLL di hello con l'app web 
  * registrare le DLL di hello utilizzando [Web. config](http://www.iis.net/configreference/system.webserver/isapifilters)
  * Inserire un file di applicationHost.xdt nella radice del sito hello con contenuto hello descritto in "Consentito toobe di estensioni ISAPI arbitrart caricati" [sezione di questo articolo](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples) 
    
  
    
    Per ulteriori esempi di come toouse le trasformazioni di documento XML con il sito Web, vedere [trasformare il sito Web di Microsoft Azure](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).
* Non verrà eseguita la migrazione di altri componenti, come SharePoint, le estensioni FPSE, FTP e i certificati SSL.

## <a name="how-toouse-hello-web-apps-migration-assistant"></a>Come toouse hello Web App Migration Assistant
In questa sezione passaggi tootoomigrate un esempio alcuni siti Web che utilizzano un database di SQL Server e in esecuzione in un computer Windows Server 2003 R2 (IIS 6.0) locale:

1. In IIS hello server o computer client passare troppo[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/) 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. Installare Web App Migration Assistant facendo clic su hello **dedicato Server IIS** pulsante. Altre opzioni siano opzioni hello prossimo futuro. 
3. Fare clic su hello **Install Tool** pulsante tooinstall Migration Assistant Web App nel computer.
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > È anche possibile fare clic su **scaricare per l'installazione offline** toodownload un file ZIP file per l'installazione nei server non connessi toohello internet. In alternativa, è possibile fare clic su **caricare un report di preparazione della migrazione esistente**, ovvero toowork un'opzione avanzata con un migrazione conformità report esistente che è stato generato in precedenza (illustrato più avanti).
   > 
   > 
4. In hello **applicazione installata** schermata, fare clic su **installare** tooinstall nel computer. Verranno installate anche le dipendenze corrispondenti come distribuzione Web, DacFX e IIS, se necessario. 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   Una volta installato, Migration Assistant di App Web viene avviato automaticamente.
5. Scegliere **esegue la migrazione di database e i siti da un server remoto di tooAzure**. Immettere le credenziali amministrative hello per il server remoto hello e fare clic su **continua**. 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   Naturalmente, è possibile scegliere toomigrate dal server locale hello. opzione remote Hello è utile quando si desidera che i siti Web toomigrate da un server IIS di produzione.
   
   A questo punto esamina lo strumento di migrazione hello hello configurazione del server IIS, ad esempio siti Web candidato tooidentify siti, applicazioni, i pool di applicazioni e le dipendenze per la migrazione. 
6. schermata di Hello seguente mostra tre siti Web: **sito Web predefinito**, **TimeTracker**, e **CommerceNet4**. Tutti dispongono di un database associato che si desidera toomigrate. Selezionare tutti i siti di hello tooassess desiderato e quindi fare clic su **Avanti**.
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. Fare clic su **caricare** report di conformità tooupload hello. Se si fa clic **salvare file in locale**, è possibile eseguire nuovamente lo strumento di migrazione hello e caricamento hello salvati report di conformità come indicato in precedenza.
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   Dopo aver caricato i report di conformità hello, Azure esegue l'analisi di conformità e Mostra hello risultati. Leggere i dettagli di valutazione di hello per ogni sito Web e assicurarsi di comprendere oppure sono risolti tutti i problemi prima di procedere. 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. Fare clic su **iniziare la migrazione** migrazione hello toostart. Sarà ora toolog tooAzure reindirizzato al tuo account. È importante accedere usando un account con una sottoscrizione di Azure attiva. Se non si dispone di un account di Azure, è possibile iscriversi alla versione di valutazione gratuita [qui](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_). 
9. Selezionare l'account tenant hello, sottoscrizione di Azure e toouse area per le app web di Azure migrati e il database e quindi fare clic su **avviare Migrazione**. È possibile selezionare hello toomigrate di siti Web in un secondo momento.
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. Nella schermata successiva hello è possibile modificare le impostazioni di migrazione toohello predefinito, ad esempio:
    
    * usare un database SQL di Azure esistente o crearne uno nuovo e configurarne le credenziali
    * Selezionare hello toomigrate di siti Web
    * definire i nomi per le app web di Azure hello e i database SQL collegati
    * personalizzare le impostazioni globali hello e le impostazioni a livello di sito
    
    schermata di Hello riportata di seguito mostra tutti i siti Web hello selezionato per la migrazione con le impostazioni predefinite di hello.
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > Hello **abilitare Azure Active Directory** casella di controllo nelle impostazioni personalizzate integra hello Azure web app con [Azure Active Directory](../active-directory/active-directory-whatis.md) (hello **Directory predefinita**). Per altre informazioni sulla sincronizzazione di Azure Active Directory con l'Active Directory locale, vedere [Integrazione di directory](http://msdn.microsoft.com/library/jj573653).
    > 
    > 
11. Dopo aver effettuato tutte le modifiche di hello desiderato, fare clic su **crea** toostart processo di migrazione hello. strumento di migrazione Hello verrà creare app web di Database SQL di Azure e Azure hello e quindi pubblicare database e contenuto del sito Web di hello. avanzamento della migrazione Hello è chiaramente indicato nello strumento di migrazione hello e verrà visualizzata una schermata Riepilogo fine hello, quali siti hello dettagli eseguita la migrazione, se ha avuto esito positivo, le app web di Azure appena creato toohello di collegamenti. 
    
    Se qualsiasi errore si verifica durante la migrazione, hello chiaramente sarà lo strumento di migrazione indicare modifiche di hello hello errore e il rollback. Sarà inoltre possibile segnalazione di errori in grado di toosend hello direttamente toohello engineering team facendo hello **Invia segnalazione errori** pulsante, con stack di chiamate acquisito errore hello e compilare il corpo del messaggio. 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    Se la migrazione ha esito positivo senza errori, è anche possibile fare clic su hello **lascia un commento** pulsante tooprovide commenti direttamente. 
12. Fare clic su app web di Azure di hello collegamenti toohello e verificare che la migrazione di hello ha avuto esito positivo.
13. È ora possibile gestire hello eseguita la migrazione di applicazioni web in Azure App Service. toodo, accedere hello [portale Azure](https://portal.azure.com).
14. In hello portale di Azure, aprire hello Web App pannello toosee i siti Web migrati (visualizzate come App web), quindi fare clic su uno di essi toostart gestione hello web app, ad esempio la configurazione continua la pubblicazione, la creazione di backup, il ridimensionamento automatico e il monitoraggio dell'utilizzo o prestazioni.
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

