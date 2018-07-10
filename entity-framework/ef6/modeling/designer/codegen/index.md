---
title: Szablony generowania kodu projektanta - EF6
author: divega
ms.date: 2016-10-23
ms.prod: entity-framework
ms.author: divega
ms.manager: avickers
ms.technology: entity-framework-6
ms.topic: article
ms.assetid: 56e00fa2-f9f0-48b3-8006-f8266ca7e74b
caps.latest.revision: 3
ms.openlocfilehash: e06dc1c35f8d74772e5c7d69b29553288fd652d0
ms.sourcegitcommit: f05e7b62584cf228f17390bb086a61d505712e1b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2018
ms.locfileid: "37912710"
---
# <a name="designer-code-generation-templates"></a><span data-ttu-id="399fb-102">Szablonów generowania kodu projektanta</span><span class="sxs-lookup"><span data-stu-id="399fb-102">Designer Code Generation Templates</span></span>
<span data-ttu-id="399fb-103">Podczas tworzenia modelu przy użyciu programu Entity Framework Designer klas i kontekst pochodna są generowane automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="399fb-103">When you create a model using the Entity Framework Designer your classes and derived context are automatically generated for you.</span></span> <span data-ttu-id="399fb-104">Oprócz generowania kodu domyślne oferujemy są również szablony, których można dostosować program code, który pobiera wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="399fb-104">In addition to the default code generation we also provide a number of templates that can be used to customize the code that gets generated.</span></span> <span data-ttu-id="399fb-105">Te szablony stanowią one szablonów tekstowych T4, dzięki czemu możesz dostosowywać szablony, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="399fb-105">These templates are provided as T4 Text Templates, allowing you to customize the templates if needed.</span></span>

<span data-ttu-id="399fb-106">Kod, który pobiera wygenerowany domyślnie, zależy od wersji programu Visual Studio Tworzenie modelu w:</span><span class="sxs-lookup"><span data-stu-id="399fb-106">The code that gets generated by default depends on which version of Visual Studio you create your model in:</span></span>

-   <span data-ttu-id="399fb-107">Modele utworzone w programie Visual Studio 2012 i 2013 generuje prosty klas obiektów POCO i kontekście, który pochodzi z uproszczonego DbContext.</span><span class="sxs-lookup"><span data-stu-id="399fb-107">Models created in Visual Studio 2012 & 2013 will generate simple POCO entity classes and a context that derives from the simplified DbContext.</span></span>
-   <span data-ttu-id="399fb-108">Modele utworzone w programie Visual Studio 2010, spowoduje wygenerowanie klas jednostek, które wynikają z EntityObject i kontekstu, która pochodzi z obiektu ObjectContext.</span><span class="sxs-lookup"><span data-stu-id="399fb-108">Models created in Visual Studio 2010 will generate entity classes that derive from EntityObject and a context that derives from ObjectContext.</span></span>
  > [!NOTE]    
  > <span data-ttu-id="399fb-109">Firma Microsoft zaleca, przełączanie do szablonu DbContext Generator po dodaniu modelu.</span><span class="sxs-lookup"><span data-stu-id="399fb-109">We recommend switching to the DbContext Generator template once you've added your model.</span></span>

<span data-ttu-id="399fb-110">Ta strona obejmuje dostępnych szablonów i następnie zawiera instrukcje dotyczące dodawania szablonu do modelu.</span><span class="sxs-lookup"><span data-stu-id="399fb-110">This page covers the available templates and then provides instructions for adding a template to your model.</span></span>

## <a name="available-templates"></a><span data-ttu-id="399fb-111">Dostępne szablony</span><span class="sxs-lookup"><span data-stu-id="399fb-111">Available Templates</span></span>

<span data-ttu-id="399fb-112">Poniższe szablony są dostarczane przez zespół programu Entity Framework:</span><span class="sxs-lookup"><span data-stu-id="399fb-112">The following templates are provided by the Entity Framework team:</span></span>

### <a name="dbcontext-generator"></a><span data-ttu-id="399fb-113">DbContext Generator</span><span class="sxs-lookup"><span data-stu-id="399fb-113">DbContext Generator</span></span>

<span data-ttu-id="399fb-114">Ten szablon generuje prosty klas obiektów POCO i kontekstu, która pochodzi od typu DbContext przy użyciu platformy EF6.</span><span class="sxs-lookup"><span data-stu-id="399fb-114">This template will generate simple POCO entity classes and a context that derives from DbContext using EF6.</span></span>
<span data-ttu-id="399fb-115">To jest szablon zalecana, chyba że masz powód, aby użyć jednego z innych szablonów wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="399fb-115">This is the recommended template unless you have a reason to use one of the other templates listed below.</span></span>
<span data-ttu-id="399fb-116">Jest również szablon generowania kodu, Pobierz domyślnie, jeśli używane są nowe wersje programu Visual Studio (Visual Studio 2013 lub nowszy): po utworzeniu nowego modelu ten szablon jest używany domyślnie i pliki T4 (.tt) zostały zagnieżdżone w pliku edmx.</span><span class="sxs-lookup"><span data-stu-id="399fb-116">It is also the code generation template you get by default if you are using recent versions of Visual Studio (Visual Studio 2013 onwards): When you create a new model this template is used by default and the T4 files (.tt) are nested under your .edmx file.</span></span>

#### <a name="older-versions-of-visual-studio"></a><span data-ttu-id="399fb-117">Starsze wersje programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="399fb-117">Older versions of Visual Studio</span></span>
- <span data-ttu-id="399fb-118">**Program Visual Studio 2012:** można pobrać **EF 6.x DbContextGenerator** szablonów, musisz zainstalować najnowszą **Entity Framework Tools for Visual Studio** — zobacz [pobrać jednostki Framework](~/ef6/fundamentals/install.md) strony, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="399fb-118">**Visual Studio 2012:** To get the **EF 6.x DbContextGenerator** templates you will need to install the latest **Entity Framework Tools for Visual Studio** - see the [Get Entity Framework](~/ef6/fundamentals/install.md) page for more information.</span></span>
- <span data-ttu-id="399fb-119">**Program Visual Studio 2010:** **EF 6.x DbContextGenerator** szablony nie są dostępne dla programu Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="399fb-119">**Visual Studio 2010:** The **EF 6.x DbContextGenerator** templates are not available for Visual Studio 2010.</span></span>

#### <a name="dbcontext-generator-for-ef-5x"></a><span data-ttu-id="399fb-120">Generator DbContext dla platformy EF 5.x</span><span class="sxs-lookup"><span data-stu-id="399fb-120">DbContext Generator for EF 5.x</span></span>

<span data-ttu-id="399fb-121">Jeśli używasz starszej wersji pakietu EntityFramework NuGet (po jednej z wersji głównej 5) należy użyć **EF 5.x DbContext Generator** szablonu.</span><span class="sxs-lookup"><span data-stu-id="399fb-121">If you are using an older version of the EntityFramework NuGet package (one with a major version of 5) you will need to use the **EF 5.x DbContext Generator** template.</span></span>

<span data-ttu-id="399fb-122">Jeśli używasz programu Visual Studio 2013 lub 2012 ten szablon jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="399fb-122">If you are using Visual Studio 2013 or 2012 this template is already installed.</span></span>

<span data-ttu-id="399fb-123">Jeśli używasz programu Visual Studio 2010 będzie konieczne wybranie **Online** karcie podczas dodawania szablonu, aby go pobrać z galerii Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="399fb-123">If you are using Visual Studio 2010 you will need to select the **Online** tab when adding the template to download it from Visual Studio Gallery.</span></span> <span data-ttu-id="399fb-124">Alternatywnie można zainstalować szablonu bezpośrednio z galerii programu Visual Studio wcześniej.</span><span class="sxs-lookup"><span data-stu-id="399fb-124">Alternatively you can install the template directly from Visual Studio Gallery ahead of time.</span></span> <span data-ttu-id="399fb-125">Ponieważ szablony są wliczone w nowszych wersjach programu Visual Studio w wersji w galerii można zainstalować tylko w programie Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="399fb-125">Because the templates are included in later versions of Visual Studio the versions on the gallery can only be installed on Visual Studio 2010.</span></span>

- [<span data-ttu-id="399fb-126">EF 5.x DbContext Generator dla języka C#</span><span class="sxs-lookup"><span data-stu-id="399fb-126">EF 5.x DbContext Generator for C#</span></span>](http://visualstudiogallery.msdn.microsoft.com/da740968-02f9-42a9-9ee4-1a9a06d896a2)
- [<span data-ttu-id="399fb-127">EF 5.x DbContext Generator dla witryn sieci Web w języku C#</span><span class="sxs-lookup"><span data-stu-id="399fb-127">EF 5.x DbContext Generator for C# Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/5d01a981-91b8-492c-b42c-c771c3f31e03)
- [<span data-ttu-id="399fb-128">EF 5.x DbContext Generator VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-128">EF 5.x DbContext Generator for VB.NET</span></span>](http://visualstudiogallery.msdn.microsoft.com/875c882d-333e-455a-8dae-5353510527dd?src=featured)
- [<span data-ttu-id="399fb-129">EF 5.x DbContext Generator dla witryn sieci Web VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-129">EF 5.x DbContext Generator for VB.NET Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/d4d7d4cd-c2d0-43e6-8944-12f6ff8f2614)

#### <a name="dbcontext-generator-for-ef-4x"></a><span data-ttu-id="399fb-130">Generator DbContext dla platformy EF 4.x</span><span class="sxs-lookup"><span data-stu-id="399fb-130">DbContext Generator for EF 4.x</span></span>

<span data-ttu-id="399fb-131">Jeśli używasz starszej wersji pakietu EntityFramework NuGet (po jednym z głównych wersję 4) należy użyć **EF 4.x DbContext Generator** szablonu.</span><span class="sxs-lookup"><span data-stu-id="399fb-131">If you are using an older version of the EntityFramework NuGet package (one with a major version of 4) you will need to use the **EF 4.x DbContext Generator** template.</span></span> <span data-ttu-id="399fb-132">To można znaleźć w **Online** karcie podczas dodawania szablonu lub szablonu można zainstalować bezpośrednio z galerii programu Visual Studio wcześniej.</span><span class="sxs-lookup"><span data-stu-id="399fb-132">This can be found in the **Online** tab when adding the template, or you can install the template directly from Visual Studio Gallery ahead of time.</span></span>

- [<span data-ttu-id="399fb-133">EF 4.x DbContext Generator dla języka C#</span><span class="sxs-lookup"><span data-stu-id="399fb-133">EF 4.x DbContext Generator for C#</span></span>](http://visualstudiogallery.msdn.microsoft.com/7812b04c-db36-4817-8a84-e73c452410a2)
- [<span data-ttu-id="399fb-134">EF 4.x DbContext Generator dla witryn sieci Web w języku C#</span><span class="sxs-lookup"><span data-stu-id="399fb-134">EF 4.x DbContext Generator for C# Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/de0e9bc6-e86a-4448-8a2e-a1260a53203e)
- [<span data-ttu-id="399fb-135">EF 4.x DbContext Generator VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-135">EF 4.x DbContext Generator for VB.NET</span></span>](http://visualstudiogallery.msdn.microsoft.com/73679ae5-e358-4e76-a538-c7b5e04ac073)
- [<span data-ttu-id="399fb-136">EF 4.x DbContext Generator dla witryn sieci Web VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-136">EF 4.x DbContext Generator for VB.NET Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/86f5a660-306e-4831-840c-2e4ee7474a92)

### <a name="entityobject-generator"></a><span data-ttu-id="399fb-137">EntityObject Generator</span><span class="sxs-lookup"><span data-stu-id="399fb-137">EntityObject Generator</span></span>

<span data-ttu-id="399fb-138">Ten szablon spowoduje wygenerowanie klas jednostek, które wynikają z EntityObject i kontekstu, która pochodzi z obiektu ObjectContext.</span><span class="sxs-lookup"><span data-stu-id="399fb-138">This template will generate entity classes that derive from EntityObject and a context that derives from ObjectContext.</span></span>

> [!NOTE]
> <span data-ttu-id="399fb-139">Należy wziąć pod uwagę przy użyciu generatora DbContext</span><span class="sxs-lookup"><span data-stu-id="399fb-139">Consider using the DbContext Generator</span></span>

<span data-ttu-id="399fb-140">DbContext Generator jest teraz zalecane szablon dla nowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="399fb-140">The DbContext Generator is now the recommended template for new applications.</span></span> <span data-ttu-id="399fb-141">DbContext Generator wykorzystuje prostsze API DbContext.</span><span class="sxs-lookup"><span data-stu-id="399fb-141">The DbContext Generator takes advantage of the simpler DbContext API.</span></span> <span data-ttu-id="399fb-142">EntityObject Generator jest nadal dostępne do obsługi istniejących aplikacji.</span><span class="sxs-lookup"><span data-stu-id="399fb-142">The EntityObject Generator continues to be available to support existing applications.</span></span>

<span data-ttu-id="399fb-143">**Visual Studio 2010, 2012 &amp; 2013**</span><span class="sxs-lookup"><span data-stu-id="399fb-143">**Visual Studio 2010, 2012 &amp; 2013**</span></span>

<span data-ttu-id="399fb-144">Będzie konieczne wybranie **Online** karcie podczas dodawania szablonu, aby go pobrać z galerii Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="399fb-144">You will need to select the **Online** tab when adding the template to download it from Visual Studio Gallery.</span></span> <span data-ttu-id="399fb-145">Alternatywnie można zainstalować szablonu bezpośrednio z galerii programu Visual Studio wcześniej.</span><span class="sxs-lookup"><span data-stu-id="399fb-145">Alternatively you can install the template directly from Visual Studio Gallery ahead of time.</span></span>

- [<span data-ttu-id="399fb-146">EF 6.x EntityObject Generator dla języka C#</span><span class="sxs-lookup"><span data-stu-id="399fb-146">EF 6.x EntityObject Generator for C#</span></span>](http://visualstudiogallery.msdn.microsoft.com/66612113-549c-4a9e-a14a-f629ceb3f89a)
- [<span data-ttu-id="399fb-147">EF 6.x EntityObject Generator dla witryn sieci Web w języku C#</span><span class="sxs-lookup"><span data-stu-id="399fb-147">EF 6.x EntityObject Generator for C# Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/076140f3-6dbe-451f-a0e0-16b6d2bd8996)
- [<span data-ttu-id="399fb-148">EF 6.x EntityObject Generator VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-148">EF 6.x EntityObject Generator for VB.NET</span></span>](http://visualstudiogallery.msdn.microsoft.com/ff479d55-2c85-43c5-a4d6-21cd659435ea)
- [<span data-ttu-id="399fb-149">EF 6.x EntityObject Generator dla witryn sieci Web VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-149">EF 6.x EntityObject Generator for VB.NET Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/668e2b92-c142-4da2-8e60-866c6346fc6a)

<span data-ttu-id="399fb-150">**Generator EntityObject dla platformy EF 5.x**</span><span class="sxs-lookup"><span data-stu-id="399fb-150">**EntityObject Generator for EF 5.x**</span></span>


<span data-ttu-id="399fb-151">Jeśli używasz programu Visual Studio 2012 lub 2013 będzie konieczne wybranie **Online** karcie podczas dodawania szablonu, aby go pobrać z galerii Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="399fb-151">If you are using Visual Studio 2012 or 2013 you will need to select the **Online** tab when adding the template to download it from Visual Studio Gallery.</span></span> <span data-ttu-id="399fb-152">Alternatywnie można zainstalować szablonu bezpośrednio z galerii programu Visual Studio wcześniej.</span><span class="sxs-lookup"><span data-stu-id="399fb-152">Alternatively you can install the template directly from Visual Studio Gallery ahead of time.</span></span> <span data-ttu-id="399fb-153">Ponieważ szablony są wliczone w programie Visual Studio 2010 wersji w galerii można zainstalować tylko w programie Visual Studio 2012 &amp; 2013.</span><span class="sxs-lookup"><span data-stu-id="399fb-153">Because the templates are included in Visual Studio 2010 the versions on the gallery can only be installed on Visual Studio 2012 &amp; 2013.</span></span>

- [<span data-ttu-id="399fb-154">EF 5.x EntityObject Generator dla języka C#</span><span class="sxs-lookup"><span data-stu-id="399fb-154">EF 5.x EntityObject Generator for C#</span></span>](http://visualstudiogallery.msdn.microsoft.com/1da40393-b5ec-404a-a000-6a7e6e911339)
- [<span data-ttu-id="399fb-155">EF 5.x EntityObject Generator dla witryn sieci Web w języku C#</span><span class="sxs-lookup"><span data-stu-id="399fb-155">EF 5.x EntityObject Generator for C# Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/94b48556-fcf0-4b9b-8615-20f9066ae9ac)
- [<span data-ttu-id="399fb-156">EF 5.x EntityObject Generator VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-156">EF 5.x EntityObject Generator for VB.NET</span></span>](http://visualstudiogallery.msdn.microsoft.com/92c0129e-40dc-488c-a836-7e30846dfb30)
- [<span data-ttu-id="399fb-157">EF 5.x EntityObject Generator dla witryn sieci Web VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-157">EF 5.x EntityObject Generator for VB.NET Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/5dd7f75c-8c98-4eb7-b4bc-06f0d0b03b41)

<span data-ttu-id="399fb-158">Wystarczy ObjectContext generowania kodu bez konieczności edytowania szablonu możesz [powrócić do generowania kodu EntityObject](~/ef6/modeling/designer/codegen/legacy-objectcontext.md).</span><span class="sxs-lookup"><span data-stu-id="399fb-158">If you just want ObjectContext code generation without needing to edit the template you can [revert to EntityObject code generation](~/ef6/modeling/designer/codegen/legacy-objectcontext.md).</span></span>

<span data-ttu-id="399fb-159">Jeśli używasz programu Visual Studio 2010, ten szablon jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="399fb-159">If you are using Visual Studio 2010 this template is already installed.</span></span> <span data-ttu-id="399fb-160">Jeśli tworzysz nowy model w programie Visual Studio 2010, ten szablon jest używany przez domyślny, ale .tt, w których pliki nie są uwzględniane w projekcie.</span><span class="sxs-lookup"><span data-stu-id="399fb-160">If you create a new model in Visual Studio 2010 this template is used by default but the .tt files are not included in your project.</span></span> <span data-ttu-id="399fb-161">Jeśli chcesz dostosować szablon, należy dodać go do projektu.</span><span class="sxs-lookup"><span data-stu-id="399fb-161">If you want to customize the template you will need to add it to your project.</span></span>

### <a name="self-tracking-entities-ste-generator"></a><span data-ttu-id="399fb-162">Śledzenie własnym Generator jednostki (set)</span><span class="sxs-lookup"><span data-stu-id="399fb-162">Self-Tracking Entities (STE) Generator</span></span>

<span data-ttu-id="399fb-163">Ten szablon generuje klas jednostek Self-Tracking i kontekstu, która pochodzi z obiektu ObjectContext.</span><span class="sxs-lookup"><span data-stu-id="399fb-163">This template will generate Self-Tracking Entity classes and a context that derives from ObjectContext.</span></span> <span data-ttu-id="399fb-164">W aplikacji EF kontekst jest odpowiedzialny za śledzenie zmian w jednostkach.</span><span class="sxs-lookup"><span data-stu-id="399fb-164">In an EF application, a context is responsible for tracking changes in the entities.</span></span> <span data-ttu-id="399fb-165">Jednak w scenariuszach N-warstwowa kontekst może nie być dostępne w warstwie, która modyfikuje jednostki.</span><span class="sxs-lookup"><span data-stu-id="399fb-165">However, in N-Tier scenarios, the context might not be available on the tier that modifies the entities.</span></span> <span data-ttu-id="399fb-166">Jednostki własnym śledzenie pomóc śledzić zmiany w dowolnej warstwy.</span><span class="sxs-lookup"><span data-stu-id="399fb-166">Self-tracking entities help you track changes in any tier.</span></span> <span data-ttu-id="399fb-167">Aby uzyskać więcej informacji, zobacz [jednostek Self-Tracking](~/ef6/fundamentals/disconnected-entities/self-tracking-entities/index.md).</span><span class="sxs-lookup"><span data-stu-id="399fb-167">For more information, see [Self-Tracking Entities](~/ef6/fundamentals/disconnected-entities/self-tracking-entities/index.md).</span></span>

> [!NOTE]
> <span data-ttu-id="399fb-168">WKLEJ szablon niezalecane</span><span class="sxs-lookup"><span data-stu-id="399fb-168">STE Template Not Recommended</span></span>

<span data-ttu-id="399fb-169">Nie zalecamy już przy użyciu szablonu Wklej kod w nowej aplikacji, jej nadal będzie dostępna do obsługi istniejących aplikacji.</span><span class="sxs-lookup"><span data-stu-id="399fb-169">We no longer recommend using the STE template in new applications, it continues to be available to support existing applications.</span></span> <span data-ttu-id="399fb-170">Odwiedź stronę [artykułu odłączone jednostki](~/ef6/fundamentals/disconnected-entities/index.md) innych opcji, firma Microsoft zaleca w scenariuszach N-warstwowej.</span><span class="sxs-lookup"><span data-stu-id="399fb-170">Visit the [disconnected entities article](~/ef6/fundamentals/disconnected-entities/index.md) for other options we recommend for N-Tier scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="399fb-171">Dostępna jest wersja 6.x nie EF, Wklej kod szablonu.</span><span class="sxs-lookup"><span data-stu-id="399fb-171">There is no EF 6.x version of the STE template.</span></span>


> [!NOTE]
> <span data-ttu-id="399fb-172">Nie ma żadnych wersji programu Visual Studio 2013 szablonu Wklej kod.</span><span class="sxs-lookup"><span data-stu-id="399fb-172">There is no Visual Studio 2013 version of the STE template.</span></span>

### <a name="visual-studio-2012"></a><span data-ttu-id="399fb-173">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="399fb-173">Visual Studio 2012</span></span>

<span data-ttu-id="399fb-174">Jeśli używasz programu Visual Studio 2012 będzie konieczne wybranie **Online** karcie podczas dodawania szablonu, aby go pobrać z galerii Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="399fb-174">If you are using Visual Studio 2012 you will need to select the **Online** tab when adding the template to download it from Visual Studio Gallery.</span></span> <span data-ttu-id="399fb-175">Alternatywnie można zainstalować szablonu bezpośrednio z galerii programu Visual Studio wcześniej.</span><span class="sxs-lookup"><span data-stu-id="399fb-175">Alternatively you can install the template directly from Visual Studio Gallery ahead of time.</span></span> <span data-ttu-id="399fb-176">Ponieważ szablony są zawarte w Visual Studio 2010 w wersji w galerii można zainstalować tylko w programie Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="399fb-176">Because the templates are included in Visual Studio 2010 the versions on the gallery can only be installed on Visual Studio 2012.</span></span>

- [<span data-ttu-id="399fb-177">EF 5.x WKLEJ Generator dla języka C#</span><span class="sxs-lookup"><span data-stu-id="399fb-177">EF 5.x STE Generator for C#</span></span>](http://visualstudiogallery.msdn.microsoft.com/a3ac10a5-9365-4096-bb58-d9a1ba71db8f)
- [<span data-ttu-id="399fb-178">EF 5.x WKLEJ Generator dla witryn sieci Web w języku C#</span><span class="sxs-lookup"><span data-stu-id="399fb-178">EF 5.x STE Generator for C# Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/1b55ab82-eeb4-47ba-8d35-3c7c8b5f5a8c)
- [<span data-ttu-id="399fb-179">Generator WKLEJ 5.x EF VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-179">EF 5.x STE Generator for VB.NET</span></span>](http://visualstudiogallery.msdn.microsoft.com/1ba8c6a3-44e9-4e1f-b21e-596f3168474b)
- [<span data-ttu-id="399fb-180">EF 5.x WKLEJ Generator dla witryn sieci Web VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-180">EF 5.x STE Generator for VB.NET Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/a9fd5f0a-9af4-4e32-9c09-0e057072152e)

#### <a name="visual-studio-2010"></a><span data-ttu-id="399fb-181">Program Visual Studio 2010 **</span><span class="sxs-lookup"><span data-stu-id="399fb-181">Visual Studio 2010**</span></span>

<span data-ttu-id="399fb-182">Jeśli używasz programu Visual Studio 2010, ten szablon jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="399fb-182">If you are using Visual Studio 2010 this template is already installed.</span></span>

### <a name="poco-entity-generator"></a><span data-ttu-id="399fb-183">Obiektów POCO Generator jednostki</span><span class="sxs-lookup"><span data-stu-id="399fb-183">POCO Entity Generator</span></span>

<span data-ttu-id="399fb-184">Ten szablon generuje klas obiektów POCO i kontekstu, która pochodzi z obiektu ObjectContext</span><span class="sxs-lookup"><span data-stu-id="399fb-184">This template will generate POCO entity classes and a context that derives from ObjectContext</span></span>

> [!NOTE]
> <span data-ttu-id="399fb-185">Należy wziąć pod uwagę przy użyciu generatora DbContext</span><span class="sxs-lookup"><span data-stu-id="399fb-185">Consider using the DbContext Generator</span></span>

<span data-ttu-id="399fb-186">DbContext Generator jest teraz zalecane szablon Generowanie klas POCO w nowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="399fb-186">The DbContext Generator is now the recommended template for generating POCO classes in new applications.</span></span> <span data-ttu-id="399fb-187">DbContext Generator korzysta z nowego interfejsu API typu DbContext i może generować prostsze POCO klasy.</span><span class="sxs-lookup"><span data-stu-id="399fb-187">The DbContext Generator takes advantage of the new DbContext API and can generate simpler POCO classes.</span></span> <span data-ttu-id="399fb-188">Generator jednostki obiektów POCO jest nadal dostępne do obsługi istniejących aplikacji.</span><span class="sxs-lookup"><span data-stu-id="399fb-188">The POCO Entity Generator continues to be available to support existing applications.</span></span>

> [!NOTE]
> <span data-ttu-id="399fb-189">Nie ma żadnych EF 5.x i 6.x EF wersję szablonu Wklej kod.</span><span class="sxs-lookup"><span data-stu-id="399fb-189">There is no EF 5.x or EF 6.x version of the STE template.</span></span>

> [!NOTE]
> <span data-ttu-id="399fb-190">Nie ma żadnych wersji programu Visual Studio 2013 szablonu POCO.</span><span class="sxs-lookup"><span data-stu-id="399fb-190">There is no Visual Studio 2013 version of the POCO template.</span></span>

#### <a name="visual-studio-2012-amp-visual-studio-2010"></a><span data-ttu-id="399fb-191">Program Visual Studio 2012 &amp; programu Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="399fb-191">Visual Studio 2012 &amp; Visual Studio 2010</span></span>

<span data-ttu-id="399fb-192">Będzie konieczne wybranie **Online** karcie podczas dodawania szablonu, aby go pobrać z galerii Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="399fb-192">You will need to select the **Online** tab when adding the template to download it from Visual Studio Gallery.</span></span> <span data-ttu-id="399fb-193">Alternatywnie można zainstalować szablonu bezpośrednio z galerii programu Visual Studio wcześniej.</span><span class="sxs-lookup"><span data-stu-id="399fb-193">Alternatively you can install the template directly from Visual Studio Gallery ahead of time.</span></span>

- [<span data-ttu-id="399fb-194">EF 4.x POCO Generator dla języka C#</span><span class="sxs-lookup"><span data-stu-id="399fb-194">EF 4.x POCO Generator for C#</span></span>](http://visualstudiogallery.msdn.microsoft.com/23df0450-5677-4926-96cc-173d02752313)
- [<span data-ttu-id="399fb-195">EF 4.x POCO Generator dla witryn sieci Web w języku C#</span><span class="sxs-lookup"><span data-stu-id="399fb-195">EF 4.x POCO Generator for C# Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/fe568da5-aa1a-4178-a2a5-48813c707a7f)
- [<span data-ttu-id="399fb-196">EF 4.x POCO Generator VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-196">EF 4.x POCO Generator for VB.NET</span></span>](http://visualstudiogallery.msdn.microsoft.com/53ecbded-8936-4299-ab04-1e44e5489752)
- [<span data-ttu-id="399fb-197">EF 4.x POCO Generator dla witryn sieci Web VB.NET</span><span class="sxs-lookup"><span data-stu-id="399fb-197">EF 4.x POCO Generator for VB.NET Web Sites</span></span>](http://visualstudiogallery.msdn.microsoft.com/463c5aca-05ad-4cdb-910b-2e4f83269e34)

### <a name="what-are-the-web-sites-templates"></a><span data-ttu-id="399fb-198">Co to są szablony "Witryny sieci Web"</span><span class="sxs-lookup"><span data-stu-id="399fb-198">What are the "Web Sites" Templates</span></span>

<span data-ttu-id="399fb-199">Szablony "Witryny sieci Web" (czyli **EF 5.x Generator DbContext dla języka C\# witryn sieci Web**) są przeznaczone do użytku w projektów witryny sieci Web utworzone za pomocą **pliku —&gt; New -&gt; witryny sieci Web...** . Są one różne od aplikacji sieci Web utworzone za pomocą **pliku —&gt; New -&gt; projektu...** , które używają szablonów standardowych.</span><span class="sxs-lookup"><span data-stu-id="399fb-199">The "Web Sites" templates (i.e. **EF 5.x DbContext Generator for C\# Web Sites**) are for use in Web Site projects created via **File -&gt; New -&gt; Web Site...**. These are different from Web Applications, created via **File -&gt; New -&gt; Project...**, which use the standard templates.</span></span> <span data-ttu-id="399fb-200">Firma Microsoft oferuje osobnymi szablonami, ponieważ system szablonu elementu w programie Visual Studio wymaga, aby je.</span><span class="sxs-lookup"><span data-stu-id="399fb-200">We provide separate templates because the item template system in Visual Studio requires them.</span></span>

## <a name="using-a-template"></a><span data-ttu-id="399fb-201">Przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="399fb-201">Using a Template</span></span>

<span data-ttu-id="399fb-202">Aby rozpocząć korzystanie z szablonów generowania kodu, kliknij prawym przyciskiem myszy pusty miejscu na powierzchni projektowej, w Projektancie platformy EF i wybierz **Dodaj element generowanie kodu...** .</span><span class="sxs-lookup"><span data-stu-id="399fb-202">To start using a code generation template, right-click an empty spot on the design surface in the EF Designer and select **Add Code Generation Item...**.</span></span>

![Add_Code_Gen_Item](~/ef6/media/add-code-gen-item.png)

<span data-ttu-id="399fb-204">Jeśli masz już zainstalowaną szablonu chcesz użyć (lub został on uwzględniony w programie Visual Studio), a następnie będzie on dostępny w obszarze **kodu** lub **danych** sekcji w menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="399fb-204">If you've already installed the template you want to use (or it was included in Visual Studio), then it will be available under either the **Code** or **Data** section from the left menu.</span></span>

![Zainstalowany](~/ef6/media/installed.png)

<span data-ttu-id="399fb-206">Jeśli nie masz jeszcze szablonu zainstalowany, wybierz opcję **Online** z menu po lewej stronie i wyszukaj odpowiedni szablon.</span><span class="sxs-lookup"><span data-stu-id="399fb-206">If you don't already have the template installed, select **Online** from the left menu and search for the template you want.</span></span>

![Wyszukaj](~/ef6/media/search.png) 

<span data-ttu-id="399fb-208">Jeśli używasz programu Visual Studio 2012, nowe pliki .tt będzie można zagnieździć w file.\* edmx</span><span class="sxs-lookup"><span data-stu-id="399fb-208">If you are using Visual Studio 2012, the new .tt files will be nested under the .edmx file.\*</span></span>

> [!NOTE]
> <span data-ttu-id="399fb-209">W przypadku modeli utworzonych w programie Visual Studio 2012, musisz usunąć szablonów używanych dla domyślnego generowania kodu w przeciwnym razie otrzymasz klasy zduplikowane oraz wygenerowany kontekst.</span><span class="sxs-lookup"><span data-stu-id="399fb-209">For models created in Visual Studio 2012 you will need to delete the templates used for default code generation, otherwise you will have duplicate classes and context generated.</span></span> <span data-ttu-id="399fb-210">Domyślne pliki są  **&lt;nazwę modelu&gt;.tt** i  **&lt;nazwę modelu&gt;. context.tt**.</span><span class="sxs-lookup"><span data-stu-id="399fb-210">The default files are **&lt;model name&gt;.tt** and **&lt;model name&gt;.context.tt**.</span></span> 

![VS2012_Templates](~/ef6/media/vs2012-templates.png)

<span data-ttu-id="399fb-212">Jeśli używasz programu Visual Studio 2010 pliki tt są dodawane bezpośrednio do swojego projektu.</span><span class="sxs-lookup"><span data-stu-id="399fb-212">If you are using Visual Studio 2010, the tt files are added directly to your project.</span></span>  

![VS2010_Templates](~/ef6/media/vs2010-templates.png)