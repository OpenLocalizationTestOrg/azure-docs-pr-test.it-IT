---
title: note sulla versione di catalogo dati aaaAzure | Documenti Microsoft
description: Note sulla versione del Catalogo dati di Azure.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="adf34-103">Note sulla versione del Catalogo dati di Azure</span><span class="sxs-lookup"><span data-stu-id="adf34-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="adf34-104">Note sulla versione di hello 20 novembre 2015 di Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="adf34-104">Notes for hello November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="adf34-105">Apertura di origini di dati in Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="adf34-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="adf34-106">Quando si utilizza l'opzione "Apri in Power BI Desktop" hello hello **Azure Data Catalog** portale, gli utenti possono verificarsi uno dei due problemi in hello applicazione Power BI Desktop:</span><span class="sxs-lookup"><span data-stu-id="adf34-106">When using hello "Open in Power BI Desktop" option from hello **Azure Data Catalog** portal, users may encounter one of two problems in hello Power BI Desktop application:</span></span>

* <span data-ttu-id="adf34-107">Viene visualizzata una finestra di dialogo con titolo hello "Non è possibile tooOpen documento"</span><span class="sxs-lookup"><span data-stu-id="adf34-107">A dialog box with hello title "Unable tooOpen Document" is displayed</span></span>
* <span data-ttu-id="adf34-108">si apre Hello applicazione Power BI Desktop, ma sembra che file hello toobe vuoto</span><span class="sxs-lookup"><span data-stu-id="adf34-108">hello Power BI Desktop application opens, but hello file appears toobe empty</span></span>

<span data-ttu-id="adf34-109">Per ogni situazione, è possibile risolvere il problema di hello scaricando e installando l'ultima versione di hello di Power BI Desktop da [PowerBI.com](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="adf34-109">For each situation, hello problem can be resolved by downloading and installing hello latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="adf34-110">Note sulla versione di hello 13 novembre 2015 di Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="adf34-110">Notes for hello November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-tooteradata"></a><span data-ttu-id="adf34-111">La registrazione e connessione tooTeradata</span><span class="sxs-lookup"><span data-stu-id="adf34-111">Registering and connecting tooTeradata</span></span>
<span data-ttu-id="adf34-112">Quando ci si connette a origini dati tooTeradata utenti sia installato il driver ODBC di Teradata corretto di hello che corrispondono ai bit hello (32 bit o 64 bit) del software hello in uso.</span><span class="sxs-lookup"><span data-stu-id="adf34-112">When connecting tooTeradata data sources users must have installed hello correct Teradata ODBC driver that match hello bitness (32-bit or 64-bit) of hello software being used.</span></span>

<span data-ttu-id="adf34-113">A partire da questo servizio ADC data di rilascio, hello più recente [driver ODBC di Teradata per windows (versione 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) è compatibile con Office 2013, ma non con Office 2016.</span><span class="sxs-lookup"><span data-stu-id="adf34-113">As of this ADC release date, hello most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="adf34-114">Note sulla versione di hello il 13 luglio 2015 di Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="adf34-114">Notes for hello July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-toooracle-database"></a><span data-ttu-id="adf34-115">La registrazione e la connessione di Database tooOracle</span><span class="sxs-lookup"><span data-stu-id="adf34-115">Registering and connecting tooOracle Database</span></span>
<span data-ttu-id="adf34-116">Quando la connessione degli utenti di origini dati di tooOracle Database deve essere installato driver Oracle corretti hello che corrispondono ai bit hello (32 bit o 64 bit) del software hello in uso.</span><span class="sxs-lookup"><span data-stu-id="adf34-116">When connecting tooOracle Database data sources users must have installed hello correct Oracle drivers that match hello bitness (32-bit or 64-bit) of hello software being used.</span></span>

* <span data-ttu-id="adf34-117">Verrà utilizzato durante la registrazione di origini dati Oracle in un computer che esegue Windows a 32 bit, driver Oracle a 32 bit hello</span><span class="sxs-lookup"><span data-stu-id="adf34-117">When registering Oracle data sources on a computer running 32-bit Windows, hello 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="adf34-118">Verrà utilizzato durante la registrazione di origini dati Oracle in un computer che esegue Windows a 64 bit, driver Oracle a 64 bit hello</span><span class="sxs-lookup"><span data-stu-id="adf34-118">When registering Oracle data sources on a computer running 64-bit Windows, hello 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="adf34-119">Quando ci si connette a origini dati tooOracle utilizzando Excel in un computer con una versione a 32 bit hello di Microsoft Office, è incluso in Windows a 64 bit, verrà utilizzato driver Oracle a 32 bit hello</span><span class="sxs-lookup"><span data-stu-id="adf34-119">When connecting tooOracle data sources using Excel on a computer running hello 32-bit version of Microsoft Office, including on 64-bit Windows, hello 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="adf34-120">Verrà utilizzato durante la connessione a origini dati tooOracle utilizzando Excel in un computer con una versione a 64 bit di Microsoft Office hello, driver Oracle a 64 bit hello</span><span class="sxs-lookup"><span data-stu-id="adf34-120">When connecting tooOracle data sources using Excel on a computer running hello 64-bit version of Microsoft Office, hello 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-toosql-server-reporting-services"></a><span data-ttu-id="adf34-121">La registrazione e connessione tooSQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="adf34-121">Registering and connecting tooSQL Server Reporting Services</span></span>
<span data-ttu-id="adf34-122">Il supporto per le origini dati di SQL Server Reporting Services (SSRS) è attualmente limitata tooNative solo i server in modalità.</span><span class="sxs-lookup"><span data-stu-id="adf34-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited tooNative Mode servers only.</span></span> <span data-ttu-id="adf34-123">Il supporto per SSRS in modalità SharePoint verrà aggiunto in una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="adf34-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="adf34-124">Apertura degli asset di dati in Excel</span><span class="sxs-lookup"><span data-stu-id="adf34-124">Opening data assets in Excel</span></span>
<span data-ttu-id="adf34-125">Quando si apre l'asset di dati in Microsoft Excel dal hello **Azure Data Catalog** portale, gli utenti potrebbero essere richieste con un **avviso di protezione di Microsoft Excel** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="adf34-125">When opening data assets in Microsoft Excel from hello **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="adf34-126">Si tratta di standard, il comportamento previsto e gli utenti possono selezionare **abilitare** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="adf34-126">This is standard, expected behavior, and users can select **Enable** toocontinue.</span></span>

<span data-ttu-id="adf34-127">Per altre informazioni, vedere [Attivazione o disattivazione degli avvisi di protezione relativi ai collegamenti a siti Web sospetti e a file scaricati da tali siti](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span><span class="sxs-lookup"><span data-stu-id="adf34-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="adf34-128">Configurazione di proxy e criteri e registrazione dell'origine dati</span><span class="sxs-lookup"><span data-stu-id="adf34-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="adf34-129">Gli utenti possono riscontrare situazioni in cui possono registrare nel portale di Azure Data Catalog toohello, ma quando tentano di toolog su toohello strumento di registrazione origine dati che viene rilevato un messaggio di errore che ne impedisce l'accesso.</span><span class="sxs-lookup"><span data-stu-id="adf34-129">Users may encounter a situation where they can log on toohello Azure Data Catalog portal, but when they attempt toolog on toohello data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="adf34-130">Le possibili cause di questo comportamento problematico sono due:</span><span class="sxs-lookup"><span data-stu-id="adf34-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="adf34-131">**Causa 1: Configurazione di Active Directory Federation Services** strumento per la registrazione di origine dati hello utilizza gli accessi utente toovalidate di autenticazione basata su form in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="adf34-131">**Cause 1: Active Directory Federation Services configuration** hello data source registration tool uses Forms Authentication toovalidate user logons against Active Directory.</span></span> <span data-ttu-id="adf34-132">Per l'accesso con esito positivo, autenticazione basata su form deve essere abilitato in Criteri di autenticazione globali hello dall'amministratore di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="adf34-132">For successful logon, Forms Authentication must be enabled in hello Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="adf34-133">In alcuni casi, questo errore può verificarsi solo quando l'utente hello è nella rete aziendale hello o solo quando si connette utente hello dalla rete aziendale esterna hello.</span><span class="sxs-lookup"><span data-stu-id="adf34-133">In some situations, this error behavior may occur only when hello user is on hello company network, or only when hello user is connecting from outside hello company network.</span></span> <span data-ttu-id="adf34-134">Criteri di autenticazione globali Hello consente toobe di metodi di autenticazione abilitato separatamente per le connessioni extranet e intranet.</span><span class="sxs-lookup"><span data-stu-id="adf34-134">hello Global Authentication Policy allows authentication methods toobe enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="adf34-135">Se l'autenticazione basata su form non è abilitato per la rete hello dal quale hello utente si connette, potrebbero verificarsi errori di accesso.</span><span class="sxs-lookup"><span data-stu-id="adf34-135">Logon errors may occur if Forms Authentication is not enabled for hello network from which hello user is connecting.</span></span>

<span data-ttu-id="adf34-136">Per altre informazioni, vedere [Configurare i criteri di autenticazione](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="adf34-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="adf34-137">**Causa 2: Configurazione del proxy di rete** se la rete aziendale hello utilizza un server proxy, lo strumento di registrazione hello potrebbe non essere in grado di tooconnect tooAzure Active Directory tramite proxy hello.</span><span class="sxs-lookup"><span data-stu-id="adf34-137">**Cause 2: Network proxy configuration** If hello corporate network uses a proxy server, hello registration tool may not be able tooconnect tooAzure Active Directory through hello proxy.</span></span> <span data-ttu-id="adf34-138">Gli utenti possono verificare che lo strumento di registrazione hello modificando il file di configurazione dello strumento hello, aggiunta di questo file toohello sezione:</span><span class="sxs-lookup"><span data-stu-id="adf34-138">Users can ensure that hello registration tool by editing hello tool’s configuration file, adding this section toohello file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="adf34-139">toolocate hello RegistrationTool.exe.config file, avviare lo strumento di registrazione hello e quindi aprire l'utilità Gestione attività Windows hello.</span><span class="sxs-lookup"><span data-stu-id="adf34-139">toolocate hello RegistrationTool.exe.config file, launch hello registration tool, and then open hello Windows Task Manager utility.</span></span> <span data-ttu-id="adf34-140">Nella scheda dettagli di hello in Gestione attività, fare clic su RegistrationTool.exe e scegliere Apri percorso file dal menu a comparsa hello.</span><span class="sxs-lookup"><span data-stu-id="adf34-140">On hello Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from hello pop-up menu.</span></span>
