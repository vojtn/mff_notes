
# Procesy vývoje software
Proces vývoje SW je strukturovaná sada aktivit nutná k vývoji softwarového systému. Dělí se na čtyři základní fáze, které se od sebe liší svým cílem: 
- **Analýza** (co se má vytvořit),
- **Návrh** (jak se to technicky vytvoří) 
- **Implementace** (samotné programování)
- **Testování** (ověření funkčnosti a kvality).

| Model vývoje | Charakteristika | Výhody | Nevýhody |
| --- | --- | --- | --- |
| **Plan-driven (Vodopád)** | Všechny aktivity se plánují striktně předem. | Jasně definované úkoly a milníky. | Velmi nákladné a pomalé reakce na změny požadavků stakeholderů. |
| **Agile / Iterativní** | Plánování je inkrementální a průběžné.  | Rychlejší dodání, snadná reakce na změny, častý feedback. | Hůře měřitelný progres pro management, riziko zhoršení struktury kódu časem. |

---

# Analýza požadavků
Cílem analýzy je formulace vize projektu a porozumění těm, pro které se systém tvoří, tedy identifikaze stakeholderů a také formalizace požadavků. 

## **Stakeholder** 
Jakákoliv osoba nebo skupina, která má na projektu zájem nebo jím bude ovlivněna. Je kriticky důležité identifikovat *všechny*, protože opomenutý stakeholder znamená opomenutý požadavek, což vede k chybám v pozdějších fázích vývoje.

**Techniky:** pro sběr dat:
- *Interviews* (otevřené a uzavřené rozhovory pro hloubkové zjištění potřeb)
- *Event-storming* (rychlý skupinový workshop pro vizuální mapování byznys procesů).
- *Sketching*
- *Prototyping* - mock up, HTML nebo Figma

## Požadavky
- **Funkční** (co má systém dělat, např. "uživatel se může přihlásit") 
- **Kvalitativní / Ne-funkční** (jak dobře to má dělat, např. bezpečnost, výkon, rozšiřitelnost).

### Funkční požadavky
Způsoby specifikace funkčních požadavků:

* **User Story:** (User requirements) 
Strukturovaná věta formátu: *WHO (Jako [role]), WHAT (chci [akce]), WHY (abych [hodnota/důvod])*.

```
As a publisher, I need to register a published dataset into the catalog so that consumers 
can easily find the dataset using various search criteria and see the details about the 
dataset, including the download link
```


* **Use Case:** (System requirements) 
Strukturovaný textový scénář obsahující: 
- Actors 
- Preconditions
- Basic flow (hlavní scénář)
- Alternative flows (odbočky/chyby)
- Postconditions
Vlastnosti
- větší detail
- popsán scénář interakce se systémem
- popisuje jednotlivé kroky

```
Use Case Description:
    Brief summary of the use case
Actor:
    Description of the primary actor involved in the use case
Goal:
    Clear and concise goal of the use case
Preconditions:
    Conditions that must be met before the use case can occur
Triggers:
    Events that trigger the use case
Description:
    Detailed description of the use case
Postconditions:
    Conditions that must be met after the use case is complete
Extensions:
    Additional information or variations of the use case
```

```
## Creating a new application
### Actor: 
Applicant

### Goal:
The aplicant wants to create a new aplication for a study programme at the faculty.

### Precondition:
The applicant succesfully registered or login with previsouly registered account.
The faculty has opened the application procces for applicants.

### Basic flow:
- System Login:
  - The applicant can create a new application, after his registration or login to student system
- Create application
  - The applicant chooses study programme and specify all needed data such as language of programme and form of study. 
- System response
    - After applicant confirmation, the system stores provided data to the internal system and sends notification about succesfull creation of application.
    
### Alternative Flow:
During creation of the application the applicant can change his mind and not finish the procces or cancel it, in both cases data will not be stored.

### Postconditions:
The applicant is notified about the succesful creation of application. The valid application is stored in system database. 

### Exceptions:
The applicant can provide wrong information.
The application can be created after deadline.

### Special Requirements:
The applicant has to create it in time, that means before deadline specified by the faculty. 

```

* **UML Use Case diagram:** Zobrazuje aktéry a případy užití, využívá vazby *include* (nutná závislost, vkládá povinné chování) a *extend* (volitelné rozšíření chování).

* **UML Activity diagram:** Modeluje procesy pomocí *executable, control* a *object nodes*.

* **UML State diagram:** Modeluje životní cyklus objektu pomocí stavů (states) a přechodů.

### Nefunkční požadavky
- rozšířitelsnot
- avalability
- scalability
- performance
- security
- testability

## Doménový model
Slouží k utřídění a pochopení byznys konceptů a vztahů v dané doméně. Poskytuje jednotný jazyk napříč technickým i netechnickým týmem.
Také se někdy nazývá Konceptuální model nebo Business vacabulary

* **UML Diagram tříd:** Model se vizualizuje pomocí klíčových prvků: *třída, atribut, asociace, multiplicity atributů a tříd, asociační třídy a generalizace/specializace (dědičnost)*.

* **Pravidla definice:** Názvy tříd, atributů a asociací nesmí vznikat ad-hoc. Musí být striktně ukotveny v byznys slovníku (jazyku non-technical lidí v organizaci). Třídy musí mít dobrou sémantickou definici, aby každý člen týmu chápal jejich přesný význam.


---

# Návrh / Design
- návrh architektury
- datových struktur
- interfaces/API
- návrh UX/UI

## Architektura
Architektura je základní struktura softwarového systému, která definuje jeho hlavní části (moduly/komponenty), jejich zodpovědnosti a vztahy mezi nimi.

### Kroky při návrhu architektury

Při návrhu architektury z požadavků (User Stories / Use Cases) postupujeme takto:

1. **Identifikace responsibilities:** Rozdělení funkcionality na menší části pro prezentační, aplikační (business) a datovou vrstvu.
2. **Dekompozice do modulů:** Rozdělení systému na základní moduly kódu (případně další zanořená dekompozice).
3. **Návrh závislostí:** Určení, jak spolu moduly komunikují a závisí na sobě.
4. **Návrh architektury:** Výběr vhodného architektonického stylu.

### Typy architektury (Styly)

* **Layered monolith:** Tradiční monolit rozdělený horizontálně na technické vrstvy (Prezentační -> Business -> Datová).

* **Modularized monolith:** Monolit rozdělený vertikálně podle byznys domén (např. modul Objednávky, modul Uživatelé), přičemž každý modul má uvnitř své vlastní vrstvy.

* **Service-based architecture:** Systém je rozdělen na samostatně běžící služby (např. mikroservices), které spolu komunikují po síti.


### Principy návrhu
Při návrhu musíme uplatňovat tyto principy:

* **High cohesion (Vysoká soudržnost):** Jak moc spolu souvisí prvky uvnitř jednoho modulu (modul by měl dělat jen jednu konkrétní věc).
* **Low coupling (Nízká provázanost):** Jak moc jsou moduly závislé jeden na druhém (chceme minimalizovat závislosti).
* **Separation of concerns:** Rozdělení systému do částí tak, aby se každá starala o svůj specifický problém (např. oddělení výpočtů od vykreslování UI).
* **Information hiding:** Zapouzdření a skrytí interních implementačních detailů modulu před vnějším světem.
* **Layering:** Organizace kódu do hierarchických vrstev, kde vyšší vrstva volá nižší, ale ne naopak.
* **Domain boundaries:** Hranice modulů by měly respektovat logické hranice samotného byznysu (domény).


## C4 model
Jednoduchý vizuální jazyk pro popis a znázornění architektury v různých úrovních detailu.

* **System:** Nejvyšší pohled na to, jak systém zapadá do okolního světa.
* **Kontejner:** Samostatně spustitelná část systému (např. webová aplikace, databáze, mobilní appka).
* **Komponenta:** Seskupení tříd/kódu uvnitř kontejneru, plnící určitou funkci.
* **Kód:** Detailní návrh tříd (UML).

---

## Návrh datových struktur

Musíme rozlišovat dva typy struktur:

1. **Algoritmické:** Navrhované pro optimalizaci práce s daty v paměti (stromy, hash mapy).
2. **Doménové:** Slouží pro reprezentaci dat o reálném světě v softwaru (typicky pro databáze a API, např. relační tabulky, JSON, XML).

### Tvorba doménových struktur

* **Vazba na analýzu:** Doménové struktury by měly vždy vycházet z *Doménového modelu* (z fáze analýzy). Je to dobré proto, aby kód, databáze i API používaly stejnou terminologii (byznys slovník) a nedocházelo ke zmatkům.


* **Zápis (Pseudo-schema):** Pro návrh API/výměny dat se používají jazyky jako *JSON Schema* nebo *XML Schema*

## JSON schema
Blog post

```json
{
  "$id": "https://example.com/blog-post.schema.json",
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "description": "A representation of a blog post",
  "type": "object",
  "required": ["title", "content", "author"],
  "properties": {
    "title": {
      "type": "string"
    },
    "content": {
      "type": "string"
    },
    "publishedDate": {
      "type": "string",
      "format": "date-time"
    },
    "author": {
      "$ref": "https://example.com/user-profile.schema.json"
    },
    "tags": {
      "type": "array",
      "items": {
        "type": "string"
      }
    }
  }
}


```
data

```json
{
  "title": "New Blog Post",
  "content": "This is the content of the blog post...",
  "publishedDate": "2023-08-25T15:00:00Z",
  "author": {
    "username": "authoruser",
    "email": "author@example.com"
  },
  "tags": ["Technology", "Programming"]
}

```

## XML schema
Example schema for ship order

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

<xs:element name="shiporder">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="orderperson" type="xs:string"/>
      <xs:element name="shipto">
        <xs:complexType>
          <xs:sequence>
            <xs:element name="name" type="xs:string"/>
            <xs:element name="address" type="xs:string"/>
            <xs:element name="city" type="xs:string"/>
            <xs:element name="country" type="xs:string"/>
          </xs:sequence>
        </xs:complexType>
      </xs:element>
      <xs:element name="item" maxOccurs="unbounded">
        <xs:complexType>
          <xs:sequence>
            <xs:element name="title" type="xs:string"/>
            <xs:element name="note" type="xs:string" minOccurs="0"/>
            <xs:element name="quantity" type="xs:positiveInteger"/>
            <xs:element name="price" type="xs:decimal"/>
          </xs:sequence>
        </xs:complexType>
      </xs:element>
    </xs:sequence>
    <xs:attribute name="orderid" type="xs:string" use="required"/>
  </xs:complexType>
</xs:element>

</xs:schema>
```

```xml
<?xml version="1.0" encoding="UTF-8"?>

<shiporder orderid="889923"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:noNamespaceSchemaLocation="shiporder.xsd">
  <orderperson>John Smith</orderperson>
  <shipto>
    <name>Ola Nordmann</name>
    <address>Langgt 23</address>
    <city>4000 Stavanger</city>
    <country>Norway</country>
  </shipto>
  <item>
    <title>Empire Burlesque</title>
    <note>Special Edition</note>
    <quantity>1</quantity>
    <price>10.90</price>
  </item>
  <item>
    <title>Hide your heart</title>
    <quantity>1</quantity>
    <price>9.90</price>
  </item>
</shiporder>
```


---

## Návrh rozhraní a API

* **Důležitost:** Rozhraní (Interfaces) jsou klíčová pro *modularizaci* a *information hiding*. Definují striktní kontrakt (co modul umí), aniž by prozradila, jak to dělá. Umožňují paralelní vývoj a snadnou výměnu implementace.

---

# Testování
Proces testování softwaru se dělí do tří hlavních fází:

1. **Development testing:** Testování během vývoje (provádí programátoři).
2. **Release testing:** Testování kompletního systému před vydáním (provádí QA tým).
3. **User testing:** Testování reálnými uživateli (Beta testování, UAT).

### Druhy testů v Development fázi

* **Unit (Jednotkové) testy:** Testují nejmenší kousky kódu (jednu třídu/metodu) v izolaci.


```cs
/// .NET MSTESTS
[TestMethod]
public void TestString()
{
/// Arrange

string a = "a";

/// Act

stirng a = a + "b"

/// Assert

Assert.IsEqaual()

}


```

* **Integrační testy:** Testují spolupráci více modulů/tříd dohromady nebo komunikaci s databází.

* **Systémové testy:** Testují systém jako celek.

### Nástroje a koncepty testování

* **Struktura testu:** Typický unit test má 4 fáze: *Set up* (příprava dat), *Execute* (spuštění kódu), *Validate / Assert* (ověření výsledku) a *Tear down* (úklid po testu).


* **Mockování:** Princip, kdy v Unit testech nahradíme reálné závislosti (např. databázi, externí API) falešným objektem (mockem), abychom testovali kód skutečně v izolaci.


* **Black box vs. White box:** Při *White box* testování známe vnitřní strukturu zdrojového kódu a testujeme jeho větve. Při *Black box* testování neznáme kód a testujeme systém pouze přes jeho veřejné rozhraní (vstupy a výstupy).


* **Verification vs. Validation:**
* *Verification:* Ověření, že systém děláme správně (podle specifikace).
* *Validation:* Ověření, že děláme správný systém (ten, co zákazník reálně potřebuje).


* **Test condition (Testovací podmínka):** Testovatelný aspekt komponenty, který typicky identifikujeme na základě scénářů z Use Case nebo z User Stories. Představuje to, *co konkrétně* chceme z daného požadavku otestovat.

* **Test case (Testovací případ):** Sada vstupů a očekávaných výsledků vytvořená pro otestování konkrétní podmínky. Test case musí být strukturován a měl by obsahovat název, testovací data a testovací scénář popsaný jako sekvenci atomických akcí testera a ověřitelných reakcí systému.

* **Test procedure (Testovací procedura):** Sekvence testovacích případů seřazená v pořadí, v jakém se mají vykonat.


## Ukázkový Test Case

Zde je příklad testu pro metodu vkládání zpráv do fóra.

* **Název:** Přidání zprávy do prázdného vlákna.
* **Condition:** Ověření, že systém správně uloží nový komentář.
* **Preconditions:** V databázi existuje prázdné diskusní vlákno.
* **Covered Test Conditions**
* **Test Steps**:
* **Actions:** Zavolám metodu `addMessage()` s platným autorem a textem, následně zavolám `getMessage()` pro načtení vlákna.
* **Expected result:** Vlákno obsahuje přesně jednu zprávu a její obsah i autor odpovídá tomu, co jsem vložil.

* Testovací data - jaké data jsou na vstupu - zprava



## Automatizace
* **Automatizace:** Spočívá v převodu manuálních kroků (Test cases) do spustitelných skriptů pomocí specializovaných nástrojů.

* Skript obvykle dodržuje jasnou strukturu fází: *set up* (příprava prostředí), *execute and validate* (spuštění kódu a kontrola výsledku) a *tear down* (úklid dat).

* Při automatizaci izolujeme testovaný kód od externích závislostí. K tomu slouží **Mocking** – tvorba falešných objektů (např. nahrazení reálného mail serveru za mock, aby testy neposílaly skutečné e-maily).

Continuous Integration (CI/CD Pipeline)

## Pokrytí kódu (Code Coverage)

### Definice
* Pokrytí je relativní poměr řádek testovaného kódu, které se spustí alespoň jednou během provádění testů, a celkového počtu řádek imperativního kódu testovaného programu, modulu nebo třídy.
* Jedná se o jeden z hlavních konceptů pro vyhodnocování nástrojů a kvality testování software.
* Zjednodušeně řečeno: Tato metrika nám říká, jaké procento našeho zdrojového kódu reálně "proběhlo", když se spustily automatizované testy.

### Pokrytí na 100%?
Existují dva pohledy:

* **Argumentace pro ANO (100% pokrytí máme):** Lze to tvrdit u velmi jednoduchých modulů. Obhajoba musí obsahovat stručný kategorický rozbor všech přípustných kombinací vstupních hodnot a stavů (např. platný vstup, neplatný vstup, hraniční hodnoty) s odkazem na to, že pro každý tento případ existuje test.

* **Argumentace pro NE (Častější případ z praxe):** Většinou 100% nedosáhneme. Důvodem je to, že může existovat specifický vstup nebo stav, který testy nepokrývají a kde se předpokládá jiné chování v těle metody (tedy existuje větev kódu, která se v testech nikdy nezavolá).


### Příklad z praxe (Neotestované větve)
Představme si metodu `removeMessage(id)`, kterou testujeme na tyto scénáře:
1. Zavolání metody na platné ID zprávu úspěšně smaže.
2. Zavolání metody na nesmyslný formát ID (neplatný vstup) vyhodí na začátku metody výjimku.

**Proč zde nemáme 100% pokrytí?**
Pokud by někdo zavolal `removeMessage()` na platné ID dvakrát za sebou, první volání zprávu smaže, ale to druhé volání ji už v databázi nenajde. Program by měl pravděpodobně vyhodit výjimku, ale tentokrát v úplně jiné větvi kódu, než když byl špatný formát ID. Jelikož jsme tento specifický případ (mazání již smazaného záznamu) netestovali, tato chybová větev kódu se při testech nikdy nespustí a zůstane nepokrytá.


## Defect report


## regression testing
Regression Testing is a type of software testing performed to ensure that recent code changes do not negatively affect existing functionality. It helps maintain system stability after updates, bug fixes, or enhancements.

    Re-executes previously passed test cases
    Ensures new changes do not break existing features
    Detects unintended side effects early
    Improves software reliability and stability

## Test Driven Development
Pri bugu se nejprve napisou testy a az pote se upravuje kod a overuje se, jestli se tyto testy uz prochazeji

# Sprava verzi
	– Popsat účel a použití systémů pro správu verzí při vývoji rozsáhlého software a práci v týmech (typicky nabízené funkce těchto systémů a jejich použití pro řešení běžných situací)
	– Popsat běžné způsoby integrace verzovacích systémů s nástroji pro správu projektů
	– Vysvětlit hlavní koncepty (lokální a vzdálené repozitáře, pracovní kopie (working copy), commit, větve)
	– Popsat a použít operace clone, pull, push, add, diff, commit, branch, merge, log, blame nástroje git
	– Popsat koncept feature branch v kontextu procesu vývoje a udržování software
	– Vysvětlit konflikty mezi verzemi, důvody vzniku a způsoby řešení
	– Systémy pro sestavování software
	– Popsat hlavní účel a typicky nabízené funkce
– Vysvětlit hlavní koncepty (cíl, závislosti, akce)

účely:
- historie vývoje systém
- concurrent vývoj mezi tými a lidmi
- snadné přechody mezi verzemi, například zpět


## Kategorie verzovacich systemu
### Centralizovane
Jen centralni repozitare 
- CVS
- SVN

### Distribuovane
soukrome repozitare a vetve 
- Git
- Mercurial
- Bazaar


## Pojmy
Lokální repozitář
- lokální kopie
- vývojář zde provádí změny a vývoj

Vzdalený repozitář 

Pracovní kopie (working copy)

Commit

Větve

Tag
- snapshot s human-friednly nazvem
- logicka kopie celeho stromu

## git operace

clone

pull

push

add

diff
- zobrazi necommitnute a nestagenute zmeny
- nebo porovna branche

commit
- commitne staged upravy

branch
- zobrazi aktualni vetve a vytvori novou

merge
- mergne vetev do soucasne 

log
- zobrazi historiy commitu

blame
- zobrazi jmeno autora a metadata

stash
- stack of unfinished changes

show 


## Feature branch
Idealni pro vyvoj mit pro kazdou vyvijenou feature valstni branch

## Konflikt
Vytvoreny 3 verze souboru
Ozna4eny <<<<<<< and >>>>>>> ve zdroj8ku


## Best practices (branches and merging)
- vetve pro experimentalni featury

- oddelovat release a development vetve
    - bugfixy

- mergovat casto
    -> mensi conflikty jsou jednodussi na vyreseni

## Systemy pro sestavovani software

# Mereni vykonnosti
TODO

## Profiling

### Sampling

### Recording



## Nástroje

# Návrh API, tříd a metod

## Objektový návrh

### Dekompozice
* rozdělení složitého systému na menší, samostatné části
* cílem je snížit složitost systému a usnadnit jeho pochopení, implementaci a údržbu
* v objektovém návrhu se systém typicky rozděluje na **třídy a objekty**
* třídy by měly mít jasně definovanou odpovědnost

### Zapouzdření

* skrytí vnitřní implementace objektu před okolím
* objekt poskytuje pouze definované rozhraní
* vnitřní stav objektu by neměl být přímo přístupný zvenčí
* změna interní implementace by neměla vyžadovat změny v kódu, který objekt používá

Příklad:

```csharp
public class BankAccount
{
    private decimal balance;

    public void Deposit(decimal amount)
    {
        if (amount > 0)
            balance += amount;
    }

    public decimal GetBalance()
    {
        return balance;
    }
}
```

Uživatel třídy nemusí vědět, **jak** je zůstatek uložen. Pracuje pouze s veřejným rozhraním.

### Rozhraní

* definuje, **co objekt umí**, ale ne **jak to dělá**
* v C# například `interface`
* umožňuje oddělit rozhraní od implementace
* podporuje polymorfismus a snižuje závislost mezi částmi systému

```csharp
public interface IPaymentService
{
    void Pay(decimal amount);
}
```

---

# API

**Application Programming Interface**

* rozhraní umožňující komunikaci mezi dvěma částmi softwaru
* definuje, jaké operace lze provádět a jakým způsobem
* může existovat například:

  * mezi třídami
  * mezi moduly/knihovnami
  * mezi aplikací a operačním systémem
  * mezi klientem a serverem

API tedy **nemusí být pouze webové API**.


## Rest API
**REST = Representational State Transfer**

* architektonický styl pro distribuované systémy
* REST definoval Roy Fielding ve své disertační práci
* **REST není protokol**
* REST API typicky využívá HTTP, ale REST jako takový není synonymem pro HTTP API
* data mohou být reprezentována například pomocí JSON(typicky) nebo XML

Vlastnosti:
- bezstavovy
- client-server
- layer system
- cacheable
- každá Resource ma svůj endpoint - identifikace pomoci URI
- operace pomoci HTTP dotazů (VERBS) - GET, POST, PUT, DELETE
- využití HTTP metod pro CRUD operace

### Vrstvy

0. The swamp of POX 
- URL Design
- Old XML

1. Resources
- endpoint for each resource
- self describing
- 
2. HTTP Verbs
- GET, POST, DELETE, PATCH
- Status codes
- URL query argumetns

3. Hypermedia Controls
- hyppertext -> HATEOAS

### Příklad

| | /gallery|
| -  | - |
| GET | |
| POST | |
| PUT | | 
| DELETE | |

## HTTP API

* obecný pojem pro API dostupné prostřednictvím HTTP
* nemusí dodržovat REST principy
* může používat JSON
* může používat HTTP metody libovolným způsobem
* může být například navrženo jako **RPC API**

Například:

```text
POST /api/getStudent
POST /api/deleteStudent
POST /api/updateStudent
```

Technicky jde o HTTP API, ale nemusí jít o REST API.
## Rozdíl mezi HTTP API a REST API
HTTP API nevyuživaji všechny metody HTTP
typicky vše pře GET a specifikace v textu jako GetStudent, DeleteStudetn

## REST API

* HTTP API navržené podle principů REST
* pracuje s resources
* používá URI pro identifikaci resources
* používá HTTP metody s jejich standardním významem
* používá HTTP status codes
* je stateless
* může využívat HATEOAS

**Každé REST API používající HTTP je HTTP API, ale ne každé HTTP API je REST API.**

### JSON není podmínkou RESTu

* REST API může používat JSON
* může používat také XML nebo jiný formát reprezentace
* JSON je pouze běžný formát používaný v REST API


## Principy návrhu REST API

Při návrhu REST API:

1. Identifikovat resources.
2. Každému resource navrhnout vhodné URI.
3. Používat HTTP metody podle jejich významu.
4. Používat správné HTTP status codes.
5. API navrhnout jako stateless.
6. Používat konzistentní strukturu URL.
7. Používat query parameters pro filtrování, řazení a stránkování.
8. Definovat formát requestů a response.
9. Řešit validaci vstupu a chybové odpovědi.
10. Zabezpečit API – například pomocí HTTPS a autentizace/autorizace.

Příklad:

```text
GET    /students?faculty=mff&limit=20
GET    /students/123
POST   /students
PATCH  /students/123
DELETE /students/123
```

---

# Zaklady bezpecnosti web apps

## SQl Injection

### Princip
* útočník vloží škodlivý SQL kód do vstupu aplikace
* aplikace tento vstup nesprávně vloží přímo do SQL dotazu
* útočník tak může změnit význam SQL dotazu
* může například získat, změnit nebo odstranit data

```text
SELECT * FROM users
WHERE username = 'uživatelský_vstup'
```

Pokud aplikace slepě skládá SQL z uživatelského vstupu, může útočník změnit výsledný SQL dotaz.


```
1 ; Drop Database
```

### Ochrana
**Primární ochrana: parametrizované dotazy.**
### Ochrana

**Primární ochrana: parametrizované dotazy.**

Například:

```csharp
var user = db.Users
    .FirstOrDefault(x => x.Name == username);
```

nebo přímo v SQL:

```sql
SELECT *
FROM Users
WHERE Name = @name
```

Další ochrana:

* parametrizované dotazy / prepared statements
* ORM (např. Entity Framework) při správném použití
* validace vstupu
* omezení databázových oprávnění aplikace
* nevytvářet SQL dotazy prostým konkatenováním stringů

### Pozor

Použití `mysqli_real_escape_string()` nebo podobných funkcí není ideální hlavní ochrana.


Alternativně

PHP
```php
mysqli_real_escape_string()
```



## Cross-side scripting

### Princip útoku
* útočník vloží škodlivý JavaScript do webové aplikace
* aplikace tento obsah následně zobrazí jinému uživateli jako součást HTML
* JavaScript se potom spustí v prohlížeči oběti

```html
<script>
    alert('XSS');
</script>
```

### Ochrana
* **output encoding / escaping**

  * při vkládání uživatelského textu do HTML převést speciální znaky na bezpečné HTML entity
* sanitizace HTML, pokud aplikace skutečně umožňuje uživatelům zadávat HTML
* Content Security Policy (**CSP**)
* bezpečné používání DOM API
* vhodné nastavení cookies, například `HttpOnly` a `Secure`

V PHP například:

```php
htmlspecialchars($input, ENT_QUOTES, 'UTF-8');
```

## Protokol HTTPS

### HTTP
- protokol pro přenos informací mezi dvěma systémy (jako server a web browser)
- typicky nad TCP
- data posíláné jako plain text -> 
- žádné zabezpečení -> komunikace je nachylná k útokům

### HTTPS
(Hypertext Transfer Protocol Secure)
- zabezpečený HTTP
- požaduje certifikát SSL (Secure Socket Layer), později nahrazen TSL (Transport Layer Security) -> nadstavba nad HTTP
- kryptografie - private and public key
- autentizace - oveření identity pomocí certifikátu

### Digitální certifikát
- podepsaný veřejný šífrovací klíč
- vydavá nějaká certifikační autorita
- prohližeč může ověřit podpis certifikační autority 


## Autorizace vs Autentizace
### Autentizace 
- oveření identity a pravosti uživatele (Kdo jsi?)  

### Autorizace 
- proces ověření správných rolí nebo přístupových práv (co smíš dělat?)
- opravnění pro nějakou činnost
    