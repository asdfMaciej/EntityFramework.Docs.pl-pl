---
title: Pierwsze wstawienie kodu, aktualizowanie i usuwanie procedur składowanych - EF6
author: divega
ms.date: 2016-10-23
ms.prod: entity-framework
ms.author: divega
ms.manager: avickers
ms.technology: entity-framework-6
ms.topic: article
ms.assetid: 9a7ae7f9-4072-4843-877d-506dd7eef576
caps.latest.revision: 3
ms.openlocfilehash: bb27d416dcf931a29005160be7eae3806803b1b6
ms.sourcegitcommit: 390f3a37bc55105ed7cc5b0e0925b7f9c9e80ba6
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/09/2018
ms.locfileid: "37914119"
---
# <a name="code-first-insert-update-and-delete-stored-procedures"></a><span data-ttu-id="e9485-102">Pierwsze wstawienie kodu, aktualizowanie i usuwanie procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="e9485-102">Code First Insert, Update, and Delete Stored Procedures</span></span>
> [!NOTE]
> <span data-ttu-id="e9485-103">**EF6 począwszy tylko** — funkcje, interfejsów API itp. z opisem na tej stronie zostały wprowadzone w programie Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="e9485-103">**EF6 Onwards Only** - The features, APIs, etc. discussed in this page were introduced in Entity Framework 6.</span></span> <span data-ttu-id="e9485-104">Jeśli używasz starszej wersji, niektóre lub wszystkie informacje, nie ma zastosowania.</span><span class="sxs-lookup"><span data-stu-id="e9485-104">If you are using an earlier version, some or all of the information does not apply.</span></span>  

<span data-ttu-id="e9485-105">Domyślnie program Code First służy do konfigurowania wszystkich jednostek, aby wykonać Wstawianie, aktualizowanie i usuwanie poleceń przy użyciu bezpośredniego dostępu do tabel.</span><span class="sxs-lookup"><span data-stu-id="e9485-105">By default, Code First will configure all entities to perform insert, update and delete commands using direct table access.</span></span> <span data-ttu-id="e9485-106">Uruchamianie platformy EF6 można skonfigurować przez model Code First i używanie procedur składowanych w przypadku niektórych lub wszystkich jednostek w modelu.</span><span class="sxs-lookup"><span data-stu-id="e9485-106">Starting in EF6 you can configure your Code First model to use stored procedures for some or all entities in your model.</span></span>  

## <a name="basic-entity-mapping"></a><span data-ttu-id="e9485-107">Mapowania jednostki podstawowe</span><span class="sxs-lookup"><span data-stu-id="e9485-107">Basic Entity Mapping</span></span>  

<span data-ttu-id="e9485-108">Możesz zdecydować się na korzystanie z procedur składowanych do wstawiania, aktualizacji i usunąć za pomocą interfejsu API Fluent.</span><span class="sxs-lookup"><span data-stu-id="e9485-108">You can opt into using stored procedures for insert, update and delete using the Fluent API.</span></span>  

``` csharp
modelBuilder
  .Entity<Blog>()
  .MapToStoredProcedures();
```  

<span data-ttu-id="e9485-109">W ten sposób spowoduje, że Code First na potrzeby niektóre konwencje kompilacji oczekiwanego kształt procedur składowanych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="e9485-109">Doing this will cause Code First to use some conventions to build the expected shape of the stored procedures in the database.</span></span>  

- <span data-ttu-id="e9485-110">Trzy procedury składowane o nazwie  **\<type_name\>_Wstaw**,  **\<type_name\>_aktualizuj** i  **\<type_ Nazwa\>_Usuń** (np. Blog_Insert i Blog_Update Blog_Delete).</span><span class="sxs-lookup"><span data-stu-id="e9485-110">Three stored procedures named **\<type_name\>_Insert**, **\<type_name\>_Update** and **\<type_name\>_Delete** (e.g. Blog_Insert, Blog_Update and Blog_Delete).</span></span>  
- <span data-ttu-id="e9485-111">Nazwy parametrów odpowiadają nazwy właściwości.</span><span class="sxs-lookup"><span data-stu-id="e9485-111">Parameter names correspond to the property names.</span></span>  
    > [!NOTE]
> <span data-ttu-id="e9485-112">Jeśli używasz HasColumnName() lub atrybut kolumny można zmienić nazwy kolumny dla danej właściwości ta nazwa jest używana dla parametrów zamiast nazwy właściwości.</span><span class="sxs-lookup"><span data-stu-id="e9485-112">If you use HasColumnName() or the Column attribute to rename the column for a given property then this name is used for parameters instead of the property name.</span></span>  
- <span data-ttu-id="e9485-113">**Procedura składowana insert** będzie mieć parametr dla każdej właściwości, z wyjątkiem tych oznaczone jako wygenerowane (tożsamość lub obliczona).</span><span class="sxs-lookup"><span data-stu-id="e9485-113">**The insert stored procedure** will have a parameter for every property, except for those marked as store generated (identity or computed).</span></span> <span data-ttu-id="e9485-114">Procedura składowana powinien zwrócić zestawu wyników z kolumny dla każdej właściwości wygenerowane.</span><span class="sxs-lookup"><span data-stu-id="e9485-114">The stored procedure should return a result set with a column for each store generated property.</span></span>  
- <span data-ttu-id="e9485-115">**Procedura składowana aktualizacji** będzie mieć parametr dla każdej właściwości, z wyjątkiem tych oznaczone wzorzec wygenerowane "Obliczane".</span><span class="sxs-lookup"><span data-stu-id="e9485-115">**The update stored procedure** will have a parameter for every property, except for those marked with a store generated pattern of 'Computed'.</span></span> <span data-ttu-id="e9485-116">Niektóre tokeny współbieżności wymaga parametru dla oryginalnej wartości, zobacz *tokeny współbieżności* sekcji poniżej, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="e9485-116">Some concurrency tokens require a parameter for the original value, see the *Concurrency Tokens* section below for details.</span></span> <span data-ttu-id="e9485-117">Procedura składowana powinien zwrócić zestawu wyników z kolumny dla każdej właściwości obliczanej.</span><span class="sxs-lookup"><span data-stu-id="e9485-117">The stored procedure should return a result set with a column for each computed property.</span></span>  
- <span data-ttu-id="e9485-118">**Usuń procedurę składowaną** powinien mieć parametr wartość klucza jednostki (lub wiele parametrów, jeśli jednostka ma klucz złożony).</span><span class="sxs-lookup"><span data-stu-id="e9485-118">**The delete stored procedure** should have a parameter for the key value of the entity (or multiple parameters if the entity has a composite key).</span></span> <span data-ttu-id="e9485-119">Ponadto procedury usuwania powinny mieć również parametry żadnych kluczy obcych skojarzenia niezależnie od tabeli docelowej (relacje, które nie mają odpowiednich właściwości klucza obcego zadeklarowane w jednostce).</span><span class="sxs-lookup"><span data-stu-id="e9485-119">Additionally, the delete procedure should also have parameters for any independent association foreign keys on the target table (relationships that do not have corresponding foreign key properties declared in the entity).</span></span> <span data-ttu-id="e9485-120">Niektóre tokeny współbieżności wymaga parametru dla oryginalnej wartości, zobacz *tokeny współbieżności* sekcji poniżej, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="e9485-120">Some concurrency tokens require a parameter for the original value, see the *Concurrency Tokens* section below for details.</span></span>  

<span data-ttu-id="e9485-121">Na przykład, przy użyciu następującej klasy:</span><span class="sxs-lookup"><span data-stu-id="e9485-121">Using the following class as an example:</span></span>  

``` csharp
public class Blog  
{  
  public int BlogId { get; set; }  
  public string Name { get; set; }  
  public string Url { get; set; }  
}
```  

<span data-ttu-id="e9485-122">Wartość domyślna, który będzie procedur składowanych:</span><span class="sxs-lookup"><span data-stu-id="e9485-122">The default stored procedures would be:</span></span>  

``` SQL
CREATE PROCEDURE [dbo].[Blog_Insert]  
  @Name nvarchar(max),  
  @Url nvarchar(max)  
AS  
BEGIN
  INSERT INTO [dbo].[Blogs] ([Name], [Url])
  VALUES (@Name, @Url)

  SELECT SCOPE_IDENTITY() AS BlogId
END
CREATE PROCEDURE [dbo].[Blog_Update]  
  @BlogId int,  
  @Name nvarchar(max),  
  @Url nvarchar(max)  
AS  
  UPDATE [dbo].[Blogs]
  SET [Name] = @Name, [Url] = @Url     
  WHERE BlogId = @BlogId;
CREATE PROCEDURE [dbo].[Blog_Delete]  
  @BlogId int  
AS  
  DELETE FROM [dbo].[Blogs]
  WHERE BlogId = @BlogId
```  

### <a name="overriding-the-defaults"></a><span data-ttu-id="e9485-123">Zastępowanie ustawień domyślnych</span><span class="sxs-lookup"><span data-stu-id="e9485-123">Overriding the Defaults</span></span>  

<span data-ttu-id="e9485-124">Można zastąpić część lub całość co zostało skonfigurowane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e9485-124">You can override part or all of what was configured by default.</span></span>  

<span data-ttu-id="e9485-125">Można zmienić nazwę jednej lub kilku procedur składowanych.</span><span class="sxs-lookup"><span data-stu-id="e9485-125">You can change the name of one or more stored procedures.</span></span> <span data-ttu-id="e9485-126">Ten przykład zmienia nazwę procedury składowanej aktualizacji tylko.</span><span class="sxs-lookup"><span data-stu-id="e9485-126">This example renames the update stored procedure only.</span></span>  

``` csharp
modelBuilder  
  .Entity<Blog>()  
  .MapToStoredProcedures(s =>  
    s.Update(u => u.HasName("modify_blog")));
```  

<span data-ttu-id="e9485-127">Ten przykład zmienia nazwę wszystkich trzech procedur składowanych.</span><span class="sxs-lookup"><span data-stu-id="e9485-127">This example renames all three stored procedures.</span></span>  

``` csharp
modelBuilder  
  .Entity<Blog>()  
  .MapToStoredProcedures(s =>  
    s.Update(u => u.HasName("modify_blog"))  
     .Delete(d => d.HasName("delete_blog"))  
     .Insert(i => i.HasName("insert_blog")));
```  

<span data-ttu-id="e9485-128">W tych przykładach wywołania są ze sobą w sposób, ale możesz również użyć składni bloku lambda.</span><span class="sxs-lookup"><span data-stu-id="e9485-128">In these examples the calls are chained together, but you can also use lambda block syntax.</span></span>  

``` csharp
modelBuilder  
  .Entity<Blog>()  
  .MapToStoredProcedures(s =>  
    {  
      s.Update(u => u.HasName("modify_blog"));  
      s.Delete(d => d.HasName("delete_blog"));  
      s.Insert(i => i.HasName("insert_blog"));  
    });
```  

<span data-ttu-id="e9485-129">Ten przykład zmienia nazwę parametru dla właściwości BlogId na procedury składowanej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="e9485-129">This example renames the parameter for the BlogId property on the update stored procedure.</span></span>  

``` csharp
modelBuilder  
  .Entity<Blog>()  
  .MapToStoredProcedures(s =>  
    s.Update(u => u.Parameter(b => b.BlogId, "blog_id")));
```  

<span data-ttu-id="e9485-130">Te wywołania są wszystkie chainable i konfigurowalna.</span><span class="sxs-lookup"><span data-stu-id="e9485-130">These calls are all chainable and composable.</span></span> <span data-ttu-id="e9485-131">Oto przykład, który zmienia nazwę wszystkich trzech procedur przechowywanych i ich parametrów.</span><span class="sxs-lookup"><span data-stu-id="e9485-131">Here is an example that renames all three stored procedures and their parameters.</span></span>  

``` csharp
modelBuilder  
  .Entity<Blog>()  
  .MapToStoredProcedures(s =>  
    s.Update(u => u.HasName("modify_blog")  
                   .Parameter(b => b.BlogId, "blog_id")  
                   .Parameter(b => b.Name, "blog_name")  
                   .Parameter(b => b.Url, "blog_url"))  
     .Delete(d => d.HasName("delete_blog")  
                   .Parameter(b => b.BlogId, "blog_id"))  
     .Insert(i => i.HasName("insert_blog")  
                   .Parameter(b => b.Name, "blog_name")  
                   .Parameter(b => b.Url, "blog_url")));
```  

<span data-ttu-id="e9485-132">Można również zmienić nazwy kolumn w zestawie wyników, zawierającą wartości z bazy danych, wygenerowane.</span><span class="sxs-lookup"><span data-stu-id="e9485-132">You can also change the name of the columns in the result set that contains database generated values.</span></span>  

``` csharp
modelBuilder
  .Entity<Blog>()
  .MapToStoredProcedures(s =>
    s.Insert(i => i.Result(b => b.BlogId, "generated_blog_identity")));
```

``` SQL
CREATE PROCEDURE [dbo].[Blog_Insert]  
  @Name nvarchar(max),  
  @Url nvarchar(max)  
AS  
BEGIN
  INSERT INTO [dbo].[Blogs] ([Name], [Url])
  VALUES (@Name, @Url)

  SELECT SCOPE_IDENTITY() AS generated_blog_id
END
```  

## <a name="relationships-without-a-foreign-key-in-the-class-independent-associations"></a><span data-ttu-id="e9485-133">Relacje bez klucza obcego w klasie (niezależnie od skojarzeń)</span><span class="sxs-lookup"><span data-stu-id="e9485-133">Relationships Without a Foreign Key in the Class (Independent Associations)</span></span>  

<span data-ttu-id="e9485-134">Gdy właściwość klucza obcego jest uwzględniony w definicji klasy, odpowiedniego parametru można zmieniać nazwy w taki sam sposób jak inne właściwości.</span><span class="sxs-lookup"><span data-stu-id="e9485-134">When a foreign key property is included in the class definition, the corresponding parameter can be renamed in the same way as any other property.</span></span> <span data-ttu-id="e9485-135">Gdy istnieje relacja bez właściwości klucza obcego w klasie, domyślna nazwa parametru jest  **\<navigation_property_name\>_\<primary_key_name\>**.</span><span class="sxs-lookup"><span data-stu-id="e9485-135">When a relationship exists without a foreign key property in the class, the default parameter name is **\<navigation_property_name\>_\<primary_key_name\>**.</span></span>  

<span data-ttu-id="e9485-136">Na przykład następujące definicje klas spowodowałoby parametr Blog_BlogId jest oczekiwany w procedurach przechowywanych do wstawiania i aktualizowania wpisów.</span><span class="sxs-lookup"><span data-stu-id="e9485-136">For example, the following class definitions would result in a Blog_BlogId parameter being expected in the stored procedures to insert and update Posts.</span></span>  

``` csharp
public class Blog  
{  
  public int BlogId { get; set; }  
  public string Name { get; set; }  
  public string Url { get; set; }

  public List<Post> Posts { get; set; }  
}  

public class Post  
{  
  public int PostId { get; set; }  
  public string Title { get; set; }  
  public string Content { get; set; }  

  public Blog Blog { get; set; }  
}
```  

### <a name="overriding-the-defaults"></a><span data-ttu-id="e9485-137">Zastępowanie ustawień domyślnych</span><span class="sxs-lookup"><span data-stu-id="e9485-137">Overriding the Defaults</span></span>  

<span data-ttu-id="e9485-138">Możesz zmienić parametry dla kluczy obcych, które nie są uwzględnione w klasie, podając ścieżkę do właściwość klucza podstawowego do parametru metody.</span><span class="sxs-lookup"><span data-stu-id="e9485-138">You can change parameters for foreign keys that are not included in the class by supplying the path to the primary key property to the Parameter method.</span></span>  

``` csharp
modelBuilder
  .Entity<Post>()  
  .MapToStoredProcedures(s =>  
    s.Insert(i => i.Parameter(p => p.Blog.BlogId, "blog_id")));
```  

<span data-ttu-id="e9485-139">Jeśli nie masz właściwości nawigacji jednostki zależne (tj.)</span><span class="sxs-lookup"><span data-stu-id="e9485-139">If you don’t have a navigation property on the dependent entity (i.e</span></span> <span data-ttu-id="e9485-140">nie właściwości Post.Blog) możesz użyć metody skojarzenia, aby zidentyfikować drugiej stronie relacji, a następnie skonfigurować parametry, które odpowiadają każdej z właściwości kluczy.</span><span class="sxs-lookup"><span data-stu-id="e9485-140">no Post.Blog property) then you can use the Association method to identify the other end of the relationship and then configure the parameters that correspond to each of the key property(s).</span></span>  

``` csharp
modelBuilder
  .Entity<Post>()  
  .MapToStoredProcedures(s =>  
    s.Insert(i => i.Navigation<Blog>(  
      b => b.Posts,  
      c => c.Parameter(b => b.BlogId, "blog_id"))));
```  

## <a name="concurrency-tokens"></a><span data-ttu-id="e9485-141">Tokeny współbieżności</span><span class="sxs-lookup"><span data-stu-id="e9485-141">Concurrency Tokens</span></span>  

<span data-ttu-id="e9485-142">Aktualizowanie i usuwanie przechowywane procedury może być również konieczne przeciwdziałania współbieżności:</span><span class="sxs-lookup"><span data-stu-id="e9485-142">Update and delete stored procedures may also need to deal with concurrency:</span></span>  

- <span data-ttu-id="e9485-143">Jeśli jednostka zawiera tokeny współbieżności, procedury składowanej mogą opcjonalnie mieć parametr wyjściowy, która zwraca liczbę wierszy, zaktualizowane lub usunięte (wierszy).</span><span class="sxs-lookup"><span data-stu-id="e9485-143">If the entity contains concurrency tokens, the stored procedure can optionally have an output parameter that returns the number of rows updated/deleted (rows affected).</span></span> <span data-ttu-id="e9485-144">Taki parametr musi być skonfigurowany przy użyciu metody RowsAffectedParameter.</span><span class="sxs-lookup"><span data-stu-id="e9485-144">Such a parameter must be configured using the RowsAffectedParameter method.</span></span>  
<span data-ttu-id="e9485-145">Domyślnie EF używa wartość zwrotną z elementu ExecuteNonQuery, aby określić, ile wierszy została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="e9485-145">By default EF uses the return value from ExecuteNonQuery to determine how many rows were affected.</span></span> <span data-ttu-id="e9485-146">Określanie parametru wyjściowego odnośnych wierszy jest przydatne, jeśli po wykonaniu dowolnej logiki w swojej procedury sproc, które mogłyby spowodować wartość zwracaną ExecuteNonQuery jest niepoprawny (z perspektywy firmy EF) na końcu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="e9485-146">Specifying a rows affected output parameter is useful if you perform any logic in your sproc that would result in the return value of ExecuteNonQuery being incorrect (from EF's perspective) at the end of execution.</span></span>  
- <span data-ttu-id="e9485-147">Dla każdego współbieżności będzie token ma parametr o nazwie  **\<property_name\>_Original** (tj. Timestamp_Original).</span><span class="sxs-lookup"><span data-stu-id="e9485-147">For each concurrency token there will be a parameter named **\<property_name\>_Original** (i.e. Timestamp_Original).</span></span> <span data-ttu-id="e9485-148">To zostaną przekazane oryginalnej wartości tej właściwości – wartości po otrzymaniu kwerendy od bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e9485-148">This will be passed the original value of this property – the value when queried from the database.</span></span>  
    - <span data-ttu-id="e9485-149">Tokeny współbieżności, które są obliczane przez bazy danych — takich jak sygnatury czasowe — będzie miał tylko oryginalny parametru wartości.</span><span class="sxs-lookup"><span data-stu-id="e9485-149">Concurrency tokens that are computed by the database – such as timestamps – will only have an original value parameter.</span></span>  
    - <span data-ttu-id="e9485-150">Obliczane inne niż właściwości, które są ustawione jako tokeny współbieżności Ponadto będziesz mieć parametr nową wartość w ramach procedury aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="e9485-150">Non-computed properties that are set as concurrency tokens will also have a parameter for the new value in the update procedure.</span></span> <span data-ttu-id="e9485-151">Używa konwencji nazewnictwa już omówiono nowe wartości.</span><span class="sxs-lookup"><span data-stu-id="e9485-151">This uses the naming conventions already discussed for new values.</span></span> <span data-ttu-id="e9485-152">Przykładem takiego tokenu będzie przy użyciu adresu URL blogu jako tokenem współbieżności, nowa wartość jest wymagana, ponieważ to mogą być aktualizowane na nową wartość w kodzie (w przeciwieństwie do token sygnatury czasowej, które są aktualizowane tylko przez bazę danych).</span><span class="sxs-lookup"><span data-stu-id="e9485-152">An example of such a token would be using a Blog's URL as a concurrency token, the new value is required because this can be updated to a new value by your code (unlike a Timestamp token which is only updated by the database).</span></span>  

<span data-ttu-id="e9485-153">Jest to przykład klasy i aktualizować procedury składowanej z tokenem współbieżności sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="e9485-153">This is an example class and update stored procedure with a timestamp concurrency token.</span></span>  

``` csharp
public class Blog  
{  
  public int BlogId { get; set; }  
  public string Name { get; set; }  
  public string Url { get; set; }  
  [Timestamp]
  public byte[] Timestamp { get; set; }
}
```

``` SQL
CREATE PROCEDURE [dbo].[Blog_Update]  
  @BlogId int,  
  @Name nvarchar(max),  
  @Url nvarchar(max),
  @Timestamp_Original rowversion  
AS  
  UPDATE [dbo].[Blogs]
  SET [Name] = @Name, [Url] = @Url     
  WHERE BlogId = @BlogId AND [Timestamp] = @Timestamp_Original
```  

<span data-ttu-id="e9485-154">Oto przykład klasy i aktualizować procedury składowanej przy użyciu tokenu nieobliczaną współbieżności.</span><span class="sxs-lookup"><span data-stu-id="e9485-154">Here is an example class and update stored procedure with non-computed concurrency token.</span></span>  

``` csharp
public class Blog  
{  
  public int BlogId { get; set; }  
  public string Name { get; set; }  
  [ConcurrencyCheck]
  public string Url { get; set; }  
}
```

``` SQL
CREATE PROCEDURE [dbo].[Blog_Update]  
  @BlogId int,  
  @Name nvarchar(max),  
  @Url nvarchar(max),
  @Url_Original nvarchar(max),
AS  
  UPDATE [dbo].[Blogs]
  SET [Name] = @Name, [Url] = @Url     
  WHERE BlogId = @BlogId AND [Url] = @Url_Original
```  

### <a name="overriding-the-defaults"></a><span data-ttu-id="e9485-155">Zastępowanie ustawień domyślnych</span><span class="sxs-lookup"><span data-stu-id="e9485-155">Overriding the Defaults</span></span>  

<span data-ttu-id="e9485-156">Opcjonalnie możesz wprowadzić parametr odnośnych wierszy.</span><span class="sxs-lookup"><span data-stu-id="e9485-156">You can optionally introduce a rows affected parameter.</span></span>  

``` csharp
modelBuilder  
  .Entity<Blog>()  
  .MapToStoredProcedures(s =>  
    s.Update(u => u.RowsAffectedParameter("rows_affected")));
```  

<span data-ttu-id="e9485-157">Tokeny współbieżności bazy danych jest obliczana — gdzie oryginalną wartość jest przekazywana — po prostu umożliwia parametr standardowe, zmiana nazwy mechanizm Zmień nazwę parametru, aby uzyskać oryginalną wartość.</span><span class="sxs-lookup"><span data-stu-id="e9485-157">For database computed concurrency tokens – where only the original value is passed – you can just use the standard parameter renaming mechanism to rename the parameter for the original value.</span></span>  

``` csharp
modelBuilder  
  .Entity<Blog>()  
  .MapToStoredProcedures(s =>  
    s.Update(u => u.Parameter(b => b.Timestamp, "blog_timestamp")));
```  

<span data-ttu-id="e9485-158">Tokeny współbieżności nieobliczaną — gdzie zarówno oryginalne i nowe wartości są przekazywane — możesz użyć przeciążenia parametr, który pozwala podać nazwę dla każdego parametru.</span><span class="sxs-lookup"><span data-stu-id="e9485-158">For non-computed concurrency tokens – where both the original and new value are passed – you can use an overload of Parameter that allows you to supply a name for each parameter.</span></span>  

``` csharp
modelBuilder
 .Entity<Blog>()
 .MapToStoredProcedures(s => s.Update(u => u.Parameter(b => b.Url, "blog_url", "blog_original_url")));
```  

## <a name="many-to-many-relationships"></a><span data-ttu-id="e9485-159">Wiele do wielu relacji</span><span class="sxs-lookup"><span data-stu-id="e9485-159">Many to Many Relationships</span></span>  

<span data-ttu-id="e9485-160">Użyjemy następujących klas jako przykład w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e9485-160">We’ll use the following classes as an example in this section.</span></span>  

``` csharp
public class Post  
{  
  public int PostId { get; set; }  
  public string Title { get; set; }  
  public string Content { get; set; }  

  public List<Tag> Tags { get; set; }  
}  

public class Tag  
{  
  public int TagId { get; set; }  
  public string TagName { get; set; }  

  public List<Post> Posts { get; set; }  
}
```  

<span data-ttu-id="e9485-161">Wiele do wielu relacji można mapować do procedur składowanych z następującą składnią.</span><span class="sxs-lookup"><span data-stu-id="e9485-161">Many to many relationships can be mapped to stored procedures with the following syntax.</span></span>  

``` csharp
modelBuilder  
  .Entity<Post>()  
  .HasMany(p => p.Tags)  
  .WithMany(t => t.Posts)  
  .MapToStoredProcedures();
```  

<span data-ttu-id="e9485-162">Jeśli zostanie podana żadna inna konfiguracja domyślnie jest używany następujący kształt procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="e9485-162">If no other configuration is supplied then the following stored procedure shape is used by default.</span></span>  

- <span data-ttu-id="e9485-163">Dwie procedury składowane o nazwie  **\<type_one\>\<type_two\>_Wstaw** i  **\<type_one\>\<type_two \>_Usuń** (tj. PostTag_Insert i PostTag_Delete).</span><span class="sxs-lookup"><span data-stu-id="e9485-163">Two stored procedures named **\<type_one\>\<type_two\>_Insert** and **\<type_one\>\<type_two\>_Delete** (i.e. PostTag_Insert and PostTag_Delete).</span></span>  
- <span data-ttu-id="e9485-164">Parametry będą kluczowe wartości dla każdego typu.</span><span class="sxs-lookup"><span data-stu-id="e9485-164">The parameters will be the key value(s) for each type.</span></span> <span data-ttu-id="e9485-165">Nazwa każdego parametru jest **\<type_name\>_\<property_name\>** (tj. Post_PostId i Tag_TagId).</span><span class="sxs-lookup"><span data-stu-id="e9485-165">The name of each parameter being **\<type_name\>_\<property_name\>** (i.e. Post_PostId and Tag_TagId).</span></span>

<span data-ttu-id="e9485-166">Poniżej przedstawiono przykład wstawiania i aktualizowania procedur składowanych.</span><span class="sxs-lookup"><span data-stu-id="e9485-166">Here are example insert and update stored procedures.</span></span>  

``` SQL
CREATE PROCEDURE [dbo].[PostTag_Insert]  
  @Post_PostId int,  
  @Tag_TagId int  
AS  
  INSERT INTO [dbo].[Post_Tags] (Post_PostId, Tag_TagId)   
  VALUES (@Post_PostId, @Tag_TagId)
CREATE PROCEDURE [dbo].[PostTag_Delete]  
  @Post_PostId int,  
  @Tag_TagId int  
AS  
  DELETE FROM [dbo].[Post_Tags]    
  WHERE Post_PostId = @Post_PostId AND Tag_TagId = @Tag_TagId
```  

### <a name="overriding-the-defaults"></a><span data-ttu-id="e9485-167">Zastępowanie ustawień domyślnych</span><span class="sxs-lookup"><span data-stu-id="e9485-167">Overriding the Defaults</span></span>  

<span data-ttu-id="e9485-168">Nazwy procedury i parametr można skonfigurować w sposób podobny do jednostki przechowywanej procedur.</span><span class="sxs-lookup"><span data-stu-id="e9485-168">The procedure and parameter names can be configured in a similar way to entity stored procedures.</span></span>  

``` csharp
modelBuilder  
  .Entity<Post>()  
  .HasMany(p => p.Tags)  
  .WithMany(t => t.Posts)  
  .MapToStoredProcedures(s =>  
    s.Insert(i => i.HasName("add_post_tag")  
                   .LeftKeyParameter(p => p.PostId, "post_id")  
                   .RightKeyParameter(t => t.TagId, "tag_id"))  
     .Delete(d => d.HasName("remove_post_tag")  
                   .LeftKeyParameter(p => p.PostId, "post_id")  
                   .RightKeyParameter(t => t.TagId, "tag_id")));
```  