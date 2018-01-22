---
title: "Einführung in Razor-Seiten in ASP.NET Core"
author: Rick-Anderson
description: "Diese Dokumentation stellt eine Übersicht über die Verwendung von Razor-Seiten in ASP.NET Core bereit, um die Entwicklung von auf Seiten bezogene Szenarios zu vereinfachen."
ms.author: riande
manager: wpickett
ms.date: 09/12/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/razor-pages/index
ms.openlocfilehash: 2c9f4291d458032e6aea961707e74e1e1da90b0a
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="introduction-to-razor-pages-in-aspnet-core"></a><span data-ttu-id="107eb-103">Einführung in Razor-Seiten in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="107eb-103">Introduction to Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="107eb-104">Von [Rick Anderson](https://twitter.com/RickAndMSFT) und [Ryan Nowak](https://github.com/rynowak)</span><span class="sxs-lookup"><span data-stu-id="107eb-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Ryan Nowak](https://github.com/rynowak)</span></span>

<span data-ttu-id="107eb-105">Razor-Seiten ist ein neues Feature von ASP.NET Core MVC, mit dem codierungsseitige Szenarios einfacher und produktiver werden.</span><span class="sxs-lookup"><span data-stu-id="107eb-105">Razor Pages is a new feature of ASP.NET Core MVC that makes coding page-focused scenarios easier and more productive.</span></span>

<span data-ttu-id="107eb-106">Weitere Informationen zu einem Tutorial, in dem der Model-View-Controller-Ansatz verwendet wird, finden Sie unter [Getting started with ASP.NET Core MVC (Erste Schritte mit ASP.NET Core MVC)](xref:tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="107eb-106">If you're looking for a tutorial that uses the Model-View-Controller approach, see [Getting started with ASP.NET Core MVC](xref:tutorials/first-mvc-app/start-mvc).</span></span>

<span data-ttu-id="107eb-107">Dieses Dokument bietet eine Einführung in Razor-Seiten.</span><span class="sxs-lookup"><span data-stu-id="107eb-107">This document provides an introduction to Razor Pages.</span></span> <span data-ttu-id="107eb-108">Es handelt sich nicht um ein Schritt-für-Schritt-Tutorial.</span><span class="sxs-lookup"><span data-stu-id="107eb-108">It's not a step by step tutorial.</span></span> <span data-ttu-id="107eb-109">Wenn es Ihnen Probleme bereitet, die Ausführungen in einigen Abschnitten nachzuvollziehen, lesen Sie [Erste Schritte mit Razor-Seiten](xref:tutorials/razor-pages/razor-pages-start).</span><span class="sxs-lookup"><span data-stu-id="107eb-109">If you find some of the sections difficult to follow, see [Getting started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start).</span></span>

<a name="prerequisites"></a>

## <a name="aspnet-core-20-prerequisites"></a><span data-ttu-id="107eb-110">Anforderungen von ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="107eb-110">ASP.NET Core 2.0 prerequisites</span></span>

<span data-ttu-id="107eb-111">Installieren Sie [.NET Core](https://www.microsoft.com/net/core) 2.0.0 oder höher.</span><span class="sxs-lookup"><span data-stu-id="107eb-111">Install [.NET Core](https://www.microsoft.com/net/core) 2.0.0 or later.</span></span>

<span data-ttu-id="107eb-112">Wenn Sie Visual Studio verwenden, installieren Sie [Visual Studio](https://www.visualstudio.com/vs/) 2017 Version 15.3 oder höher mit folgenden Workloads:</span><span class="sxs-lookup"><span data-stu-id="107eb-112">If you're using Visual Studio, install [Visual Studio](https://www.visualstudio.com/vs/) 2017 version 15.3 or later with the following workloads:</span></span>

* <span data-ttu-id="107eb-113">**ASP.NET und Webentwicklung**</span><span class="sxs-lookup"><span data-stu-id="107eb-113">**ASP.NET and web development**</span></span>
* <span data-ttu-id="107eb-114">**Plattformübergreifende .NET Core-Entwicklung**</span><span class="sxs-lookup"><span data-stu-id="107eb-114">**.NET Core cross-platform development**</span></span>

<a name="rpvs17"></a>

## <a name="creating-a-razor-pages-project"></a><span data-ttu-id="107eb-115">Erstellen eines Projekts mit Razor-Seiten</span><span class="sxs-lookup"><span data-stu-id="107eb-115">Creating a Razor Pages project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="107eb-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="107eb-116">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="107eb-117">Weitere Informationen zum Erstellen eines Projekts mit Razor-Seiten mithilfe von Visual Studio finden Sie unter [Getting started with Razor Pages (Erste Schritte mit Razor-Seiten)](xref:tutorials/razor-pages/razor-pages-start).</span><span class="sxs-lookup"><span data-stu-id="107eb-117">See [Getting started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start) for detailed instructions on how to create a Razor Pages project using Visual Studio.</span></span>

#   <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="107eb-118">Visual Studio für Mac</span><span class="sxs-lookup"><span data-stu-id="107eb-118">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="107eb-119">Führen Sie `dotnet new razor` über die Befehlszeile aus.</span><span class="sxs-lookup"><span data-stu-id="107eb-119">Run `dotnet new razor` from the command line.</span></span>

<span data-ttu-id="107eb-120">Öffnen Sie die generierte Datei *.csproj* aus Visual Studio für Mac.</span><span class="sxs-lookup"><span data-stu-id="107eb-120">Open the generated *.csproj* file from Visual Studio for Mac.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="107eb-121">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="107eb-121">Visual Studio Code</span></span>](#tab/visual-studio-code) 

<span data-ttu-id="107eb-122">Führen Sie `dotnet new razor` über die Befehlszeile aus.</span><span class="sxs-lookup"><span data-stu-id="107eb-122">Run `dotnet new razor` from the command line.</span></span>

#   <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="107eb-123">.NET Core-CLI</span><span class="sxs-lookup"><span data-stu-id="107eb-123">.NET Core CLI</span></span>](#tab/netcore-cli) 

<span data-ttu-id="107eb-124">Führen Sie `dotnet new razor` über die Befehlszeile aus.</span><span class="sxs-lookup"><span data-stu-id="107eb-124">Run `dotnet new razor` from the command line.</span></span>

---

## <a name="razor-pages"></a><span data-ttu-id="107eb-125">Razor-Seiten</span><span class="sxs-lookup"><span data-stu-id="107eb-125">Razor Pages</span></span>

<span data-ttu-id="107eb-126">Razor-Seiten ist in *Startup.cs* aktiviert:</span><span class="sxs-lookup"><span data-stu-id="107eb-126">Razor Pages is enabled in *Startup.cs*:</span></span>

[!code-cs[main](index/sample/RazorPagesIntro/Startup.cs?name=snippet_Startup)]

<span data-ttu-id="107eb-127">Sehen Sie sich diese einfache Seite an: <a name="OnGet"></a></span><span class="sxs-lookup"><span data-stu-id="107eb-127">Consider a basic page: <a name="OnGet"></a></span></span>

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Index.cshtml)]

<span data-ttu-id="107eb-128">Der vorherige Code ähnelt stark einer Razor-Umgebungsdatei.</span><span class="sxs-lookup"><span data-stu-id="107eb-128">The preceding code looks a lot like a Razor view file.</span></span> <span data-ttu-id="107eb-129">Der Unterschied besteht in der `@page`-Anweisung.</span><span class="sxs-lookup"><span data-stu-id="107eb-129">What makes it different is the `@page` directive.</span></span> <span data-ttu-id="107eb-130">`@page` macht die Datei zu einer MVC-Aktion, d.h. dass Anfragen direkt ohne einen Controller verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="107eb-130">`@page` makes the file into an MVC action - which means that it handles requests directly, without going through a controller.</span></span> <span data-ttu-id="107eb-131">`@page` muss die erste Razor-Anweisung auf einer Seite sein.</span><span class="sxs-lookup"><span data-stu-id="107eb-131">`@page` must be the first Razor directive on a page.</span></span> <span data-ttu-id="107eb-132">`@page` wirkt sich auf das Verhalten aller anderen Razor-Konstrukte aus.</span><span class="sxs-lookup"><span data-stu-id="107eb-132">`@page` affects the behavior of other Razor constructs.</span></span>

<span data-ttu-id="107eb-133">Eine ähnliche Seite, die die `PageModel`-Klasse verwendet, wird in den folgenden zwei Dateien angezeigt.</span><span class="sxs-lookup"><span data-stu-id="107eb-133">A similar page, using a `PageModel` class, is shown in the following two files.</span></span> <span data-ttu-id="107eb-134">Die Datei *Pages/Index2.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="107eb-134">The *Pages/Index2.cshtml* file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Index2.cshtml)]

<span data-ttu-id="107eb-135">Die CodeBehind-Datei *Pages/Index2.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="107eb-135">The *Pages/Index2.cshtml.cs* "code-behind" file:</span></span>

[!code-cs[main](index/sample/RazorPagesIntro/Pages/Index2.cshtml.cs)]

<span data-ttu-id="107eb-136">Die `PageModel`-Klassendatei hat standardmäßig den gleichen Namen wie die Datei mit Razor-Seiten, nur dass außerdem *cs* angefügt wird.</span><span class="sxs-lookup"><span data-stu-id="107eb-136">By convention, the `PageModel` class file has the same name as the Razor Page file with *.cs* appended.</span></span> <span data-ttu-id="107eb-137">Die vorherige Datei mit Razor-Seiten lautet beispielsweise *Pages/Index2.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="107eb-137">For example, the previous Razor Page is *Pages/Index2.cshtml*.</span></span> <span data-ttu-id="107eb-138">Die Datei mit der `PageModel`-Klasse heißt *Pages/Index2.cshtml.cs*.</span><span class="sxs-lookup"><span data-stu-id="107eb-138">The file containing the `PageModel` class is named *Pages/Index2.cshtml.cs*.</span></span>

<span data-ttu-id="107eb-139">Die Zuordnungen von URL-Pfaden zu Seiten werden durch den Speicherort der Seite im Dateisystem bestimmt.</span><span class="sxs-lookup"><span data-stu-id="107eb-139">The associations of URL paths to pages are determined by the page's location in the file system.</span></span> <span data-ttu-id="107eb-140">Die folgende Tabelle zeigt einen Pfad zu Razor-Seiten und die entsprechende URL:</span><span class="sxs-lookup"><span data-stu-id="107eb-140">The following table shows a Razor Page path and the matching URL:</span></span>

| <span data-ttu-id="107eb-141">Dateiname und Pfad</span><span class="sxs-lookup"><span data-stu-id="107eb-141">File name and path</span></span>               | <span data-ttu-id="107eb-142">Entsprechende URL</span><span class="sxs-lookup"><span data-stu-id="107eb-142">matching URL</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="107eb-143">*/Pages/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="107eb-143">*/Pages/Index.cshtml*</span></span> | <span data-ttu-id="107eb-144">`/` oder `/Index`</span><span class="sxs-lookup"><span data-stu-id="107eb-144">`/` or `/Index`</span></span> |
| <span data-ttu-id="107eb-145">*/Pages/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="107eb-145">*/Pages/Contact.cshtml*</span></span> | `/Contact` |
| <span data-ttu-id="107eb-146">*/Pages/Store/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="107eb-146">*/Pages/Store/Contact.cshtml*</span></span> | `/Store/Contact` |
| <span data-ttu-id="107eb-147">*/Pages/Store/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="107eb-147">*/Pages/Store/Index.cshtml*</span></span> | <span data-ttu-id="107eb-148">`/Store` oder `/Store/Index`</span><span class="sxs-lookup"><span data-stu-id="107eb-148">`/Store` or `/Store/Index`</span></span> |

<span data-ttu-id="107eb-149">Notizen:</span><span class="sxs-lookup"><span data-stu-id="107eb-149">Notes:</span></span>

* <span data-ttu-id="107eb-150">Die Runtime sucht standardmäßig im Ordner *Pages* (Seiten) nach Dateien mit Razor-Seiten.</span><span class="sxs-lookup"><span data-stu-id="107eb-150">The runtime looks for Razor Pages files in the *Pages* folder by default.</span></span>
* <span data-ttu-id="107eb-151">Wenn eine Seite nicht in einer URL enthalten ist, ist `Index` die Standardseite.</span><span class="sxs-lookup"><span data-stu-id="107eb-151">`Index` is the default page when a URL doesn't include a page.</span></span>

## <a name="writing-a-basic-form"></a><span data-ttu-id="107eb-152">Schreiben eines einfachen Formulars</span><span class="sxs-lookup"><span data-stu-id="107eb-152">Writing a basic form</span></span>

<span data-ttu-id="107eb-153">Features von Razor-Seiten erstellen allgemeine Muster, die einfach mit Webbrowsern verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="107eb-153">Razor Pages features are designed to make common patterns used with web browsers easy.</span></span> <span data-ttu-id="107eb-154">Die [Modellbindung](xref:mvc/models/model-binding), [Taghilfsprogramme](xref:mvc/views/tag-helpers/intro) und alle HTML-Hilfsprogramme *funktionieren nur* mit den Eigenschaften, die in einer Klasse der Razor-Seiten definiert wurden.</span><span class="sxs-lookup"><span data-stu-id="107eb-154">[Model binding](xref:mvc/models/model-binding), [Tag Helpers](xref:mvc/views/tag-helpers/intro), and HTML helpers all *just work* with the properties defined in a Razor Page class.</span></span> <span data-ttu-id="107eb-155">Nehmen wir z.B. eine Seite, die ein allgemeines Kontaktformular für das `Contact`-Modell implementiert:</span><span class="sxs-lookup"><span data-stu-id="107eb-155">Consider a page that implements a basic "contact us" form for the `Contact` model:</span></span>

<span data-ttu-id="107eb-156">Für die Beispiele in diesem Dokument wird `DbContext` in der Datei [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) initialisiert.</span><span class="sxs-lookup"><span data-stu-id="107eb-156">For the samples in this document, the `DbContext` is initialized in the [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) file.</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Startup.cs?highlight=15-16)]

<span data-ttu-id="107eb-157">Das Datenmodell:</span><span class="sxs-lookup"><span data-stu-id="107eb-157">The data model:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Data/Customer.cs)]

<span data-ttu-id="107eb-158">Der db-Kontext:</span><span class="sxs-lookup"><span data-stu-id="107eb-158">The db context:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Data/AppDbContext.cs)]

<span data-ttu-id="107eb-159">Die Umgebungsdatei *Pages/Create.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="107eb-159">The *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Create.cshtml)]

<span data-ttu-id="107eb-160">Die CodeBehind-Datei *Pages/Create.cshtml.cs* für die Ansicht:</span><span class="sxs-lookup"><span data-stu-id="107eb-160">The *Pages/Create.cshtml.cs* code-behind file for the view:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_ALL)]

<span data-ttu-id="107eb-161">Die `PageModel`-Klasse heißt standardmäßig `<PageName>Model` und befindet sich im selben Namespace wie die Seite.</span><span class="sxs-lookup"><span data-stu-id="107eb-161">By convention, the `PageModel` class is called `<PageName>Model` and is in the same namespace as the page.</span></span>

<span data-ttu-id="107eb-162">Mit der Klasse `PageModel` kann die Logik einer Seite von deren Darstellung getrennt werden.</span><span class="sxs-lookup"><span data-stu-id="107eb-162">The `PageModel` class allows separation of the logic of a page from its presentation.</span></span> <span data-ttu-id="107eb-163">Sie definiert Seitenhandler für Anforderungen, die an die Seite geschickt wurden, und für zum Rendern der Seite verwendete Daten.</span><span class="sxs-lookup"><span data-stu-id="107eb-163">It defines page handlers for requests sent to the page and the data used to render the page.</span></span> <span data-ttu-id="107eb-164">Durch diese Trennung können Sie Seitenabhängigkeiten durch [Abhängigkeiteneinschleusung](xref:fundamentals/dependency-injection) verwalten und [Komponententests](xref:testing/razor-pages-testing) für die Seiten durchführen.</span><span class="sxs-lookup"><span data-stu-id="107eb-164">This separation allows you to manage page dependencies through [dependency injection](xref:fundamentals/dependency-injection) and to [unit test](xref:testing/razor-pages-testing) the pages.</span></span>

<span data-ttu-id="107eb-165">Die Seite hat eine `OnPostAsync`-*Handlermethode*, die auf `POST`-Anforderungen ausgeführt wird (wenn ein Benutzer das Formular sendet).</span><span class="sxs-lookup"><span data-stu-id="107eb-165">The page has an `OnPostAsync` *handler method*, which runs on `POST` requests (when a user posts the form).</span></span> <span data-ttu-id="107eb-166">Sie können Handlermethoden für alle HTTP-Verben hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="107eb-166">You can add handler methods for any HTTP verb.</span></span> <span data-ttu-id="107eb-167">Die am häufigsten verwendeten Handler sind:</span><span class="sxs-lookup"><span data-stu-id="107eb-167">The most common handlers are:</span></span>

* <span data-ttu-id="107eb-168">`OnGet`, um den für eine Seite erforderlichen Status zu initialisieren.</span><span class="sxs-lookup"><span data-stu-id="107eb-168">`OnGet` to initialize state needed for the page.</span></span> <span data-ttu-id="107eb-169">[OnGet](#OnGet)-Beispiel</span><span class="sxs-lookup"><span data-stu-id="107eb-169">[OnGet](#OnGet) sample.</span></span>
* <span data-ttu-id="107eb-170">`OnPost`, um Formularübermittlungen zu behandeln</span><span class="sxs-lookup"><span data-stu-id="107eb-170">`OnPost` to handle form submissions.</span></span>

<span data-ttu-id="107eb-171">Das Namenssuffix `Async` ist optional. Es wird jedoch standardmäßig häufig für asynchrone Funktionen verwendet.</span><span class="sxs-lookup"><span data-stu-id="107eb-171">The `Async` naming suffix is optional but is often used by convention for asynchronous functions.</span></span> <span data-ttu-id="107eb-172">Der `OnPostAsync`-Code im vorhergehenden Beispiel ähnelt dem, was Sie normalerweise in einem Controller schreiben würden.</span><span class="sxs-lookup"><span data-stu-id="107eb-172">The `OnPostAsync` code in the preceding example looks similar to what you would normally write in a controller.</span></span> <span data-ttu-id="107eb-173">Der vorhergehende Code ist typisch für Razor-Seiten.</span><span class="sxs-lookup"><span data-stu-id="107eb-173">The preceding code is typical for Razor Pages.</span></span> <span data-ttu-id="107eb-174">Die meisten primitiven MVC-Typen wie die [Modellbindung](xref:mvc/models/model-binding), die [Validierung](xref:mvc/models/validation) und Aktionsergebnisse werden freigegeben.</span><span class="sxs-lookup"><span data-stu-id="107eb-174">Most of the MVC primitives like [model binding](xref:mvc/models/model-binding), [validation](xref:mvc/models/validation), and action results are shared.</span></span>  <!-- Review: Ryan, can we get a list of what is shared and what isn't? -->

<span data-ttu-id="107eb-175">Die vorherige `OnPostAsync`-Methode:</span><span class="sxs-lookup"><span data-stu-id="107eb-175">The previous `OnPostAsync` method:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync)]

<span data-ttu-id="107eb-176">Der grundlegende Ablauf von `OnPostAsync`:</span><span class="sxs-lookup"><span data-stu-id="107eb-176">The basic flow of `OnPostAsync`:</span></span>

<span data-ttu-id="107eb-177">Prüfen auf Validierungsfehler</span><span class="sxs-lookup"><span data-stu-id="107eb-177">Check for validation errors.</span></span>

*  <span data-ttu-id="107eb-178">Wenn keine Fehler vorliegen, werden die Daten gespeichert und weitergeleitet.</span><span class="sxs-lookup"><span data-stu-id="107eb-178">If there are no errors, save the data and redirect.</span></span>
*  <span data-ttu-id="107eb-179">Wenn es Fehler gibt, zeigen Sie die Seite erneut mit den Validierungsmeldungen an.</span><span class="sxs-lookup"><span data-stu-id="107eb-179">If there are errors, show the page again with validation messages.</span></span> <span data-ttu-id="107eb-180">Die clientseitige Validierung ist identisch mit herkömmlichen ASP.NET Core MVC-Anwendungen,</span><span class="sxs-lookup"><span data-stu-id="107eb-180">Client-side validation is identical to traditional ASP.NET Core MVC applications.</span></span> <span data-ttu-id="107eb-181">denn Validierungsfehler werden oftmals auf dem Client erkannt und nie an den Server übermittelt.</span><span class="sxs-lookup"><span data-stu-id="107eb-181">In many cases, validation errors would be detected on the client, and never submitted to the server.</span></span>

<span data-ttu-id="107eb-182">Wenn die Daten erfolgreich eingegeben wurden, ruft die `OnPostAsync`-Handlermethode die `RedirectToPage`-Hilfsmethode auf, um eine Instanz von `RedirectToPageResult` zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="107eb-182">When the data is entered successfully, the `OnPostAsync` handler method calls the `RedirectToPage` helper method to return an instance of `RedirectToPageResult`.</span></span> <span data-ttu-id="107eb-183">`RedirectToPage` ist ein neues Aktionsergebnis und ähnelt `RedirectToAction` oder `RedirectToRoute`, ist aber für Seiten angepasst.</span><span class="sxs-lookup"><span data-stu-id="107eb-183">`RedirectToPage` is a new action result, similar to `RedirectToAction` or `RedirectToRoute`, but customized for pages.</span></span> <span data-ttu-id="107eb-184">Im vorhergehenden Beispiel leitet es an die Stammindexseite (`/Index`) weiter.</span><span class="sxs-lookup"><span data-stu-id="107eb-184">In the preceding sample, it redirects to the root Index page (`/Index`).</span></span> <span data-ttu-id="107eb-185">Informationen zu `RedirectToPage` finden Sie im Abschnitt [URL-Generierung für Seiten](#url_gen).</span><span class="sxs-lookup"><span data-stu-id="107eb-185">`RedirectToPage` is detailed in the [URL generation for Pages](#url_gen) section.</span></span>

<span data-ttu-id="107eb-186">Wenn das übermittelte Formular Validierungsfehler enthält (die an den Server übergeben wurden), ruft die `OnPostAsync`-Handlermethode die `Page`-Hilfsmethode auf.</span><span class="sxs-lookup"><span data-stu-id="107eb-186">When the submitted form has validation errors (that are passed to the server), the`OnPostAsync` handler method calls the `Page` helper method.</span></span> <span data-ttu-id="107eb-187">`Page` gibt eine Instanz von `PageResult` zurück.</span><span class="sxs-lookup"><span data-stu-id="107eb-187">`Page` returns an instance of `PageResult`.</span></span> <span data-ttu-id="107eb-188">Der Vorgang, bei dem `Page` zurückgegeben wird, ähnelt dem Vorgang, bei dem Aktionen im Controller `View` zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="107eb-188">Returning `Page` is similar to how actions in controllers return `View`.</span></span> <span data-ttu-id="107eb-189">`PageResult` ist der standardmäßige <!-- Review  -->-Rückgabetyp für eine Handlermethode.</span><span class="sxs-lookup"><span data-stu-id="107eb-189">`PageResult` is the default <!-- Review  --> return type for a handler method.</span></span> <span data-ttu-id="107eb-190">Eine Handlermethode, die `void` zurückgibt, rendert die Seite.</span><span class="sxs-lookup"><span data-stu-id="107eb-190">A handler method that returns `void` renders the page.</span></span>

<span data-ttu-id="107eb-191">Die Eigenschaft `Customer` verwendet das `[BindProperty]`-Attribut, um die Modellbindung zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="107eb-191">The `Customer` property uses `[BindProperty]` attribute to opt in to model binding.</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_PageModel&highlight=10-11)]

<span data-ttu-id="107eb-192">Razor-Seiten binden Eigenschaften standardmäßig nur an Nicht-GET-Verben.</span><span class="sxs-lookup"><span data-stu-id="107eb-192">Razor Pages, by default, bind properties only with non-GET verbs.</span></span> <span data-ttu-id="107eb-193">Durch die Bindung an Eigenschaften können Sie den Umfang von Codes reduzieren, den Sie schreiben müssen.</span><span class="sxs-lookup"><span data-stu-id="107eb-193">Binding to properties can reduce the amount of code you have to write.</span></span> <span data-ttu-id="107eb-194">Die Bindung reduziert den Code mithilfe der gleichen Eigenschaft, um Formularfelder (`<input asp-for="Customer.Name" />`) zu rendern und die Eingabe zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="107eb-194">Binding reduces code by using the same property to render form fields (`<input asp-for="Customer.Name" />`) and accept the input.</span></span>

<span data-ttu-id="107eb-195">Die Startseite (*Index.cshtml*):</span><span class="sxs-lookup"><span data-stu-id="107eb-195">The home page (*Index.cshtml*):</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml)]

<span data-ttu-id="107eb-196">Die CodeBehind-Datei *Index.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="107eb-196">The code behind *Index.cshtml.cs* file:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs)]

<span data-ttu-id="107eb-197">Die Datei *Index.cshtml* enthält das folgende Markup, um einen Bearbeitungslink für jeden Kontakt zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="107eb-197">The *Index.cshtml* file contains the following markup to create an edit link for each contact:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=21)]

<span data-ttu-id="107eb-198">Das [Anchor-Taghilfsprogramm](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) verwendet das Attribut `asp-route-{value}`, um einen Link zur Bearbeitungsseite zu generieren.</span><span class="sxs-lookup"><span data-stu-id="107eb-198">The [Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) used the `asp-route-{value}` attribute to generate a link to the Edit page.</span></span> <span data-ttu-id="107eb-199">Der Link enthält die Routendaten mit der Kontakt-ID.</span><span class="sxs-lookup"><span data-stu-id="107eb-199">The link contains route data with the contact ID.</span></span> <span data-ttu-id="107eb-200">Beispielsweise `http://localhost:5000/Edit/1`.</span><span class="sxs-lookup"><span data-stu-id="107eb-200">For example, `http://localhost:5000/Edit/1`.</span></span>

<span data-ttu-id="107eb-201">Die Datei *Pages/Edit.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="107eb-201">The *Pages/Edit.cshtml* file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Edit.cshtml?highlight=1)]

<span data-ttu-id="107eb-202">Die erste Zeile enthält die `@page "{id:int}"`-Anweisung.</span><span class="sxs-lookup"><span data-stu-id="107eb-202">The first line contains the `@page "{id:int}"` directive.</span></span> <span data-ttu-id="107eb-203">Die Routingbeschränkung `"{id:int}"` weist die Seite an, die Anforderungen für die Seite zu akzeptieren, die `int`-Routingdaten enthalten.</span><span class="sxs-lookup"><span data-stu-id="107eb-203">The routing constraint`"{id:int}"` tells the page to accept requests to the page that contain `int` route data.</span></span> <span data-ttu-id="107eb-204">Wenn eine Anforderung an die Seite bestimmte Routingdaten nicht enthält, die in einen `int` konvertiert werden können, gibt die Runtime einen Fehler vom Typ „HTTP 404: Nicht gefunden“ zurück.</span><span class="sxs-lookup"><span data-stu-id="107eb-204">If a request to the page doesn't contain route data that can be converted to an `int`, the runtime returns an HTTP 404 (not found) error.</span></span>

<span data-ttu-id="107eb-205">Die Datei *Pages/Edit.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="107eb-205">The *Pages/Edit.cshtml.cs* file:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Edit.cshtml.cs)]

<span data-ttu-id="107eb-206">Die Datei *index.cshtml* enthält auch Markup zum Erstellen der Schaltfläche „Löschen“ für jeden benutzerdefinierten Kontakt:</span><span class="sxs-lookup"><span data-stu-id="107eb-206">The *Index.cshtml* file also contains markup to create a delete button for each customer contact:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=22-23)]

<span data-ttu-id="107eb-207">Wenn die „Löschen“-Schaltfläche in HTML gerendert wird, enthält ihr `formaction`-Element Parameter für Folgendes:</span><span class="sxs-lookup"><span data-stu-id="107eb-207">When the delete button is rendered in HTML, its `formaction` includes parameters for:</span></span>

* <span data-ttu-id="107eb-208">Die benutzerdefinierte Kontakt-ID, die vom `asp-route-id`-Attribut angegeben wird</span><span class="sxs-lookup"><span data-stu-id="107eb-208">The customer contact ID specified by the `asp-route-id` attribute.</span></span>
* <span data-ttu-id="107eb-209">Der `handler`, der vom `asp-page-handler`-Attribut angegeben wird</span><span class="sxs-lookup"><span data-stu-id="107eb-209">The `handler` specified by the `asp-page-handler` attribute.</span></span>

<span data-ttu-id="107eb-210">Hier sehen Sie ein Beispiel für eine gerenderte „Löschen“-Schaltfläche mit einer benutzerdefinierten Kontakt-ID von `1`:</span><span class="sxs-lookup"><span data-stu-id="107eb-210">Here is an example of a rendered delete button with a customer contact ID of `1`:</span></span>

```html
<button type="submit" formaction="/?id=1&amp;handler=delete">delete</button>
```

<span data-ttu-id="107eb-211">Wenn die Schaltfläche ausgewählt wird, wird eine `POST`-Anforderung an den Server gesendet.</span><span class="sxs-lookup"><span data-stu-id="107eb-211">When the button is selected, a form `POST` request is sent to the server.</span></span> <span data-ttu-id="107eb-212">Durch Konvention wird der Name der Handlermethode auf Grundlage des Werts des `handler`-Parameters entsprechend des Schemas `OnPost[handler]Async` ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="107eb-212">By convention, the name of the handler method is selected based the value of the `handler` parameter according to the scheme `OnPost[handler]Async`.</span></span>

<span data-ttu-id="107eb-213">Da der `handler` in diesem Beispiel `delete` ist, wird die Handlermethode `OnPostDeleteAsync` verwendet, um die `POST`-Anforderung zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="107eb-213">Because the `handler` is `delete` in this example, the `OnPostDeleteAsync` handler method is used to process the `POST` request.</span></span> <span data-ttu-id="107eb-214">Wenn der `asp-page-handler` auf einen anderen Wert festgelegt wird, wie z.B. `remove`, wird eine Seitenhandlermethode mit dem Namen `OnPostRemoveAsync` ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="107eb-214">If the `asp-page-handler` is set to a different value, such as `remove`, a page handler method with the name `OnPostRemoveAsync` is selected.</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs?range=26-37)]

<span data-ttu-id="107eb-215">Die `OnPostDeleteAsync`-Methode:</span><span class="sxs-lookup"><span data-stu-id="107eb-215">The `OnPostDeleteAsync` method:</span></span>

* <span data-ttu-id="107eb-216">Akzeptiert die `id` der Abfragezeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="107eb-216">Accepts the `id` from the query string.</span></span>
* <span data-ttu-id="107eb-217">Fragt mit `FindAsync` die Datenbank nach dem Kundenkontakt ab.</span><span class="sxs-lookup"><span data-stu-id="107eb-217">Queries the database for the customer contact with `FindAsync`.</span></span>
* <span data-ttu-id="107eb-218">Wenn der Kundenkontakt gefunden wird, wird er aus der Liste der Kundenkontakte entfernt.</span><span class="sxs-lookup"><span data-stu-id="107eb-218">If the customer contact is found, they're removed from the list of customer contacts.</span></span> <span data-ttu-id="107eb-219">Die Datenbank wurde aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="107eb-219">The database is updated.</span></span>
* <span data-ttu-id="107eb-220">Ruft `RedirectToPage` auf, um die Stammindexseite (`/Index`) umzuleiten.</span><span class="sxs-lookup"><span data-stu-id="107eb-220">Calls `RedirectToPage` to redirect to the root Index page (`/Index`).</span></span>

<a name="xsrf"></a>

## <a name="xsrfcsrf-and-razor-pages"></a><span data-ttu-id="107eb-221">XSRF/CSRF und Razor-Seiten</span><span class="sxs-lookup"><span data-stu-id="107eb-221">XSRF/CSRF and Razor Pages</span></span>

<span data-ttu-id="107eb-222">Sie müssen keinen Code für die [Antifälschungsvalidierung](xref:security/anti-request-forgery) schreiben.</span><span class="sxs-lookup"><span data-stu-id="107eb-222">You don't have to write any code for [antiforgery validation](xref:security/anti-request-forgery).</span></span> <span data-ttu-id="107eb-223">Die Generierung und Validierung von Antifälschungstoken ist automatisch in Razor-Seiten enthalten.</span><span class="sxs-lookup"><span data-stu-id="107eb-223">Antiforgery token generation and validation are automatically included in Razor Pages.</span></span>

<a name="layout"></a>
## <a name="using-layouts-partials-templates-and-tag-helpers-with-razor-pages"></a><span data-ttu-id="107eb-224">Verwenden von Layouts, Teilansichten, Vorlagen und Taghilfsprogrammen mit Razor-Seiten</span><span class="sxs-lookup"><span data-stu-id="107eb-224">Using Layouts, partials, templates, and Tag Helpers with Razor Pages</span></span>

<span data-ttu-id="107eb-225">Razor-Seiten funktionieren mit allen Funktionen des Razor-Anzeigemoduls.</span><span class="sxs-lookup"><span data-stu-id="107eb-225">Pages work with all the features of the Razor view engine.</span></span> <span data-ttu-id="107eb-226">Layouts, Teilansichten, Vorlagen, Taghilfsprogramme, *_ViewStart.cshtml*, *_ViewImports.cshtml* funktionieren auf die gleiche Weise wie für herkömmliche Razor-Ansichten.</span><span class="sxs-lookup"><span data-stu-id="107eb-226">Layouts, partials, templates, Tag Helpers, *_ViewStart.cshtml*, *_ViewImports.cshtml* work in the same way they do for conventional Razor views.</span></span>

<span data-ttu-id="107eb-227">Lassen Sie uns diese Seite mithilfe einiger dieser Funktionen entwirren.</span><span class="sxs-lookup"><span data-stu-id="107eb-227">Let's declutter this page by taking advantage of some of those features.</span></span>

<span data-ttu-id="107eb-228">Fügen Sie einer *Pages/_Layout.cshtml* eine [Layoutseite](xref:mvc/views/layout) hinzu:</span><span class="sxs-lookup"><span data-stu-id="107eb-228">Add a [layout page](xref:mvc/views/layout) to *Pages/_Layout.cshtml*:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_LayoutSimple.cshtml)]

<span data-ttu-id="107eb-229">Das [Layout](xref:mvc/views/layout):</span><span class="sxs-lookup"><span data-stu-id="107eb-229">The [Layout](xref:mvc/views/layout):</span></span>

* <span data-ttu-id="107eb-230">Steuert das Layout der einzelnen Seiten, es sei denn, das Layout wird für eine Seite deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="107eb-230">Controls the layout of each page (unless the page opts out of layout).</span></span>
* <span data-ttu-id="107eb-231">Importiert HTML-Strukturen, z.B. JavaScript und Stylesheets.</span><span class="sxs-lookup"><span data-stu-id="107eb-231">Imports HTML structures such as JavaScript and stylesheets.</span></span>

<span data-ttu-id="107eb-232">Weitere Informationen finden Sie unter [Layoutseite](xref:mvc/views/layout).</span><span class="sxs-lookup"><span data-stu-id="107eb-232">See [layout page](xref:mvc/views/layout) for more information.</span></span>

<span data-ttu-id="107eb-233">Die Eigenschaft [Layout](xref:mvc/views/layout#specifying-a-layout) wird in *Pages/_ViewStart.cshtml* festgelegt:</span><span class="sxs-lookup"><span data-stu-id="107eb-233">The [Layout](xref:mvc/views/layout#specifying-a-layout) property is set in *Pages/_ViewStart.cshtml*:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewStart.cshtml)]

<span data-ttu-id="107eb-234">**Hinweis:** Das Layout befindet sich im Ordner *Pages* (Seiten).</span><span class="sxs-lookup"><span data-stu-id="107eb-234">**Note:** The layout is in the *Pages* folder.</span></span> <span data-ttu-id="107eb-235">Seiten suchen hierarchisch nach anderen Ansichten (Layouts, Vorlagen oder Teilansichten) und beginnen im gleichen Ordner wie die aktuelle Seite.</span><span class="sxs-lookup"><span data-stu-id="107eb-235">Pages look for other views (layouts, templates, partials) hierarchically, starting in the same folder as the current page.</span></span> <span data-ttu-id="107eb-236">Ein Layout im Ordner *Seiten* kann aus jeder Razor-Seite unter dem Ordner *Pages* verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="107eb-236">A layout in the *Pages* folder can be used from any Razor page under the *Pages* folder.</span></span>

<span data-ttu-id="107eb-237">Wir empfehlen Ihnen, die Layoutdatei **nicht** im Ordner *Views/Shared* (Ansichten/Freigegeben) zu platzieren.</span><span class="sxs-lookup"><span data-stu-id="107eb-237">We recommend you **not** put the layout file in the *Views/Shared* folder.</span></span> <span data-ttu-id="107eb-238">*Views/Shared* ist ein MVC-Ansichtsmuster.</span><span class="sxs-lookup"><span data-stu-id="107eb-238">*Views/Shared* is an MVC views pattern.</span></span> <span data-ttu-id="107eb-239">Razor-Seiten basieren auf der Ordnerhierarchie, nicht auf Pfadkonventionen.</span><span class="sxs-lookup"><span data-stu-id="107eb-239">Razor Pages are meant to rely on folder hierarchy, not path conventions.</span></span>

<span data-ttu-id="107eb-240">Die Ansichtensuche in einer Razor-Seite enthält den Ordner *Pages*.</span><span class="sxs-lookup"><span data-stu-id="107eb-240">View search from a Razor Page includes the *Pages* folder.</span></span> <span data-ttu-id="107eb-241">Die Layouts, Vorlagen und Teilansichten, die Sie mit MVC-Controllern und herkömmlichen Razor-Ansichten verwenden, *funktionieren einfach so*.</span><span class="sxs-lookup"><span data-stu-id="107eb-241">The layouts, templates, and partials you're using with MVC controllers and conventional Razor views *just work*.</span></span>

<span data-ttu-id="107eb-242">Fügen Sie eine Datei *Pages/_ViewImports.cshtml* hinzu:</span><span class="sxs-lookup"><span data-stu-id="107eb-242">Add a *Pages/_ViewImports.cshtml* file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml)]

<span data-ttu-id="107eb-243">`@namespace` wird weiter unten im Tutorial erläutert.</span><span class="sxs-lookup"><span data-stu-id="107eb-243">`@namespace` is explained later in the tutorial.</span></span> <span data-ttu-id="107eb-244">Die `@addTagHelper`-Anweisung bringt die [integrierten Taghilfsprogramme](xref:mvc/views/tag-helpers/builtin-th/Index) zu allen Seiten in der Ordner *Pages*.</span><span class="sxs-lookup"><span data-stu-id="107eb-244">The `@addTagHelper` directive brings in the [built-in Tag Helpers](xref:mvc/views/tag-helpers/builtin-th/Index) to all the pages in the *Pages* folder.</span></span>

<a name="namespace"></a>

<span data-ttu-id="107eb-245">Wenn die `@namespace`-Anweisung explizit auf eine Seite angewendet wird:</span><span class="sxs-lookup"><span data-stu-id="107eb-245">When the `@namespace` directive is used explicitly on a page:</span></span>

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Customers/Namespace2.cshtml?highlight=2)]

<span data-ttu-id="107eb-246">Die Anweisung legt den Namespace für die Seite fest.</span><span class="sxs-lookup"><span data-stu-id="107eb-246">The directive sets the namespace for the page.</span></span> <span data-ttu-id="107eb-247">Die `@model`-Anweisung muss den Namespace nicht enthalten.</span><span class="sxs-lookup"><span data-stu-id="107eb-247">The `@model` directive doesn't need to include the namespace.</span></span>

<span data-ttu-id="107eb-248">Wenn sich die `@namespace`-Anweisung in *_ViewImports.cshtml* befindet, stellt der angegebene Namespace das Präfix für den generierten Namespace auf der Seite bereit, die die `@namespace`-Anweisung importiert.</span><span class="sxs-lookup"><span data-stu-id="107eb-248">When the `@namespace` directive is contained in *_ViewImports.cshtml*, the specified namespace supplies the prefix for the generated namespace in the Page that imports the `@namespace` directive.</span></span> <span data-ttu-id="107eb-249">Der Rest der generierten Namespaces (der Suffixteil) ist der durch Punkte getrennte relative Pfad zwischen dem Ordner mit *_ViewImports.cshtml* und dem Ordner, der die Seite enthält.</span><span class="sxs-lookup"><span data-stu-id="107eb-249">The rest of the generated namespace (the suffix portion) is the dot-separated relative path between the folder containing *_ViewImports.cshtml* and the folder containing the page.</span></span>

<span data-ttu-id="107eb-250">Die CodeBehind-Datei *Pages/Customers/Edit.cshtml.cs* legt den Namespace z.B. explizit fest:</span><span class="sxs-lookup"><span data-stu-id="107eb-250">For example, the code behind file *Pages/Customers/Edit.cshtml.cs* explicitly sets the namespace:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/Edit.cshtml.cs?name=snippet_namespace)]

<span data-ttu-id="107eb-251">Die Datei *Pages/_ViewImports.cshtml* legt den folgenden Namespace fest:</span><span class="sxs-lookup"><span data-stu-id="107eb-251">The *Pages/_ViewImports.cshtml* file sets the following namespace:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml?highlight=1)]

<span data-ttu-id="107eb-252">Der generierte Namespace für die Razor-Seite *Pages/Customers/Edit.cshtml* ist identisch mit der CodeBehind-Datei.</span><span class="sxs-lookup"><span data-stu-id="107eb-252">The generated namespace for the *Pages/Customers/Edit.cshtml* Razor Page is the same as the code behind file.</span></span> <span data-ttu-id="107eb-253">Die `@namespace`-Anweisung wurde entworfen, damit die einem Projekt hinzugefügten C#-Klassen und mit Seiten generierter Code *einfach so funktionieren*, ohne dass eine `@using`-Anweisung für die CodeBehind-Datei hinzugefügt werden muss.</span><span class="sxs-lookup"><span data-stu-id="107eb-253">The `@namespace` directive was designed so the C# classes added to a project and pages-generated code *just work* without having to add an `@using` directive for the code behind file.</span></span>

<span data-ttu-id="107eb-254">**Hinweis:** `@namespace` funktioniert auch mit konventionellen Razor-Ansichten.</span><span class="sxs-lookup"><span data-stu-id="107eb-254">**Note:** `@namespace` also works with conventional Razor views.</span></span>

<span data-ttu-id="107eb-255">Die ursprüngliche Umgebungsdatei *Pages/Create.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="107eb-255">The original *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Create.cshtml?highlight=2)]

<span data-ttu-id="107eb-256">Die aktualisierte Umgebungsdatei *Pages/Create.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="107eb-256">The updated *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/Create.cshtml?highlight=2)]

<span data-ttu-id="107eb-257">Die [Razor-Seiten-Startprojekt](#rpvs17) enthält die Seite *Pages/_ValidationScriptsPartial.cshtml*, die die clientseitige Validierung bindet.</span><span class="sxs-lookup"><span data-stu-id="107eb-257">The [Razor Pages starter project](#rpvs17) contains the *Pages/_ValidationScriptsPartial.cshtml*, which hooks up client-side validation.</span></span>

<a name="url_gen"></a>

## <a name="url-generation-for-pages"></a><span data-ttu-id="107eb-258">URL-Generierung für Seiten</span><span class="sxs-lookup"><span data-stu-id="107eb-258">URL generation for Pages</span></span>

<span data-ttu-id="107eb-259">Die zuvor gezeigte `Create`-Seite verwendet `RedirectToPage`:</span><span class="sxs-lookup"><span data-stu-id="107eb-259">The `Create` page, shown previously, uses `RedirectToPage`:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync&highlight=10)]

<span data-ttu-id="107eb-260">Die App hat die folgende Datei/Ordner-Struktur:</span><span class="sxs-lookup"><span data-stu-id="107eb-260">The app has the following file/folder structure:</span></span>

* <span data-ttu-id="107eb-261">*/Pages*</span><span class="sxs-lookup"><span data-stu-id="107eb-261">*/Pages*</span></span>

  * <span data-ttu-id="107eb-262">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="107eb-262">*Index.cshtml*</span></span>
  * <span data-ttu-id="107eb-263">*/Customer*</span><span class="sxs-lookup"><span data-stu-id="107eb-263">*/Customer*</span></span>

    * <span data-ttu-id="107eb-264">*Create.cshtml*</span><span class="sxs-lookup"><span data-stu-id="107eb-264">*Create.cshtml*</span></span>
    * <span data-ttu-id="107eb-265">*Edit.cshtml*</span><span class="sxs-lookup"><span data-stu-id="107eb-265">*Edit.cshtml*</span></span>
    * <span data-ttu-id="107eb-266">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="107eb-266">*Index.cshtml*</span></span>

<span data-ttu-id="107eb-267">Die Seiten *Pages/Customers/Create.cshtml* und *Pages/Customers/Edit.cshtml* leiten bei Erfolg an *Pages/Index.cshtml* weiter.</span><span class="sxs-lookup"><span data-stu-id="107eb-267">The *Pages/Customers/Create.cshtml* and *Pages/Customers/Edit.cshtml* pages redirect to *Pages/Index.cshtml* after success.</span></span> <span data-ttu-id="107eb-268">Die Zeichenfolge `/Index` ist Teil des URI, der auf die vorhergehende Seite zugreifen soll.</span><span class="sxs-lookup"><span data-stu-id="107eb-268">The string `/Index` is part of the URI to access the preceding page.</span></span> <span data-ttu-id="107eb-269">Die Zeichenfolge `/Index` kann für das Generieren von URIs für die Seite *Pages/Index.cshtml* verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="107eb-269">The string `/Index` can be used to generate URIs to the *Pages/Index.cshtml* page.</span></span> <span data-ttu-id="107eb-270">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="107eb-270">For example:</span></span>

* `Url.Page("/Index", ...)`
* `<a asp-page="/Index">My Index Page</a>`
* `RedirectToPage("/Index")`

<span data-ttu-id="107eb-271">Der Seitenname ist der Pfad zu der Seite vom Stammordner */Pages* (einschließlich eines vorangestellten `/`, z.B. `/Index`).</span><span class="sxs-lookup"><span data-stu-id="107eb-271">The page name is the path to the page from the root */Pages* folder (including a leading `/`, for example `/Index`).</span></span> <span data-ttu-id="107eb-272">Die vorherigen Beispiele für die URL-Generierung sind viel umfangreicher an Features als eine einfache hartcodierte URL.</span><span class="sxs-lookup"><span data-stu-id="107eb-272">The preceding URL generation samples are much more feature rich than just hardcoding a URL.</span></span> <span data-ttu-id="107eb-273">Bei der URL-Generierung wird [Routing](xref:mvc/controllers/routing) verwendet. Außerdem können damit Parameter generiert und entsprechend der Definition der Route im Zielpfad codiert werden.</span><span class="sxs-lookup"><span data-stu-id="107eb-273">URL generation uses [routing](xref:mvc/controllers/routing) and can generate and encode parameters according to how the route is defined in the destination path.</span></span>

<span data-ttu-id="107eb-274">Die URL-Generierung für Seiten unterstützt relative Namen.</span><span class="sxs-lookup"><span data-stu-id="107eb-274">URL generation for pages supports relative names.</span></span> <span data-ttu-id="107eb-275">In der folgenden Tabelle wird dargestellt, welche Indexseite für verschiedene `RedirectToPage`-Parameter aus *Pages/Customers/Create.cshtml* ausgewählt wird:</span><span class="sxs-lookup"><span data-stu-id="107eb-275">The following table shows which Index page is selected with different `RedirectToPage` parameters from *Pages/Customers/Create.cshtml*:</span></span>

| <span data-ttu-id="107eb-276">RedirectToPage(x)</span><span class="sxs-lookup"><span data-stu-id="107eb-276">RedirectToPage(x)</span></span>| <span data-ttu-id="107eb-277">Seite</span><span class="sxs-lookup"><span data-stu-id="107eb-277">Page</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="107eb-278">RedirectToPage("/Index")</span><span class="sxs-lookup"><span data-stu-id="107eb-278">RedirectToPage("/Index")</span></span> | <span data-ttu-id="107eb-279">*Pages/Index*</span><span class="sxs-lookup"><span data-stu-id="107eb-279">*Pages/Index*</span></span> |
| <span data-ttu-id="107eb-280">RedirectToPage("./Index");</span><span class="sxs-lookup"><span data-stu-id="107eb-280">RedirectToPage("./Index");</span></span> | <span data-ttu-id="107eb-281">*Pages/Customers/Index*</span><span class="sxs-lookup"><span data-stu-id="107eb-281">*Pages/Customers/Index*</span></span> |
| <span data-ttu-id="107eb-282">RedirectToPage("../Index")</span><span class="sxs-lookup"><span data-stu-id="107eb-282">RedirectToPage("../Index")</span></span> | <span data-ttu-id="107eb-283">*Pages/Index*</span><span class="sxs-lookup"><span data-stu-id="107eb-283">*Pages/Index*</span></span> |
| <span data-ttu-id="107eb-284">RedirectToPage("Index")</span><span class="sxs-lookup"><span data-stu-id="107eb-284">RedirectToPage("Index")</span></span>  | <span data-ttu-id="107eb-285">*Pages/Customers/Index*</span><span class="sxs-lookup"><span data-stu-id="107eb-285">*Pages/Customers/Index*</span></span> |

<span data-ttu-id="107eb-286">`RedirectToPage("Index")`, `RedirectToPage("./Index")` und `RedirectToPage("../Index")` sind *relative Namen*.</span><span class="sxs-lookup"><span data-stu-id="107eb-286">`RedirectToPage("Index")`, `RedirectToPage("./Index")`, and `RedirectToPage("../Index")`  are *relative names*.</span></span> <span data-ttu-id="107eb-287">Der `RedirectToPage`-Parameter wird mit dem Pfad der aktuellen Seite *kombiniert*, um den Namen der Zielseite zu berechnen.</span><span class="sxs-lookup"><span data-stu-id="107eb-287">The `RedirectToPage` parameter is *combined* with the path of the current page to compute the name of the destination page.</span></span>  <!-- Review: Original had The provided string is combined with the page name of the current page to compute the name of the destination page. -- page name, not page path -->

<span data-ttu-id="107eb-288">Das Verknüpfen relativer Namen eignet sich beim Erstellen von Websites mit einer komplexen Struktur.</span><span class="sxs-lookup"><span data-stu-id="107eb-288">Relative name linking is useful when building sites with a complex structure.</span></span> <span data-ttu-id="107eb-289">Wenn Sie relative Namen verwenden, um Seiten in einem Ordner zu verknüpfen, können Sie diesen Ordner umbenennen.</span><span class="sxs-lookup"><span data-stu-id="107eb-289">If you use relative names to link between pages in a folder, you can rename that folder.</span></span> <span data-ttu-id="107eb-290">Alle Links funktionieren weiterhin, da sie nicht den Namen des Ordners enthalten.</span><span class="sxs-lookup"><span data-stu-id="107eb-290">All the links still work (because they didn't include the folder name).</span></span>

## <a name="tempdata"></a><span data-ttu-id="107eb-291">TempData</span><span class="sxs-lookup"><span data-stu-id="107eb-291">TempData</span></span>

<span data-ttu-id="107eb-292">ASP.NET Core macht die Eigenschaft [TempData](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) auf einem [Controller](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.controller) verfügbar.</span><span class="sxs-lookup"><span data-stu-id="107eb-292">ASP.NET Core exposes the [TempData](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) property on a [controller](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.controller).</span></span> <span data-ttu-id="107eb-293">Diese Eigenschaft speichert Daten, bis sie gelesen wurden.</span><span class="sxs-lookup"><span data-stu-id="107eb-293">This property stores data until it is read.</span></span> <span data-ttu-id="107eb-294">Die Methoden `Keep` und `Peek` können verwendet werden, um die Daten zu überprüfen, ohne sie zu löschen.</span><span class="sxs-lookup"><span data-stu-id="107eb-294">The `Keep` and `Peek` methods can be used to examine the data without deletion.</span></span> <span data-ttu-id="107eb-295">`TempData` eignet sich für die Weiterleitung, wenn Daten für mehr als eine Anforderung benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="107eb-295">`TempData` is  useful for redirection, when data is needed for more than a single request.</span></span>

<span data-ttu-id="107eb-296">Das `[TempData]`-Attribut ist neu in ASP.NET Core 2.0 und wird auf Domänencontrollern und Seiten unterstützt.</span><span class="sxs-lookup"><span data-stu-id="107eb-296">The `[TempData]` attribute is new in ASP.NET Core 2.0 and is supported on controllers and pages.</span></span>

<span data-ttu-id="107eb-297">Im folgenden Code wird der Wert von `Message` mit `TempData` festgelegt:</span><span class="sxs-lookup"><span data-stu-id="107eb-297">The following code sets the value of `Message` using `TempData`:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateDot.cshtml.cs?highlight=10-11,25&name=snippet_Temp)]

<span data-ttu-id="107eb-298">Das folgende Markup in der Datei *Pages/Customers/Index.cshtml* zeigt den Wert von `Message` mit `TempData` an.</span><span class="sxs-lookup"><span data-stu-id="107eb-298">The following markup in the *Pages/Customers/Index.cshtml* file displays the value of `Message` using `TempData`.</span></span>

```cshtml
<h3>Msg: @Model.Message</h3>
```

<span data-ttu-id="107eb-299">Die CodeBehind-Datei *Pages/Customers/Index.cshtml.cs* wendet das `[TempData]`-Attribut auf die Eigenschaft `Message`.</span><span class="sxs-lookup"><span data-stu-id="107eb-299">The *Pages/Customers/Index.cshtml.cs* code-behind file applies the `[TempData]` attribute to the `Message` property.</span></span>

```cs
[TempData]
public string Message { get; set; }
```

<span data-ttu-id="107eb-300">Weitere Informationen finden Sie unter [TempData](xref:fundamentals/app-state#temp).</span><span class="sxs-lookup"><span data-stu-id="107eb-300">See [TempData](xref:fundamentals/app-state#temp) for more information.</span></span>

<a name="mhpp"></a>
## <a name="multiple-handlers-per-page"></a><span data-ttu-id="107eb-301">Mehrere Handler pro Seite</span><span class="sxs-lookup"><span data-stu-id="107eb-301">Multiple handlers per page</span></span>

<span data-ttu-id="107eb-302">Die folgende Seite generiert mit dem `asp-page-handler`-Taghilfsprogramm Markup für zwei Handler:</span><span class="sxs-lookup"><span data-stu-id="107eb-302">The following page generates markup for two page handlers using the `asp-page-handler` Tag Helper:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?highlight=12-13)]

<!-- Review: the FormActionTagHelper applies to all <form /> elements on a Razor page, even when there is no `asp-` attribute   -->

<span data-ttu-id="107eb-303">Das Formular im vorherigen Beispiel hat zwei Sendeschaltflächen, und jede verwendet `FormActionTagHelper`, um an eine andere URL zu übermitteln.</span><span class="sxs-lookup"><span data-stu-id="107eb-303">The form in the preceding example has two submit buttons, each using the `FormActionTagHelper` to submit to a different URL.</span></span> <span data-ttu-id="107eb-304">Das `asp-page-handler`-Attribut ist eine Ergänzung für `asp-page`.</span><span class="sxs-lookup"><span data-stu-id="107eb-304">The `asp-page-handler` attribute is a companion to `asp-page`.</span></span> <span data-ttu-id="107eb-305">`asp-page-handler` generiert URLs, die als Übermittlungsziel jeweils die durch eine Seite festgelegte Handlermethode verwenden.</span><span class="sxs-lookup"><span data-stu-id="107eb-305">`asp-page-handler` generates URLs that submit to each of the handler methods defined by a page.</span></span> <span data-ttu-id="107eb-306">`asp-page` wird nicht angegeben, weil das Beispiel mit der aktuellen Seite verknüpft.</span><span class="sxs-lookup"><span data-stu-id="107eb-306">`asp-page` is not specified because the sample is linking to the current page.</span></span>

<span data-ttu-id="107eb-307">Die CodeBehind-Datei:</span><span class="sxs-lookup"><span data-stu-id="107eb-307">The code-behind file:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml.cs?highlight=20,32)]

<span data-ttu-id="107eb-308">Der vorherige Code verwendet *benannte Handlermethoden*.</span><span class="sxs-lookup"><span data-stu-id="107eb-308">The preceding code uses *named handler methods*.</span></span> <span data-ttu-id="107eb-309">Benannte Handlermethoden werden aus dem Text im Namen nach `On<HTTP Verb>` und vor `Async` (falls vorhanden) erstellt.</span><span class="sxs-lookup"><span data-stu-id="107eb-309">Named handler methods are created by taking the text in the name after `On<HTTP Verb>` and before `Async` (if present).</span></span> <span data-ttu-id="107eb-310">Im vorherigen Beispiel sind OnPost**JoinList**Async und OnPost**JoinListUC**Async die Seitenmethoden.</span><span class="sxs-lookup"><span data-stu-id="107eb-310">In the preceding example, the page methods are OnPost**JoinList**Async and OnPost**JoinListUC**Async.</span></span> <span data-ttu-id="107eb-311">Wenn Sie *OnPost* und *Async* entfernen, lauten die Handlernamen `JoinList` und `JoinListUC`.</span><span class="sxs-lookup"><span data-stu-id="107eb-311">With *OnPost* and *Async* removed, the handler names are `JoinList` and `JoinListUC`.</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?range=12-13)]

<span data-ttu-id="107eb-312">Mit dem vorherigen Code lautet der URL-Pfad, der an `OnPostJoinListAsync` übermittelt, `http://localhost:5000/Customers/CreateFATH?handler=JoinList`.</span><span class="sxs-lookup"><span data-stu-id="107eb-312">Using the preceding code, the URL path that submits to `OnPostJoinListAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinList`.</span></span> <span data-ttu-id="107eb-313">Der URL-Pfad, der an `OnPostJoinListUCAsync` übermittelt, lautet `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`.</span><span class="sxs-lookup"><span data-stu-id="107eb-313">The URL path that submits to `OnPostJoinListUCAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`.</span></span>

## <a name="customizing-routing"></a><span data-ttu-id="107eb-314">Anpassen des Routings</span><span class="sxs-lookup"><span data-stu-id="107eb-314">Customizing Routing</span></span>

<span data-ttu-id="107eb-315">Wenn Sie nicht möchten, dass die Abfragezeichenfolge `?handler=JoinList` in der URL enthalten ist, können Sie die Route ändern, damit der Handlername im Pfadteil der URL eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="107eb-315">If you don't like the query string `?handler=JoinList` in the URL, you can change the route to put the handler name in the path portion of the URL.</span></span> <span data-ttu-id="107eb-316">Sie können die Route anpassen, indem Sie eine Routenvorlage in doppelten Anführungszeichen nach der `@page`-Anweisung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="107eb-316">You can customize the route by adding a route template enclosed in double quotes after the `@page` directive.</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateRoute.cshtml?highlight=1)]

<span data-ttu-id="107eb-317">Die vorherige Route platziert den Handlernamen im URL-Pfad statt in die Abfragezeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="107eb-317">The preceding route puts the handler name in the URL path instead of the query string.</span></span> <span data-ttu-id="107eb-318">Das `?` nach `handler` bedeutet, dass der Routenparameter optional ist.</span><span class="sxs-lookup"><span data-stu-id="107eb-318">The `?` following `handler` means the route parameter is optional.</span></span>

<span data-ttu-id="107eb-319">Sie können einer Seitenroute mit `@page` weitere Segmente und Parameter hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="107eb-319">You can use `@page` to add additional segments and parameters to a page's route.</span></span> <span data-ttu-id="107eb-320">Alles, was hier angegeben wird, wird der Standardroute der Seite **angefügt**.</span><span class="sxs-lookup"><span data-stu-id="107eb-320">Whatever's there is **appended** to the default route of the page.</span></span> <span data-ttu-id="107eb-321">Die Verwendung eines absoluten oder des virtuellen Pfads, um die Seitenroute (z.B. `"~/Some/Other/Path"`) zu ändern, wird nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="107eb-321">Using an absolute or virtual path to change the page's route (like `"~/Some/Other/Path"`) is not supported.</span></span>

## <a name="configuration-and-settings"></a><span data-ttu-id="107eb-322">Konfiguration und Einstellungen</span><span class="sxs-lookup"><span data-stu-id="107eb-322">Configuration and settings</span></span>

<span data-ttu-id="107eb-323">Um die erweiterten Optionen zu konfigurieren, verwenden Sie die Erweiterungsmethode `AddRazorPagesOptions` auf dem MVC-Generator:</span><span class="sxs-lookup"><span data-stu-id="107eb-323">To configure advanced options, use the extension method `AddRazorPagesOptions` on the MVC builder:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/StartupAdvanced.cs?name=snippet_1)]

<span data-ttu-id="107eb-324">Derzeit können Sie `RazorPagesOptions` verwenden, um das Stammverzeichnis für Seiten festzulegen oder Anwendungsmodellkonventionen für Seiten hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="107eb-324">Currently you can use the `RazorPagesOptions` to set the root directory for pages, or add application model conventions for pages.</span></span> <span data-ttu-id="107eb-325">Auf diese Weise wird in Zukunft eine höhere Erweiterbarkeit erreicht.</span><span class="sxs-lookup"><span data-stu-id="107eb-325">We'll enable more extensibility this way in the future.</span></span>

<span data-ttu-id="107eb-326">Informationen zum Vorkompilieren von Ansichten finden Sie unter [Razor view compilation and precompilation in ASP.NET Core (Razor-Ansichtenkompilierung und Vorkompilierung in ASP.NET)](xref:mvc/views/view-compilation).</span><span class="sxs-lookup"><span data-stu-id="107eb-326">To precompile views, see [Razor view compilation](xref:mvc/views/view-compilation) .</span></span>

<span data-ttu-id="107eb-327">[Laden Sie Beispielcode herunter, oder zeigen Sie ihn an](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/index/sample).</span><span class="sxs-lookup"><span data-stu-id="107eb-327">[Download or view sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/index/sample).</span></span>

<span data-ttu-id="107eb-328">Lesen Sie auch den Artikel [Getting started with Razor Pages in ASP.NET Core (Erste Schritte mit Razor-Seiten in ASP.NET Core)](xref:tutorials/razor-pages/razor-pages-start), der auf diese Einführung aufbaut.</span><span class="sxs-lookup"><span data-stu-id="107eb-328">See [Getting started with Razor Pages in ASP.NET Core](xref:tutorials/razor-pages/razor-pages-start), which builds on this introduction.</span></span>

### <a name="specify-that-razor-pages-are-at-the-content-root"></a><span data-ttu-id="107eb-329">Festlegen des Inhaltsstammverzeichnisses für Razor-Seiten</span><span class="sxs-lookup"><span data-stu-id="107eb-329">Specify that Razor Pages are at the content root</span></span>

<span data-ttu-id="107eb-330">Standardmäßig lautet das Stammverzeichnis für Razor-Seiten */Pages*.</span><span class="sxs-lookup"><span data-stu-id="107eb-330">By default, Razor Pages are rooted in the */Pages* directory.</span></span> <span data-ttu-id="107eb-331">Fügen Sie [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot) zu [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) hinzu, um anzugeben, dass sich Ihre Razor-Dateien im Inhaltsstammverzeichnis ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) der App befinden:</span><span class="sxs-lookup"><span data-stu-id="107eb-331">Add [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at the content root ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) of the app:</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesAtContentRoot();
```

### <a name="specify-that-razor-pages-are-at-a-custom-root-directory"></a><span data-ttu-id="107eb-332">Festlegen eines benutzerdefinierten Stammverzeichnisses für Razor-Seiten</span><span class="sxs-lookup"><span data-stu-id="107eb-332">Specify that Razor Pages are at a custom root directory</span></span>

<span data-ttu-id="107eb-333">Fügen Sie [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot) zu [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) hinzu, um anzugeben, dass Ihre Razor-Seiten sich in einem benutzerdefinierten Stammverzeichnis in der App befinden (geben Sie einen relativen Pfad an):</span><span class="sxs-lookup"><span data-stu-id="107eb-333">Add [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at a custom root directory in the app (provide a relative path):</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesRoot("/path/to/razor/pages");
```

## <a name="see-also"></a><span data-ttu-id="107eb-334">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="107eb-334">See also</span></span>

* [<span data-ttu-id="107eb-335">Getting started with Razor Pages (Erste Schritte mit Razor-Seiten)</span><span class="sxs-lookup"><span data-stu-id="107eb-335">Getting started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* [<span data-ttu-id="107eb-336">Autorisierungskonventionen für Razor-Seiten</span><span class="sxs-lookup"><span data-stu-id="107eb-336">Razor Pages authorization conventions</span></span>](xref:security/authorization/razor-pages-authorization)
* [<span data-ttu-id="107eb-337">Benutzerdefinierte Routen- und Seitenmodellanbieter für Razor-Seiten</span><span class="sxs-lookup"><span data-stu-id="107eb-337">Razor Pages custom route and page model providers</span></span>](xref:mvc/razor-pages/razor-pages-convention-features)
* [<span data-ttu-id="107eb-338">Unit- und Integrationstests für Razor-Seiten</span><span class="sxs-lookup"><span data-stu-id="107eb-338">Razor Pages unit and integration testing</span></span>](xref:testing/razor-pages-testing)