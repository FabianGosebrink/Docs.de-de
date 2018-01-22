---
title: "Hinzufügen der Validierung"
author: rick-anderson
description: "Erläutert, wie einer Razor-Seite Validierung hinzugefügt wird."
keywords: ASP.NET Core, Validierung, DataAnnotations, Razor, Razor-Seiten
ms.author: riande
manager: wpickett
ms.date: 08/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/validation
ms.openlocfilehash: bd794ae2217c2a56f36cd46c2f12f1c80f6b4f2b
ms.sourcegitcommit: fe880bf4ed1c8116071c0e47c0babf3623b7f44a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="adding-validation-to-a-razor-page"></a><span data-ttu-id="8a950-104">Hinzufügen der Validierung zu einer Razor-Seite</span><span class="sxs-lookup"><span data-stu-id="8a950-104">Adding validation to a Razor Page</span></span>

<span data-ttu-id="8a950-105">Von [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8a950-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="8a950-106">In diesem Abschnitt wird dem Modell `Movie` Validierungslogik hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="8a950-106">In this section validation logic is added to the `Movie` model.</span></span> <span data-ttu-id="8a950-107">Die Validierungsregeln werden erzwungen, wenn ein Benutzer einen Film erstellt oder bearbeitet.</span><span class="sxs-lookup"><span data-stu-id="8a950-107">The validation rules are enforced any time a user creates or edits a movie.</span></span>

## <a name="validation"></a><span data-ttu-id="8a950-108">Validierung</span><span class="sxs-lookup"><span data-stu-id="8a950-108">Validation</span></span>

<span data-ttu-id="8a950-109">Ein wesentlicher Grundsatz der Softwareentwicklung heißt [DRY](https://wikipedia.org/wiki/Don%27t_repeat_yourself) (**D**on't **R**epeat **Y**ourself, dt. Wiederholen Sie sich nicht).</span><span class="sxs-lookup"><span data-stu-id="8a950-109">A key tenet of software development is called [DRY](https://wikipedia.org/wiki/Don%27t_repeat_yourself) ("**D**on't **R**epeat **Y**ourself").</span></span> <span data-ttu-id="8a950-110">Razor-Seiten sind für Entwicklungsaufgaben gedacht, bei denen Funktionalität einmal angegeben und in der gesamten App übernommen wird.</span><span class="sxs-lookup"><span data-stu-id="8a950-110">Razor Pages encourages development where functionality is specified once, and it's reflected throughout the app.</span></span> <span data-ttu-id="8a950-111">Der DRY-Ansatz kann die Codemenge in einer App reduzieren.</span><span class="sxs-lookup"><span data-stu-id="8a950-111">DRY can help reduce the amount of code in an app.</span></span> <span data-ttu-id="8a950-112">Durch diesen Ansatz wird Code weniger fehleranfällig und lässt sich leichter testen und verwalten.</span><span class="sxs-lookup"><span data-stu-id="8a950-112">DRY makes the code less error prone, and easier to test and maintain.</span></span>

<span data-ttu-id="8a950-113">Die von Razor-Seiten und Entity Framework gebotene Unterstützung der Validierung ist ein gutes Beispiel des DRY-Prinzips.</span><span class="sxs-lookup"><span data-stu-id="8a950-113">The validation support provided by Razor Pages and Entity Framework is a good example of the DRY principle.</span></span> <span data-ttu-id="8a950-114">Validierungsregeln werden an zentraler Stelle (in der Modellklasse) deklarativ angegeben und überall in der App erzwungen.</span><span class="sxs-lookup"><span data-stu-id="8a950-114">Validation rules are declaratively specified in one place (in the model class), and the rules are enforced everywhere in the app.</span></span>

### <a name="adding-validation-rules-to-the-movie-model"></a><span data-ttu-id="8a950-115">Hinzufügen von Validierungsregeln zum Modell „Movie“</span><span class="sxs-lookup"><span data-stu-id="8a950-115">Adding validation rules to the movie model</span></span>

<span data-ttu-id="8a950-116">Öffnen Sie Datei *Movie.cs*.</span><span class="sxs-lookup"><span data-stu-id="8a950-116">Open the *Movie.cs* file.</span></span> <span data-ttu-id="8a950-117">[DataAnnotations](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) bietet eine integrierte Gruppe von Validierungsattributen, die deklarativ auf eine Klasse oder Eigenschaft angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="8a950-117">[DataAnnotations](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) provides a built-in set of validation attributes that are applied declaratively to a class or property.</span></span> <span data-ttu-id="8a950-118">„DataAnnotations“ enthält auch Formatierungsattribute wie `DataType`, die bei der Formatierung helfen und keine Validierung bieten.</span><span class="sxs-lookup"><span data-stu-id="8a950-118">DataAnnotations also contains formatting attributes like `DataType` that help with formatting and don't provide validation.</span></span>

<span data-ttu-id="8a950-119">Aktualisieren Sie die `Movie`-Klasse, um die Validierungsattribute `Required`, `StringLength`, `RegularExpression` und `Range` zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="8a950-119">Update the `Movie` class to take advantage of the `Required`, `StringLength`, `RegularExpression`, and `Range` validation attributes.</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Models/MovieDateRatingDA.cs?name=snippet1)]

<span data-ttu-id="8a950-120">Validierungsattribute geben das Verhalten an, das für Modelleigenschaften erzwungen wird:</span><span class="sxs-lookup"><span data-stu-id="8a950-120">Validation attributes specify behavior that's enforced on model properties:</span></span>

* <span data-ttu-id="8a950-121">Die Attribute `Required` und `MinimumLength` geben an, dass eine Eigenschaft über einen Wert verfügen muss.</span><span class="sxs-lookup"><span data-stu-id="8a950-121">The `Required` and `MinimumLength` attributes indicate that a property must have a value.</span></span> <span data-ttu-id="8a950-122">Nichts hindert Benutzer allerdings daran, Leerzeichen einzugeben, um die Validierungseinschränkung für einen Nullable-Typ zu umgehen.</span><span class="sxs-lookup"><span data-stu-id="8a950-122">However, nothing prevents a user from entering whitespace to satisfy the validation constraint for a nullable type.</span></span> <span data-ttu-id="8a950-123">[Werttypen](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/value-types), bei denen es sich nicht um Nullable-Typen handelt (wie z.B. `decimal`, `int`, `float` und `DateTime`), sind grundsätzlich erforderlich und benötigen das Attribut `Required` nicht.</span><span class="sxs-lookup"><span data-stu-id="8a950-123">Non-nullable [value types](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/value-types) (such as `decimal`, `int`, `float`, and `DateTime`) are inherently required and don't need the `Required` attribute.</span></span>
* <span data-ttu-id="8a950-124">Das Attribut `RegularExpression` schränkt die Zeichen ein, die ein Benutzer eingeben kann.</span><span class="sxs-lookup"><span data-stu-id="8a950-124">The `RegularExpression` attribute limits the characters that the user can enter.</span></span> <span data-ttu-id="8a950-125">Im oben stehenden Code sind für `Genre` und `Rating` nur Buchstaben erlaubt (Leerzeichen, Ziffern und Sonderzeichen sind nicht zulässig).</span><span class="sxs-lookup"><span data-stu-id="8a950-125">In the preceding code, `Genre` and `Rating` must use only letters (whitespace, numbers, and special characters aren't allowed).</span></span>
* <span data-ttu-id="8a950-126">Das Attribut `Range` schränkt einen Wert auf einen bestimmten Bereich ein.</span><span class="sxs-lookup"><span data-stu-id="8a950-126">The `Range` attribute constrains a value to a specified range.</span></span>
* <span data-ttu-id="8a950-127">Das Attribut `StringLength` legt die Höchstlänge einer Zeichenfolge und optional die Mindestlänge fest.</span><span class="sxs-lookup"><span data-stu-id="8a950-127">The `StringLength` attribute sets the maximum length of a string, and optionally the minimum length.</span></span> 

<span data-ttu-id="8a950-128">Dadurch, dass Validierungsregeln von ASP.NET Core automatisch erzwungen werden, wird eine App stabiler.</span><span class="sxs-lookup"><span data-stu-id="8a950-128">Having validation rules automatically enforced by ASP.NET Core helps make an app more robust.</span></span> <span data-ttu-id="8a950-129">Die automatische Validierung für Modelle hilft beim Schutz der App, da Sie nicht daran denken müssen, diesen anzuwenden, sobald neuer Code hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="8a950-129">Automatic validation on models helps protect the app because you don't have to remember to apply them when new code is added.</span></span>

### <a name="validation-error-ui-in-razor-pages"></a><span data-ttu-id="8a950-130">Benutzeroberflächenoption für Validierungsfehler in Razor-Seiten</span><span class="sxs-lookup"><span data-stu-id="8a950-130">Validation Error UI in Razor Pages</span></span>

<span data-ttu-id="8a950-131">Führen Sie die App aus, und navigieren Sie zu „Pages/Movies“.</span><span class="sxs-lookup"><span data-stu-id="8a950-131">Run the app and navigate to Pages/Movies.</span></span>

<span data-ttu-id="8a950-132">Klicken Sie auf den Link **Neu erstellen**.</span><span class="sxs-lookup"><span data-stu-id="8a950-132">Select the **Create New** link.</span></span> <span data-ttu-id="8a950-133">Füllen Sie das Formular mit einigen ungültigen Werten aus.</span><span class="sxs-lookup"><span data-stu-id="8a950-133">Complete the form with some invalid values.</span></span> <span data-ttu-id="8a950-134">Wenn die clientseitige jQuery-Validierung den Fehler erkennt, wird eine Fehlermeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8a950-134">When jQuery client-side validation detects the error, it displays an error message.</span></span>

![Ansichtsformular „Movie“ mit mehreren clientseitigen jQuery-Validierungsfehlern](validation/_static/val.png)

> [!NOTE]
> <span data-ttu-id="8a950-136">Sie können ggf. in das Feld `Price` keine Dezimaltrennzeichen oder Kommas eingeben.</span><span class="sxs-lookup"><span data-stu-id="8a950-136">You may not be able to enter decimal points or commas in the `Price` field.</span></span> <span data-ttu-id="8a950-137">Zur Unterstützung der [jQuery-Validierung](https://jqueryvalidation.org/) in nicht englischen Gebietsschemas, in denen ein Komma („,“) als Dezimaltrennzeichen verwendet wird, und Nicht-US-englischen Datums- und Uhrzeitformaten müssen Sie Schritte zur Globalisierung Ihrer App ausführen.</span><span class="sxs-lookup"><span data-stu-id="8a950-137">To support [jQuery validation](https://jqueryvalidation.org/) in non-English locales that use a comma (",") for a decimal point, and non US-English date formats, you must take steps to globalize your app.</span></span> <span data-ttu-id="8a950-138">Weitere Informationen finden Sie unter [Zusätzliche Ressourcen](#additional-resources).</span><span class="sxs-lookup"><span data-stu-id="8a950-138">See [Additional resources](#additional-resources) for more information.</span></span> <span data-ttu-id="8a950-139">Geben Sie einstweilen ganze Zahlen wie 10 ein.</span><span class="sxs-lookup"><span data-stu-id="8a950-139">For now, just enter whole numbers like 10.</span></span>

<span data-ttu-id="8a950-140">Wie Sie sehen, hat das Formular in allen Feldern mit einem ungültigen Wert automatisch eine Validierungsfehlermeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8a950-140">Notice how the form has automatically rendered a validation error message in each field containing an invalid value.</span></span> <span data-ttu-id="8a950-141">Die Fehlermeldungen werden sowohl auf Clientseite (mithilfe von JavaScript und jQuery) als auch auf Serverseite erzwungen (wenn ein Benutzer JavaScript deaktiviert hat).</span><span class="sxs-lookup"><span data-stu-id="8a950-141">The errors are enforced both client-side (using JavaScript and jQuery) and server-side (when a user has JavaScript disabled).</span></span>

<span data-ttu-id="8a950-142">Ein entscheidender Vorteil ist, dass **keine** Codeänderungen auf den Seiten „Erstellen“ oder „Bearbeiten“ erforderlich waren.</span><span class="sxs-lookup"><span data-stu-id="8a950-142">A significant benefit is that **no** code changes were necessary in the Create  or Edit pages.</span></span> <span data-ttu-id="8a950-143">Nach Anwenden von „DataAnnotations“ auf das Modell wurde die Benutzeroberflächenvalidierung aktiviert.</span><span class="sxs-lookup"><span data-stu-id="8a950-143">Once DataAnnotations were applied to the model, the validation UI was enabled.</span></span> <span data-ttu-id="8a950-144">Die in diesem Tutorial erstellten Razor-Seiten haben die Validierungsregeln automatisch übernommen (mithilfe der Validierungsattribute für die Eigenschaften der Modellklasse `Movie`).</span><span class="sxs-lookup"><span data-stu-id="8a950-144">The Razor Pages created in this tutorial automatically picked up the validation rules (using validation attributes on the properties of the `Movie` model class).</span></span> <span data-ttu-id="8a950-145">Testen Sie die Validierung mithilfe der Seite „Bearbeiten“. Es erfolgt dieselbe Validierung.</span><span class="sxs-lookup"><span data-stu-id="8a950-145">Test validation using the Edit page, the same validation is applied.</span></span>

<span data-ttu-id="8a950-146">Die Formulardaten werden erst an den Server zurückgesendet, wenn auf Clientseite keine Validierungsfehler auftreten.</span><span class="sxs-lookup"><span data-stu-id="8a950-146">The form data is not posted to the server until there are no client-side validation errors.</span></span> <span data-ttu-id="8a950-147">Überprüfen Sie, ob Formulardaten nicht zurückgesendet werden, mithilfe einer oder mehrerer der folgenden Vorgehensweisen:</span><span class="sxs-lookup"><span data-stu-id="8a950-147">Verify form data is not posted by one or more of the following approaches:</span></span>

* <span data-ttu-id="8a950-148">Setzen Sie einen Haltepunkt in der `OnPostAsync`-Methode.</span><span class="sxs-lookup"><span data-stu-id="8a950-148">Put a break point in the `OnPostAsync` method.</span></span> <span data-ttu-id="8a950-149">Senden Sie das Formular (wählen Sie **Erstellen** oder **Speichern**).</span><span class="sxs-lookup"><span data-stu-id="8a950-149">Submit the form (select **Create** or **Save**).</span></span> <span data-ttu-id="8a950-150">Der Haltepunkt wird niemals erreicht.</span><span class="sxs-lookup"><span data-stu-id="8a950-150">The break point is never hit.</span></span>
* <span data-ttu-id="8a950-151">Verwenden Sie das [Tool Fiddler](http://www.telerik.com/fiddler).</span><span class="sxs-lookup"><span data-stu-id="8a950-151">Use the [Fiddler tool](http://www.telerik.com/fiddler).</span></span>
* <span data-ttu-id="8a950-152">Verwenden Sie die Browserentwicklungstools zum Überwachen des Netzwerkdatenverkehrs.</span><span class="sxs-lookup"><span data-stu-id="8a950-152">Use the browser developer tools to monitor network traffic.</span></span>

### <a name="server-side-validation"></a><span data-ttu-id="8a950-153">Serverseitige Validierung</span><span class="sxs-lookup"><span data-stu-id="8a950-153">Server-side validation</span></span>

<span data-ttu-id="8a950-154">Wenn JavaScript im Browser deaktiviert ist, erfolgt beim Senden des Formulars mit Fehlern eine Bereitstellung auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="8a950-154">When JavaScript is disabled in the browser, submitting the form with errors will post to the server.</span></span>

<span data-ttu-id="8a950-155">Testen Sie optional die serverseitige Validierung:</span><span class="sxs-lookup"><span data-stu-id="8a950-155">Optional, test server-side validation:</span></span>

* <span data-ttu-id="8a950-156">Deaktivieren Sie JavaScript im Browser.</span><span class="sxs-lookup"><span data-stu-id="8a950-156">Disable JavaScript in the browser.</span></span> <span data-ttu-id="8a950-157">Wenn Sie JavaScript im Browser nicht deaktivieren können, probieren Sie einen anderen Browser.</span><span class="sxs-lookup"><span data-stu-id="8a950-157">If you can't disable JavaScript in the browser, try another browser.</span></span>
* <span data-ttu-id="8a950-158">Setzen Sie auf der Seite „Erstellen“ oder „Bearbeiten“ in der `OnPostAsync`-Methode einen Haltepunkt.</span><span class="sxs-lookup"><span data-stu-id="8a950-158">Set a break point in the `OnPostAsync` method of the Create or Edit page.</span></span>
* <span data-ttu-id="8a950-159">Senden Sie ein Formular mit Validierungsfehlern.</span><span class="sxs-lookup"><span data-stu-id="8a950-159">Submit a form with validation errors.</span></span>
* <span data-ttu-id="8a950-160">Überprüfen Sie, ob der Modellstatus ungültig ist:</span><span class="sxs-lookup"><span data-stu-id="8a950-160">Verify the model state is invalid:</span></span>

  ```csharp
   if (!ModelState.IsValid)
   {
      return Page();
   }
  ```

<span data-ttu-id="8a950-161">Der folgende Code zeigt einen Teil der Seite *Create.cshtml*, deren Gerüst Sie zuvor im Tutorial erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="8a950-161">The following code shows a portion of the *Create.cshtml* page that you scaffolded earlier in the tutorial.</span></span> <span data-ttu-id="8a950-162">Sie wird von den Seiten „Erstellen“ und „Bearbeiten“ zum Anzeigen des anfänglichen Formulars und zum erneuten Anzeigen des Formulars bei einem Fehler verwendet.</span><span class="sxs-lookup"><span data-stu-id="8a950-162">It's used by the Create and Edit pages to display the initial form and to redisplay the form in the event of an error.</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Create.cshtml?range=14-20)]

<span data-ttu-id="8a950-163">Das [Hilfsprogramm für Eingabetags](xref:mvc/views/working-with-forms) verwendet die Attribute von [DataAnnotations](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) und generiert HTML-Attribute, die auf der Clientseite für die jQuery-Validierung erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="8a950-163">The [Input Tag Helper](xref:mvc/views/working-with-forms) uses the [DataAnnotations](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) attributes and produces HTML attributes needed for jQuery Validation on the client-side.</span></span> <span data-ttu-id="8a950-164">Das [Hilfsprogramm für Validierungstags](xref:mvc/views/working-with-forms#the-validation-tag-helpers) zeigt Validierungsfehler.</span><span class="sxs-lookup"><span data-stu-id="8a950-164">The [Validation Tag Helper](xref:mvc/views/working-with-forms#the-validation-tag-helpers) displays validation errors.</span></span> <span data-ttu-id="8a950-165">Weitere Informationen finden Sie unter [Validierung](xref:mvc/models/validation).</span><span class="sxs-lookup"><span data-stu-id="8a950-165">See [Validation](xref:mvc/models/validation) for more information.</span></span>

<span data-ttu-id="8a950-166">Die Seiten „Erstellen“ und „Bearbeiten“ weisen keine Validierungsregeln auf.</span><span class="sxs-lookup"><span data-stu-id="8a950-166">The Create and Edit pages have no validation rules in them.</span></span> <span data-ttu-id="8a950-167">Die Validierungsregeln und Fehlerzeichenfolgen werden nur in der `Movie`-Klasse angegeben.</span><span class="sxs-lookup"><span data-stu-id="8a950-167">The validation rules and the error strings are specified only in the `Movie` class.</span></span> <span data-ttu-id="8a950-168">Diese Validierungsregeln gelten automatisch für Razor-Seiten, die das Modell `Movie` bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="8a950-168">These validation rules are automatically applied to Razor Pages that edit the `Movie` model.</span></span>

<span data-ttu-id="8a950-169">Wenn Validierungslogik geändert werden muss, erfolgt dies nur im Modell.</span><span class="sxs-lookup"><span data-stu-id="8a950-169">When validation logic needs to change, it's done only in the model.</span></span> <span data-ttu-id="8a950-170">Die Validierung erfolgt in der gesamten Anwendung einheitlich (Validierungslogik ist zentral definiert).</span><span class="sxs-lookup"><span data-stu-id="8a950-170">Validation is applied consistently throughout the application (validation logic is defined in one place).</span></span> <span data-ttu-id="8a950-171">Die zentrale Validierung unterstützt sauberen Code und erleichtert dessen Verwaltung und Aktualisierung.</span><span class="sxs-lookup"><span data-stu-id="8a950-171">Validation in one place helps keep the code clean, and makes it easier to maintain and update.</span></span>

## <a name="using-datatype-attributes"></a><span data-ttu-id="8a950-172">Verwenden von „DataType“-Attributen</span><span class="sxs-lookup"><span data-stu-id="8a950-172">Using DataType Attributes</span></span>

<span data-ttu-id="8a950-173">Untersuchen Sie die Klasse `Movie`.</span><span class="sxs-lookup"><span data-stu-id="8a950-173">Examine the `Movie` class.</span></span> <span data-ttu-id="8a950-174">Der Namespace `System.ComponentModel.DataAnnotations` stellt zusätzlich zu der integrierten Gruppe von Validierungsattributen Formatierungsattribute bereit.</span><span class="sxs-lookup"><span data-stu-id="8a950-174">The `System.ComponentModel.DataAnnotations` namespace provides formatting attributes in addition to the built-in set of validation attributes.</span></span> <span data-ttu-id="8a950-175">Das `DataType`-Attribut wird nur auf die Eigenschaften `ReleaseDate` und `Price` angewendet.</span><span class="sxs-lookup"><span data-stu-id="8a950-175">The `DataType` attribute is applied to the `ReleaseDate` and `Price` properties.</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/MovieDateRatingDA.cs?highlight=2,6&name=snippet2)]

<span data-ttu-id="8a950-176">Die `DataType`-Attribute geben dem Anzeigemodul nur Hinweise zum Formatieren der Daten (und liefern Attribute wie `<a>` für URLs und `<a href="mailto:EmailAddress.com">` für E-Mail).</span><span class="sxs-lookup"><span data-stu-id="8a950-176">The `DataType` attributes only provide hints for the view engine to format the data (and supplies attributes such as `<a>` for URL's and `<a href="mailto:EmailAddress.com">` for email).</span></span> <span data-ttu-id="8a950-177">Verwenden Sie das `RegularExpression`-Attribut, um das Format der Daten zu validieren.</span><span class="sxs-lookup"><span data-stu-id="8a950-177">Use the `RegularExpression` attribute to validate the format of the data.</span></span> <span data-ttu-id="8a950-178">Das `DataType`-Attribut wird verwendet, um einen Datentyp anzugeben, der spezifischer als der datenbankinterne Typ ist.</span><span class="sxs-lookup"><span data-stu-id="8a950-178">The `DataType` attribute is used to specify a data type that is more specific than the database intrinsic type.</span></span> <span data-ttu-id="8a950-179">`DataType`-Attribute sind keine Validierungsattribute.</span><span class="sxs-lookup"><span data-stu-id="8a950-179">`DataType` attributes are not validation attributes.</span></span> <span data-ttu-id="8a950-180">In der Beispielanwendung wird nur das Datum ohne Uhrzeit angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8a950-180">In the sample application, only the date is displayed, without time.</span></span>

<span data-ttu-id="8a950-181">Die `DataType`-Enumeration stellt viele Datentypen bereit, wie z.B. „Date“, „Time“, „PhoneNumber“, „Currency“, „EmailAddress“ usw.</span><span class="sxs-lookup"><span data-stu-id="8a950-181">The `DataType` Enumeration provides for many data types, such as Date, Time, PhoneNumber, Currency, EmailAddress, and more.</span></span> <span data-ttu-id="8a950-182">Das `DataType`-Attribut kann der Anwendung auch ermöglichen, typspezifische Features bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="8a950-182">The `DataType` attribute can also enable the application to automatically provide type-specific features.</span></span> <span data-ttu-id="8a950-183">Ein Link des Typs `mailto:` kann beispielsweise für `DataType.EmailAddress` erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="8a950-183">For example, a `mailto:` link can be created for `DataType.EmailAddress`.</span></span> <span data-ttu-id="8a950-184">In Browsern mit HTML5-Unterstützung kann für `DataType.Date` eine Datumsauswahl bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="8a950-184">A date selector can be provided for `DataType.Date` in browsers that support HTML5.</span></span> <span data-ttu-id="8a950-185">Die `DataType`-Attribute geben `data-`-Attribute (ausgesprochen „Datadash“) von HTML5 aus, die HTML5-Browser nutzen.</span><span class="sxs-lookup"><span data-stu-id="8a950-185">The `DataType` attributes emits HTML 5 `data-` (pronounced data dash) attributes that HTML 5 browsers consume.</span></span> <span data-ttu-id="8a950-186">Die `DataType`-Attribute bieten **keine** Validierung.</span><span class="sxs-lookup"><span data-stu-id="8a950-186">The `DataType` attributes do **not** provide any validation.</span></span>

<span data-ttu-id="8a950-187">`DataType.Date` gibt nicht das Format des Datums an, das angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="8a950-187">`DataType.Date` does not specify the format of the date that is displayed.</span></span> <span data-ttu-id="8a950-188">Standardmäßig wird das Datenfeld gemäß den Standardformaten basierend auf `CultureInfo` des Servers angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8a950-188">By default, the data field is displayed according to the default formats based on the server's `CultureInfo`.</span></span>

<span data-ttu-id="8a950-189">Das `DisplayFormat`-Attribut dient zum expliziten Angeben des Datumsformats:</span><span class="sxs-lookup"><span data-stu-id="8a950-189">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
public DateTime ReleaseDate { get; set; }
```

<span data-ttu-id="8a950-190">Die Einstellung `ApplyFormatInEditMode` gibt an, dass die Formatierung angewendet werden soll, wenn der Wert zur Bearbeitung angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="8a950-190">The `ApplyFormatInEditMode` setting specifies that the formatting should be applied when the value is displayed for editing.</span></span> <span data-ttu-id="8a950-191">Dieses Verhalten ist für einige Felder ggf. nicht wünschenswert.</span><span class="sxs-lookup"><span data-stu-id="8a950-191">You might not want that behavior for some fields.</span></span> <span data-ttu-id="8a950-192">In Währungswerten möchten Sie beispielsweise wahrscheinlich nicht das Währungssymbol auf der Bearbeitungsoberfläche anzeigen.</span><span class="sxs-lookup"><span data-stu-id="8a950-192">For example, in currency values, you probably do not want the currency symbol in the edit UI.</span></span>

<span data-ttu-id="8a950-193">Das `DisplayFormat`-Attribut kann eigenständig verwendet werden, doch meist empfiehlt es sich, das `DataType`-Attribut zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="8a950-193">The `DisplayFormat` attribute can be used by itself, but it's generally a good idea to use the `DataType` attribute.</span></span> <span data-ttu-id="8a950-194">Das `DataType`-Attribut übermittelt die Semantik der Daten im Gegensatz zu deren Rendern auf einem Bildschirm. Es bietet die folgenden Vorteile, die „DisplayFormat“ nicht bietet:</span><span class="sxs-lookup"><span data-stu-id="8a950-194">The `DataType` attribute conveys the semantics of the data as opposed to how to render it on a screen, and provides the following benefits that you don't get with DisplayFormat:</span></span>

* <span data-ttu-id="8a950-195">Der Browser kann HTML5-Features aktivieren (z.B. zum Anzeigen eines Kalendersteuerelements, des dem Gebietsschema entsprechenden Währungssymbols, von E-Mail-Links usw.).</span><span class="sxs-lookup"><span data-stu-id="8a950-195">The browser can enable HTML5 features (for example to show a calendar control, the locale-appropriate currency symbol, email links, etc.)</span></span>
* <span data-ttu-id="8a950-196">Standardmäßig rendert der Browser Daten mit dem ordnungsgemäßen auf Ihrem Gebietsschema basierenden Format.</span><span class="sxs-lookup"><span data-stu-id="8a950-196">By default, the browser will render data using the correct format based on your locale.</span></span>
* <span data-ttu-id="8a950-197">Das `DataType`-Attribut kann dem ASP.NET Core-Framework ermöglichen, die richtige Feldvorlage zum Rendern der Daten auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="8a950-197">The `DataType` attribute can enable the ASP.NET Core framework to choose the right field template to render the data.</span></span> <span data-ttu-id="8a950-198">`DisplayFormat`, falls eigenständig genutzt, verwendet die Zeichenfolgenvorlage.</span><span class="sxs-lookup"><span data-stu-id="8a950-198">The `DisplayFormat` if used by itself uses the string template.</span></span>

<span data-ttu-id="8a950-199">Hinweis: Die jQuery-Validierung funktioniert nicht mit dem `Range`-Attribut und `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="8a950-199">Note: jQuery validation does not work with the `Range` attribute and `DateTime`.</span></span> <span data-ttu-id="8a950-200">Bei folgendem Code wird z.B. stets ein clientseitiger Validierungsfehler angezeigt, auch wenn sich das Datum im angegebenen Bereich befindet:</span><span class="sxs-lookup"><span data-stu-id="8a950-200">For example, the following code will always display a client-side validation error, even when the date is in the specified range:</span></span>

```csharp
[Range(typeof(DateTime), "1/1/1966", "1/1/2020")]
   ```

<span data-ttu-id="8a950-201">Es wird allgemein nicht empfohlen, feste Datumsangaben in Ihren Modellen zu kompilieren, weshalb vom Einsatz des `Range`-Attributs und von `DateTime` abgeraten wird.</span><span class="sxs-lookup"><span data-stu-id="8a950-201">It's generally not a good practice to compile hard dates in your models, so using the `Range` attribute and `DateTime` is discouraged.</span></span>

<span data-ttu-id="8a950-202">Der folgende Code zeigt die Kombination von Attributen in einer Zeile:</span><span class="sxs-lookup"><span data-stu-id="8a950-202">The following code shows combining attributes on one line:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/MovieDateRatingDAmult.cs?name=snippet1)]

<span data-ttu-id="8a950-203">[Erste Schritte mit Razor-Seiten und EF Core](xref:data/ef-rp/intro) zeigt erweiterte EF Core-Vorgänge mit Razor-Seiten.</span><span class="sxs-lookup"><span data-stu-id="8a950-203">[Getting started with Razor Pages and EF Core](xref:data/ef-rp/intro) shows more advanced EF Core operations with Razor Pages.</span></span>

### <a name="publish-to-azure"></a><span data-ttu-id="8a950-204">Veröffentlichen in Azure</span><span class="sxs-lookup"><span data-stu-id="8a950-204">Publish to Azure</span></span>

<span data-ttu-id="8a950-205">Anweisungen zum Veröffentlichen dieser App in Azure finden Sie unter [Veröffentlichen einer ASP.NET Core-Web-App in Azure App Service mit Visual Studio](xref:tutorials/publish-to-azure-webapp-using-vs).</span><span class="sxs-lookup"><span data-stu-id="8a950-205">See [Publish an ASP.NET Core web app to Azure App Service using Visual Studio](xref:tutorials/publish-to-azure-webapp-using-vs) for instructions on how to publish this app to Azure.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a950-206">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="8a950-206">Additional resources</span></span>

* [<span data-ttu-id="8a950-207">Arbeiten mit Formularen</span><span class="sxs-lookup"><span data-stu-id="8a950-207">Working with Forms</span></span>](xref:mvc/views/working-with-forms)
* [<span data-ttu-id="8a950-208">Globalisierung und Lokalisierung</span><span class="sxs-lookup"><span data-stu-id="8a950-208">Globalization and localization</span></span>](xref:fundamentals/localization)
* [<span data-ttu-id="8a950-209">Einführung in Taghilfsprogramme</span><span class="sxs-lookup"><span data-stu-id="8a950-209">Introduction to Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="8a950-210">Erstellen von Taghilfsprogrammen</span><span class="sxs-lookup"><span data-stu-id="8a950-210">Authoring Tag Helpers</span></span>](xref:mvc/views/tag-helpers/authoring)

>[!div class="step-by-step"]
<span data-ttu-id="8a950-211">[Zurück: Hinzufügen eines neuen Feldes](xref:tutorials/razor-pages/new-field)
[Weiter: Hochladen von Dateien](xref:tutorials/razor-pages/uploading-files)</span><span class="sxs-lookup"><span data-stu-id="8a950-211">[Previous: Adding a new field](xref:tutorials/razor-pages/new-field)
[Next: Uploading files](xref:tutorials/razor-pages/uploading-files)</span></span>