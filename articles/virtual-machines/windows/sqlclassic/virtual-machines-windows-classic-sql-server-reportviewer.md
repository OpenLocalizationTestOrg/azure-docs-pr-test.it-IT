---
title: aaaUse ReportViewer in un sito Web | Documenti Microsoft
description: In questo argomento viene descritto come toobuild un sito Web di Microsoft Azure con il controllo ReportViewer di Visual Studio hello che visualizza un report archiviati in una macchina virtuale di Microsoft Azure.
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a>Usare ReportViewer in un sito Web ospitato in Azure
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

È possibile compilare un sito Web di Microsoft Azure con hello controllo ReportViewer di Visual Studio che consente di visualizzare un report archiviato in una macchina virtuale di Microsoft Azure. Hello controllo ReportViewer è in un'applicazione Web creata mediante hello modello applicazione Web ASP.NET.

> [!IMPORTANT]
> modelli di applicazione Web ASP.NET MVC Hello supporta il controllo ReportViewer hello.

tooincorporate ReportViewer nel sito Web di Microsoft Azure, è necessario hello toocomplete seguenti attività.

* **Aggiungere** assembly toohello pacchetto di distribuzione
* **Configurare** l'autenticazione e l'autorizzazione
* **Pubblicare** hello tooAzure applicazione Web ASP.NET

## <a name="prerequisites"></a>Prerequisiti
Nella sezione hello "indicazioni generali e procedure consigliate" in [SQL Server Business Intelligence in macchine virtuali di Azure](../classic/ps-sql-bi.md).

> [!NOTE]
> I controlli ReportViewer vengono offerti con Visual Studio Standard Edition o versione successiva. Se si utilizza hello Web Developer Express Edition, è necessario installare hello [MICROSOFT REPORT VIEWER 2012 RUNTIME](https://www.microsoft.com/download/details.aspx?id=35747) le funzionalità di runtime toouse hello ReportViewer.
> 
> ReportViewer configurato in modalità di elaborazione locale non è supportato in Microsoft Azure.

## <a name="adding-assemblies-toohello-deployment-package"></a>Aggiunta di assembly toohello pacchetto di distribuzione
Quando si ospitano l'applicazione di ASP.NET in locale, gli assembly di ReportViewer hello vengono solitamente installati direttamente nella hello global assembly cache (GAC) del server IIS hello durante l'installazione di Visual Studio e accessibili direttamente da un'applicazione hello. Tuttavia, quando si ospita l'applicazione ASP.NET nel cloud hello, Microsoft Azure non consente a qualsiasi componente installato toobe in hello Global Assembly Cache, pertanto è necessario assicurarsi che gli assembly di ReportViewer hello sono disponibili localmente per l'applicazione. È possibile effettuare questa operazione aggiungendo riferimenti toothem nel progetto e configurarli toobe copiato in locale.

In modalità di elaborazione remota hello controllo ReportViewer utilizza hello seguente assembly:

* **Microsoft.ReportViewer.WebForms.dll**: contiene codice di ReportViewer hello, che è necessario toouse ReportViewer nella pagina. Un riferimento per questo assembly viene aggiunto il progetto tooyour quando si elimina un controllo ReportViewer in una pagina ASP.NET nel progetto.
* **Microsoft.ReportViewer.Common.dll**: contiene le classi usate dal controllo ReportViewer hello in fase di esecuzione. Non viene automaticamente aggiunto tooyour progetto.

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a>tooadd tooMicrosoft.ReportViewer.Common un riferimento
* Mouse sul progetto **riferimenti** nodo e selezionare **Aggiungi riferimento**, selezionare l'assembly hello nella scheda .NET hello e fare clic su **OK**.

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a>assembly hello toomake accessibili localmente dall'applicazione ASP.NET
1. In hello **riferimenti** cartella, fare clic su assembly Microsoft.ReportViewer.Common hello in modo che le proprietà visualizzate nel riquadro Proprietà hello.
2. Nel riquadro Proprietà hello, impostare **Copia localmente** tooTrue.
3. Ripetere i passaggi 1 e 2 per Microsoft.ReportViewer.WebForms.

### <a name="tooget-reportviewer-language-pack"></a>tooget ReportViewer Language Pack
1. Installare hello appropriato Microsoft Report Viewer 2012 Runtime redistributable package [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386).
2. Lingua hello selezionare dall'elenco a discesa hello e pagina hello Ottiene toohello reindirizzato pagina dell'area download corrispondente.
3. Fare clic su **scaricare** download hello toostart di ReportViewerLP.exe.
4. Dopo aver scaricato ReportViewerLP.exe, fare clic su **eseguire** tooinstall immediatamente, oppure fare clic su **salvare** toosave è tooyour computer. Se si fa clic **salvare**, ricordare hello nome della cartella hello in cui salvare il file hello.
5. Individuare hello cartella in cui è stato salvato il file hello. Fare clic con il pulsante destro del mouse su ReportViewerLP.exe, scegliere **Esegui come amministratore** e quindi fare clic su **Sì**.
6. Dopo aver eseguito ReportViewerLP.exe, si noterà c:\windows\assembly hello contiene i file di risorse hello **disponibili** e **Microsoft** .

### <a name="tooconfigure-for-localized-reportviewer-control"></a>tooconfigure per il controllo ReportViewer localizzato
1. Scaricare e installare hello Microsoft Report Viewer 2012 Runtime redistributable package dall'hello seguente di sopra di istruzioni specificate.
2. Creare <language> cartella hello di progetto e copiarvi hello associati sono file di assembly di risorse. sono Hello toobe i file di assembly risorse copiati: **Microsoft.ReportViewer.Webforms.Resources.dll** e **Microsoft.ReportViewer.Common.Resources.dll**. Selezionare i file di assembly di risorse hello e nel riquadro Proprietà hello impostare **copiare tooOutput Directory** troppo "**Copia sempre**".
3. Impostare hello Culture e UICulture per il progetto web hello. Per ulteriori informazioni su come tooset hello delle impostazioni cultura e le impostazioni cultura dell'interfaccia utente per una pagina Web ASP.NET, vedere [come: Set hello delle impostazioni cultura e le impostazioni cultura dell'interfaccia utente per la globalizzazione di pagine Web ASP.NET](http://go.microsoft.com/fwlink/?LinkId=237461).

## <a name="configuring-authentication-and-authorization"></a>Configurazione dell'autenticazione e dell'autorizzazione
Hello ReportViewer deve toouse le credenziali appropriate tooauthenticate con il server di report hello e credenziali hello devono essere autorizzate dal hello report server di report tooaccess hello desiderato. Per informazioni sull'autenticazione, vedere il white paper relativo alle hello [server di report di macchina virtuale basato su Microsoft Azure e di controllo Visualizzatore report di Reporting Services](https://msdn.microsoft.com/library/azure/dn753698.aspx).

## <a name="publish-hello-aspnet-web-application-tooazure"></a>Pubblicare hello tooAzure applicazione Web ASP.NET
Per istruzioni sulla pubblicazione di un tooAzure di applicazione Web ASP.NET, vedere [procedura: eseguire la migrazione e pubblicare un'applicazione Web di tooAzure da Visual Studio](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) e [Introduzione alle applicazioni Web e ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md).

> [!IMPORTANT]
> Se hello comando Aggiungi progetto di distribuzione di Azure o Aggiungi progetto servizio Cloud di Azure non viene visualizzato nel menu di scelta rapida hello in Esplora soluzioni, potrebbe essere framework di destinazione hello toochange per hello progetto too.NET Framework 4.
> 
> i comandi di Hello due forniscono essenzialmente hello stessa funzionalità. Uno o hello altro comando verrà visualizzato nel menu di scelta rapida hello a seconda della versione di hello Microsoft Azure SDK è installato.
> 
> 

## <a name="resources"></a>Risorse
[Report di Microsoft](http://go.microsoft.com/fwlink/?LinkId=205399)

[SQL Server Business Intelligence in Macchine virtuali di Azure](../classic/ps-sql-bi.md)

[Utilizzare PowerShell tooCreate un Azure VM con un Server in modalità nativa Report](../classic/ps-sql-report.md)

