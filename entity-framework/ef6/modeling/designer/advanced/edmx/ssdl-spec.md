---
title: Specyfikacja SSDL - EF6
author: divega
ms.date: 2016-10-23
ms.prod: entity-framework
ms.author: divega
ms.manager: avickers
ms.technology: entity-framework-6
ms.topic: article
ms.assetid: a4af4b1a-40f4-48cc-b2e0-fa8f5d9d5419
caps.latest.revision: 3
ms.openlocfilehash: ac76d416d806e18b3acfabe746a7015191b3a9e1
ms.sourcegitcommit: f05e7b62584cf228f17390bb086a61d505712e1b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2018
ms.locfileid: "37912782"
---
# <a name="ssdl-specification"></a><span data-ttu-id="2ed73-102">Specyfikacja SSDL</span><span class="sxs-lookup"><span data-stu-id="2ed73-102">SSDL Specification</span></span>
<span data-ttu-id="2ed73-103">Język definicji schematu Store (SSDL) to oparty na standardzie XML język, który opisuje model magazynu w aplikacji Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2ed73-103">Store schema definition language (SSDL) is an XML-based language that describes the storage model of an Entity Framework application.</span></span>

<span data-ttu-id="2ed73-104">W aplikacji Entity Framework metadanych modelu magazynu jest ładowany z pliku ssdl (napisanego w SSDL) do wystąpienia System.Data.Metadata.Edm.StoreItemCollection i są dostępne za pomocą metody Klasa System.Data.Metadata.Edm.MetadataWorkspace.</span><span class="sxs-lookup"><span data-stu-id="2ed73-104">In an Entity Framework application, storage model metadata is loaded from a .ssdl file (written in SSDL) into an instance of the System.Data.Metadata.Edm.StoreItemCollection and is accessible by using methods in the System.Data.Metadata.Edm.MetadataWorkspace class.</span></span> <span data-ttu-id="2ed73-105">Entity Framework używa magazynu metadanych modelu do przekształcania zapytania względem modelu koncepcyjnego polecenia specyficzne dla magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-105">Entity Framework uses storage model metadata to translate queries against the conceptual model to store-specific commands.</span></span>

<span data-ttu-id="2ed73-106">Entity Framework Designer (Projektant EF) przechowuje informacje o modelu magazynu w pliku edmx w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="2ed73-106">The Entity Framework Designer (EF Designer) stores storage model information in an .edmx file at design time.</span></span> <span data-ttu-id="2ed73-107">W czasie kompilacji w Projektancie jednostki używa informacji w pliku edmx można utworzyć pliku ssdl, które są wymagane przez Entity Framework w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="2ed73-107">At build time the Entity Designer uses information in an .edmx file to create the .ssdl file that is needed by Entity Framework at runtime.</span></span>

<span data-ttu-id="2ed73-108">Wersje SSDL są zróżnicowane według przestrzeni nazw XML.</span><span class="sxs-lookup"><span data-stu-id="2ed73-108">Versions of SSDL are differentiated by XML namespaces.</span></span>

| <span data-ttu-id="2ed73-109">Wersja SSDL</span><span class="sxs-lookup"><span data-stu-id="2ed73-109">SSDL Version</span></span> | <span data-ttu-id="2ed73-110">Namespace XML</span><span class="sxs-lookup"><span data-stu-id="2ed73-110">XML Namespace</span></span>                                     |
|:-------------|:--------------------------------------------------|
| <span data-ttu-id="2ed73-111">SSDL v1</span><span class="sxs-lookup"><span data-stu-id="2ed73-111">SSDL v1</span></span>      | http://schemas.microsoft.com/ado/2006/04/edm/ssdl |
| <span data-ttu-id="2ed73-112">SSDL v2</span><span class="sxs-lookup"><span data-stu-id="2ed73-112">SSDL v2</span></span>      | http://schemas.microsoft.com/ado/2009/02/edm/ssdl |
| <span data-ttu-id="2ed73-113">SSDL v3</span><span class="sxs-lookup"><span data-stu-id="2ed73-113">SSDL v3</span></span>      | http://schemas.microsoft.com/ado/2009/11/edm/ssdl |

## <a name="association-element-ssdl"></a><span data-ttu-id="2ed73-114">Elementu Association (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-114">Association Element (SSDL)</span></span>

<span data-ttu-id="2ed73-115">**Skojarzenia** element język definicji schematu magazynu (SSDL) określa kolumny tabeli, które uczestniczą w ograniczenie klucza obcego w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-115">An **Association** element in store schema definition language (SSDL) specifies table columns that participate in a foreign key constraint in the underlying database.</span></span> <span data-ttu-id="2ed73-116">Dwa elementy End wymagany element podrzędny Określ tabele końców skojarzenie i liczebność na każdym końcu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-116">Two required child End elements specify tables at the ends of the association and the multiplicity at each end.</span></span> <span data-ttu-id="2ed73-117">Opcjonalny element ReferentialConstraint określa głównym i zależnym końcach asocjacji, a także kolumn uczestniczących w programie.</span><span class="sxs-lookup"><span data-stu-id="2ed73-117">An optional ReferentialConstraint element specifies the principal and dependent ends of the association as well as the participating columns.</span></span> <span data-ttu-id="2ed73-118">Jeśli nie **ReferentialConstraint** elementu, AssociationSetMapping element może służyć do określania mapowań kolumn dla skojarzenia.</span><span class="sxs-lookup"><span data-stu-id="2ed73-118">If no **ReferentialConstraint** element is present, an AssociationSetMapping element must be used to specify the column mappings for the association.</span></span>

<span data-ttu-id="2ed73-119">**Skojarzenia** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-119">The **Association** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-120">Dokumentacja (zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-120">Documentation (zero or one)</span></span>
-   <span data-ttu-id="2ed73-121">Końcowy (dokładnie dwa)</span><span class="sxs-lookup"><span data-stu-id="2ed73-121">End (exactly two)</span></span>
-   <span data-ttu-id="2ed73-122">ReferentialConstraint (zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-122">ReferentialConstraint (zero or one)</span></span>
-   <span data-ttu-id="2ed73-123">Elementów adnotacji (zero lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-123">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-124">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-124">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-125">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **skojarzenia** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-125">The following table describes the attributes that can be applied to the **Association** element.</span></span>

| <span data-ttu-id="2ed73-126">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-126">Attribute Name</span></span> | <span data-ttu-id="2ed73-127">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-127">Is Required</span></span> | <span data-ttu-id="2ed73-128">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-128">Value</span></span>                                                                            |
|:---------------|:------------|:---------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-129">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="2ed73-129">**Name**</span></span>       | <span data-ttu-id="2ed73-130">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-130">Yes</span></span>         | <span data-ttu-id="2ed73-131">Nazwa odpowiedniego ograniczenie klucza obcego w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-131">The name of the corresponding foreign key constraint in the underlying database.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-132">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **skojarzenia** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-132">Any number of annotation attributes (custom XML attributes) may be applied to the **Association** element.</span></span> <span data-ttu-id="2ed73-133">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-133">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-134">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-134">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-135">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-135">Example</span></span>

<span data-ttu-id="2ed73-136">W poniższym przykładzie przedstawiono **skojarzenia** element, który używa **ReferentialConstraint** elementu, aby określić kolumny, które uczestniczą w **klucza Obcego\_CustomerOrders**  ograniczenie klucza obcego:</span><span class="sxs-lookup"><span data-stu-id="2ed73-136">The following example shows an **Association** element that uses a **ReferentialConstraint** element to specify the columns that participate in the **FK\_CustomerOrders** foreign key constraint:</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```
 

 

## <a name="associationset-element-ssdl"></a><span data-ttu-id="2ed73-137">Obiekt AssociationSet — Element (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-137">AssociationSet Element (SSDL)</span></span>

<span data-ttu-id="2ed73-138">**AssociationSet** element język definicji schematu magazynu (SSDL) reprezentuje ograniczenie klucza obcego między dwiema tabelami w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-138">The **AssociationSet** element in store schema definition language (SSDL) represents a foreign key constraint between two tables in the underlying database.</span></span> <span data-ttu-id="2ed73-139">Kolumny tabeli, które uczestniczą w ograniczenie klucza obcego są określone w elemencie Association.</span><span class="sxs-lookup"><span data-stu-id="2ed73-139">The table columns that participate in the foreign key constraint are specified in an Association element.</span></span> <span data-ttu-id="2ed73-140">**Skojarzenia** element, który odpowiada danej **AssociationSet** element jest określony w **skojarzenia** atrybutu **AssociationSet**  elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-140">The **Association** element that corresponds to a given **AssociationSet** element is specified in the **Association** attribute of the **AssociationSet** element.</span></span>

<span data-ttu-id="2ed73-141">SSDL zestawów skojarzeń są mapowane do zestawów skojarzeń CSDL przez AssociationSetMapping element.</span><span class="sxs-lookup"><span data-stu-id="2ed73-141">SSDL association sets are mapped to CSDL association sets by an AssociationSetMapping element.</span></span> <span data-ttu-id="2ed73-142">Jednak jeśli zestawu skojarzeń CSDL dla danego skojarzenia CSDL jest zdefiniowana za pomocą elementu ReferentialConstraint bez odpowiedniej **AssociationSetMapping** elementu jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="2ed73-142">However, if the CSDL association for a given CSDL association set is defined by using a ReferentialConstraint element , no corresponding **AssociationSetMapping** element is necessary.</span></span> <span data-ttu-id="2ed73-143">W takim przypadku **AssociationSetMapping** elementu, zostanie ona zastąpiona mapowania definiuje **ReferentialConstraint** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-143">In this case, if an **AssociationSetMapping** element is present, the mappings it defines will be overridden by the **ReferentialConstraint** element.</span></span>

<span data-ttu-id="2ed73-144">**AssociationSet** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-144">The **AssociationSet** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-145">Dokumentacja (zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-145">Documentation (zero or one)</span></span>
-   <span data-ttu-id="2ed73-146">END (zero lub dwóch)</span><span class="sxs-lookup"><span data-stu-id="2ed73-146">End (zero or two)</span></span>
-   <span data-ttu-id="2ed73-147">Elementów adnotacji (zero lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-147">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-148">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-148">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-149">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **AssociationSet** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-149">The following table describes the attributes that can be applied to the **AssociationSet** element.</span></span>

| <span data-ttu-id="2ed73-150">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-150">Attribute Name</span></span>  | <span data-ttu-id="2ed73-151">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-151">Is Required</span></span> | <span data-ttu-id="2ed73-152">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-152">Value</span></span>                                                                                                |
|:----------------|:------------|:-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-153">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="2ed73-153">**Name**</span></span>        | <span data-ttu-id="2ed73-154">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-154">Yes</span></span>         | <span data-ttu-id="2ed73-155">Nazwa ograniczenia klucza obcego, że skojarzenie ustawione reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="2ed73-155">The name of the foreign key constraint that the association set represents.</span></span>                          |
| <span data-ttu-id="2ed73-156">**Skojarzenie**</span><span class="sxs-lookup"><span data-stu-id="2ed73-156">**Association**</span></span> | <span data-ttu-id="2ed73-157">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-157">Yes</span></span>         | <span data-ttu-id="2ed73-158">Nazwa skojarzenia, który definiuje kolumny, które uczestniczą w ograniczenie klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-158">The name of the association that defines the columns that participate in the foreign key constraint.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-159">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **AssociationSet** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-159">Any number of annotation attributes (custom XML attributes) may be applied to the **AssociationSet** element.</span></span> <span data-ttu-id="2ed73-160">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-160">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-161">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-161">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-162">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-162">Example</span></span>

<span data-ttu-id="2ed73-163">W poniższym przykładzie przedstawiono **AssociationSet** elementu, który reprezentuje `FK_CustomerOrders` ograniczenie klucza obcego w bazie danych:</span><span class="sxs-lookup"><span data-stu-id="2ed73-163">The following example shows an **AssociationSet** element that represents the `FK_CustomerOrders` foreign key constraint in the underlying database:</span></span>

``` xml
 <AssociationSet Name="FK_CustomerOrders"
                 Association="ExampleModel.Store.FK_CustomerOrders">
   <End Role="Customers" EntitySet="Customers" />
   <End Role="Orders" EntitySet="Orders" />
 </AssociationSet>
```
 

 

## <a name="collectiontype-element-ssdl"></a><span data-ttu-id="2ed73-164">Element CollectionType (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-164">CollectionType Element (SSDL)</span></span>

<span data-ttu-id="2ed73-165">**CollectionType** element język definicji schematu magazynu (SSDL) określa, że typ zwracany przez funkcję jest kolekcją.</span><span class="sxs-lookup"><span data-stu-id="2ed73-165">The **CollectionType** element in store schema definition language (SSDL) specifies that a function’s return type is a collection.</span></span> <span data-ttu-id="2ed73-166">**CollectionType** element jest elementem podrzędnym elementu ReturnType.</span><span class="sxs-lookup"><span data-stu-id="2ed73-166">The **CollectionType** element is a child of the ReturnType element.</span></span> <span data-ttu-id="2ed73-167">Typ kolekcji jest określony za pomocą elementu podrzędnego RowType:</span><span class="sxs-lookup"><span data-stu-id="2ed73-167">The type of collection is specified by using the RowType child element:</span></span>

> [!NOTE]
> <span data-ttu-id="2ed73-168">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **CollectionType** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-168">Any number of annotation attributes (custom XML attributes) may be applied to the **CollectionType** element.</span></span> <span data-ttu-id="2ed73-169">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-169">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-170">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-170">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-171">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-171">Example</span></span>

<span data-ttu-id="2ed73-172">W poniższym przykładzie pokazano funkcję, która używa **CollectionType** elementu, aby określić, że funkcja zwraca Kolekcja wierszy.</span><span class="sxs-lookup"><span data-stu-id="2ed73-172">The following example shows a function that uses a **CollectionType** element to specify that the function returns a collection of rows.</span></span>

``` xml
   <Function Name="GetProducts" IsComposable="true" Schema="dbo">
     <ReturnType>
       <CollectionType>
         <RowType>
           <Property Name="ProductID" Type="int" Nullable="false" />
           <Property Name="CategoryID" Type="bigint" Nullable="false" />
           <Property Name="ProductName" Type="nvarchar" MaxLength="40" Nullable="false" />
           <Property Name="UnitPrice" Type="money" />
           <Property Name="Discontinued" Type="bit" />
         </RowType>
       </CollectionType>
     </ReturnType>
   </Function>
```
 

 

## <a name="commandtext-element-ssdl"></a><span data-ttu-id="2ed73-173">Element CommandText (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-173">CommandText Element (SSDL)</span></span>

<span data-ttu-id="2ed73-174">**CommandText** element w język definicji schematu magazynu (SSDL) jest elementem podrzędnym elementu funkcji, która pozwala na zdefiniowanie instrukcji SQL, który jest wykonywany w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-174">The **CommandText** element in store schema definition language (SSDL) is a child of the Function element that allows you to define a SQL statement that is executed at the database.</span></span> <span data-ttu-id="2ed73-175">**CommandText** elementu pozwala na dodawanie funkcji, która jest podobna do procedury składowanej w bazie danych, ale należy zdefiniować **CommandText** elementu w modelu magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-175">The **CommandText** element allows you to add functionality that is similar to a stored procedure in the database, but you define the **CommandText** element in the storage model.</span></span>

<span data-ttu-id="2ed73-176">**CommandText** elementu nie może mieć elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-176">The **CommandText** element cannot have child elements.</span></span> <span data-ttu-id="2ed73-177">Treść **CommandText** element musi być prawidłową instrukcję SQL do podstawowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-177">The body of the **CommandText** element must be a valid SQL statement for the underlying database.</span></span>

<span data-ttu-id="2ed73-178">Atrybuty nie są stosowane do **CommandText** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-178">No attributes are applicable to the **CommandText** element.</span></span>

### <a name="example"></a><span data-ttu-id="2ed73-179">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-179">Example</span></span>

<span data-ttu-id="2ed73-180">W poniższym przykładzie przedstawiono **funkcja** element z element podrzędny **CommandText** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-180">The following example shows a **Function** element with a child **CommandText** element.</span></span> <span data-ttu-id="2ed73-181">Udostępnianie **UpdateProductInOrder** działać jako metodę dla obiektu ObjectContext importując go do modelu koncepcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-181">Expose the **UpdateProductInOrder** function as a method on the ObjectContext by importing it into the conceptual model.</span></span>  

``` xml
 <Function Name="UpdateProductInOrder" IsComposable="false">
   <CommandText>
     UPDATE Orders
     SET ProductId = @productId
     WHERE OrderId = @orderId;
   </CommandText>
   <Parameter Name="productId"
              Mode="In"
              Type="int"/>
   <Parameter Name="orderId"
              Mode="In"
              Type="int"/>
 </Function>
```
 

 

## <a name="definingquery-element-ssdl"></a><span data-ttu-id="2ed73-182">Element DefiningQuery (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-182">DefiningQuery Element (SSDL)</span></span>

 <span data-ttu-id="2ed73-183">**DefiningQuery** element język definicji schematu magazynu (SSDL) pozwala na wykonanie instrukcji SQL bezpośrednio w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-183">The **DefiningQuery** element in store schema definition language (SSDL) allows you to execute a SQL statement directly in the underlying database.</span></span> <span data-ttu-id="2ed73-184">**DefiningQuery** element jest najczęściej używany jak widok bazy danych, ale widok jest zdefiniowany w modelu pamięci masowej zamiast bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-184">The **DefiningQuery** element is commonly used like a database view, but the view is defined in the storage model instead of the database.</span></span> <span data-ttu-id="2ed73-185">Widok zdefiniowany w **DefiningQuery** elementu mogą być mapowane na typ jednostki w modelu koncepcyjnym za pośrednictwem elementu obiekcie EntitySetMapping.</span><span class="sxs-lookup"><span data-stu-id="2ed73-185">The view defined in a **DefiningQuery** element can be mapped to an entity type in the conceptual model through an EntitySetMapping element.</span></span> <span data-ttu-id="2ed73-186">Te mapowania są przeznaczone tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-186">These mappings are read-only.</span></span>  

<span data-ttu-id="2ed73-187">Poniższa składnia SSDL pokazuje deklaracji **EntitySet** następuje **DefiningQuery** element, który zawiera zapytanie służy do pobierania tego widoku.</span><span class="sxs-lookup"><span data-stu-id="2ed73-187">The following SSDL syntax shows the declaration of an **EntitySet** followed by the **DefiningQuery** element that contains a query used to retrieve the view.</span></span>

``` xml
 <Schema>
     <EntitySet Name="Tables" EntityType="Self.STable">
         <DefiningQuery>
           SELECT  TABLE_CATALOG,
                   'test' as TABLE_SCHEMA,
                   TABLE_NAME
           FROM    INFORMATION_SCHEMA.TABLES
         </DefiningQuery>
     </EntitySet>
 </Schema>
```
 

<span data-ttu-id="2ed73-188">Aby włączyć scenariuszach odczytu i zapisu za pośrednictwem widoków, można użyć procedur składowanych platformy Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2ed73-188">You can use stored procedures in the Entity Framework to enable read-write scenarios over views.</span></span> <span data-ttu-id="2ed73-189">Widok źródła danych lub widoku SQL jednostki można użyć jako tabeli podstawowej dla pobierania danych i przetwarzania przez procedury składowane zmiany.</span><span class="sxs-lookup"><span data-stu-id="2ed73-189">You can use either a data source view or an Entity SQL view as the base table for retrieving data and for change processing by stored procedures.</span></span>

<span data-ttu-id="2ed73-190">Możesz użyć **DefiningQuery** elementu docelowego programu Microsoft SQL Server Compact 3.5.</span><span class="sxs-lookup"><span data-stu-id="2ed73-190">You can use the **DefiningQuery** element to target Microsoft SQL Server Compact 3.5.</span></span> <span data-ttu-id="2ed73-191">Chociaż program SQL Server Compact 3.5 nie obsługuje procedur przechowywanych, można zaimplementować podobne funkcje za pomocą **DefiningQuery** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-191">Though SQL Server Compact 3.5 does not support stored procedures, you can implement similar functionality with the **DefiningQuery** element.</span></span> <span data-ttu-id="2ed73-192">Jest innym miejscu, gdzie mogą być przydatne podczas tworzenia procedur składowanych do pokonania niezgodność typów danych, używany w języku programowania i te źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-192">Another place where it can be useful is in creating stored procedures to overcome a mismatch between the data types used in the programming language and those of the data source.</span></span> <span data-ttu-id="2ed73-193">Można napisać **DefiningQuery** które pobiera zestaw parametrów, a następnie wywołuje procedurę składowaną z innym zestawem parametrów, na przykład procedury przechowywanej, która powoduje usunięcie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-193">You could write a **DefiningQuery** that takes a certain set of parameters and then calls a stored procedure with a different set of parameters, for example, a stored procedure that deletes data.</span></span>

 

## <a name="dependent-element-ssdl"></a><span data-ttu-id="2ed73-194">Element zależne (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-194">Dependent Element (SSDL)</span></span>

<span data-ttu-id="2ed73-195">**Zależne** element język definicji schematu magazynu (SSDL) jest element podrzędny do elementu ReferentialConstraint, który definiuje zależne koniec ograniczenie klucza obcego (nazywany także ograniczenie referencyjne).</span><span class="sxs-lookup"><span data-stu-id="2ed73-195">The **Dependent** element in store schema definition language (SSDL) is a child element to the ReferentialConstraint element that defines the dependent end of a foreign key constraint (also called a referential constraint).</span></span> <span data-ttu-id="2ed73-196">**Zależne** element określa kolumny (lub kolumny) w tabeli, która będzie odwoływać się do kolumny klucza podstawowego (lub kolumny).</span><span class="sxs-lookup"><span data-stu-id="2ed73-196">The **Dependent** element specifies the column (or columns) in a table that reference a primary key column (or columns).</span></span> <span data-ttu-id="2ed73-197">**PropertyRef** elementy Określ kolumny, które są wywoływane.</span><span class="sxs-lookup"><span data-stu-id="2ed73-197">**PropertyRef** elements specify which columns are referenced.</span></span> <span data-ttu-id="2ed73-198">Główny element określa kolumny klucza podstawowego, które są przywoływane przez kolumn, które są określone w **zależne** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-198">The Principal element specifies the primary key columns that are referenced by columns that are specified in the **Dependent** element.</span></span>

<span data-ttu-id="2ed73-199">**Zależne** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-199">The **Dependent** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-200">PropertyRef (jeden lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-200">PropertyRef (one or more)</span></span>
-   <span data-ttu-id="2ed73-201">Elementów adnotacji (zero lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-201">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-202">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-202">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-203">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **zależne** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-203">The following table describes the attributes that can be applied to the **Dependent** element.</span></span>

| <span data-ttu-id="2ed73-204">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-204">Attribute Name</span></span> | <span data-ttu-id="2ed73-205">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-205">Is Required</span></span> | <span data-ttu-id="2ed73-206">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-206">Value</span></span>                                                                                                                                                       |
|:---------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-207">**Rola**</span><span class="sxs-lookup"><span data-stu-id="2ed73-207">**Role**</span></span>       | <span data-ttu-id="2ed73-208">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-208">Yes</span></span>         | <span data-ttu-id="2ed73-209">Taką samą wartość jak **roli** atrybut odpowiedni element End (jeśli jest używana); w przeciwnym razie nazwę tabeli, która zawiera kolumna źródłowa odwołania.</span><span class="sxs-lookup"><span data-stu-id="2ed73-209">The same value as the **Role** attribute (if used) of the corresponding End element; otherwise, the name of the table that contains the referencing column.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-210">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **zależne** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-210">Any number of annotation attributes (custom XML attributes) may be applied to the **Dependent** element.</span></span> <span data-ttu-id="2ed73-211">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla CSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-211">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="2ed73-212">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-212">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-213">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-213">Example</span></span>

<span data-ttu-id="2ed73-214">W poniższym przykładzie pokazano element Association używający **ReferentialConstraint** elementu, aby określić kolumny, które uczestniczą w **klucza Obcego\_CustomerOrders** klucza obcego ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="2ed73-214">The following example shows an Association element that uses a **ReferentialConstraint** element to specify the columns that participate in the **FK\_CustomerOrders** foreign key constraint.</span></span> <span data-ttu-id="2ed73-215">**Zależne** element Określa **CustomerId** kolumny **kolejności** tabeli jako zależne koniec tego ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="2ed73-215">The **Dependent** element specifies the **CustomerId** column of the **Order** table as the dependent end of the constraint.</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```
 

 

## <a name="documentation-element-ssdl"></a><span data-ttu-id="2ed73-216">Element documentation (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-216">Documentation Element (SSDL)</span></span>

<span data-ttu-id="2ed73-217">**Dokumentacji** element język definicji schematu magazynu (SSDL) może służyć do Podaj informacje dotyczące obiektu, który jest zdefiniowany w elemencie rodzica.</span><span class="sxs-lookup"><span data-stu-id="2ed73-217">The **Documentation** element in store schema definition language (SSDL) can be used to provide information about an object that is defined in a parent element.</span></span>

<span data-ttu-id="2ed73-218">**Dokumentacji** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-218">The **Documentation** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-219">**Podsumowanie**: Krótki opis elementu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-219">**Summary**: A brief description of the parent element.</span></span> <span data-ttu-id="2ed73-220">(element zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-220">(zero or one element)</span></span>
-   <span data-ttu-id="2ed73-221">**LongDescription**: rozbudowany opis elementu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-221">**LongDescription**: An extensive description of the parent element.</span></span> <span data-ttu-id="2ed73-222">(element zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-222">(zero or one element)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-223">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-223">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-224">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **dokumentacji** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-224">Any number of annotation attributes (custom XML attributes) may be applied to the **Documentation** element.</span></span> <span data-ttu-id="2ed73-225">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla CSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-225">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="2ed73-226">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-226">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="2ed73-227">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-227">Example</span></span>

<span data-ttu-id="2ed73-228">W poniższym przykładzie przedstawiono **dokumentacji** element jako element podrzędny elementu EntityType.</span><span class="sxs-lookup"><span data-stu-id="2ed73-228">The following example shows the **Documentation** element as a child element of an EntityType element.</span></span>

``` xml
 <EntityType Name="Customers">
   <Documentation>
     <Summary>Summary here.</Summary>
     <LongDescription>Long description here.</LongDescription>
   </Documentation>
   <Key>
     <PropertyRef Name="CustomerId" />
   </Key>
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
 </EntityType>
```
 

 

## <a name="end-element-ssdl"></a><span data-ttu-id="2ed73-229">Element end (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-229">End Element (SSDL)</span></span>

<span data-ttu-id="2ed73-230">**Zakończenia** element język definicji schematu magazynu (SSDL) Określa tabelę i liczba wierszy na jednym końcu ograniczenie klucza obcego w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-230">The **End** element in store schema definition language (SSDL) specifies the table and number of rows at one end of a foreign key constraint in the underlying database.</span></span> <span data-ttu-id="2ed73-231">**Zakończenia** element może być elementem podrzędnym elementu Association lub elementu AssociationSet.</span><span class="sxs-lookup"><span data-stu-id="2ed73-231">The **End** element can be a child of the Association element or the AssociationSet element.</span></span> <span data-ttu-id="2ed73-232">W każdym przypadku możliwe podrzędnych elementów i atrybuty stosowane są różne.</span><span class="sxs-lookup"><span data-stu-id="2ed73-232">In each case, the possible child elements and applicable attributes are different.</span></span>

### <a name="end-element-as-a-child-of-the-association-element"></a><span data-ttu-id="2ed73-233">Końcowy Element jako element podrzędny elementu Association</span><span class="sxs-lookup"><span data-stu-id="2ed73-233">End Element as a Child of the Association Element</span></span>

<span data-ttu-id="2ed73-234">**Zakończenia** — element (jako element podrzędny elementu **skojarzenia** elementu) Określa tabelę i liczba wierszy na końcu ograniczenie klucza obcego z **typu** i **Liczebność** odpowiednio atrybutów.</span><span class="sxs-lookup"><span data-stu-id="2ed73-234">An **End** element (as a child of the **Association** element) specifies the table and number of rows at the end of a foreign key constraint with the **Type** and **Multiplicity** attributes respectively.</span></span> <span data-ttu-id="2ed73-235">Koniec ograniczenie klucza obcego są zdefiniowane jako część skojarzenia SSDL; skojarzenie SSDL musi mieć dokładnie punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-235">Ends of a foreign key constraint are defined as part of an SSDL association; an SSDL association must have exactly two ends.</span></span>

<span data-ttu-id="2ed73-236">**Zakończenia** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-236">An **End** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-237">Dokumentacja (zero lub jeden element)</span><span class="sxs-lookup"><span data-stu-id="2ed73-237">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="2ed73-238">OnDelete (zero lub jeden element)</span><span class="sxs-lookup"><span data-stu-id="2ed73-238">OnDelete (zero or one element)</span></span>
-   <span data-ttu-id="2ed73-239">Elementów adnotacji (zero lub więcej elementów)</span><span class="sxs-lookup"><span data-stu-id="2ed73-239">Annotation elements (zero or more elements)</span></span>

#### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-240">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-240">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-241">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **zakończenia** elementu, gdy jest elementem podrzędnym elementu **skojarzenia** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-241">The following table describes the attributes that can be applied to the **End** element when it is the child of an **Association** element.</span></span>

| <span data-ttu-id="2ed73-242">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-242">Attribute Name</span></span>   | <span data-ttu-id="2ed73-243">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-243">Is Required</span></span> | <span data-ttu-id="2ed73-244">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-244">Value</span></span>                                                                                                                                                                                                                                                                                                                                                                                      |
|:-----------------|:------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-245">**Typ**</span><span class="sxs-lookup"><span data-stu-id="2ed73-245">**Type**</span></span>         | <span data-ttu-id="2ed73-246">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-246">Yes</span></span>         | <span data-ttu-id="2ed73-247">W pełni kwalifikowana nazwa zestawu jednostek SSDL, który znajduje się na końcu ograniczenie klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-247">The fully qualified name of the SSDL entity set that is at the end of the foreign key constraint.</span></span>                                                                                                                                                                                                                                                                                          |
| <span data-ttu-id="2ed73-248">**Rola**</span><span class="sxs-lookup"><span data-stu-id="2ed73-248">**Role**</span></span>         | <span data-ttu-id="2ed73-249">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-249">No</span></span>          | <span data-ttu-id="2ed73-250">Wartość **roli** atrybutu w elemencie jednostki albo zależnych od odpowiadającego im elementu ReferentialConstraint (jeśli są używane).</span><span class="sxs-lookup"><span data-stu-id="2ed73-250">The value of the **Role** attribute in either the Principal or Dependent element of the corresponding ReferentialConstraint element (if used).</span></span>                                                                                                                                                                                                                                             |
| <span data-ttu-id="2ed73-251">**Liczebność**</span><span class="sxs-lookup"><span data-stu-id="2ed73-251">**Multiplicity**</span></span> | <span data-ttu-id="2ed73-252">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-252">Yes</span></span>         | <span data-ttu-id="2ed73-253">**1**, **od 0 do 1**, lub **\*** w zależności od liczby wierszy, które mogą być na końcu ograniczenie klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-253">**1**, **0..1**, or **\*** depending on the number of rows that can be at the end of the foreign key constraint.</span></span> <br/> <span data-ttu-id="2ed73-254">**1** wskazuje, że dokładnie jeden wiersz istnieje na końcu ograniczenie klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-254">**1** indicates that exactly one row exists at the foreign key constraint end.</span></span> <br/> <span data-ttu-id="2ed73-255">**od 0 do 1** wskazuje, że istnieje zero lub jeden wiersz na końcu ograniczenie klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-255">**0..1** indicates that zero or one row exists at the foreign key constraint end.</span></span> <br/> <span data-ttu-id="2ed73-256">**\*** oznacza, że wartość zero, jeden lub więcej wierszy na końcu ograniczenie klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-256">**\*** indicates that zero, one, or more rows exist at the foreign key constraint end.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-257">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **zakończenia** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-257">Any number of annotation attributes (custom XML attributes) may be applied to the **End** element.</span></span> <span data-ttu-id="2ed73-258">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla CSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-258">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="2ed73-259">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-259">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

#### <a name="example"></a><span data-ttu-id="2ed73-260">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-260">Example</span></span>

<span data-ttu-id="2ed73-261">W poniższym przykładzie przedstawiono **skojarzenia** element, który definiuje **klucza Obcego\_CustomerOrders** ograniczenie klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-261">The following example shows an **Association** element that defines the **FK\_CustomerOrders** foreign key constraint.</span></span> <span data-ttu-id="2ed73-262">**Liczebność** wartościom określonym w każdym **zakończenia** elementu wskazują tę liczbę wierszy w **zamówienia** tabeli może być skojarzony z wiersza w **klientów**  tabeli, ale tylko jeden wiersz w **klientów** tabeli może być skojarzony z wiersza w **zamówienia** tabeli.</span><span class="sxs-lookup"><span data-stu-id="2ed73-262">The **Multiplicity** values specified on each **End** element indicate that many rows in the **Orders** table can be associated with a row in the **Customers** table, but only one row in the **Customers** table can be associated with a row in the **Orders** table.</span></span> <span data-ttu-id="2ed73-263">Ponadto **OnDelete** element wskazuje, że wszystkie wiersze, w **zamówienia** odwoływać się do danego wiersza w tabeli **klientów** tabeli zostanie usunięte, gdy wiersz **klientów** tabeli zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="2ed73-263">Additionally, the **OnDelete** element indicates that all rows in the **Orders** table that reference a particular row in the **Customers** table will be deleted if the row in the **Customers** table is deleted.</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```
 

### <a name="end-element-as-a-child-of-the-associationset-element"></a><span data-ttu-id="2ed73-264">Końcowy Element jako element podrzędny elementu AssociationSet</span><span class="sxs-lookup"><span data-stu-id="2ed73-264">End Element as a Child of the AssociationSet Element</span></span>

<span data-ttu-id="2ed73-265">**Zakończenia** — element (jako element podrzędny elementu **AssociationSet** elementu) Określa tabelę na jednym końcu ograniczenie klucza obcego w źródłowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-265">The **End** element (as a child of the **AssociationSet** element) specifies a table at one end of a foreign key constraint in the underlying database.</span></span>

<span data-ttu-id="2ed73-266">**Zakończenia** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-266">An **End** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-267">Dokumentacja (zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-267">Documentation (zero or one)</span></span>
-   <span data-ttu-id="2ed73-268">Elementów adnotacji (zero lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-268">Annotation elements (zero or more)</span></span>

#### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-269">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-269">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-270">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **zakończenia** elementu, gdy jest elementem podrzędnym elementu **AssociationSet** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-270">The following table describes the attributes that can be applied to the **End** element when it is the child of an **AssociationSet** element.</span></span>

| <span data-ttu-id="2ed73-271">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-271">Attribute Name</span></span> | <span data-ttu-id="2ed73-272">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-272">Is Required</span></span> | <span data-ttu-id="2ed73-273">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-273">Value</span></span>                                                                                                                  |
|:---------------|:------------|:-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-274">**Obiekt EntitySet**</span><span class="sxs-lookup"><span data-stu-id="2ed73-274">**EntitySet**</span></span>  | <span data-ttu-id="2ed73-275">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-275">Yes</span></span>         | <span data-ttu-id="2ed73-276">Nazwa zestawu jednostek SSDL, który znajduje się na końcu ograniczenie klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-276">The name of the SSDL entity set that is at the end of the foreign key constraint.</span></span>                                      |
| <span data-ttu-id="2ed73-277">**Rola**</span><span class="sxs-lookup"><span data-stu-id="2ed73-277">**Role**</span></span>       | <span data-ttu-id="2ed73-278">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-278">No</span></span>          | <span data-ttu-id="2ed73-279">Wartość jednej z **roli** atrybuty określone w jednym **zakończenia** elementu odpowiednie skojarzenia.</span><span class="sxs-lookup"><span data-stu-id="2ed73-279">The value of one of the **Role** attributes specified on one **End** element of the corresponding Association element.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-280">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **zakończenia** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-280">Any number of annotation attributes (custom XML attributes) may be applied to the **End** element.</span></span> <span data-ttu-id="2ed73-281">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla CSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-281">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="2ed73-282">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-282">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

#### <a name="example"></a><span data-ttu-id="2ed73-283">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-283">Example</span></span>

<span data-ttu-id="2ed73-284">W poniższym przykładzie przedstawiono **EntityContainer** element z **AssociationSet** elementu przy użyciu dwóch **zakończenia** elementy:</span><span class="sxs-lookup"><span data-stu-id="2ed73-284">The following example shows an **EntityContainer** element with an **AssociationSet** element with two **End** elements:</span></span>

``` xml
 <EntityContainer Name="ExampleModelStoreContainer">
   <EntitySet Name="Customers"
              EntityType="ExampleModel.Store.Customers"
              Schema="dbo" />
   <EntitySet Name="Orders"
              EntityType="ExampleModel.Store.Orders"
              Schema="dbo" />
   <AssociationSet Name="FK_CustomerOrders"
                   Association="ExampleModel.Store.FK_CustomerOrders">
     <End Role="Customers" EntitySet="Customers" />
     <End Role="Orders" EntitySet="Orders" />
   </AssociationSet>
 </EntityContainer>
```
 

 

## <a name="entitycontainer-element-ssdl"></a><span data-ttu-id="2ed73-285">Element EntityContainer (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-285">EntityContainer Element (SSDL)</span></span>

<span data-ttu-id="2ed73-286">**EntityContainer** element język definicji schematu magazynu (SSDL) zawiera opis struktury źródła danych w aplikacji Entity Framework: zestawy jednostek SSDL (zdefiniowanymi w elementów EntitySet) reprezentują tabele w bazy danych, typy jednostek SSDL (zdefiniowany w elementach typu EntityType) reprezentują wierszy w tabeli i zestawów skojarzeń (zdefiniowany w obiekcie AssociationSet elementy) reprezentują ograniczenia klucza obcego w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-286">An **EntityContainer** element in store schema definition language (SSDL) describes the structure of the underlying data source in an Entity Framework application: SSDL entity sets (defined in EntitySet elements) represent tables in a database, SSDL entity types (defined in EntityType elements) represent rows in a table, and association sets (defined in AssociationSet elements) represent foreign key constraints in a database.</span></span> <span data-ttu-id="2ed73-287">Kontener jednostek modelu magazynu jest mapowany na model koncepcyjny kontener jednostek, za pośrednictwem elementu w elemencie EntityContainerMapping.</span><span class="sxs-lookup"><span data-stu-id="2ed73-287">A storage model entity container maps to a conceptual model entity container through the EntityContainerMapping element.</span></span>

<span data-ttu-id="2ed73-288">**EntityContainer** element może mieć zero lub jeden elementów dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="2ed73-288">An **EntityContainer** element can have zero or one Documentation elements.</span></span> <span data-ttu-id="2ed73-289">Jeśli **dokumentacji** element jest obecny, musi poprzedzać wszystkie inne elementy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="2ed73-289">If a **Documentation** element is present, it must precede all other child elements.</span></span>

<span data-ttu-id="2ed73-290">**EntityContainer** element może mieć zero lub więcej z następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-290">An **EntityContainer** element can have zero or more of the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-291">Obiekt EntitySet</span><span class="sxs-lookup"><span data-stu-id="2ed73-291">EntitySet</span></span>
-   <span data-ttu-id="2ed73-292">Obiekt AssociationSet</span><span class="sxs-lookup"><span data-stu-id="2ed73-292">AssociationSet</span></span>
-   <span data-ttu-id="2ed73-293">Elementów adnotacji</span><span class="sxs-lookup"><span data-stu-id="2ed73-293">Annotation elements</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-294">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-294">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-295">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **EntityContainer** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-295">The table below describes the attributes that can be applied to the **EntityContainer** element.</span></span>

| <span data-ttu-id="2ed73-296">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-296">Attribute Name</span></span> | <span data-ttu-id="2ed73-297">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-297">Is Required</span></span> | <span data-ttu-id="2ed73-298">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-298">Value</span></span>                                                                   |
|:---------------|:------------|:------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-299">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="2ed73-299">**Name**</span></span>       | <span data-ttu-id="2ed73-300">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-300">Yes</span></span>         | <span data-ttu-id="2ed73-301">Nazwa kontenera jednostek.</span><span class="sxs-lookup"><span data-stu-id="2ed73-301">The name of the entity container.</span></span> <span data-ttu-id="2ed73-302">Ta nazwa nie może zawierać kropek (.).</span><span class="sxs-lookup"><span data-stu-id="2ed73-302">This name cannot contain periods (.).</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-303">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **EntityContainer** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-303">Any number of annotation attributes (custom XML attributes) may be applied to the **EntityContainer** element.</span></span> <span data-ttu-id="2ed73-304">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-304">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-305">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-305">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-306">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-306">Example</span></span>

<span data-ttu-id="2ed73-307">W poniższym przykładzie przedstawiono **EntityContainer** element, który definiuje dwa zestawy jednostek i jedno skojarzenie zestawu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-307">The following example shows an **EntityContainer** element that defines two entity sets and one association set.</span></span> <span data-ttu-id="2ed73-308">Należy zauważyć, że nazwy jednostki typu i skojarzenia typów są kwalifikowana przez nazwę przestrzeni nazw modelu koncepcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-308">Note that entity type and association type names are qualified by the conceptual model namespace name.</span></span>

``` xml
 <EntityContainer Name="ExampleModelStoreContainer">
   <EntitySet Name="Customers"
              EntityType="ExampleModel.Store.Customers"
              Schema="dbo" />
   <EntitySet Name="Orders"
              EntityType="ExampleModel.Store.Orders"
              Schema="dbo" />
   <AssociationSet Name="FK_CustomerOrders"
                   Association="ExampleModel.Store.FK_CustomerOrders">
     <End Role="Customers" EntitySet="Customers" />
     <End Role="Orders" EntitySet="Orders" />
   </AssociationSet>
 </EntityContainer>
```
 

 

## <a name="entityset-element-ssdl"></a><span data-ttu-id="2ed73-309">Element EntitySet (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-309">EntitySet Element (SSDL)</span></span>

 <span data-ttu-id="2ed73-310">**EntitySet** element język definicji schematu magazynu (SSDL) reprezentuje tabelę lub widok w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-310">An **EntitySet** element in store schema definition language (SSDL) represents a table or view in the underlying database.</span></span> <span data-ttu-id="2ed73-311">Element EntityType SSDL reprezentuje wiersz w tabeli lub widoku.</span><span class="sxs-lookup"><span data-stu-id="2ed73-311">An EntityType element in SSDL represents a row in the table or view.</span></span> <span data-ttu-id="2ed73-312">**EntityType** atrybutu **EntitySet** element określa typ jednostki SSDL konkretnego, który reprezentuje wierszy w zestawie jednostek SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-312">The **EntityType** attribute of an **EntitySet** element specifies the particular SSDL entity type that represents rows in an SSDL entity set.</span></span> <span data-ttu-id="2ed73-313">Mapowanie między zestaw jednostek CSDL a SSDL zestaw jednostek jest określona w obiekcie EntitySetMapping elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-313">The mapping between a CSDL entity set and an SSDL entity set is specified in an EntitySetMapping element.</span></span>

<span data-ttu-id="2ed73-314">**EntitySet** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-314">The **EntitySet** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-315">Dokumentacja (zero lub jeden element)</span><span class="sxs-lookup"><span data-stu-id="2ed73-315">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="2ed73-316">DefiningQuery (zero lub jeden element)</span><span class="sxs-lookup"><span data-stu-id="2ed73-316">DefiningQuery (zero or one element)</span></span>
-   <span data-ttu-id="2ed73-317">Elementów adnotacji</span><span class="sxs-lookup"><span data-stu-id="2ed73-317">Annotation elements</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-318">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-318">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-319">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **EntitySet** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-319">The following table describes the attributes that can be applied to the **EntitySet** element.</span></span>

> [!NOTE]
> <span data-ttu-id="2ed73-320">Niektóre atrybuty (niewymienione w tym) może być kwalifikowana za pomocą **przechowywania** aliasu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-320">Some attributes (not listed here) may be qualified with the **store** alias.</span></span> <span data-ttu-id="2ed73-321">Te atrybuty są używane przez kreatora Model aktualizacji, podczas aktualizowania modelu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-321">These attributes are used by the Update Model Wizard when updating a model.</span></span>

 

| <span data-ttu-id="2ed73-322">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-322">Attribute Name</span></span> | <span data-ttu-id="2ed73-323">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-323">Is Required</span></span> | <span data-ttu-id="2ed73-324">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-324">Value</span></span>                                                                                    |
|:---------------|:------------|:-----------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-325">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="2ed73-325">**Name**</span></span>       | <span data-ttu-id="2ed73-326">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-326">Yes</span></span>         | <span data-ttu-id="2ed73-327">Nazwa zestawu jednostek.</span><span class="sxs-lookup"><span data-stu-id="2ed73-327">The name of the entity set.</span></span>                                                              |
| <span data-ttu-id="2ed73-328">**Typ EntityType**</span><span class="sxs-lookup"><span data-stu-id="2ed73-328">**EntityType**</span></span> | <span data-ttu-id="2ed73-329">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-329">Yes</span></span>         | <span data-ttu-id="2ed73-330">W pełni kwalifikowana nazwa typu jednostki, dla której zestaw jednostek zawiera wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="2ed73-330">The fully-qualified name of the entity type for which the entity set contains instances.</span></span> |
| <span data-ttu-id="2ed73-331">**Schemat**</span><span class="sxs-lookup"><span data-stu-id="2ed73-331">**Schema**</span></span>     | <span data-ttu-id="2ed73-332">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-332">No</span></span>          | <span data-ttu-id="2ed73-333">Schemat bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-333">The database schema.</span></span>                                                                     |
| <span data-ttu-id="2ed73-334">**Tabela**</span><span class="sxs-lookup"><span data-stu-id="2ed73-334">**Table**</span></span>      | <span data-ttu-id="2ed73-335">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-335">No</span></span>          | <span data-ttu-id="2ed73-336">Tabela bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-336">The database table.</span></span>                                                                      |
 
 
 
 
 
 

> [!NOTE]
> <span data-ttu-id="2ed73-337">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **EntitySet** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-337">Any number of annotation attributes (custom XML attributes) may be applied to the **EntitySet** element.</span></span> <span data-ttu-id="2ed73-338">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-338">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-339">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-339">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-340">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-340">Example</span></span>

<span data-ttu-id="2ed73-341">W poniższym przykładzie przedstawiono **EntityContainer** element, który ma dwa **EntitySet** elementy i jeden **AssociationSet** elementu:</span><span class="sxs-lookup"><span data-stu-id="2ed73-341">The following example shows an **EntityContainer** element that has two **EntitySet** elements and one **AssociationSet** element:</span></span>

``` xml
 <EntityContainer Name="ExampleModelStoreContainer">
   <EntitySet Name="Customers"
              EntityType="ExampleModel.Store.Customers"
              Schema="dbo" />
   <EntitySet Name="Orders"
              EntityType="ExampleModel.Store.Orders"
              Schema="dbo" />
   <AssociationSet Name="FK_CustomerOrders"
                   Association="ExampleModel.Store.FK_CustomerOrders">
     <End Role="Customers" EntitySet="Customers" />
     <End Role="Orders" EntitySet="Orders" />
   </AssociationSet>
 </EntityContainer>
```
 

 

## <a name="entitytype-element-ssdl"></a><span data-ttu-id="2ed73-342">Element EntityType (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-342">EntityType Element (SSDL)</span></span>

<span data-ttu-id="2ed73-343">**EntityType** element język definicji schematu magazynu (SSDL) reprezentuje wiersz w tabeli lub widoku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-343">An **EntityType** element in store schema definition language (SSDL) represents a row in a table or view of the underlying database.</span></span> <span data-ttu-id="2ed73-344">Element EntitySet SSDL reprezentuje tabelę lub widok, w którym występują wiersze.</span><span class="sxs-lookup"><span data-stu-id="2ed73-344">An EntitySet element in SSDL represents the table or view in which rows occur.</span></span> <span data-ttu-id="2ed73-345">**EntityType** atrybutu **EntitySet** element określa typ jednostki SSDL konkretnego, który reprezentuje wierszy w zestawie jednostek SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-345">The **EntityType** attribute of an **EntitySet** element specifies the particular SSDL entity type that represents rows in an SSDL entity set.</span></span> <span data-ttu-id="2ed73-346">Mapowanie między typem encji SSDL i typ jednostki CSDL jest określony w elemencie EntityTypeMapping.</span><span class="sxs-lookup"><span data-stu-id="2ed73-346">The mapping between an SSDL entity type and a CSDL entity type is specified in an EntityTypeMapping element.</span></span>

<span data-ttu-id="2ed73-347">**EntityType** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-347">The **EntityType** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-348">Dokumentacja (zero lub jeden element)</span><span class="sxs-lookup"><span data-stu-id="2ed73-348">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="2ed73-349">Klucz (zero lub jeden element)</span><span class="sxs-lookup"><span data-stu-id="2ed73-349">Key (zero or one element)</span></span>
-   <span data-ttu-id="2ed73-350">Elementów adnotacji</span><span class="sxs-lookup"><span data-stu-id="2ed73-350">Annotation elements</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-351">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-351">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-352">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **EntityType** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-352">The table below describes the attributes that can be applied to the **EntityType** element.</span></span>

| <span data-ttu-id="2ed73-353">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-353">Attribute Name</span></span> | <span data-ttu-id="2ed73-354">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-354">Is Required</span></span> | <span data-ttu-id="2ed73-355">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-355">Value</span></span>                                                                                                                                                                  |
|:---------------|:------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-356">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="2ed73-356">**Name**</span></span>       | <span data-ttu-id="2ed73-357">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-357">Yes</span></span>         | <span data-ttu-id="2ed73-358">Nazwa typu jednostki.</span><span class="sxs-lookup"><span data-stu-id="2ed73-358">The name of the entity type.</span></span> <span data-ttu-id="2ed73-359">Ta wartość jest zwykle taka sama jak nazwa tabeli, w którym typ jednostki reprezentuje wiersz.</span><span class="sxs-lookup"><span data-stu-id="2ed73-359">This value is usually the same as the name of the table in which the entity type represents a row.</span></span> <span data-ttu-id="2ed73-360">Ta wartość może zawierać nie kropki (.).</span><span class="sxs-lookup"><span data-stu-id="2ed73-360">This value can contain no periods (.).</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-361">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **EntityType** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-361">Any number of annotation attributes (custom XML attributes) may be applied to the **EntityType** element.</span></span> <span data-ttu-id="2ed73-362">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-362">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-363">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-363">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-364">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-364">Example</span></span>

<span data-ttu-id="2ed73-365">W poniższym przykładzie przedstawiono **EntityType** elementu o dwie właściwości:</span><span class="sxs-lookup"><span data-stu-id="2ed73-365">The following example shows an **EntityType** element with two properties:</span></span>

``` xml
 <EntityType Name="Customers">
   <Documentation>
     <Summary>Summary here.</Summary>
     <LongDescription>Long description here.</LongDescription>
   </Documentation>
   <Key>
     <PropertyRef Name="CustomerId" />
   </Key>
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
 </EntityType>
```
 

 

## <a name="function-element-ssdl"></a><span data-ttu-id="2ed73-366">Function — Element (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-366">Function Element (SSDL)</span></span>

<span data-ttu-id="2ed73-367">**Funkcja** element język definicji schematu magazynu (SSDL) określa procedury przechowywanej, która istnieje w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-367">The **Function** element in store schema definition language (SSDL) specifies a stored procedure that exists in the underlying database.</span></span>

<span data-ttu-id="2ed73-368">**Funkcja** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-368">The **Function** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-369">Dokumentacja (zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-369">Documentation (zero or one)</span></span>
-   <span data-ttu-id="2ed73-370">Parametr (zero lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-370">Parameter (zero or more)</span></span>
-   <span data-ttu-id="2ed73-371">CommandText (zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-371">CommandText (zero or one)</span></span>
-   <span data-ttu-id="2ed73-372">ReturnType (zero lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-372">ReturnType (zero or more)</span></span>
-   <span data-ttu-id="2ed73-373">Elementów adnotacji (zero lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-373">Annotation elements (zero or more)</span></span>

<span data-ttu-id="2ed73-374">Zwracana typ dla funkcji, należy określić albo **ReturnType** element lub **ReturnType** atrybutu (patrz poniżej), ale nie oba.</span><span class="sxs-lookup"><span data-stu-id="2ed73-374">A return type for a function must be specified with either the **ReturnType** element or the **ReturnType** attribute (see below), but not both.</span></span>

<span data-ttu-id="2ed73-375">Procedury składowane, które są określone w modelu magazynu można zaimportować do modelu koncepcyjnego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ed73-375">Stored procedures that are specified in the storage model can be imported into the conceptual model of an application.</span></span> <span data-ttu-id="2ed73-376">Aby uzyskać więcej informacji, zobacz [wykonywanie zapytań za pomocą procedur składowanych](~/ef6/modeling/designer/stored-procedures/query.md).</span><span class="sxs-lookup"><span data-stu-id="2ed73-376">For more information, see [Querying with Stored Procedures](~/ef6/modeling/designer/stored-procedures/query.md).</span></span> <span data-ttu-id="2ed73-377">**Funkcja** elementu może również służyć do definiowania funkcji niestandardowych w modelu magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-377">The **Function** element can also be used to define custom functions in the storage model.</span></span>  

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-378">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-378">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-379">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **funkcja** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-379">The following table describes the attributes that can be applied to the **Function** element.</span></span>

> [!NOTE]
> <span data-ttu-id="2ed73-380">Niektóre atrybuty (niewymienione w tym) może być kwalifikowana za pomocą **przechowywania** aliasu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-380">Some attributes (not listed here) may be qualified with the **store** alias.</span></span> <span data-ttu-id="2ed73-381">Te atrybuty są używane przez kreatora Model aktualizacji, podczas aktualizowania modelu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-381">These attributes are used by the Update Model Wizard when updating a model.</span></span>

 

| <span data-ttu-id="2ed73-382">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-382">Attribute Name</span></span>             | <span data-ttu-id="2ed73-383">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-383">Is Required</span></span> | <span data-ttu-id="2ed73-384">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-384">Value</span></span>                                                                                                                                                                                                              |
|:---------------------------|:------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-385">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="2ed73-385">**Name**</span></span>                   | <span data-ttu-id="2ed73-386">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-386">Yes</span></span>         | <span data-ttu-id="2ed73-387">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="2ed73-387">The name of the stored procedure.</span></span>                                                                                                                                                                                  |
| <span data-ttu-id="2ed73-388">**ReturnType**</span><span class="sxs-lookup"><span data-stu-id="2ed73-388">**ReturnType**</span></span>             | <span data-ttu-id="2ed73-389">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-389">No</span></span>          | <span data-ttu-id="2ed73-390">Zwracany typ procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="2ed73-390">The return type of the stored procedure.</span></span>                                                                                                                                                                           |
| <span data-ttu-id="2ed73-391">**Aggregate**</span><span class="sxs-lookup"><span data-stu-id="2ed73-391">**Aggregate**</span></span>              | <span data-ttu-id="2ed73-392">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-392">No</span></span>          | <span data-ttu-id="2ed73-393">**Wartość true,** Jeśli procedura składowana ma zwracać wartości zagregowanej; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="2ed73-393">**True** if the stored procedure returns an aggregate value; otherwise **False**.</span></span>                                                                                                                                  |
| <span data-ttu-id="2ed73-394">**Wbudowane**</span><span class="sxs-lookup"><span data-stu-id="2ed73-394">**BuiltIn**</span></span>                | <span data-ttu-id="2ed73-395">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-395">No</span></span>          | <span data-ttu-id="2ed73-396">**Wartość true,** Jeśli funkcja jest wbudowaną<sup>1</sup> funkcji; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="2ed73-396">**True** if the function is a built-in<sup>1</sup> function; otherwise **False**.</span></span>                                                                                                                                  |
| <span data-ttu-id="2ed73-397">**StoreFunctionName**</span><span class="sxs-lookup"><span data-stu-id="2ed73-397">**StoreFunctionName**</span></span>      | <span data-ttu-id="2ed73-398">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-398">No</span></span>          | <span data-ttu-id="2ed73-399">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="2ed73-399">The name of the stored procedure.</span></span>                                                                                                                                                                                  |
| <span data-ttu-id="2ed73-400">**NiladicFunction**</span><span class="sxs-lookup"><span data-stu-id="2ed73-400">**NiladicFunction**</span></span>        | <span data-ttu-id="2ed73-401">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-401">No</span></span>          | <span data-ttu-id="2ed73-402">**Wartość true,** Jeśli funkcja znajduje się bez parametrów<sup>2</sup> funkcji; **False** inaczej.</span><span class="sxs-lookup"><span data-stu-id="2ed73-402">**True** if the function is a niladic<sup>2</sup> function; **False** otherwise.</span></span>                                                                                                                                   |
| <span data-ttu-id="2ed73-403">**IsComposable**</span><span class="sxs-lookup"><span data-stu-id="2ed73-403">**IsComposable**</span></span>           | <span data-ttu-id="2ed73-404">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-404">No</span></span>          | <span data-ttu-id="2ed73-405">**Wartość true,** Jeśli funkcja jest konfigurowalna<sup>3</sup> funkcji; **False** inaczej.</span><span class="sxs-lookup"><span data-stu-id="2ed73-405">**True** if the function is a composable<sup>3</sup> function; **False** otherwise.</span></span>                                                                                                                                |
| <span data-ttu-id="2ed73-406">**ParameterTypeSemantics**</span><span class="sxs-lookup"><span data-stu-id="2ed73-406">**ParameterTypeSemantics**</span></span> | <span data-ttu-id="2ed73-407">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-407">No</span></span>          | <span data-ttu-id="2ed73-408">Wyliczenie, które definiuje semantyka typów, używany do rozpoznawania przeciążenia funkcji.</span><span class="sxs-lookup"><span data-stu-id="2ed73-408">The enumeration that defines the type semantics used to resolve function overloads.</span></span> <span data-ttu-id="2ed73-409">Wyliczenia jest zdefiniowany w manifeście dostawcy dla definicji funkcji.</span><span class="sxs-lookup"><span data-stu-id="2ed73-409">The enumeration is defined in the provider manifest per function definition.</span></span> <span data-ttu-id="2ed73-410">Wartość domyślna to **AllowImplicitConversion**.</span><span class="sxs-lookup"><span data-stu-id="2ed73-410">The default value is **AllowImplicitConversion**.</span></span> |
| <span data-ttu-id="2ed73-411">**Schemat**</span><span class="sxs-lookup"><span data-stu-id="2ed73-411">**Schema**</span></span>                 | <span data-ttu-id="2ed73-412">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-412">No</span></span>          | <span data-ttu-id="2ed73-413">Nazwa schematu, w którym zdefiniowano procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="2ed73-413">The name of the schema in which the stored procedure is defined.</span></span>                                                                                                                                                   |

 

<span data-ttu-id="2ed73-414"><sup>1</sup> wbudowana funkcja jest funkcją, która jest zdefiniowana w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-414"><sup>1</sup> A built-in function is a function that is defined in the database.</span></span> <span data-ttu-id="2ed73-415">Aby uzyskać informacje na temat funkcji, które są zdefiniowane w modelu magazynu Zobacz Element CommandText (SSDL).</span><span class="sxs-lookup"><span data-stu-id="2ed73-415">For information about functions that are defined in the storage model, see CommandText Element (SSDL).</span></span>

<span data-ttu-id="2ed73-416"><sup>2</sup> funkcję bez parametrów jest funkcją, która przyjmuje żadnych parametrów i, gdy zostanie wywołana, nie wymaga nawiasów.</span><span class="sxs-lookup"><span data-stu-id="2ed73-416"><sup>2</sup> A niladic function is a function that accepts no parameters and, when called, does not require parentheses.</span></span>

<span data-ttu-id="2ed73-417"><sup>3</sup> dwie funkcje są konfigurowalna, jeśli jedna funkcja może zwracać dane wejściowe dla innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="2ed73-417"><sup>3</sup> Two functions are composable if the output of one function can be the input for the other function.</span></span>

> [!NOTE]
> <span data-ttu-id="2ed73-418">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **funkcja** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-418">Any number of annotation attributes (custom XML attributes) may be applied to the **Function** element.</span></span> <span data-ttu-id="2ed73-419">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-419">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-420">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-420">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-421">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-421">Example</span></span>

<span data-ttu-id="2ed73-422">W poniższym przykładzie przedstawiono **funkcja** element, który odpowiada **UpdateOrderQuantity** procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="2ed73-422">The following example shows a **Function** element that corresponds to the **UpdateOrderQuantity** stored procedure.</span></span> <span data-ttu-id="2ed73-423">Procedura składowana akceptuje dwa parametry i zwracać wartości.</span><span class="sxs-lookup"><span data-stu-id="2ed73-423">The stored procedure accepts two parameters and does not return a value.</span></span>

``` xml
 <Function Name="UpdateOrderQuantity"
           Aggregate="false"
           BuiltIn="false"
           NiladicFunction="false"
           IsComposable="false"
           ParameterTypeSemantics="AllowImplicitConversion"
           Schema="dbo">
   <Parameter Name="orderId" Type="int" Mode="In" />
   <Parameter Name="newQuantity" Type="int" Mode="In" />
 </Function>
```
 

 

## <a name="key-element-ssdl"></a><span data-ttu-id="2ed73-424">Kluczowym elementem (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-424">Key Element (SSDL)</span></span>

<span data-ttu-id="2ed73-425">**Klucz** element język definicji schematu magazynu (SSDL) reprezentuje klucz podstawowy tabeli w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-425">The **Key** element in store schema definition language (SSDL) represents the primary key of a table in the underlying database.</span></span> <span data-ttu-id="2ed73-426">**Klucz** jest elementem podrzędnym elementu EntityType, który reprezentuje wiersz w tabeli.</span><span class="sxs-lookup"><span data-stu-id="2ed73-426">**Key** is a child element of an EntityType element, which represents a row in a table.</span></span> <span data-ttu-id="2ed73-427">Klucz podstawowy jest zdefiniowany w **klucz** elementu odwołując się do elementów właściwości, które są zdefiniowane na **EntityType** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-427">The primary key is defined in the **Key** element by referencing one or more Property elements that are defined on the **EntityType** element.</span></span>

<span data-ttu-id="2ed73-428">**Klucz** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-428">The **Key** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-429">PropertyRef (jeden lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-429">PropertyRef (one or more)</span></span>
-   <span data-ttu-id="2ed73-430">Elementów adnotacji</span><span class="sxs-lookup"><span data-stu-id="2ed73-430">Annotation elements</span></span>

<span data-ttu-id="2ed73-431">Atrybuty nie są stosowane do **klucz** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-431">No attributes are applicable to the **Key** element.</span></span>

### <a name="example"></a><span data-ttu-id="2ed73-432">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-432">Example</span></span>

<span data-ttu-id="2ed73-433">W poniższym przykładzie przedstawiono **EntityType** element z kluczem, który odwołuje się do jednej właściwości:</span><span class="sxs-lookup"><span data-stu-id="2ed73-433">The following example shows an **EntityType** element with a key that references one property:</span></span>

``` xml
 <EntityType Name="Customers">
   <Documentation>
     <Summary>Summary here.</Summary>
     <LongDescription>Long description here.</LongDescription>
   </Documentation>
   <Key>
     <PropertyRef Name="CustomerId" />
   </Key>
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
 </EntityType>
```
 

 

## <a name="ondelete-element-ssdl"></a><span data-ttu-id="2ed73-434">Element OnDelete (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-434">OnDelete Element (SSDL)</span></span>

<span data-ttu-id="2ed73-435">**OnDelete** element język definicji schematu magazynu (SSDL) odzwierciedla zachowanie bazy danych, po usunięciu wiersza, który uczestniczy w ograniczenie klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-435">The **OnDelete** element in store schema definition language (SSDL) reflects the database behavior when a row that participates in a foreign key constraint is deleted.</span></span> <span data-ttu-id="2ed73-436">Jeśli ustawiono akcję **Cascade**, a następnie również zostaną usunięte wiersze, które odwołują się wiersz, który jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="2ed73-436">If the action is set to **Cascade**, then rows that reference a row that is being deleted will also be deleted.</span></span> <span data-ttu-id="2ed73-437">Jeśli ustawiono akcję **Brak**, a następnie nie zostaną również usunięte wiersze, które odwołują się wiersz, który jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="2ed73-437">If the action is set to **None**, then rows that reference a row that is being deleted are not also deleted.</span></span> <span data-ttu-id="2ed73-438">**OnDelete** element jest elementem podrzędnym elementu End.</span><span class="sxs-lookup"><span data-stu-id="2ed73-438">An **OnDelete** element is a child element of an End element.</span></span>

<span data-ttu-id="2ed73-439">**OnDelete** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-439">An **OnDelete** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-440">Dokumentacja (zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-440">Documentation (zero or one)</span></span>
-   <span data-ttu-id="2ed73-441">Elementów adnotacji (zero lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-441">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-442">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-442">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-443">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **OnDelete** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-443">The following table describes the attributes that can be applied to the **OnDelete** element.</span></span>

| <span data-ttu-id="2ed73-444">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-444">Attribute Name</span></span> | <span data-ttu-id="2ed73-445">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-445">Is Required</span></span> | <span data-ttu-id="2ed73-446">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-446">Value</span></span>                                                                                               |
|:---------------|:------------|:----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-447">**Akcja**</span><span class="sxs-lookup"><span data-stu-id="2ed73-447">**Action**</span></span>     | <span data-ttu-id="2ed73-448">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-448">Yes</span></span>         | <span data-ttu-id="2ed73-449">**Kaskadowe** lub **Brak**.</span><span class="sxs-lookup"><span data-stu-id="2ed73-449">**Cascade** or **None**.</span></span> <span data-ttu-id="2ed73-450">(Wartość **ograniczeniami** jest prawidłowy, ale ma takie samo zachowanie jako **Brak**.)</span><span class="sxs-lookup"><span data-stu-id="2ed73-450">(The value **Restricted** is valid but has the same behavior as **None**.)</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-451">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **OnDelete** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-451">Any number of annotation attributes (custom XML attributes) may be applied to the **OnDelete** element.</span></span> <span data-ttu-id="2ed73-452">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-452">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-453">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-453">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-454">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-454">Example</span></span>

<span data-ttu-id="2ed73-455">W poniższym przykładzie przedstawiono **skojarzenia** element, który definiuje **klucza Obcego\_CustomerOrders** ograniczenie klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-455">The following example shows an **Association** element that defines the **FK\_CustomerOrders** foreign key constraint.</span></span> <span data-ttu-id="2ed73-456">**OnDelete** element wskazuje, że wszystkie wiersze w **zamówienia** odwoływać się do danego wiersza w tabeli **klientów** tabeli zostanie usunięte, gdy wiersz **Klientów** tabeli zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="2ed73-456">The **OnDelete** element indicates that all rows in the **Orders** table that reference a particular row in the **Customers** table will be deleted if the row in the **Customers** table is deleted.</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```
 

 

## <a name="parameter-element-ssdl"></a><span data-ttu-id="2ed73-457">Parameter — Element (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-457">Parameter Element (SSDL)</span></span>

<span data-ttu-id="2ed73-458">**Parametru** język definicji schematu magazynu (SSDL) element jest elementem podrzędnym elementu funkcji, który określa parametry dla procedury przechowywanej w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-458">The **Parameter** element in store schema definition language (SSDL) is a child of the Function element that specifies parameters for a stored procedure in the database.</span></span>

<span data-ttu-id="2ed73-459">**Parametru** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-459">The **Parameter** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-460">Dokumentacja (zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-460">Documentation (zero or one)</span></span>
-   <span data-ttu-id="2ed73-461">Elementów adnotacji (zero lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-461">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-462">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-462">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-463">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **parametru** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-463">The table below describes the attributes that can be applied to the **Parameter** element.</span></span>

| <span data-ttu-id="2ed73-464">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-464">Attribute Name</span></span> | <span data-ttu-id="2ed73-465">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-465">Is Required</span></span> | <span data-ttu-id="2ed73-466">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-466">Value</span></span>                                                                                                                                                                                                                           |
|:---------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-467">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="2ed73-467">**Name**</span></span>       | <span data-ttu-id="2ed73-468">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-468">Yes</span></span>         | <span data-ttu-id="2ed73-469">Nazwa parametru.</span><span class="sxs-lookup"><span data-stu-id="2ed73-469">The name of the parameter.</span></span>                                                                                                                                                                                                      |
| <span data-ttu-id="2ed73-470">**Typ**</span><span class="sxs-lookup"><span data-stu-id="2ed73-470">**Type**</span></span>       | <span data-ttu-id="2ed73-471">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-471">Yes</span></span>         | <span data-ttu-id="2ed73-472">Typ parametru.</span><span class="sxs-lookup"><span data-stu-id="2ed73-472">The parameter type.</span></span>                                                                                                                                                                                                             |
| <span data-ttu-id="2ed73-473">**Tryb**</span><span class="sxs-lookup"><span data-stu-id="2ed73-473">**Mode**</span></span>       | <span data-ttu-id="2ed73-474">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-474">No</span></span>          | <span data-ttu-id="2ed73-475">**W**, **się**, lub **InOut** w zależności od tego, czy parametr jest danych wejściowych, danych wyjściowych lub parametr input/output.</span><span class="sxs-lookup"><span data-stu-id="2ed73-475">**In**, **Out**, or **InOut** depending on whether the parameter is an input, output, or input/output parameter.</span></span>                                                                                                                |
| <span data-ttu-id="2ed73-476">**Element MaxLength**</span><span class="sxs-lookup"><span data-stu-id="2ed73-476">**MaxLength**</span></span>  | <span data-ttu-id="2ed73-477">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-477">No</span></span>          | <span data-ttu-id="2ed73-478">Maksymalna długość parametru.</span><span class="sxs-lookup"><span data-stu-id="2ed73-478">The maximum length of the parameter.</span></span>                                                                                                                                                                                            |
| <span data-ttu-id="2ed73-479">**Precyzja**</span><span class="sxs-lookup"><span data-stu-id="2ed73-479">**Precision**</span></span>  | <span data-ttu-id="2ed73-480">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-480">No</span></span>          | <span data-ttu-id="2ed73-481">Dokładność parametru.</span><span class="sxs-lookup"><span data-stu-id="2ed73-481">The precision of the parameter.</span></span>                                                                                                                                                                                                 |
| <span data-ttu-id="2ed73-482">**Skala**</span><span class="sxs-lookup"><span data-stu-id="2ed73-482">**Scale**</span></span>      | <span data-ttu-id="2ed73-483">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-483">No</span></span>          | <span data-ttu-id="2ed73-484">Skala parametru.</span><span class="sxs-lookup"><span data-stu-id="2ed73-484">The scale of the parameter.</span></span>                                                                                                                                                                                                     |
| <span data-ttu-id="2ed73-485">**SRID**</span><span class="sxs-lookup"><span data-stu-id="2ed73-485">**SRID**</span></span>       | <span data-ttu-id="2ed73-486">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-486">No</span></span>          | <span data-ttu-id="2ed73-487">Identyfikator odwołania przestrzennego systemu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-487">Spatial System Reference Identifier.</span></span> <span data-ttu-id="2ed73-488">Prawidłowy tylko dla parametrów typów przestrzennych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-488">Valid only for parameters of spatial types.</span></span> <span data-ttu-id="2ed73-489">Aby uzyskać więcej informacji, zobacz [SRID](http://en.wikipedia.org/wiki/SRID) i [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ed73-489">For more information, see [SRID](http://en.wikipedia.org/wiki/SRID) and [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-490">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **parametru** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-490">Any number of annotation attributes (custom XML attributes) may be applied to the **Parameter** element.</span></span> <span data-ttu-id="2ed73-491">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-491">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-492">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-492">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-493">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-493">Example</span></span>

<span data-ttu-id="2ed73-494">W poniższym przykładzie przedstawiono **funkcja** element, który ma dwa **parametru** elementy, które określają parametry wejściowe:</span><span class="sxs-lookup"><span data-stu-id="2ed73-494">The following example shows a **Function** element that has two **Parameter** elements that specify input parameters:</span></span>

``` xml
 <Function Name="UpdateOrderQuantity"
           Aggregate="false"
           BuiltIn="false"
           NiladicFunction="false"
           IsComposable="false"
           ParameterTypeSemantics="AllowImplicitConversion"
           Schema="dbo">
   <Parameter Name="orderId" Type="int" Mode="In" />
   <Parameter Name="newQuantity" Type="int" Mode="In" />
 </Function>
```
 

 

## <a name="principal-element-ssdl"></a><span data-ttu-id="2ed73-495">Element jednostki (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-495">Principal Element (SSDL)</span></span>

<span data-ttu-id="2ed73-496">**Jednostki** element język definicji schematu magazynu (SSDL) jest element podrzędny do elementu ReferentialConstraint, który definiuje główny koniec ograniczenie klucza obcego (nazywany także ograniczenie referencyjne).</span><span class="sxs-lookup"><span data-stu-id="2ed73-496">The **Principal** element in store schema definition language (SSDL) is a child element to the ReferentialConstraint element that defines the principal end of a foreign key constraint (also called a referential constraint).</span></span> <span data-ttu-id="2ed73-497">**Jednostki** element określa kolumny klucza podstawowego (lub kolumny) w tabeli, która odwołuje się do niej innej kolumny (lub kolumny).</span><span class="sxs-lookup"><span data-stu-id="2ed73-497">The **Principal** element specifies the primary key column (or columns) in a table that is referenced by another column (or columns).</span></span> <span data-ttu-id="2ed73-498">**PropertyRef** elementy Określ kolumny, które są wywoływane.</span><span class="sxs-lookup"><span data-stu-id="2ed73-498">**PropertyRef** elements specify which columns are referenced.</span></span> <span data-ttu-id="2ed73-499">Element zależne Określa kolumny, które odwołują się kolumny klucza podstawowego, które są określone w **jednostki** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-499">The Dependent element specifies columns that reference the primary key columns that are specified in the **Principal** element.</span></span>

<span data-ttu-id="2ed73-500">**Jednostki** element może mieć następujących elementów podrzędnych (w podanej kolejności):</span><span class="sxs-lookup"><span data-stu-id="2ed73-500">The **Principal** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="2ed73-501">PropertyRef (jeden lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-501">PropertyRef (one or more)</span></span>
-   <span data-ttu-id="2ed73-502">Elementów adnotacji (zero lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-502">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-503">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-503">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-504">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **jednostki** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-504">The following table describes the attributes that can be applied to the **Principal** element.</span></span>

| <span data-ttu-id="2ed73-505">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-505">Attribute Name</span></span> | <span data-ttu-id="2ed73-506">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-506">Is Required</span></span> | <span data-ttu-id="2ed73-507">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-507">Value</span></span>                                                                                                                                                      |
|:---------------|:------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-508">**Rola**</span><span class="sxs-lookup"><span data-stu-id="2ed73-508">**Role**</span></span>       | <span data-ttu-id="2ed73-509">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-509">Yes</span></span>         | <span data-ttu-id="2ed73-510">Taką samą wartość jak **roli** atrybut odpowiedni element End (jeśli jest używana); w przeciwnym razie nazwę tabeli, która zawiera odwołuje się do kolumny.</span><span class="sxs-lookup"><span data-stu-id="2ed73-510">The same value as the **Role** attribute (if used) of the corresponding End element; otherwise, the name of the table that contains the referenced column.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-511">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **jednostki** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-511">Any number of annotation attributes (custom XML attributes) may be applied to the **Principal** element.</span></span> <span data-ttu-id="2ed73-512">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla CSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-512">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="2ed73-513">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-513">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-514">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-514">Example</span></span>

<span data-ttu-id="2ed73-515">W poniższym przykładzie pokazano element Association używający **ReferentialConstraint** elementu, aby określić kolumny, które uczestniczą w **klucza Obcego\_CustomerOrders** klucza obcego ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="2ed73-515">The following example shows an Association element that uses a **ReferentialConstraint** element to specify the columns that participate in the **FK\_CustomerOrders** foreign key constraint.</span></span> <span data-ttu-id="2ed73-516">**Jednostki** element Określa **CustomerId** kolumny **klienta** tabeli jako główny koniec tego ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="2ed73-516">The **Principal** element specifies the **CustomerId** column of the **Customer** table as the principal end of the constraint.</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```
 

 

## <a name="property-element-ssdl"></a><span data-ttu-id="2ed73-517">Property — Element (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-517">Property Element (SSDL)</span></span>

<span data-ttu-id="2ed73-518">**Właściwość** element język definicji schematu magazynu (SSDL) reprezentuje kolumnę w tabeli w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-518">The **Property** element in store schema definition language (SSDL) represents a column in a table in the underlying database.</span></span> <span data-ttu-id="2ed73-519">**Właściwość** elementy są elementami podrzędnymi typu EntityType elementy, które reprezentują wierszy w tabeli.</span><span class="sxs-lookup"><span data-stu-id="2ed73-519">**Property** elements are children of EntityType elements, which represent rows in a table.</span></span> <span data-ttu-id="2ed73-520">Każdy **właściwość** elementu zdefiniowanego w **EntityType** element reprezentuje kolumnę.</span><span class="sxs-lookup"><span data-stu-id="2ed73-520">Each **Property** element defined on an **EntityType** element represents a column.</span></span>

<span data-ttu-id="2ed73-521">A **właściwość** elementu nie może mieć żadnych elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-521">A **Property** element cannot have any child elements.</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-522">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-522">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-523">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **właściwość** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-523">The following table describes the attributes that can be applied to the **Property** element.</span></span>

| <span data-ttu-id="2ed73-524">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-524">Attribute Name</span></span>            | <span data-ttu-id="2ed73-525">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-525">Is Required</span></span> | <span data-ttu-id="2ed73-526">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-526">Value</span></span>                                                                                                                                                                                                                           |
|:--------------------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-527">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="2ed73-527">**Name**</span></span>                  | <span data-ttu-id="2ed73-528">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-528">Yes</span></span>         | <span data-ttu-id="2ed73-529">Nazwa odpowiednią kolumnę.</span><span class="sxs-lookup"><span data-stu-id="2ed73-529">The name of the corresponding column.</span></span>                                                                                                                                                                                           |
| <span data-ttu-id="2ed73-530">**Typ**</span><span class="sxs-lookup"><span data-stu-id="2ed73-530">**Type**</span></span>                  | <span data-ttu-id="2ed73-531">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-531">Yes</span></span>         | <span data-ttu-id="2ed73-532">Typ odpowiednią kolumnę.</span><span class="sxs-lookup"><span data-stu-id="2ed73-532">The type of the corresponding column.</span></span>                                                                                                                                                                                           |
| <span data-ttu-id="2ed73-533">**Dopuszcza wartości null**</span><span class="sxs-lookup"><span data-stu-id="2ed73-533">**Nullable**</span></span>              | <span data-ttu-id="2ed73-534">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-534">No</span></span>          | <span data-ttu-id="2ed73-535">**Wartość true,** (wartość domyślna) lub **False** w zależności od tego, czy odpowiednia kolumna może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="2ed73-535">**True** (the default value) or **False** depending on whether the corresponding column can have a null value.</span></span>                                                                                                                  |
| <span data-ttu-id="2ed73-536">**DefaultValue**</span><span class="sxs-lookup"><span data-stu-id="2ed73-536">**DefaultValue**</span></span>          | <span data-ttu-id="2ed73-537">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-537">No</span></span>          | <span data-ttu-id="2ed73-538">Wartość domyślna w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="2ed73-538">The default value of the corresponding column.</span></span>                                                                                                                                                                                  |
| <span data-ttu-id="2ed73-539">**Element MaxLength**</span><span class="sxs-lookup"><span data-stu-id="2ed73-539">**MaxLength**</span></span>             | <span data-ttu-id="2ed73-540">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-540">No</span></span>          | <span data-ttu-id="2ed73-541">Maksymalna długość odpowiednią kolumnę.</span><span class="sxs-lookup"><span data-stu-id="2ed73-541">The maximum length of the corresponding column.</span></span>                                                                                                                                                                                 |
| <span data-ttu-id="2ed73-542">**Wartości**</span><span class="sxs-lookup"><span data-stu-id="2ed73-542">**FixedLength**</span></span>           | <span data-ttu-id="2ed73-543">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-543">No</span></span>          | <span data-ttu-id="2ed73-544">**Wartość true,** lub **False** w zależności od tego, czy odpowiadająca wartość w kolumnie będą przechowywane jako ciąg znaków o stałej długości.</span><span class="sxs-lookup"><span data-stu-id="2ed73-544">**True** or **False** depending on whether the corresponding column value will be stored as a fixed length string.</span></span>                                                                                                              |
| <span data-ttu-id="2ed73-545">**Precyzja**</span><span class="sxs-lookup"><span data-stu-id="2ed73-545">**Precision**</span></span>             | <span data-ttu-id="2ed73-546">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-546">No</span></span>          | <span data-ttu-id="2ed73-547">Dokładność odpowiednią kolumnę.</span><span class="sxs-lookup"><span data-stu-id="2ed73-547">The precision of the corresponding column.</span></span>                                                                                                                                                                                      |
| <span data-ttu-id="2ed73-548">**Skala**</span><span class="sxs-lookup"><span data-stu-id="2ed73-548">**Scale**</span></span>                 | <span data-ttu-id="2ed73-549">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-549">No</span></span>          | <span data-ttu-id="2ed73-550">Skala odpowiednią kolumnę.</span><span class="sxs-lookup"><span data-stu-id="2ed73-550">The scale of the corresponding column.</span></span>                                                                                                                                                                                          |
| <span data-ttu-id="2ed73-551">**Unicode**</span><span class="sxs-lookup"><span data-stu-id="2ed73-551">**Unicode**</span></span>               | <span data-ttu-id="2ed73-552">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-552">No</span></span>          | <span data-ttu-id="2ed73-553">**Wartość true,** lub **False** w zależności od tego, czy odpowiadająca wartość w kolumnie będą przechowywane jako ciąg Unicode.</span><span class="sxs-lookup"><span data-stu-id="2ed73-553">**True** or **False** depending on whether the corresponding column value will be stored as a Unicode string.</span></span>                                                                                                                   |
| <span data-ttu-id="2ed73-554">**Sortowanie**</span><span class="sxs-lookup"><span data-stu-id="2ed73-554">**Collation**</span></span>             | <span data-ttu-id="2ed73-555">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-555">No</span></span>          | <span data-ttu-id="2ed73-556">Ciąg, który określa kolejność sortowania, które ma być używany w źródle danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-556">A string that specifies the collating sequence to be used in the data source.</span></span>                                                                                                                                                   |
| <span data-ttu-id="2ed73-557">**SRID**</span><span class="sxs-lookup"><span data-stu-id="2ed73-557">**SRID**</span></span>                  | <span data-ttu-id="2ed73-558">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-558">No</span></span>          | <span data-ttu-id="2ed73-559">Identyfikator odwołania przestrzennego systemu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-559">Spatial System Reference Identifier.</span></span> <span data-ttu-id="2ed73-560">Prawidłowy tylko w przypadku właściwości typów przestrzennych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-560">Valid only for properties of spatial types.</span></span> <span data-ttu-id="2ed73-561">Aby uzyskać więcej informacji, zobacz [SRID](http://en.wikipedia.org/wiki/SRID) i [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ed73-561">For more information, see [SRID](http://en.wikipedia.org/wiki/SRID) and [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span></span> |
| <span data-ttu-id="2ed73-562">**Element StoreGeneratedPattern**</span><span class="sxs-lookup"><span data-stu-id="2ed73-562">**StoreGeneratedPattern**</span></span> | <span data-ttu-id="2ed73-563">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-563">No</span></span>          | <span data-ttu-id="2ed73-564">**Brak**, **tożsamości** (jeśli odpowiadająca wartość w kolumnie jest tożsamość, która jest generowana w bazie danych) lub **obliczane** (jeśli odpowiadająca wartość w kolumnie jest obliczana w bazie danych).</span><span class="sxs-lookup"><span data-stu-id="2ed73-564">**None**, **Identity** (if the corresponding column value is an identity that is generated in the database), or **Computed** (if the corresponding column value is computed in the database).</span></span> <span data-ttu-id="2ed73-565">Nie obowiązuje dla właściwości RowType.</span><span class="sxs-lookup"><span data-stu-id="2ed73-565">Not Valid for RowType properties.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-566">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **właściwość** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-566">Any number of annotation attributes (custom XML attributes) may be applied to the **Property** element.</span></span> <span data-ttu-id="2ed73-567">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-567">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-568">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-568">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-569">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-569">Example</span></span>

<span data-ttu-id="2ed73-570">W poniższym przykładzie przedstawiono **EntityType** element z dwóch podrzędnych **właściwość** elementy:</span><span class="sxs-lookup"><span data-stu-id="2ed73-570">The following example shows an **EntityType** element with two child **Property** elements:</span></span>

``` xml
 <EntityType Name="Customers">
   <Documentation>
     <Summary>Summary here.</Summary>
     <LongDescription>Long description here.</LongDescription>
   </Documentation>
   <Key>
     <PropertyRef Name="CustomerId" />
   </Key>
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
 </EntityType>
```
 

 

## <a name="propertyref-element-ssdl"></a><span data-ttu-id="2ed73-571">Element PropertyRef (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-571">PropertyRef Element (SSDL)</span></span>

<span data-ttu-id="2ed73-572">**PropertyRef** element język definicji schematu magazynu (SSDL) odwołuje się do właściwości zdefiniowany dla elementu EntityType, aby wskazać, że właściwość wykona jedną z następujących ról:</span><span class="sxs-lookup"><span data-stu-id="2ed73-572">The **PropertyRef** element in store schema definition language (SSDL) references a property defined on an EntityType element to indicate that the property will perform one of the following roles:</span></span>

-   <span data-ttu-id="2ed73-573">Być częścią klucza podstawowego w tabeli, która **EntityType** reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="2ed73-573">Be part of the primary key of the table that the **EntityType** represents.</span></span> <span data-ttu-id="2ed73-574">Co najmniej jeden **PropertyRef** elementy mogą być używane do definiowania klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="2ed73-574">One or more **PropertyRef** elements can be used to define a primary key.</span></span> <span data-ttu-id="2ed73-575">Aby uzyskać więcej informacji zobacz element klucza.</span><span class="sxs-lookup"><span data-stu-id="2ed73-575">For more information, see Key element.</span></span>
-   <span data-ttu-id="2ed73-576">Być zakończenia zależnych lub jednostki z ograniczeniem referencyjnym.</span><span class="sxs-lookup"><span data-stu-id="2ed73-576">Be the dependent or principal end of a referential constraint.</span></span> <span data-ttu-id="2ed73-577">Aby uzyskać więcej informacji zobacz ReferentialConstraint element.</span><span class="sxs-lookup"><span data-stu-id="2ed73-577">For more information, see ReferentialConstraint element.</span></span>

<span data-ttu-id="2ed73-578">**PropertyRef** element może mieć tylko następujących elementów podrzędnych:</span><span class="sxs-lookup"><span data-stu-id="2ed73-578">The **PropertyRef** element can only have the following child elements:</span></span>

-   <span data-ttu-id="2ed73-579">Dokumentacja (zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-579">Documentation (zero or one)</span></span>
-   <span data-ttu-id="2ed73-580">Elementów adnotacji</span><span class="sxs-lookup"><span data-stu-id="2ed73-580">Annotation elements</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-581">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-581">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-582">W poniższej tabeli opisano atrybuty, które mogą być stosowane do **PropertyRef** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-582">The table below describes the attributes that can be applied to the **PropertyRef** element.</span></span>

| <span data-ttu-id="2ed73-583">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-583">Attribute Name</span></span> | <span data-ttu-id="2ed73-584">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-584">Is Required</span></span> | <span data-ttu-id="2ed73-585">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-585">Value</span></span>                                |
|:---------------|:------------|:-------------------------------------|
| <span data-ttu-id="2ed73-586">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="2ed73-586">**Name**</span></span>       | <span data-ttu-id="2ed73-587">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-587">Yes</span></span>         | <span data-ttu-id="2ed73-588">Nazwa właściwości, której dotyczy odwołanie.</span><span class="sxs-lookup"><span data-stu-id="2ed73-588">The name of the referenced property.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="2ed73-589">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **PropertyRef** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-589">Any number of annotation attributes (custom XML attributes) may be applied to the **PropertyRef** element.</span></span> <span data-ttu-id="2ed73-590">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla CSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-590">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="2ed73-591">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-591">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="2ed73-592">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-592">Example</span></span>

<span data-ttu-id="2ed73-593">W poniższym przykładzie przedstawiono **PropertyRef** element używany do definiowania klucza podstawowego, odwołując się do właściwości, która jest zdefiniowana na **EntityType** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-593">The following example shows a **PropertyRef** element used to define a primary key by referencing a property that is defined on an **EntityType** element.</span></span>

``` xml
 <EntityType Name="Customers">
   <Documentation>
     <Summary>Summary here.</Summary>
     <LongDescription>Long description here.</LongDescription>
   </Documentation>
   <Key>
     <PropertyRef Name="CustomerId" />
   </Key>
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
 </EntityType>
```
 

 

## <a name="referentialconstraint-element-ssdl"></a><span data-ttu-id="2ed73-594">Element ReferentialConstraint (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-594">ReferentialConstraint Element (SSDL)</span></span>

<span data-ttu-id="2ed73-595">**ReferentialConstraint** element język definicji schematu magazynu (SSDL) reprezentuje ograniczenie klucza obcego (nazywane również ograniczenia integralności referencyjnej) w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-595">The **ReferentialConstraint** element in store schema definition language (SSDL) represents a foreign key constraint (also called a referential integrity constraint) in the underlying database.</span></span> <span data-ttu-id="2ed73-596">Kończy się głównym i zależnym ograniczenia są odpowiednio określone przez elementy podrzędne jednostki i zależnych od ustawień lokalnych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-596">The principal and dependent ends of the constraint are specified by the Principal and Dependent child elements, respectively.</span></span> <span data-ttu-id="2ed73-597">Kolumn, które uczestniczą w głównym i zależnym kończy się są przywoływane z elementami PropertyRef.</span><span class="sxs-lookup"><span data-stu-id="2ed73-597">Columns that participate in the principal and dependent ends are referenced with PropertyRef elements.</span></span>

<span data-ttu-id="2ed73-598">**ReferentialConstraint** element jest podrzędnym elementem opcjonalnym elementu Association.</span><span class="sxs-lookup"><span data-stu-id="2ed73-598">The **ReferentialConstraint** element is an optional child element of the Association element.</span></span> <span data-ttu-id="2ed73-599">Jeśli **ReferentialConstraint** element nie jest używany do mapowania ograniczenie klucza obcego, który jest określony w **skojarzenia** AssociationSetMapping element musi być użyty w tym elemencie.</span><span class="sxs-lookup"><span data-stu-id="2ed73-599">If a **ReferentialConstraint** element is not used to map the foreign key constraint that is specified in the **Association** element, an AssociationSetMapping element must be used to do this.</span></span>

<span data-ttu-id="2ed73-600">**ReferentialConstraint** element może mieć następujące elementy podrzędne:</span><span class="sxs-lookup"><span data-stu-id="2ed73-600">The **ReferentialConstraint** element can have the following child elements:</span></span>

-   <span data-ttu-id="2ed73-601">Dokumentacja (zero lub jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-601">Documentation (zero or one)</span></span>
-   <span data-ttu-id="2ed73-602">Podmiot zabezpieczeń (dokładnie jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-602">Principal (exactly one)</span></span>
-   <span data-ttu-id="2ed73-603">Zależnych od ustawień lokalnych (dokładnie jeden)</span><span class="sxs-lookup"><span data-stu-id="2ed73-603">Dependent (exactly one)</span></span>
-   <span data-ttu-id="2ed73-604">Elementów adnotacji (zero lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-604">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-605">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-605">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-606">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **ReferentialConstraint** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-606">Any number of annotation attributes (custom XML attributes) may be applied to the **ReferentialConstraint** element.</span></span> <span data-ttu-id="2ed73-607">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-607">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-608">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-608">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="2ed73-609">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-609">Example</span></span>

<span data-ttu-id="2ed73-610">W poniższym przykładzie przedstawiono **skojarzenia** element, który używa **ReferentialConstraint** elementu, aby określić kolumny, które uczestniczą w **klucza Obcego\_CustomerOrders**  ograniczenie klucza obcego:</span><span class="sxs-lookup"><span data-stu-id="2ed73-610">The following example shows an **Association** element that uses a **ReferentialConstraint** element to specify the columns that participate in the **FK\_CustomerOrders** foreign key constraint:</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```

## <a name="returntype-element-ssdl"></a><span data-ttu-id="2ed73-611">Element ReturnType (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-611">ReturnType Element (SSDL)</span></span>

<span data-ttu-id="2ed73-612">**ReturnType** element język definicji schematu magazynu (SSDL) określa typ zwracany dla funkcji, która jest zdefiniowana w **funkcja** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-612">The **ReturnType** element in store schema definition language (SSDL) specifies the return type for a function that is defined in a **Function** element.</span></span> <span data-ttu-id="2ed73-613">Można również określić typ zwracany z funkcji **ReturnType** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-613">A function return type can also be specified with a **ReturnType** attribute.</span></span>

<span data-ttu-id="2ed73-614">Zwracany typ funkcji jest określony za pomocą **typu** atrybutu lub **ReturnType** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-614">The return type of a function is specified with the **Type** attribute or the **ReturnType** element.</span></span>

<span data-ttu-id="2ed73-615">**ReturnType** element może mieć następujące elementy podrzędne:</span><span class="sxs-lookup"><span data-stu-id="2ed73-615">The **ReturnType** element can have the following child elements:</span></span>

- <span data-ttu-id="2ed73-616">Typ CollectionType (po jednym)</span><span class="sxs-lookup"><span data-stu-id="2ed73-616">CollectionType (one)</span></span>  

> [!NOTE]
> <span data-ttu-id="2ed73-617">Dowolna liczba atrybutów adnotacji (niestandardowe atrybuty XML) można stosować do **ReturnType** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-617">Any number of annotation attributes (custom XML attributes) may be applied to the **ReturnType** element.</span></span> <span data-ttu-id="2ed73-618">Jednak atrybutów niestandardowych, które nie mogą należeć do przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-618">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="2ed73-619">W pełni kwalifikowanej nazwy dowolne dwa atrybuty niestandardowe nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-619">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="2ed73-620">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-620">Example</span></span>

<span data-ttu-id="2ed73-621">W poniższym przykładzie użyto **funkcja** zwracającego Kolekcja wierszy.</span><span class="sxs-lookup"><span data-stu-id="2ed73-621">The following example uses a **Function** that returns a collection of rows.</span></span>

``` xml
   <Function Name="GetProducts" IsComposable="true" Schema="dbo">
     <ReturnType>
       <CollectionType>
         <RowType>
           <Property Name="ProductID" Type="int" Nullable="false" />
           <Property Name="CategoryID" Type="bigint" Nullable="false" />
           <Property Name="ProductName" Type="nvarchar" MaxLength="40" Nullable="false" />
           <Property Name="UnitPrice" Type="money" />
           <Property Name="Discontinued" Type="bit" />
         </RowType>
       </CollectionType>
     </ReturnType>
   </Function>
```


## <a name="rowtype-element-ssdl"></a><span data-ttu-id="2ed73-622">Element RowType (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-622">RowType Element (SSDL)</span></span>

<span data-ttu-id="2ed73-623">A **RowType** element język definicji schematu magazynu (SSDL) definiuje strukturę nienazwane jako zwracany typ funkcji zdefiniowanych w magazynie.</span><span class="sxs-lookup"><span data-stu-id="2ed73-623">A **RowType** element in store schema definition language (SSDL) defines an unnamed structure as a return type for a function defined in the store.</span></span>

<span data-ttu-id="2ed73-624">A **RowType** element jest elementem podrzędnym **CollectionType** elementu:</span><span class="sxs-lookup"><span data-stu-id="2ed73-624">A **RowType** element is the child element of **CollectionType** element:</span></span>

<span data-ttu-id="2ed73-625">A **RowType** element może mieć następujące elementy podrzędne:</span><span class="sxs-lookup"><span data-stu-id="2ed73-625">A **RowType** element can have the following child elements:</span></span>

- <span data-ttu-id="2ed73-626">Właściwości (jeden lub więcej)</span><span class="sxs-lookup"><span data-stu-id="2ed73-626">Property (one or more)</span></span>  

### <a name="example"></a><span data-ttu-id="2ed73-627">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-627">Example</span></span>

<span data-ttu-id="2ed73-628">W poniższym przykładzie pokazano funkcję magazynu, która używa **CollectionType** elementu, aby określić, że funkcja zwraca Kolekcja wierszy (jak określono w **RowType** elementu).</span><span class="sxs-lookup"><span data-stu-id="2ed73-628">The following example shows a store function that uses a **CollectionType** element to specify that the function returns a collection of rows (as specified in the **RowType** element).</span></span>


``` xml
   <Function Name="GetProducts" IsComposable="true" Schema="dbo">
     <ReturnType>
       <CollectionType>
         <RowType>
           <Property Name="ProductID" Type="int" Nullable="false" />
           <Property Name="CategoryID" Type="bigint" Nullable="false" />
           <Property Name="ProductName" Type="nvarchar" MaxLength="40" Nullable="false" />
           <Property Name="UnitPrice" Type="money" />
           <Property Name="Discontinued" Type="bit" />
         </RowType>
       </CollectionType>
     </ReturnType>
   </Function>
```
 

 

## <a name="schema-element-ssdl"></a><span data-ttu-id="2ed73-629">Element schematu (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-629">Schema Element (SSDL)</span></span>

<span data-ttu-id="2ed73-630">**Schematu** element w język definicji schematu magazynu (SSDL) jest głównym elementem definicję modelu magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-630">The **Schema** element in store schema definition language (SSDL) is the root element of a storage model definition.</span></span> <span data-ttu-id="2ed73-631">Zawiera definicje dla obiektów, funkcji i kontenerów, które tworzą model magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-631">It contains definitions for the objects, functions, and containers that make up a storage model.</span></span>

<span data-ttu-id="2ed73-632">**Schematu** element może zawierać zero lub więcej z następujących elementów podrzędnych:</span><span class="sxs-lookup"><span data-stu-id="2ed73-632">The **Schema** element may contain zero or more of the following child elements:</span></span>

-   <span data-ttu-id="2ed73-633">Skojarzenie</span><span class="sxs-lookup"><span data-stu-id="2ed73-633">Association</span></span>
-   <span data-ttu-id="2ed73-634">Typ EntityType</span><span class="sxs-lookup"><span data-stu-id="2ed73-634">EntityType</span></span>
-   <span data-ttu-id="2ed73-635">Obiekt EntityContainer</span><span class="sxs-lookup"><span data-stu-id="2ed73-635">EntityContainer</span></span>
-   <span data-ttu-id="2ed73-636">Funkcja</span><span class="sxs-lookup"><span data-stu-id="2ed73-636">Function</span></span>

<span data-ttu-id="2ed73-637">**Schematu** element używa **Namespace** atrybut do definiowania przestrzeni nazw dla obiektów typu i skojarzenia jednostki w modelu magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-637">The **Schema** element uses the **Namespace** attribute to define the namespace for the entity type and association objects in a storage model.</span></span> <span data-ttu-id="2ed73-638">W przestrzeni nazw nie dwa obiekty mogą mieć takiej samej nazwie.</span><span class="sxs-lookup"><span data-stu-id="2ed73-638">Within a namespace, no two objects can have the same name.</span></span>

<span data-ttu-id="2ed73-639">Przestrzeń nazw modelu magazynu różni się od przestrzeni nazw XML **schematu** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-639">A storage model namespace is different from the XML namespace of the **Schema** element.</span></span> <span data-ttu-id="2ed73-640">Przestrzeń nazw modelu magazynu (zgodnie z definicją **Namespace** atrybutu) to logiczny kontener przeznaczony dla typów jednostek i typów skojarzenia.</span><span class="sxs-lookup"><span data-stu-id="2ed73-640">A storage model namespace (as defined by the **Namespace** attribute) is a logical container for entity types and association types.</span></span> <span data-ttu-id="2ed73-641">Przestrzeń nazw XML (wskazywanym przez **xmlns** atrybutu) z **schematu** element jest domyślny obszar nazw dla elementów podrzędnych i atrybutów **schematu** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-641">The XML namespace (indicated by the **xmlns** attribute) of a **Schema** element is the default namespace for child elements and attributes of the **Schema** element.</span></span> <span data-ttu-id="2ed73-642">Obszary nazw XML w postaci http://schemas.microsoft.com/ado/YYYY/MM/edm/ssdl (gdzie RRRR i MM stanowi rok i miesiąc odpowiednio) są zarezerwowane dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-642">XML namespaces of the form http://schemas.microsoft.com/ado/YYYY/MM/edm/ssdl (where YYYY and MM represent a year and month respectively) are reserved for SSDL.</span></span> <span data-ttu-id="2ed73-643">Niestandardowe elementy i atrybuty nie może być w przestrzeni nazw, które mają postać.</span><span class="sxs-lookup"><span data-stu-id="2ed73-643">Custom elements and attributes cannot be in namespaces that have this form.</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="2ed73-644">Odpowiednie atrybuty</span><span class="sxs-lookup"><span data-stu-id="2ed73-644">Applicable Attributes</span></span>

<span data-ttu-id="2ed73-645">W poniższej tabeli opisano atrybuty mogą być stosowane do **schematu** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-645">The table below describes the attributes can be applied to the **Schema** element.</span></span>

| <span data-ttu-id="2ed73-646">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2ed73-646">Attribute Name</span></span>            | <span data-ttu-id="2ed73-647">Jest wymagany</span><span class="sxs-lookup"><span data-stu-id="2ed73-647">Is Required</span></span> | <span data-ttu-id="2ed73-648">Wartość</span><span class="sxs-lookup"><span data-stu-id="2ed73-648">Value</span></span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|:--------------------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-649">**Namespace**</span><span class="sxs-lookup"><span data-stu-id="2ed73-649">**Namespace**</span></span>             | <span data-ttu-id="2ed73-650">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-650">Yes</span></span>         | <span data-ttu-id="2ed73-651">Przestrzeń nazw modelu magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-651">The namespace of the storage model.</span></span> <span data-ttu-id="2ed73-652">Wartość **Namespace** atrybut jest używany w celu utworzenia w pełni kwalifikowana nazwa typu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-652">The value of the **Namespace** attribute is used to form the fully qualified name of a type.</span></span> <span data-ttu-id="2ed73-653">Na przykład jeśli **EntityType** o nazwie *klienta* znajduje się w przestrzeni nazw ExampleModel.Store, a następnie w pełni kwalifikowana nazwa **EntityType** jest ExampleModel.Store.Customer.</span><span class="sxs-lookup"><span data-stu-id="2ed73-653">For example, if an **EntityType** named *Customer* is in the ExampleModel.Store namespace, then the fully qualified name of the **EntityType** is ExampleModel.Store.Customer.</span></span> <br/> <span data-ttu-id="2ed73-654">Nie można użyć następujących ciągów jako wartość pozycji **Namespace** atrybut: **systemu**, **przejściowy**, lub **Edm**.</span><span class="sxs-lookup"><span data-stu-id="2ed73-654">The following strings cannot be used as the value for the **Namespace** attribute: **System**, **Transient**, or **Edm**.</span></span> <span data-ttu-id="2ed73-655">Wartość **Namespace** atrybut nie może być taka sama jak wartość **Namespace** atrybutu w elemencie CSDL Schema.</span><span class="sxs-lookup"><span data-stu-id="2ed73-655">The value for the **Namespace** attribute cannot be the same as the value for the **Namespace** attribute in the CSDL Schema element.</span></span> |
| <span data-ttu-id="2ed73-656">**Alias**</span><span class="sxs-lookup"><span data-stu-id="2ed73-656">**Alias**</span></span>                 | <span data-ttu-id="2ed73-657">Nie</span><span class="sxs-lookup"><span data-stu-id="2ed73-657">No</span></span>          | <span data-ttu-id="2ed73-658">Identyfikator używany zamiast nazwy przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="2ed73-658">An identifier used in place of the namespace name.</span></span> <span data-ttu-id="2ed73-659">Na przykład jeśli **EntityType** o nazwie *klienta* znajduje się w przestrzeni nazw ExampleModel.Store i wartość **Alias** atrybut jest *StorageModel*, wówczas można użyć StorageModel.Customer jako w pełni kwalifikowana nazwa **typu EntityType.**</span><span class="sxs-lookup"><span data-stu-id="2ed73-659">For example, if an **EntityType** named *Customer* is in the ExampleModel.Store namespace and the value of the **Alias** attribute is *StorageModel*, then you can use StorageModel.Customer as the fully qualified name of the **EntityType.**</span></span>                                                                                                                                                                                                                                                                                    |
| <span data-ttu-id="2ed73-660">**Dostawcy**</span><span class="sxs-lookup"><span data-stu-id="2ed73-660">**Provider**</span></span>              | <span data-ttu-id="2ed73-661">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-661">Yes</span></span>         | <span data-ttu-id="2ed73-662">Dostawca danych.</span><span class="sxs-lookup"><span data-stu-id="2ed73-662">The data provider.</span></span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| <span data-ttu-id="2ed73-663">**ProviderManifestToken**</span><span class="sxs-lookup"><span data-stu-id="2ed73-663">**ProviderManifestToken**</span></span> | <span data-ttu-id="2ed73-664">Tak</span><span class="sxs-lookup"><span data-stu-id="2ed73-664">Yes</span></span>         | <span data-ttu-id="2ed73-665">Token, który wskazuje dostawcy, które manifest dostawcy, aby powrócić.</span><span class="sxs-lookup"><span data-stu-id="2ed73-665">A token that indicates to the provider which provider manifest to return.</span></span> <span data-ttu-id="2ed73-666">Nie format tokenu jest zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="2ed73-666">No format for the token is defined.</span></span> <span data-ttu-id="2ed73-667">Wartości dla tokenu są definiowane przez dostawcę.</span><span class="sxs-lookup"><span data-stu-id="2ed73-667">Values for the token are defined by the provider.</span></span> <span data-ttu-id="2ed73-668">Uzyskać informacji dotyczących tokenów manifestu dostawcy programu SQL Server zobacz SqlClient programu Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2ed73-668">For information about SQL Server provider manifest tokens, see SqlClient for Entity Framework.</span></span>                                                                                                                                                                                                                                                                                                                        |

 

### <a name="example"></a><span data-ttu-id="2ed73-669">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-669">Example</span></span>

<span data-ttu-id="2ed73-670">W poniższym przykładzie przedstawiono **schematu** element, który zawiera **EntityContainer** element, dwa **EntityType** elementów, a drugi **skojarzenia** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-670">The following example shows a **Schema** element that contains an **EntityContainer** element, two **EntityType** elements, and one **Association** element.</span></span>

``` xml
 <Schema Namespace="ExampleModel.Store"
       Alias="Self" Provider="System.Data.SqlClient"
       ProviderManifestToken="2008"
       xmlns="http://schemas.microsoft.com/ado/2009/11/edm/ssdl">
   <EntityContainer Name="ExampleModelStoreContainer">
     <EntitySet Name="Customers"
                EntityType="ExampleModel.Store.Customers"
                Schema="dbo" />
     <EntitySet Name="Orders"
                EntityType="ExampleModel.Store.Orders"
                Schema="dbo" />
     <AssociationSet Name="FK_CustomerOrders"
                     Association="ExampleModel.Store.FK_CustomerOrders">
       <End Role="Customers" EntitySet="Customers" />
       <End Role="Orders" EntitySet="Orders" />
     </AssociationSet>
   </EntityContainer>
   <EntityType Name="Customers">
     <Documentation>
       <Summary>Summary here.</Summary>
       <LongDescription>Long description here.</LongDescription>
     </Documentation>
     <Key>
       <PropertyRef Name="CustomerId" />
     </Key>
     <Property Name="CustomerId" Type="int" Nullable="false" />
     <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
   </EntityType>
   <EntityType Name="Orders" xmlns:c="http://CustomNamespace">
     <Key>
       <PropertyRef Name="OrderId" />
     </Key>
     <Property Name="OrderId" Type="int" Nullable="false"
               c:CustomAttribute="someValue"/>
     <Property Name="ProductId" Type="int" Nullable="false" />
     <Property Name="Quantity" Type="int" Nullable="false" />
     <Property Name="CustomerId" Type="int" Nullable="false" />
     <c:CustomElement>
       Custom data here.
     </c:CustomElement>
   </EntityType>
   <Association Name="FK_CustomerOrders">
     <End Role="Customers"
          Type="ExampleModel.Store.Customers" Multiplicity="1">
       <OnDelete Action="Cascade" />
     </End>
     <End Role="Orders"
          Type="ExampleModel.Store.Orders" Multiplicity="*" />
     <ReferentialConstraint>
       <Principal Role="Customers">
         <PropertyRef Name="CustomerId" />
       </Principal>
       <Dependent Role="Orders">
         <PropertyRef Name="CustomerId" />
       </Dependent>
     </ReferentialConstraint>
   </Association>
   <Function Name="UpdateOrderQuantity"
             Aggregate="false"
             BuiltIn="false"
             NiladicFunction="false"
             IsComposable="false"
             ParameterTypeSemantics="AllowImplicitConversion"
             Schema="dbo">
     <Parameter Name="orderId" Type="int" Mode="In" />
     <Parameter Name="newQuantity" Type="int" Mode="In" />
   </Function>
   <Function Name="UpdateProductInOrder" IsComposable="false">
     <CommandText>
       UPDATE Orders
       SET ProductId = @productId
       WHERE OrderId = @orderId;
     </CommandText>
     <Parameter Name="productId"
                Mode="In"
                Type="int"/>
     <Parameter Name="orderId"
                Mode="In"
                Type="int"/>
   </Function>
 </Schema>
```
 

 

## <a name="annotation-attributes"></a><span data-ttu-id="2ed73-671">Atrybuty adnotacji</span><span class="sxs-lookup"><span data-stu-id="2ed73-671">Annotation Attributes</span></span>

<span data-ttu-id="2ed73-672">Atrybuty adnotacji w język definicji schematu magazynu (SSDL) są niestandardowych atrybutów XML w modelu magazynu, które zapewniają dodatkowe metadane na temat elementów w modelu magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-672">Annotation attributes in store schema definition language (SSDL) are custom XML attributes in the storage model that provide extra metadata about the elements in the storage model.</span></span> <span data-ttu-id="2ed73-673">Oprócz prawidłowe struktury XML, obowiązują następujące ograniczenia adnotacji atrybutów:</span><span class="sxs-lookup"><span data-stu-id="2ed73-673">In addition to having valid XML structure, the following constraints apply to annotation attributes:</span></span>

-   <span data-ttu-id="2ed73-674">Atrybuty adnotacji nie może być w przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-674">Annotation attributes must not be in any XML namespace that is reserved for SSDL.</span></span>
-   <span data-ttu-id="2ed73-675">W pełni kwalifikowanej nazwy wszelkie atrybuty dwóch adnotacji nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-675">The fully-qualified names of any two annotation attributes must not be the same.</span></span>

<span data-ttu-id="2ed73-676">Więcej niż jeden atrybut adnotacji można stosować do danego elementu SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-676">More than one annotation attribute may be applied to a given SSDL element.</span></span> <span data-ttu-id="2ed73-677">W czasie wykonywania przy użyciu klas w przestrzeni nazw System.Data.Metadata.Edm możliwy jest metadanych elementów adnotacji.</span><span class="sxs-lookup"><span data-stu-id="2ed73-677">Metadata contained in annotation elements can be accessed at runtime by using classes in the System.Data.Metadata.Edm namespace.</span></span>

### <a name="example"></a><span data-ttu-id="2ed73-678">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-678">Example</span></span>

<span data-ttu-id="2ed73-679">W poniższym przykładzie pokazano element EntityType, który ma atrybut adnotacja zastosowana do **OrderId** właściwości.</span><span class="sxs-lookup"><span data-stu-id="2ed73-679">The following example shows an EntityType element that has an annotation attribute applied to the **OrderId** property.</span></span> <span data-ttu-id="2ed73-680">Przykład pokazują również dodawane do elementu adnotacji **EntityType** elementu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-680">The example also show an annotation element added to the **EntityType** element.</span></span>

``` xml
 <EntityType Name="Orders" xmlns:c="http://CustomNamespace">
   <Key>
     <PropertyRef Name="OrderId" />
   </Key>
   <Property Name="OrderId" Type="int" Nullable="false"
             c:CustomAttribute="someValue"/>
   <Property Name="ProductId" Type="int" Nullable="false" />
   <Property Name="Quantity" Type="int" Nullable="false" />
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <c:CustomElement>
     Custom data here.
   </c:CustomElement>
 </EntityType>
```
 

 

## <a name="annotation-elements-ssdl"></a><span data-ttu-id="2ed73-681">Elementów adnotacji (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-681">Annotation Elements (SSDL)</span></span>

<span data-ttu-id="2ed73-682">Elementy adnotacji w język definicji schematu magazynu (SSDL) są niestandardowe elementy XML w modelu magazynu, które zapewniają dodatkowe metadane na temat modelu magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ed73-682">Annotation elements in store schema definition language (SSDL) are custom XML elements in the storage model that provide extra metadata about the storage model.</span></span> <span data-ttu-id="2ed73-683">Oprócz prawidłowe struktury XML, elementów adnotacji obowiązują następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="2ed73-683">In addition to having valid XML structure, the following constraints apply to annotation elements:</span></span>

-   <span data-ttu-id="2ed73-684">Elementów adnotacji nie może być w przestrzeni nazw XML, który jest zarezerwowany dla SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-684">Annotation elements must not be in any XML namespace that is reserved for SSDL.</span></span>
-   <span data-ttu-id="2ed73-685">W pełni kwalifikowanej nazwy dowolne elementy dwóch adnotacji nie może być taka sama.</span><span class="sxs-lookup"><span data-stu-id="2ed73-685">The fully-qualified names of any two annotation elements must not be the same.</span></span>
-   <span data-ttu-id="2ed73-686">Adnotacja elementów musi występować po wszystkich innych elementów podrzędnych danego elementu SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-686">Annotation elements must appear after all other child elements of a given SSDL element.</span></span>

<span data-ttu-id="2ed73-687">Więcej niż jeden element adnotacji może być elementem podrzędnym danego elementu SSDL.</span><span class="sxs-lookup"><span data-stu-id="2ed73-687">More than one annotation element may be a child of a given SSDL element.</span></span> <span data-ttu-id="2ed73-688">Począwszy od programu .NET Framework w wersji 4, metadanych elementów adnotacji są dostępne w czasie wykonywania przy użyciu klas w przestrzeni nazw System.Data.Metadata.Edm.</span><span class="sxs-lookup"><span data-stu-id="2ed73-688">Starting with the .NET Framework version 4, metadata contained in annotation elements can be accessed at runtime by using classes in the System.Data.Metadata.Edm namespace.</span></span>

### <a name="example"></a><span data-ttu-id="2ed73-689">Przykład</span><span class="sxs-lookup"><span data-stu-id="2ed73-689">Example</span></span>

<span data-ttu-id="2ed73-690">W poniższym przykładzie pokazano element EntityType, który ma element adnotacji (**CustomElement**).</span><span class="sxs-lookup"><span data-stu-id="2ed73-690">The following example shows an EntityType element that has an annotation element (**CustomElement**).</span></span> <span data-ttu-id="2ed73-691">W przykładzie pokazano również zastosować atrybut adnotacji **OrderId** właściwości.</span><span class="sxs-lookup"><span data-stu-id="2ed73-691">The example also shows an annotation attribute applied to the **OrderId** property.</span></span>

``` xml
 <EntityType Name="Orders" xmlns:c="http://CustomNamespace">
   <Key>
     <PropertyRef Name="OrderId" />
   </Key>
   <Property Name="OrderId" Type="int" Nullable="false"
             c:CustomAttribute="someValue"/>
   <Property Name="ProductId" Type="int" Nullable="false" />
   <Property Name="Quantity" Type="int" Nullable="false" />
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <c:CustomElement>
     Custom data here.
   </c:CustomElement>
 </EntityType>
```
 

 

## <a name="facets-ssdl"></a><span data-ttu-id="2ed73-692">Zestawy reguł (SSDL)</span><span class="sxs-lookup"><span data-stu-id="2ed73-692">Facets (SSDL)</span></span>

<span data-ttu-id="2ed73-693">Aspekty w język definicji schematu magazynu (SSDL) reprezentują ograniczenia dotyczące typów kolumn, które są określone w elementach właściwości.</span><span class="sxs-lookup"><span data-stu-id="2ed73-693">Facets in store schema definition language (SSDL) represent constraints on column types that are specified in Property elements.</span></span> <span data-ttu-id="2ed73-694">Zestawy reguł są implementowane jako atrybuty XML w **właściwość** elementów.</span><span class="sxs-lookup"><span data-stu-id="2ed73-694">Facets are implemented as XML attributes on **Property** elements.</span></span>

<span data-ttu-id="2ed73-695">W poniższej tabeli opisano aspekty, które są obsługiwane przez SSDL:</span><span class="sxs-lookup"><span data-stu-id="2ed73-695">The following table describes the facets that are supported in SSDL:</span></span>

| <span data-ttu-id="2ed73-696">Zestaw reguł</span><span class="sxs-lookup"><span data-stu-id="2ed73-696">Facet</span></span>           | <span data-ttu-id="2ed73-697">Opis</span><span class="sxs-lookup"><span data-stu-id="2ed73-697">Description</span></span>                                                                                                                                                                                                                                                 |
|:----------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ed73-698">**Sortowanie**</span><span class="sxs-lookup"><span data-stu-id="2ed73-698">**Collation**</span></span>   | <span data-ttu-id="2ed73-699">Określa kolejność sortowania (lub sekwencji sortowania) do użycia podczas przeprowadzania porównania i kolejność operacji na wartościach właściwości.</span><span class="sxs-lookup"><span data-stu-id="2ed73-699">Specifies the collating sequence (or sorting sequence) to be used when performing comparison and ordering operations on values of the property.</span></span>                                                                                                             |
| <span data-ttu-id="2ed73-700">**Wartości**</span><span class="sxs-lookup"><span data-stu-id="2ed73-700">**FixedLength**</span></span> | <span data-ttu-id="2ed73-701">Określa, czy długość wartości kolumny mogą się różnić.</span><span class="sxs-lookup"><span data-stu-id="2ed73-701">Specifies whether the length of the column value can vary.</span></span>                                                                                                                                                                                                  |
| <span data-ttu-id="2ed73-702">**Element MaxLength**</span><span class="sxs-lookup"><span data-stu-id="2ed73-702">**MaxLength**</span></span>   | <span data-ttu-id="2ed73-703">Określa maksymalną długość wartości kolumny.</span><span class="sxs-lookup"><span data-stu-id="2ed73-703">Specifies the maximum length of the column value.</span></span>                                                                                                                                                                                                           |
| <span data-ttu-id="2ed73-704">**Precyzja**</span><span class="sxs-lookup"><span data-stu-id="2ed73-704">**Precision**</span></span>   | <span data-ttu-id="2ed73-705">Dla właściwości typu **dziesiętna**, określa liczbę cyfr, może mieć wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="2ed73-705">For properties of type **Decimal**, specifies the number of digits a property value can have.</span></span> <span data-ttu-id="2ed73-706">Dla właściwości typu **czasu**, **daty/godziny**, i **DateTimeOffset**, określa liczbę cyfr ułamkowych części sekundy w wartości kolumny.</span><span class="sxs-lookup"><span data-stu-id="2ed73-706">For properties of type **Time**, **DateTime**, and **DateTimeOffset**, specifies the number of digits for the fractional part of seconds of the column value.</span></span> |
| <span data-ttu-id="2ed73-707">**Skala**</span><span class="sxs-lookup"><span data-stu-id="2ed73-707">**Scale**</span></span>       | <span data-ttu-id="2ed73-708">Określa liczbę cyfr po prawej stronie przecinka dziesiętnego dla wartości kolumny.</span><span class="sxs-lookup"><span data-stu-id="2ed73-708">Specifies the number of digits to the right of the decimal point for the column value.</span></span>                                                                                                                                                                      |
| <span data-ttu-id="2ed73-709">**Unicode**</span><span class="sxs-lookup"><span data-stu-id="2ed73-709">**Unicode**</span></span>     | <span data-ttu-id="2ed73-710">Wskazuje, czy wartość kolumny jest zapisywana w formacie Unicode.</span><span class="sxs-lookup"><span data-stu-id="2ed73-710">Indicates whether the column value is stored as Unicode.</span></span>                                                                                                                                                                                                    |