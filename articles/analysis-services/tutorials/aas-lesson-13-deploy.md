---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 13: distribuire | Descrizione di "Microsoft Docs: viene descritto come esercitazione hello toodeploy progetto tooAzure Analysis Services.
servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: na ms. date: 07/17/2017 Author: owend
---
# <a name="lesson-13-deploy"></a>Lezione 13: Distribuire

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione, configurare le proprietà di distribuzione; Specifica un tooand di toodeploy server un nome per il modello di hello Azure Analysis Services. È quindi possibile distribuire istanza toothat di hello del modello. Dopo aver distribuito il modello, gli utenti possono connettersi tooit tramite un'applicazione client di creazione di report. vedere, più toolearn [distribuire tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Stimato toocomplete ora questa lezione: **5 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 12: analizza in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> È necessario disporre di [le autorizzazioni di amministratore](../analysis-services-server-admins.md) on hello remoto Analysis Services server nell'ordine toodeploy tooit.  

> [!IMPORTANT]  
> Se è installato il database di esempio hello AdventureWorksDW2014 su un Server SQL locale e si distribuisce il server di Azure Analysis Services tooan modello, un [gateway dati locale](../analysis-services-gateway.md) è obbligatorio.
  
## <a name="deploy-hello-model"></a>Distribuire il modello di hello  
  
#### <a name="tooconfigure-deployment-properties"></a>proprietà di distribuzione tooconfigure  

  
1.  In **Esplora**, hello rapida **AW Internet Sales** del progetto e quindi fare clic su **proprietà**.  
  
2.  In hello **pagine delle proprietà di AW Internet Sales** nella finestra di dialogo **Server di distribuzione**, in hello **Server** proprietà, digitare hello del server completo.  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  In hello **Database** proprietà, digitare **Adventure Works Internet Sales**.  
  
4.  In hello **nome modello** proprietà, digitare **Adventure Works Internet Sales Model**.  
  
5.  Verificare le selezioni e quindi fare clic su **OK**.  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a>hello toodeploy Adventure Works Internet Sales
  
1.  In **Esplora**, hello rapida **AW Internet Sales** progetto > **compilare**.  

2.  Pulsante destro del mouse hello **AW Internet Sales** progetto > **Distribuisci**.

    Quando si distribuisce tooAzure Analysis Services, potrebbe essere richiesta tooenter l'account. Immettere nome e password dell'account dell'organizzazione, ad esempio nancy@adventureworks.com. Questo account deve essere Admins nel server di hello.
  
    finestra di dialogo Distribuisci Hello viene visualizzato e Mostra lo stato di distribuzione hello dei metadati hello e ogni tabella inclusa nel modello di hello.  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. Dopo aver completato correttamente la distribuzione, procedere e fare clic su **Chiudi**.  
  
## <a name="conclusion"></a>Conclusione  
Congratulazioni. Sono state completate le attività di creazione e distribuzione del primo modello tabulare di Analysis Services. Questa esercitazione sono state consentono di eseguire il completamento delle attività più comuni di hello nella creazione di un modello tabulare. Ora che viene distribuito il modello Adventure Works Internet Sales, è possibile utilizzare un modello di hello toomanage di SQL Server Management Studio. creare script di processo e un piano di backup. Gli utenti possono ora connettersi toohello modello utilizzando un'applicazione client di creazione di report, ad esempio Microsoft Excel o Power BI.  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>Passaggi successivi
[Connettersi con Power BI Desktop](../analysis-services-connect-pbi.md)   
[Lezione supplementare: Sicurezza dinamica](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[Lezione supplementare: Righe di dettaglio](../tutorials/aas-supplemental-lesson-detail-rows.md)   
[Lezione supplementare: Gerarchie incomplete](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
