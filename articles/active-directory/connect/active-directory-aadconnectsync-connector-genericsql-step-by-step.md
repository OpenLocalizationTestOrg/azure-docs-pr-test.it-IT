---
title: passaggio aaaGeneric passo-passo connettore SQL | Documenti Microsoft
description: In questo articolo si verifica attraverso un semplice sistema HR utilizzando dettagliate hello connettore SQL generico.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="226d1-103">Procedura dettagliata per la creazione del connettore Generic SQL</span><span class="sxs-lookup"><span data-stu-id="226d1-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="226d1-104">Questo argomento è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="226d1-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="226d1-105">Verrà creato un semplice database delle risorse umane di esempio che sarà usato per importare alcuni utenti con la relativa appartenenza ai gruppi.</span><span class="sxs-lookup"><span data-stu-id="226d1-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-hello-sample-database"></a><span data-ttu-id="226d1-106">Preparare i database di esempio hello</span><span class="sxs-lookup"><span data-stu-id="226d1-106">Prepare hello sample database</span></span>
<span data-ttu-id="226d1-107">In un server che esegue SQL Server, eseguire script SQL hello trovato nel [appendice](#appendix-a). Questo script crea un database di esempio con il nome di hello GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="226d1-107">On a server running SQL Server, run hello SQL script found in [Appendix A](#appendix-a). This script creates a sample database with hello name GSQLDEMO.</span></span> <span data-ttu-id="226d1-108">modello a oggetti Hello per hello creati database simile a questa immagine:</span><span class="sxs-lookup"><span data-stu-id="226d1-108">hello object model for hello created database looks like this picture:</span></span>  
<span data-ttu-id="226d1-109">![Modello a oggetti](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="226d1-110">Creare anche un utente a cui si desidera toouse tooconnect toohello database.</span><span class="sxs-lookup"><span data-stu-id="226d1-110">Also create a user you want toouse tooconnect toohello database.</span></span> <span data-ttu-id="226d1-111">In questa procedura dettagliata, utente hello viene chiamato FABRIKAM\SQLUser e si trova nel dominio hello.</span><span class="sxs-lookup"><span data-stu-id="226d1-111">In this walkthrough, hello user is called FABRIKAM\SQLUser and located in hello domain.</span></span>

## <a name="create-hello-odbc-connection-file"></a><span data-ttu-id="226d1-112">Creare file di connessione ODBC hello</span><span class="sxs-lookup"><span data-stu-id="226d1-112">Create hello ODBC connection file</span></span>
<span data-ttu-id="226d1-113">Hello connettore SQL generico utilizza ODBC tooconnect toohello remote server.</span><span class="sxs-lookup"><span data-stu-id="226d1-113">hello Generic SQL Connector is using ODBC tooconnect toohello remote server.</span></span> <span data-ttu-id="226d1-114">È prima necessario toocreate un file con informazioni di connessione ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="226d1-114">First we need toocreate a file with hello ODBC connection information.</span></span>

1. <span data-ttu-id="226d1-115">Avviare l'utilità di gestione di hello ODBC nel server:</span><span class="sxs-lookup"><span data-stu-id="226d1-115">Start hello ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="226d1-117">Scheda selezionare hello **DSN su File**.</span><span class="sxs-lookup"><span data-stu-id="226d1-117">Select hello tab **File DSN**.</span></span> <span data-ttu-id="226d1-118">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="226d1-118">Click **Add...**.</span></span>  
   <span data-ttu-id="226d1-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="226d1-120">Hello out-of-box driver works costituisce, pertanto selezionarlo e fare clic su **successivo >**.</span><span class="sxs-lookup"><span data-stu-id="226d1-120">hello out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="226d1-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="226d1-122">Assegnare, ad esempio, un nome file hello **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="226d1-122">Give hello file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="226d1-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="226d1-124">Fare clic su **Finish**(Fine).</span><span class="sxs-lookup"><span data-stu-id="226d1-124">Click **Finish**.</span></span>  
   <span data-ttu-id="226d1-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="226d1-126">Connessione di hello tooconfigure Time.</span><span class="sxs-lookup"><span data-stu-id="226d1-126">Time tooconfigure hello connection.</span></span> <span data-ttu-id="226d1-127">Origine dati hello viene fornita una descrizione valida e specificare il nome di hello del server di hello che esegue SQL Server.</span><span class="sxs-lookup"><span data-stu-id="226d1-127">Give hello data source a good description and provide hello name of hello server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="226d1-129">Selezionare come tooauthenticate con SQL.</span><span class="sxs-lookup"><span data-stu-id="226d1-129">Select how tooauthenticate with SQL.</span></span> <span data-ttu-id="226d1-130">In questo caso si userà l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="226d1-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="226d1-132">Specificare il nome di hello hello del database di esempio, **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="226d1-132">Provide hello name of hello sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="226d1-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="226d1-134">In questa schermata mantenere tutte le selezioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="226d1-134">Keep everything default on this screen.</span></span> <span data-ttu-id="226d1-135">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="226d1-135">Click **Finish**.</span></span>  
   <span data-ttu-id="226d1-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="226d1-137">tooverify funzionino come previsto, fare clic su **origine dati di Test**.</span><span class="sxs-lookup"><span data-stu-id="226d1-137">tooverify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="226d1-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="226d1-139">Verificare che hello test ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="226d1-139">Make sure hello test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="226d1-141">file di configurazione ODBC Hello dovrebbe ora essere visibile nel DSN su File.</span><span class="sxs-lookup"><span data-stu-id="226d1-141">hello ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="226d1-143">È ora disponibile il file di hello è necessaria e iniziare a creare hello connettore.</span><span class="sxs-lookup"><span data-stu-id="226d1-143">We now have hello file we need and can start creating hello Connector.</span></span>

## <a name="create-hello-generic-sql-connector"></a><span data-ttu-id="226d1-144">Creare hello connettore SQL generico</span><span class="sxs-lookup"><span data-stu-id="226d1-144">Create hello Generic SQL Connector</span></span>
1. <span data-ttu-id="226d1-145">In hello UI Synchronization Service Manager, selezionare **connettori** e **crea**.</span><span class="sxs-lookup"><span data-stu-id="226d1-145">In hello Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="226d1-146">Selezionare **Generic SQL (Microsoft)** e assegnargli un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="226d1-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="226d1-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="226d1-148">Trovare il file DSN hello creato nella sezione precedente hello e caricarlo toohello server.</span><span class="sxs-lookup"><span data-stu-id="226d1-148">Find hello DSN file you created in hello previous section and upload it toohello server.</span></span> <span data-ttu-id="226d1-149">Fornire hello credenziali tooconnect toohello database.</span><span class="sxs-lookup"><span data-stu-id="226d1-149">Provide hello credentials tooconnect toohello database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="226d1-151">In questa procedura dettagliata si considera un caso semplificato in cui esistono due tipi di oggetti, **User** e **Group**.</span><span class="sxs-lookup"><span data-stu-id="226d1-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="226d1-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="226d1-153">gli attributi di hello toofind, si vuole hello connettore toodetect tali attributi esaminando tabella hello stessa.</span><span class="sxs-lookup"><span data-stu-id="226d1-153">toofind hello attributes, we want hello Connector toodetect those attributes by looking at hello table itself.</span></span> <span data-ttu-id="226d1-154">Poiché **utenti** è una parola riservata in SQL, è necessario tooprovide in quadrato parentesi quadre [].</span><span class="sxs-lookup"><span data-stu-id="226d1-154">Since **Users** is a reserved word in SQL, we need tooprovide it in square brackets [ ].</span></span>  
   <span data-ttu-id="226d1-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="226d1-156">Attributo di ancoraggio ora toodefine hello e attributo DN hello.</span><span class="sxs-lookup"><span data-stu-id="226d1-156">Time toodefine hello anchor attribute and hello DN attribute.</span></span> <span data-ttu-id="226d1-157">Per **utenti**, utilizziamo combinazione hello di hello due attributi username ed EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="226d1-157">For **Users**, we use hello combination of hello two attributes username and EmployeeID.</span></span> <span data-ttu-id="226d1-158">Per **Group**si usa GroupName, non molto plausibile in un caso reale, ma adeguato per questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="226d1-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="226d1-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="226d1-160">Non tutti i tipi di attributo possono essere rilevati in un database SQL.</span><span class="sxs-lookup"><span data-stu-id="226d1-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="226d1-161">in particolare, non è tipo di attributo di riferimento Hello.</span><span class="sxs-lookup"><span data-stu-id="226d1-161">hello reference attribute type in particular cannot.</span></span> <span data-ttu-id="226d1-162">Per il tipo di oggetto gruppo hello, dobbiamo toochange hello OwnerID e tooreference MemberID.</span><span class="sxs-lookup"><span data-stu-id="226d1-162">For hello group object type, we need toochange hello OwnerID and MemberID tooreference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="226d1-164">gli attributi di Hello è selezionato come attributi di riferimento nel passaggio precedente hello richiedono questi valori sono un riferimento al tipo di oggetto di hello.</span><span class="sxs-lookup"><span data-stu-id="226d1-164">hello attributes we selected as reference attributes in hello previous step require hello object type these values are a reference to.</span></span> <span data-ttu-id="226d1-165">In questo caso, hello il tipo di oggetto utente.</span><span class="sxs-lookup"><span data-stu-id="226d1-165">In our case, hello User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="226d1-167">Nella pagina parametri globali hello selezionare **filigrana** come strategia di hello delta.</span><span class="sxs-lookup"><span data-stu-id="226d1-167">On hello Global Parameters page, select **Watermark** as hello delta strategy.</span></span> <span data-ttu-id="226d1-168">Anche digitare nel formato di data/ora hello **AAAA-MM-gg hh: mm:**.</span><span class="sxs-lookup"><span data-stu-id="226d1-168">Also type in hello date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="226d1-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="226d1-170">In hello **Configura partizioni e gerarchie** pagina, selezionare entrambi i tipi di oggetto.</span><span class="sxs-lookup"><span data-stu-id="226d1-170">On hello **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="226d1-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="226d1-172">In hello **Seleziona tipi di oggetti** e **selezione attributi**, selezionare i tipi di oggetto e tutti gli attributi.</span><span class="sxs-lookup"><span data-stu-id="226d1-172">On hello **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="226d1-173">In hello **configurare Anchor** pagina, fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="226d1-173">On hello **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="226d1-174">Creare i profili di esecuzione</span><span class="sxs-lookup"><span data-stu-id="226d1-174">Create Run Profiles</span></span>
1. <span data-ttu-id="226d1-175">In hello UI Synchronization Service Manager, selezionare **connettori**, e **Configure Run Profiles**.</span><span class="sxs-lookup"><span data-stu-id="226d1-175">In hello Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="226d1-176">Fare clic su **New Profile**(Nuovo profilo).</span><span class="sxs-lookup"><span data-stu-id="226d1-176">Click **New Profile**.</span></span> <span data-ttu-id="226d1-177">Si inizierà con **Full Import**(Importazione completa).</span><span class="sxs-lookup"><span data-stu-id="226d1-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="226d1-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="226d1-179">Selezionare il tipo di hello **importazione completa (solo fase)**.</span><span class="sxs-lookup"><span data-stu-id="226d1-179">Select hello type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="226d1-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="226d1-181">Selezionare la partizione hello **oggetto = utente**.</span><span class="sxs-lookup"><span data-stu-id="226d1-181">Select hello partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="226d1-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="226d1-183">Selezionare **Table** (Tabella) e digitare **[USERS]**.</span><span class="sxs-lookup"><span data-stu-id="226d1-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="226d1-184">Scorrere verso il basso sezione tipo di oggetto multivalore toohello e immettere dati hello come hello seguente immagine.</span><span class="sxs-lookup"><span data-stu-id="226d1-184">Scroll down toohello multi-valued object type section and enter hello data as in hello following picture.</span></span> <span data-ttu-id="226d1-185">Selezionare **fine** passaggio hello toosave.</span><span class="sxs-lookup"><span data-stu-id="226d1-185">Select **Finish** toosave hello step.</span></span>  
   <span data-ttu-id="226d1-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="226d1-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="226d1-188">Selezionare **New Step**(Nuovo passaggio).</span><span class="sxs-lookup"><span data-stu-id="226d1-188">Select **New Step**.</span></span> <span data-ttu-id="226d1-189">Questa volta selezionare **OBJECT=Group**.</span><span class="sxs-lookup"><span data-stu-id="226d1-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="226d1-190">Hello ultima pagina, utilizzare configurazione hello come hello seguente immagine.</span><span class="sxs-lookup"><span data-stu-id="226d1-190">On hello last page, use hello configuration as in hello following picture.</span></span> <span data-ttu-id="226d1-191">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="226d1-191">Click **Finish**.</span></span>  
   <span data-ttu-id="226d1-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="226d1-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="226d1-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="226d1-194">Facoltativo: se si vuole, è possibile configurare altri profili di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="226d1-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="226d1-195">Per questa procedura dettagliata viene utilizzato solo hello importazione completa.</span><span class="sxs-lookup"><span data-stu-id="226d1-195">For this walkthrough, only hello Full Import is used.</span></span>
7. <span data-ttu-id="226d1-196">Fare clic su **OK** toofinish la modifica di profili di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="226d1-196">Click **OK** toofinish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-hello-import"></a><span data-ttu-id="226d1-197">Aggiungere alcuni importazione hello test e i dati di test</span><span class="sxs-lookup"><span data-stu-id="226d1-197">Add some test data and test hello import</span></span>
<span data-ttu-id="226d1-198">Immettere alcuni dati di prova nel database di esempio.</span><span class="sxs-lookup"><span data-stu-id="226d1-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="226d1-199">Quando si è pronti, selezionare **Run** (Esegui) e **Full import** (Importazione completa).</span><span class="sxs-lookup"><span data-stu-id="226d1-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="226d1-200">In questo esempio si ottiene un utente con due numeri di telefono e un gruppo con alcuni membri.</span><span class="sxs-lookup"><span data-stu-id="226d1-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="226d1-203">Appendice A</span><span class="sxs-lookup"><span data-stu-id="226d1-203">Appendix A</span></span>
<span data-ttu-id="226d1-204">**Database di esempio hello toocreate script SQL**</span><span class="sxs-lookup"><span data-stu-id="226d1-204">**SQL script toocreate hello sample database**</span></span>

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
