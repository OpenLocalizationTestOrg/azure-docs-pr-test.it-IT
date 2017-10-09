---
title: aaaFAQ per i database ClearDB MySql con il servizio App di Azure | Documenti Microsoft
description: Le risposte toocommon domande sull'utilizzo di database ClearDB MySQL con il servizio App di Azure.
documentationcenter: php
services: 
author: sunbuild
manager: yochayk
editor: 
tags: mysql
ms.assetid: c2ed5e78-6d7d-4d0c-b7ee-a52ae41ceab8
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: sumuth
ms.openlocfilehash: 3d9c9daca2b845ede8d3a1fdadefa7e668d62dee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="faq-for-cleardb-mysql-databases-with-azure-app-service"></a>Domande frequenti per i database MySQL ClearDB con il Servizio app di Azure
Queste domande frequenti offrono risposte a domande comuni sull'uso e l'acquisto di database MySQL ClearDB per App Web di Azure.

## <a name="what-options-do-i-have-for-mysql-on-azure"></a>Quali sono le opzioni disponibili per MySQL in Azure?
Sono disponibili diverse opzioni:

* [Database MySQL condiviso ClearDB](/marketplace/partners/cleardb/databases/)
* [Cluster Premium MySQL ClearDB](/marketplace/partners/cleardb-clusters/cluster/)
* [Cluster MySQL in esecuzione su una VM di Azure](https://github.com/azure/azure-quickstart-templates/tree/master/mysql-replication)
* [Istanza singola di MySQL in esecuzione su una VM di Azure](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

ClearDB è un servizio di hosting MySQL e gestisce l'infrastruttura di hello MySQL per l'utente. Quando si esegue la propria cluster MySQL o un database in una macchina virtuale di Azure, ha tooset di server MySQL hello e mantenerli aggiornati con le patch.

## <a name="do-i-need-a-credit-card-for-hello-web-app--mysql-template-in-hello-azure-marketplace"></a>È necessario una carta di credito per app Web hello + modello MySQL in Azure Marketplace hello?
Questo dipende dal tipo di hello di sottoscrizione in uso. Di seguito sono riportati alcuni tipi di sottoscrizione di uso comune:

* [Pagamento in base al consumo](/offers/ms-azr-0003p/): richiede una carta di credito sulla quale addebitare i costi dell'acquisto di un database MySQL a pagamento.
* [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/): include crediti da usare con i servizi di Microsoft Azure, ma non consente di acquistare risorse di terze parti. sottoscrizione abilitata per servizi di terze parti toopurchase o un database MySQL a pagamento, è necessario toouse una carta di credito. Per le app Web, è possibile creare un database MySQL ClearDB GRATUITO.
* [Abbonamento a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/) e **sviluppo Test MSDN prepagato**: tooFree simile valutazione, una sottoscrizione MSDN richiede toohave toopurchase una carta di credito una soluzione a pagamento di MySQL di ClearDB.
* [Contratto Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/): ai clienti con contratto Enterprise vengono addebitati ogni trimestre i costi per tutti gli acquisti (di terze parti) effettuati su Azure Marketplace in una fattura separata e consolidata. Verrà addebitato all'esterno di un impegno monetario hello per qualsiasi acquisti del marketplace. Si noti che, a questo punto, Azure Store non è disponibile toocustomers registrati in Azerbaigian, Croazia, Norvegia e Porto Rico. 
* [DreamSpark](https://www.dreamspark.com/Product/Product.aspx?productid=99): è possibile creare solo database ClearDB gratuiti per le app Web. Non è previsto alcun limite per il numero di hello dei database ClearDB MySQL gratuito che è possibile creare. Si noti che database liberi non toobe utilizzato per le app web di produzione, come il servizio è destinato solo versione di valutazione.

## <a name="why-was-i-charged-350-for-a-web-app--mysql-from-hello-azure-marketplace"></a>Motivo per cui è dovuto l'addebito 3.50 $ per un'app Web + MySQL da Azure Marketplace hello?
opzione di database predefinita Hello è Titan, ovvero $3.50. Durante la creazione del database non viene visualizzato il costo di hello e acquistare un database che non si intende erroneamente. Si sta tentando di toofind un'esperienza di hello tooimprove modo ma fino ad allora è necessario controllare tutti i piani tariffari selezionati per l'applicazione web e il database prima di scegliere **crea** e avvio della distribuzione hello delle risorse di hello.

## <a name="i-am-running-mysql-on-my-own-azure-virtual-machine-can-i-connect-my-azure-web-app-toomy-database"></a>Si esegue MySQL sulla propria macchina virtuale di Azure. È possibile collegare il database di toomy app web di Azure?
Sì. È possibile connettere il database di tooyour app web, purché la macchina virtuale di Azure sono assegnate app web di accesso remoto tooyour. Per altre informazioni, vedere l'articolo relativo all' [installazione di MySQL in una macchina virtuale](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="in-which-countries-are-cleardb-premium-mysql-clusters-supported"></a>In quali paesi sono supportati i cluster MySQL Premium ClearDB?
[I cluster MySQL di ClearDB Premium](/marketplace/partners/cleardb-clusters/cluster/) sono disponibili in tutte le aree di Azure in tutto il mondo con eccezione hello della Cina, Australia, Brasile meridionale e India.

## <a name="can-i-create-a-new-cluster-prior-toocreating-a-database-with-cleardb-premium-cluster-solution"></a>È possibile creare un nuovo toocreating precedenti di cluster un database con la soluzione di cluster ClearDB premium?
No, la creazione di cluster ClearDB vuoti non è supportata. Hello portale di Azure consente toocreate database in un cluster, che potrebbe creare un nuovo cluster in hello contemporaneamente.

## <a name="will-i-be-warned-if-i-try-toodelete-a-cleardb-mysql-database-that-is-in-use-by-one-of-my-applications"></a>Visualizzato un avviso se si tenta di toodelete un database ClearDB MySQL che è in uso da una delle applicazioni?
No, Azure non invierà alcuna notifica se si elimina un acquisto di Marketplace da cui dipende l'applicazione.

## <a name="which-regions-can-i-create-cleardb-databases-in"></a>In quali aree è possibile creare database ClearDB?
Azure Marketplace non è disponibile toocustomers registrati in Azerbaigian, Croazia, Norvegia o Porto Rico. ClearDB non è disponibile in queste aree.

## <a name="what-pricing-tier-should-i-choose-for-a-production-web-app-and-database"></a>Quale piano tariffario scegliere per un'app Web e un database di produzione?
Usare il piano tariffario Basic o superiore per le app Web. Per ClearDB è consigliabile un piano Saturn o Jupiter. Esaminare le funzionalità di hello & limitazioni di ogni piano tariffario per entrambi [App Web](https://azure.microsoft.com/pricing/details/app-service/) e [database ClearDB MySQL](/marketplace/partners/cleardb/databases/) hello toochoose uno adatta alle proprie esigenze.

## <a name="how-do-i-upgrade-my-cleardb-database-from-one-plan-tooanother"></a>Come aggiornare il database ClearDB da un piano tooanother?
In hello [portale di Azure](https://portal.azure.com), è possibile scalare in verticale di un database di hosting condiviso ClearDB. Leggere questo [articolo](https://blogs.msdn.microsoft.com/appserviceteam/2016/10/06/upgrade-your-cleardb-mysql-database-in-azure-portal/) toolearn altre. È attualmente non supporta l'aggiornamento per i cluster ClearDB Premium in hello portale di Azure.

## <a name="i-cant-see-my-cleardb-database-in-azure-portal"></a>Non è possibile visualizzare il database ClearDB nel Portale di Azure?
Se si crea il database ClearDB usando Gestione risorse di Azure o [nuovo portale di Azure](https://portal.azure.com), non sarà visibile in hello [portale di Azure precedente](https://manage.windowsazure.com). toowork-il problema è toolink il database manualmente toohello web app. Allo stesso modo se creare database ClearDB in hello [portale precedente](https://manage.windowsazure.com) non essere in grado di toosee il database di hello [nuovo portale di Azure](https://portal.azure.com). Non sussiste alcuna soluzione alternativa per uno scenario di quest'ultimo hello.

## <a name="who-do-i-contact-for-support-when-my-database-is-down"></a>Chi è possibile contattare per ottenere aiuto quando il database presenta un problema?
Per tutti i problemi relativi al database, contattare il [supporto ClearDB](https://www.cleardb.com/developers/help/support) . Essere preparati tooprovide con le informazioni sulla sottoscrizione di Azure.

## <a name="can-i-create-additional-users-for-my-cleardb-mysql-database-cluster-solution"></a>È possibile creare altri utenti dalla soluzione cluster database MySQL ClearDB?
No. Non è possibile creare altri utenti, ma è possibile creare altri database nel cluster database ClearDB.  

## <a name="can-basicpro-series-databases-be-upgraded-in-place-similar-tooplanetary-plans-today-on-cleardb-portal"></a>I database Basic/Pro serie possibile aggiornato sul posto simile tooPlanetary piani oggi nel portale di ClearDB?
Sì, i database della serie Basic possono essere aggiornati sul posto (da Basic 60 a Basic 500). Quelli della serie Pro possono essere aggiornati sul posto (da Pro 125 a Pro 1000) ad eccezione di Pro 60. L'aggiornamento del database Pro 60 attualmente non è supportato. 

## <a name="when-i-migrate-my-resources-from-one-subscription-tooanother-does-my-cleardb-mysql-database-get-migrated-as-well"></a>Quando esegue la migrazione di risorse da una sottoscrizione tooanother, il database ClearDB MySQL ottenere migrato nonché?
Quando si esegue la migrazione delle risorse tra le sottoscrizioni, esistono alcune [limitazioni](app-service-web/app-service-move-resources.md) . Il database MySQL ClearDB è un servizio di terze parti, pertanto non è possibile eseguirne la migrazione durante la migrazione delle sottoscrizioni di Azure. Se non si gestiscono migrazione hello del MySQL database precedente toomigrating Azure risorse, il ClearDB MySQL database possono essere disabilitati. Eseguire prima la migrazione manuale dei database e quindi eseguire la migrazione delle sottoscrizioni di Azure per l'app Web. 

## <a name="i-hit-hello-spending-limit-on-my-subscription-i-removed-hello-limit-and-my-app-service-is-online-however-hello-database-is-not-accessible-how-do-i-re-enable-hello-cleardb-database"></a>Passaggi hello limite di spesa la sottoscrizione. Rimosso il limite di hello e il servizio App è in linea, ma hello database non è accessibile. Come si abilita nuovamente i database ClearDB hello?
Contatto [ClearDB supporto](https://www.cleardb.com/developers/help/support) database hello toore attiva. Comunicare le informazioni relative alla sottoscrizione di Azure e il nome del database.

## <a name="can-i-transfer-a-cleardb-database-from-a-credit-card-subscription-tooan-ea-subscription"></a>È possibile trasferire un database ClearDB da una sottoscrizione di carta di credito sottoscrizione tooan EA?
Database ClearDB esistenti utilizzano hello carta di credito associata a una delle sottoscrizioni esistenti hello. toouse una sottoscrizione EA è necessario toomigrate il nuovo database tooa di dati:

* Acquistare un nuovo database ClearDB con la sottoscrizione con contratto Enterprise.
* Eseguire la migrazione al nuovo database tooyour di dati.
* Aggiornare l'applicazione toouse hello nuovo database.
* Eliminare il vecchio database ClearDB.

Quando si crea una nuova app web con MySQL (ClearDB) o un database di MySQL (ClearDB), sottoscrizione hello che scelta determina il pagamento per il servizio di hello. Con una sottoscrizione, EA è non verrà bloccata approvvigionamento hello di servizi di terze parti hello come ClearDB in hello portale di Azure. Le sottoscrizioni con contratto Enterprise vengono addebitate al di fuori dell'impegno monetario e vengono fatturate su base trimestrale e in modo posticipato. Hello EA cliente dovrebbe disporre di tooset di un metodo di pagamento per i servizi del marketplace di terze parti, ad esempio toopay una carta di credito.

## <a name="where-can-i-see-hello-charges-for-cleardb-resources-in-an-ea-subscription"></a>In cui è possibile visualizzare gli addebiti di hello per le risorse in una sottoscrizione EA ClearDB?
Per i clienti EA Direct, sono visibili in Enterprise Portal hello costi di Azure Marketplace. Si noti che tutti gli acquisti e l'uso di Marketplace vengono addebitati al di fuori dell'impegno monetario e vengono fatturati su base trimestrale e in modo posticipato. I clienti EA hanno toopay direttamente il provider di servizi di terze parti di toohello e può pertanto abilitando un metodo di pagamento, ad esempio una carta di credito con loro EA account.

I clienti EA indiretti è possono trovare le sottoscrizioni di Azure Marketplace nel hello **Gestisci sottoscrizioni** pagina di hello Enterprise Portal, ma prezzi è nascosto. I clienti devono contattare il proprio LSP per informazioni sugli addebiti di Marketplace.

Accesso tooAzure Marketplace per i servizi di terze parti può essere gestite da amministratori di registrazione di Azure EA. Possono disabilitare o riabilitare l'accesso too3rd entità acquisti da hello archivio Gestisci account e le sottoscrizioni nella sezione account hello hello Enterprise Portal.

## <a name="who-do-i-contact-for-questions-about-my-bill-for-cleardb-services-in-my-ea-subscription"></a>Chi contattare per domande sulla fatturazione per i servizi ClearDB nella sottoscrizione con contratto Enterprise?
Contatto [Enterprise il supporto tecnico](http://aka.ms/AzureEntSupport) con toobilling relativamente sotto la registrazione EA. Team di supporto portale EA Hello verrà rispondere alla domanda o la risoluzione del problema.

## <a name="more-information"></a>Altre informazioni
[Domande frequenti su Azure Marketplace](/marketplace/faq/)

