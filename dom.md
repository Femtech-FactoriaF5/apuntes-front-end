
<!-- TOC -->
- [1. Introducció](#1-introducci%c3%b3)
- [2. Programació amb el DOM (Document Object Model)](#2-programaci%c3%b3-amb-el-dom-document-object-model)
  - [2.1. Estructura del DOM. Interfícies principals](#21-estructura-del-dom-interf%c3%adcies-principals)
    - [2.1.1. Tipus de models DOM](#211-tipus-de-models-dom)
    - [2.1.2. Estructura del DOM](#212-estructura-del-dom)
    - [2.1.3. Adaptacions de codi per diferents navegadors](#213-adaptacions-de-codi-per-diferents-navegadors)
  - [2.2. Interfícies del DOM](#22-interf%c3%adcies-del-dom)
  - [2.3. Interficie `Node`](#23-interficie-node)
    - [2.3.1. Informació bàsica dels nodes: `nodeType` i `nodeName`](#231-informaci%c3%b3-b%c3%a0sica-dels-nodes-nodetype-i-nodename)
    - [2.3.2. Contingut textual: 'textContent'](#232-contingut-textual-textcontent)
    - [2.3.3. Relacions entre nodes: `parentNode`, `firstChild`, `lastChild`,`previousSibling` i `nextSibling`](#233-relacions-entre-nodes-parentnode-firstchild-lastchildprevioussibling-i-nextsibling)
    - [2.3.4. Obtenció de nodes descendents: 'childNodes' i 'hasChildNodes'](#234-obtenci%c3%b3-de-nodes-descendents-childnodes-i-haschildnodes)
        - [2.3.4.0.1. Inserció de nodes: `appendChild` i `insertBefore`](#23401-inserci%c3%b3-de-nodes-appendchild-i-insertbefore)
    - [2.3.5. Eliminació i substitució de nodes: 'removeChild' i 'replaceChild'](#235-eliminaci%c3%b3-i-substituci%c3%b3-de-nodes-removechild-i-replacechild)
    - [2.3.6. Copia de nodes: 'cloneNode'](#236-copia-de-nodes-clonenode)
  - [2.4. Interficie `Document`](#24-interficie-document)
    - [2.4.1. Creació de nodes: 'createTextNode' i 'createElement'](#241-creaci%c3%b3-de-nodes-createtextnode-i-createelement)
    - [2.4.2. Cerca d`elements simple:`getElementsByClassName`,](#242-cerca-delements-simplegetelementsbyclassname)
    - [2.4.3. Cerca d'elements amb selectors ('querySelector' i 'querySelectorAll')](#243-cerca-delements-amb-selectors-queryselector-i-queryselectorall)
    - [2.4.4. L'extensió `HTMLDocument`](#244-lextensi%c3%b3-htmldocument)
    - [2.4.5. Altres propietats: `body`, `documentElement` i `forms`](#245-altres-propietats-body-documentelement-i-forms)
  - [2.5. La interfície `Element`](#25-la-interf%c3%adcie-element)
    - [2.5.1. Informació bàsica dels elements: 'tagName', 'className', 'classList' i 'id'](#251-informaci%c3%b3-b%c3%a0sica-dels-elements-tagname-classname-classlist-i-id)
    - [2.5.2. Obtenció dels descendents com HTML: `innerHTML`](#252-obtenci%c3%b3-dels-descendents-com-html-innerhtml)
    - [2.5.3. Atributs: `attributtes`, `getAttribute`, `removeAttribute`, `setAttribute`](#253-atributs-attributtes-getattribute-removeattribute-setattribute)
    - [2.5.4. Modificar estils CSS: `style`](#254-modificar-estils-css-style)
    - [2.5.5. Relacions entre elements: `previousElementSibling`, `nextElementSibling`, `firstElementChild` i `lastElementChild`](#255-relacions-entre-elements-previouselementsibling-nextelementsibling-firstelementchild-i-lastelementchild)
    - [2.5.6. Cerca d`elements descendents simple:`getElementsByClassName`, `getElementsByTagName`](#256-cerca-delements-descendents-simplegetelementsbyclassname-getelementsbytagname)
    - [2.5.7. Cerca d'elements descendents amb selectors: 'querySelector', 'querySelectorAll'](#257-cerca-delements-descendents-amb-selectors-queryselector-queryselectorall)
  - [2.6. Integració de la detecció d'events amb el DOM](#26-integraci%c3%b3-de-la-detecci%c3%b3-devents-amb-el-dom)
    - [2.6.1. Afegir detecció d'esdeveniments: 'addEventListener'](#261-afegir-detecci%c3%b3-desdeveniments-addeventlistener)
    - [2.6.2. Eliminar detecció d'esdeveniments: 'removeEventListener'](#262-eliminar-detecci%c3%b3-desdeveniments-removeeventlistener)
  - [2.7. Cas pràctic: generador de factures](#27-cas-pr%c3%a0ctic-generador-de-factures)


<a id="markdown-1-introducció" name="1-introducció"></a>
# 1. Introducció

Avui dia és molt difícil trobar una pàgina o aplicació web que no requereixi modificar, afegir o eliminar alguns dels seus elements per respondre a les accions dels usuaris. Tant pot ser un menú desplegable, un diàleg d'entrada de dades o un panell que mostra el contingut d'un carretó electrònic: en tots els casos cal manipular aquests elements. Aquestes modificacions es fan a través del model d'objectes del document (DOM).

<a id="markdown-2-programació-amb-el-dom-document-object-model" name="2-programació-amb-el-dom-document-object-model"></a>
# 2. Programació amb el DOM (Document Object Model)

La manipulació del model d'objectes del document, més conegut per les seves sigles en anglès: DOM (Document Object Model), és fonamental per al desenvolupament d'aplicacions web, perquè sense aquesta capacitat no és possible alterar la visualització de les pàgines dinàmicament.

Internament, els navegadors treballen amb els documents web com si es tractés d'un arbre, i és a partir d'aquest arbre que es pot modificar la representació de la pàgina, tant afegint nous elements (paràgrafs, capçaleres, taules...) com
modificant els atributs dels nodes que ja es troben al document o eliminant-los.

A més a més, és possible cercar tant elements concrets com llistes d'elements fent servir diferents propietats i mètodes segons les vostres necessitats: a través de relacions (el primer element, el pròxim element...), cercant segons el tipus d'element, el seu identificador o fent una cerca més complexa gràcies als selectors de CSS.

A banda de manipular aquests elements, també és possible accedir-hi per fer operacions de consulta, com per exemple per extreure informació dels atributs o del text contingut.

<a id="markdown-21-estructura-del-dom-interfícies-principals" name="21-estructura-del-dom-interfícies-principals"></a>
## 2.1. Estructura del DOM. Interfícies principals

El model d'objectes del document és una interfície que facilita treballar amb documents HTML, XML i SVG. És a dir, independentment del llenguatge de programació que es faci servir, el nom dels mètodes i paràmetres per manipular-lo són idèntics, tant si es tracta de PHP, com de JavaScript o de Python, per exemple.

Aquesta interfície defineix els mètodes i propietats que permeten accedir i manipular el document com si es tractés d'un arbre de nodes, en el qual l'arrel és el node `document`, que pot contenir qualsevol quantitat de nodes fills, i les fulles són els nodes que no tinguin cap descendent (generalment el text dels elements HTML).

Tot i que el més habitual és accedir al DOM a través de JavaScript, el DOM no forma part de l'especificació de JavaScript, sinó que es troba especificat pel W3C com una sèrie d' interfícies independents de la plataforma i el llenguatge.

Per tant, els mètodes i les propietats que formen part d'aquestes interfícies no són propis de JavaScript, sinó que es troben disponibles a qualsevol llenguatge que ofereixi la capacitat de manipular el DOM, com per exemple Python, tant directament com a través de biblioteques.

```script
Especificació del DOM segons el W3C
Podeu trobar l'especificació del DOM del W3C (que és el consorci internacional que treballa per desenvolupar els estàndards utilitzats per internet)
en l'enllaç següent: http://www.w3.org/DOM.

```

**WHATWG**

```
El Web Hypertext Application Technology Working Group
(WHATWG) és una comunitat fundada per integrants d'Apple, la fundació Mozilla i Opera. En trobareu més informació en l'enllaç següent:
http://www.goo.gl/AFxeCb.
```

```
Les interfícies SVG. Podeu trobar un exemple d'ús de les interfícies SVG juntament amb JavaScript en l'enllaç següent: goo.gl/gz6Lg6.
```

Al llarg dels anys s'han produït molts canvis a l'especificació, i ha evolucionat i s'ha simplificat. Algunes de les interfícies antigues han estat declarades obsoletes i no s'han de fer servir perquè els navegadors moderns poden deixar d'admetre-les.

És important tenir-ho en compte a l'hora de consultar materials de referència, ja que és fàcil trobar informació desactualitzada. És recomanable
consultar directament la documentació del web Mozilla Developer Network (www.developer.mozilla.org) o l' `especificació viva' ( DOM Living Standard;
http://www.dom.spec.whatwg.org) per aclarir els dubtes que pugueu tenir.

Actualment hi ha dos grups treballant en les especificacions per al web, el W3C i el WHATWG. Encara que tots dos van col·laborar temporalment fins al 2012, van deixar de fer-ho a causa del fet que els objectius de WHATWG (a favor dels estàndards vius) i del W3C (especificacions estàtiques) eren contraris. Actualment el W3C actualitza la seva versió de l'especificació a partir d' instantànies de
l'especificació viva, centrant-se en la correcció d'errors.

Les especificacions proporcionades pel W3C sobre el DOM estan dividides en nivells i cadascun d'aquests nivells ho està, al seu torn, en diferents especificacions.

D'aquesta manera es poden conèixer les capacitats quant a manipulació del DOM dels diferents navegadors. Per exemple, el DOM nivell 1 és admès per
pràcticament tots els navegadors, en canvi, durant l'any 2016 l'especificació DOM3 carregar i guardar encara no l'admetia cap navegador.

Per aquesta raó, trobareu que a la documentació sobre diferents webs API s'indica el nivell de DOM necessari per utilitzar-les, ja que no funcionaran en navegadors que no admetin aquest nivell.

<a id="markdown-211-tipus-de-models-dom" name="211-tipus-de-models-dom"></a>
### 2.1.1. Tipus de models DOM

En desenvolupar aplicacions web es treballa amb la interfície `HTMLDocument`, que s'aplica als elements HTML, però l'especificació del DOM consta de més in-
terfícies que permeten manipular diferents tipus de documents. Són les següents:

- Interfície `HTMLDocument` (documents HTML): és una extensió de la interfície `Document` i afegeix l'accés a característiques pròpies dels navegadors, com són la finestra (**window**) o les pestanyes.

- Interfície `XMLDocument` (documents XML): aquesta interfície es troba en fase experimental i a finals de l'any 2016 encara no l'admet cap navegador.

- Interfícies **SVG** : es tracta d'un conjunt d'interfícies que permeten manipular directament des de JavaScript els elements d'una imatge vectorial de
  tipus SVG, per afegir formes, canviar colors... No es fa servir gaire perquè és molt complexa.

<a id="markdown-2111-estructura-del-dom" name="2111-estructura-del-dom"></a>
### 2.1.2. Estructura del DOM

Per entendre més fàcilment com s'estructura el DOM fixeu-vos en el següent codi HTML i contrasteu-lo amb la figura 1.1:

```html
<html>
  <head>
    <title>Títol</title>
  </head>
  <body>
    <h1>Això és la capçalera</h1>
    <p>Això és un paràgraf</p>
    <p>Això és un altre <strong>paràgraf</strong> amb <a>enllaç</a></p>
  </body>
</html>
```

```
Figura 1.1. Estructura d`arbre corresponent a un document HTML
```

![](https://imgur.com/gFFECM3.png)

Com es pot apreciar, l'arrel de l'arbre és el nodedocument, tot i que no forma part del codi HTML. A continuació trobem el nodehtml, que conté els nodes `head` i `body`; aquests contenen altres nodes:`title`,`h1` i `p`. Tots aquests nodes són de tipus **Element**. En canvi, l'últim element de cada branca (les fulles) són de tipus **Text** i tenen una consideració diferent.

Pareu atenció a l'últim paràgraf del document: en aquest cas el text inclou els
elements `strong` i `a`, però aquests elements no pengen del text sinó que pengen
del node `p`. Per tant, es pot concloure que un element sempre és descendent d'un altre element i mai d'un text.

<a id="markdown-212-adaptacions-de-codi-per-diferents-navegadors" name="212-adaptacions-de-codi-per-diferents-navegadors"></a>
### 2.1.3. Adaptacions de codi per diferents navegadors

S'ha de tenir en compte que encara que s'amplien les especificacions de les interfícies i dels llenguatges de programació contínuament, els navegadors antics no les admeten.

```
IE 6 al mercat xinès A l'agost del 2012, Internet Explorer 6 encara era el segon navegador més utilitzat a la Xina (22.41% dels usuaris).
```

Al web de Mozilla Developer Network es pot trobar el polyfill per implementar moltes de les característiques d`HTML5.

**Implementació `polyfill` per a JSON**

Es pot trobar la implementació completa del _polyfill_ per a l'objecte JSON en l'enllaç
següent: goo.gl/p4nm6l.

Actualment, tots els navegadors s'actualitzen automàticament de forma predeterminada. Per aquesta raó, es parla de Google Chrome o de Firefox sense indicar-ne la versió. En canvi, els navegadors més antics s'havien d'actualitzar manualment i en alguns països l'ús de navegadors obsolets (especialment Internet Explorer) ha estat molt estès fins fa pocs anys.

Afortunadament, cada vegada hi ha menys usuaris que facin servir navegadors obsolets, i molts grups han deixat fer-los compatibles perquè consideren que mentre hi hagi compatibilitat amb aquests navegadors obsolets, la gent continuarà fent-los servir i això perjudica tant els desenvolupadors com els usuaris amb navegadors actualitzats.

En cas de requerir compatibilitat amb aquests navegadors, al mateix temps que s'aprofiten les noves tecnologies, teniu a la vostra disposició dues opcions:

- Biblioteques : fer servir una biblioteca que implementi les característiques que necessiteu i que doni compatibilitat amb navegadors antics. En aquest cas, sempre que sigui possible, es recomana fer servir la biblioteca: les biblioteques implementen el
  comportament correcte per a tots els navegadors sense haver de modificar el vostre codi.

- Polyfill : consisteix a afegir, juntament amb el vostre codi, una implementació pròpia de la característica que necessiteu i que no és disponible en tots els navegadors antics. Per exemple, abans que HTML5 fos disponible per a tots els navegadors moderns, era possible fer servir polyfills per implementar algunes de les noves característiques del llenguatge sense haver de preocupar-se pels navegadors dels usuaris.

Per exemple, si voleu fer una implementació per treballar amb JSON en navegadors antics, faríeu servir un codi similar al següent:

```js
if (!window.JSON) {
        window.JSON = {
        parse: function(text) { // Codi per retornar un objecte a partir del text},
        stringify: function(obj) { // Codi per retornar una cadena de text a partir
        de l`objecte}
        }
    }
```

Cal destacar que la implementació pròpia dels navegadors d'aquestes funcions és molt més eficient que els polyfills. Per aquesta raó, és molt important comprovar primer si el navegador ja les implementa i, si no és així, cal afegir-les. Per fer-ho només cal comprovar si es troben definides a l'objecte o al prototipus, segons el cas.

Tenint en compte la complexitat afegida d'utilitzar polyfills i les seves limitacions,
és més recomanable fer servir biblioteques que ja implementin aquests polyfills o incloguin les funcionalitats que requeriu en lloc de fer la vostra pròpia implementació.

<a id="markdown-22-interfícies-del-dom" name="22-interfícies-del-dom"></a>
## 2.2. Interfícies del DOM

L'especificació del DOM està dividida en múltiples interfícies que determinen les possibles accions que es poden realitzar amb cada element; per exemple, per conèixer la classe o classes aplicades a un element, caldrà utilitzar la interfície **`Element`**; en canvi, per consultar o modificar el valor d'un atribut de l'element, s'utilitza la interfície **`Attr`**.

A continuació podeu trobar una llista de les interfícies més destacables per a la
manipulació de documents HTML:

- **`Node`** : molts dels elements del DOM hereten d'aquest tipus i, per tant, ofereixen aquestes funcionalitats. Aquesta interfície permet consultar i manipular els nodes, com per exemple navegar a través dels nodes fills, pares i contigus, cercar nodes, afegir nodes nous o eliminar-los.

- **`Document`** (herència de Node): aquesta interfície és la que s'aplica a l'arrel del document. Permet, entre altres coses, conèixer l'element actiu, manipular les galetes (més conegudes com a cookies ) i obtenir informació global del document.

- **`Element`** (herència de Node): s'aplica a tots els elements del document, és a dir, a les etiquetes que apareixen com abody,h1op. A partir d'aquesta interfície es pot obtenir una llista d'atributs, la classe de l'element, el seu id i afegir observadors per escoltar diferents events.

- **`Attr`** : aquesta interfície permet consultar i modificar els atributs d'un
  element. En versions anteriors a DOM4 la interfície `Attr` derivava de `Node`, però no es recomana fer servir aquestes funcionalitats perquè no hi hagi discrepàncies amb els navegadors més actuals.

- **`Event`** : aquesta interfície és implementada per altres interfícies de l'especificació i conté tots els mètodes comuns per representar un esdeveniment.

Cal destacar que existeix una interfície per a `text`, però no es fa servir gaire. El seu objectiu principal és representar el text contingut en unelemento `attr` (atribut).

```
Llistat d`interfícies
Podeu trobar una llista de totes les interfícies DOM en l'enllaç següent: goo.gl/X3rGDj.
```

<a id="markdown-23-interficie-node" name="23-interficie-node"></a>
## 2.3. Interficie `Node`

D'entre totes les interfícies la més important és `Node`, ja que `Document` i `Element` deriven d'aquesta. És a dir, totes les propietats i mètodes de Node són accessibles tant per a `Document` com per a `Element`.

Cal destacar que tot i que això implica que `Document` i `Element` inclouen la funcionalitat per navegar entre nodes, no s'acostuma a fer-les servir. En el cas de la primera interfície s'acostuma a cercar directament l'element que interessi (a través del tipus d'element, el seu identificador o la seva classe), mentre que el segon, a més de disposar de la capacitat de cerca, inclou propietats específiques per navegar entre els nodes de tipus `element` , filtrant-ne, així, la resta (per exemple, els de tipus `text` ).

```
Propietats de `Node`
Podeu trobar informació més detallada sobre la interficie Node en l'enllaç següent:
http://www.http://goo.gl/Rmwm4h.
```

<a id="markdown-231-informació-bàsica-dels-nodes-nodetype-i-nodename" name="231-informació-bàsica-dels-nodes-nodetype-i-nodename"></a>
### 2.3.1. Informació bàsica dels nodes: `nodeType` i `nodeName`

La propietat `nodeType` permet determinar el tipus d'un node. Conté un valor numèric corresponent a les `pseudoconstants` (recordeu que realment a JavaScript no existeixen les constants), que podeu veure a la taula taula 1.1.

```
Taula 1.1. Correspondència de valors de la propietat nodeType
```

| Pseudoconstant              | Valor |
| --------------------------- | ----- |
| ELEMENT_NODE                | 1     |
| TEXT_NODE                   | 3     |
| PROCESSING_INSTRUCTION_NODE | 7     |
| COMMENT_NODE                | 8     |
| DOCUMENT_NODE               | 9     |
| DOCUMENT_TYPE_NODE          | 10    |
| DOCUMENT_FRAGMENT_NODE      | 11    |

```
getElementById és un mètode de la interfície document que permet obtenir un element per al seu id.
```

Per exemple, per comprovar el valor de la propietat `nodeType` de `document` només cal mostrar-la per la consola:

```js
console.log(document.nodeType);
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/PGoGwP?editors=0012.

Com es pot apreciar, el valor retornat és 9 , ja que és el valor associat a `DOCUMENT_NODE`.

En canvi, si es consulta el valor de la propietat d'un element, el valor associat serà
1 , com correspon a ELEMENT_NODE:

```html
<div>
  <p id="primer">Primer paràgraf</p>
</div>
<script>
  var primer = document.getElementById(`primer`);
  console.log(primer.nodeType);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/QKWKNg?editors=1012.

Per altra banda, la propietat `nodeName` permet saber el nom del node, i això permet distingir-los entre d'altres. Aquest nom no correspon necessàriament amb el de l'etiqueta que crea el node, com es pot comprovar en l'exemple següent:

```html
<div>
  <p id="primer">Primer paràgraf</p>
</div>
<script>
  var primer = document.getElementById("primer");
  console.log(document.nodeName);
  console.log(primer.nodeName);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/EgxgjZ?editors=1012. Fixeu-vos que el nom del nodedocument és `#document`, mentre que el del'element `p` és `P`.

<a id="markdown-232-contingut-textual-textcontent" name="232-contingut-textual-textcontent"></a>
### 2.3.2. Contingut textual: 'textContent'

Aquesta propietat retorna el contingut textual:

```html
<p id="primer">Primer paràgraf</p>
<script>
  var primer = document.getElementById("primer");
  console.log(primer.textContent);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/GjRjOq?editors=1012.


<a id="markdown-233-relacions-entre-nodes-parentnode-firstchild-lastchildprevioussibling-i-nextsibling" name="233-relacions-entre-nodes-parentnode-firstchild-lastchildprevioussibling-i-nextsibling"></a>
### 2.3.3. Relacions entre nodes: `parentNode`, `firstChild`, `lastChild`,`previousSibling` i `nextSibling`

La propietat `parentNode` permet accedir al pare del node o retorna `null` si no existeix (per exemple, si el node no s'ha afegit al document).

```html
<div id="contenidor">
  <p id="primer">Primer paràgraf</p>
</div>
<script>
  var primer = document.getElementById(`primer`);
  console.log(primer.parentNode.nodeName);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/oBXRzP.

Com es pot apreciar, el nom del node retornat és `DIV`, el corresponent al node pare.
Aquest comportament permet recórrer l'arbre ascendentment; per exemple, es podria accedir al pare del pare: primer.parentNode.parentNode.nodeName.

Les propietats `firstChild` i `lastChild` permeten accedir al primer i a l'últim
fill d'un node, com es pot comprovar en l'exemple següent:

```html
<div id="contenidor">
  <p id="primer">Primer paràgraf</p>
  <p id="segon">Segon parà graf</p>
  <p id="tercer">Tercer paràgraf</p>
</div>
<script>
  var contenidor = document.getElementById(`contenidor`);
  console.log(contenidor.firstChild.textContent);
  console.log(contenidor.lastChild.textContent);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/VKwKbw?editors=1012.

Els salts de línia són interpretats com a nodes de tipus text i, per consegüent, en cas d'afegir salts de línia, tant el `firstChild` com el `lastChild` serien nodes de tipus text.

En el cas de `previousSibling` i `nextSibling` es produeix el mateix comportament, i per aquesta raó cal tenir en compte els salts de línies i tabulacions quan es tracta amb aquests mètodes.

Per altra banda, `previousSibling` i `nextSibling` permeten accedir als nodes germans, anterior i posterior respectivament, d'un mateix node:

```html
<div id="contenidor">
  <p id="primer">Primer paràgraf</p>
  <p id="segon">Segon parà graf</p>
  <p id="tercer">Tercer paràgraf</p>
</div>
<script>
  var segon = document.getElementById(`segon`);
  console.log(segon.previousSibling.textContent);
  console.log(segon.nextSibling.textContent);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/mAdAxE?editors=1012.

En executar aquest exemple es mostrarà correctament el contingut textual dels nodes anterior i posterior, és a dir,Primer paràgrafiTercer paràgraf.

<a id="markdown-234-obtenció-de-nodes-descendents-childnodes-i-haschildnodes" name="234-obtenció-de-nodes-descendents-childnodes-i-haschildnodes"></a>
### 2.3.4. Obtenció de nodes descendents: 'childNodes' i 'hasChildNodes'

`hasChildNodes`

Per altra banda, la propietat `childNodes` ens permet accedir a la llista de nodes continguts que es pot tractar com un array i conèixer la quantitat de nodes a través de la propietat `length`. Per altra banda, si només es vol saber si conté altres nodes o no, es pot invocar el mètode `hasChildNodes`, que retornarà `true` si en conté o
`false` en cas contrari.

Com que la llista de nodes es pot tractar com un array , es pot recórrer normalment:

```html
<div id="contenidor">
  <p id="primer">Primer paràgraf</p>
  <p id="segon">Segon paràgraf</p>
  <p id="tercer">Tercer paràgraf</p>
</div>
<script>
  var contenidor = document.getElementById("contenidor");

  console.log(
    "El contenidor conté altres nodes: " + contenidor.hasChildNodes()
  );

  console.log("Conté " + contenidor.childNodes.length + " nodes");

  for (var i = 0; i < contenidor.childNodes.length; i++) {
    console.log(
      "Trobat un node de tipus " +
        contenidor.childNodes[i].nodeType +
        ": " +
        contenidor.childNodes[i].nodeName
    );
  }
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/vXYXbX?editors=1012.

Fixeu-vos que en aquest cas s'han fet servir la indentació habitual, i en recórrer la llista de nodes s'han trobat quatre nodes de tipus text, corresponents als nodes generats pels salts de línia i les indentacions.

<a id="markdown-23401-inserció-de-nodes-appendchild-i-insertbefore" name="23401-inserció-de-nodes-appendchild-i-insertbefore"></a>
##### 2.3.4.0.1. Inserció de nodes: `appendChild` i `insertBefore`

Aquests dos mètodes permeten afegir un node com a fill d'un altre. La diferència és que `appendChild` afegeix el node al final de la llista de fills, mentre que amb `insertBefore` el node s'afegeix abans del node de referència passat com a argument.

```html
<div id="contenidor"></div>

<script>
  var contenidor = document.getElementById("contenidor");

  contenidor.appendChild(document.createElement("p"));
  contenidor.appendChild(document.createElement("div"));
  contenidor.insertBefore(document.createElement("h1"), contenidor.firstChild);

  console.log(
    "El contenidor conté altres nodes: " + contenidor.hasChildNodes()
  );

  console.log("Conté " + contenidor.childNodes.length + " nodes");

  for (var i = 0; i < contenidor.childNodes.length; i++) {
    console.log(
      "Trobat un node de tipus " +
        contenidor.childNodes[i].nodeType +
        ": " +
        contenidor.childNodes[i].nodeName
    );
  }
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/WGNooa?editors=1012.

```
El mètodeinsertBefore requereix que es passin dos arguments, el node que s`ha d`afegir i el node de referència o null, obligatòriament.
```

```
El mètodecreateElement forma part de la interfície Element.
```

Com es pot apreciar en aquest exemple, els nodes afegits amb `appendChild` s'han afegit en ordre, mentre que el node afegit amb `insertBefore` s'ha afegit davant del primer fill del contenidor i, per tant, ha quedat en primera posició.

S'ha de tenir en compte que en el cas d'invocar aquests mètodes passant com a paràmetre un node que ja es trobi al document, en lloc d'afegir-se, el node es mourà, és a dir, s'eliminarà de la seva posició anterior i s'afegirà a la nova:

```html
<div id="contenidor1">
  <h1 id="titol1">Aquest és el títol 1<h1>
</div>
<div id="contenidor2">
    <h1 id="titol2">Aquest és el títol 2<h1>
</div>
<script>
var contenidor2 = document.getElementById('contenidor2');
var titol1 = document.getElementById('titol1');
contenidor2.appendChild(titol1);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/ALBOjL?editors=1010.

Com es pot apreciar, una vegada s'afegeix el titol 1 al contenidor 2 s'elimina automàticament del contenidor 1.

<a id="markdown-235-eliminació-i-substitució-de-nodes-removechild-i-replacechild" name="235-eliminació-i-substitució-de-nodes-removechild-i-replacechild"></a>
### 2.3.5. Eliminació i substitució de nodes: 'removeChild' i 'replaceChild'

`replaceChild`

El mètode `removeChild` permet eliminar un node fill. S'ha de tenir en compte que per poder eliminar un node s'ha d'accedir al pare d'aquest, per tant, cal recordar que la propietat `parentNode` hi dona accés, tal com es pot veure a l'exemple següent:

```html
<div id ="contenidor1">
<h1 id ="titol1">Aquest és el títol 1<h1>
</div>
<div id ="contenidor2">
<h1 id ="titol2">Aquest és el títol 2<h1>
</div>
<script>
var titol1 = document.getElementById(`titol1`);
 titol1.parentNode.removeChild(titol1);
 </script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/rrNWpX?editors=1010.

Fixeu-vos que el titol1 ha desaparegut i només es mostra el titol2. El
contenidor1(el node pare) continua existint, però ara es troba buit.

Tot i que el node ja no forma part del contenidor, es pot conservar una referència (per exemple, la retornada pel mètoderemoveChild) i afegir-lo a un altre node:

```html
<div id ="contenidor1">
<h1 id ="titol1">Aquest és el títol 1<h1>
</div>
<div id ="contenidor2">
<h1 id ="titol2">Aquest és el títol 2<h1>
</div>
<script>
  var contenidor2 = document.getElementById(`contenidor2`);
  var titol1 = document.getElementById(`titol1`);
  var refNode = titol1.parentNode.removeChild(titol1);
  contenidor2.appendChild(refNode);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/yaLVmN?editors=1010.

Com es pot apreciar, ara elcontenidor2conté tots dos títols. Cal tenir en compte que en aquest cas concret no caldria guardar la referència perquè la variable titol1 ja la manté. Si reemplaceu el codi JavaScript pel següent, el resultat és idèntic:

```js
var contenidor2 = document.getElementById(`contenidor2`);
var titol1 = document.getElementById(`titol1`);
titol1.parentNode.removeChild(titol1);
contenidor2.appendChild(titol1);
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/WGNRZV?editors=1010.

Per altra banda,replaceChildpermet reemplaçar un node per un altre. Per
exemple, es poden intercanviar els continguts dels dos contenidors de l'exemple anterior:

```html
<div id ="contenidor1">
<h1 id ="titol1">Aquest és el títol 1<h1>
</div>
<div id ="contenidor2">
<h1 id ="titol2">Aquest és el títol 2<h1>
</div>
<script>
  var contenidor1 = document.getElementById(`contenidor1`);
  var contenidor2 = document.getElementById(`contenidor2`);
  var titol1 = document.getElementById(`titol1`);
  var titol2 = document.getElementById(`titol2`);
  var refNode = contenidor1.replaceChild(titol2, titol1);
  contenidor2.appendChild(refNode);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/qRRzLj.

En primer lloc s'obté una referència als contenidors i els nodes, seguidament es fa el reemplaça de titol1 per titol2, i finalment s'afegeix eltitol1 al segon contenidor.

Per assegurar la compatibilitat amb navegadors que no admetin el DOM4 és recomanable passar `true` com argument per fer còpies profundes.

```
Mètodes i propietats de `Document`
Podeu trobar més informació sobre la interfície Document en
l'enllaç següent: http://www.goo.gl/Rmwm4h.
```

Com que `replaceChild` retorna una referència al node reemplaçat, aquesta referència es pot fer servir per afegir aquest node al contenidor2. Cal tenir en compte que no és possible invocar el mètode `replaceChild` per fer l'intercanvi al contenidor2 perquè aquest ja no conté cap node que pugui ser reemplaçat.

<a id="markdown-236-copia-de-nodes-clonenode" name="236-copia-de-nodes-clonenode"></a>
### 2.3.6. Copia de nodes: 'cloneNode'

Aquest mètode permet clonar un node, de manera que es genera un nou node idèntic. Es pot passartruecom a paràmetre, si volem que es faci una còpia profunda del node (és a dir, que cloni també tots els seus nodes descendents); o false, en cas contrari.

En el següent exemple es pot veure com es clona la capçalera de tipus `h1` i s'afegeix cinc vegades:

```html
    <div id ="contenidor"><h1>Això és un títol<h1></div>
    <script>
    var contenidor = document.getElementById(`contenidor`);
    for (var i=0; i<5; i ++) {
    var clonedNode = contenidor.firstChild.cloneNode(true);
    console.log(clonedNode);
    contenidor.appendChild(clonedNode);
    }
    </script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/GjRApw?editors=1010.

En cas de passar false com a argument, s'haurien afegit cinc elements de tipus `h1`, però sense cap contingut, ja que el node amb el contingut textual "Això és un títol" no s'hauria clonat.

<a id="markdown-24-interficie-document" name="24-interficie-document"></a>
## 2.4. Interficie `Document`

Aquesta interfície és herència de Node i de `EventTarget` (aquesta darrera permet la utilització d'events ), així doncs, és possible manipular el document com si es tractés d'un node i gestionar events.

Les propietats que ofereix aquesta interfície no són gaire utilitzades, en canvi, és fonamental conèixer els seus mètodes, perquè permeten cercar i crear nous nodes.

En aquests materials només es tractarà un subconjunt d'aquests mètodes, els més utilitzats, ja que molts d'aquests tenen aplicacions molt concretes i no cal conèixer-los.

<a id="markdown-241-creació-de-nodes-createtextnode-i-createelement" name="241-creació-de-nodes-createtextnode-i-createelement"></a>
### 2.4.1. Creació de nodes: 'createTextNode' i 'createElement'

Aquests mètodes permeten crear nodes de text i elements, respectivament. Com que totes dues implementen la interfícieNode, es poden afegir al document, eliminar-los, reemplaçar-los o clonar-los:

```html
<h1 id="titol1">
  Aquest és el primer node de text.
  <h1>
    <script>
      var titol1 = document.getElementById(`titol1`);
      var nouNodeDeText = document.createTextNode(
        `I aquest és el segon, afegit dinàmicament`
      );
      titol1.appendChild(nouNodeDeText);
    </script>
  </h1>
</h1>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/BLamyb?editors=1010.

Com es pot apreciar, el codi HTML només inclou un fragment de text, però s'afegeix el segon dinàmicament en crear un nou node i afegint-lo al contenidor (l'element `h1`).

Per afegir-lo al principi del contenidor en lloc del final només cal substituir l'última línia per:

```js
titol1.insertBefore(nouNodeDeText, titol1.firstChild);
```

El mètode `createElement` també crea nodes, però en aquest cas són de tipus `element` i, per consegüent, implementen la interfície `Element`. Això permet crear elements d'HTML, com es pot apreciar en l'exemple següent:

```html
<div id="contenidor"></div>

<script>
  var contenidor = document.getElementById(`contenidor`);

  var nouElement = document.createElement(`h1`);
  var nouText = document.createTextNode(`Això és la capçalera`);

  nouElement.appendChild(nouText);
  contenidor.appendChild(nouElement);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/pEodaE?editors=1010.

L'argument que es passa en invocar el mètode és una cadena de text amb l'etiqueta (_tag_), és a dir, si l'argument és `h1` es crearan les etiquetes HTML `<h1></h1>`.

Aquesta etiqueta és important perquè també permet fer cerques a l'arbre de tots els nodes amb la mateixa etiqueta, per exemple: cercar tots els títols principals (h1), tots els enllaços (a)...

Fixeu-vos que no cal afegir els nous nodes al document immediatament, es pot crear una branca a la memòria (en aquest cas el node referenciat per nou element, que conté el node de text) i, una vegada afegits tots els nodes, afegir-la a l'arbre.

L'atribut `id` de qualsevol element d'un document sempre ha de ser únic.

Aquesta és la millor manera de fer-ho, perquè si s'afegeixen els nodes al document d'un en un, el navegador renderitzarà l'arbre una vegada per cada node. En canvi, si s'afegeix tota la branca, només ha de renderitzar l'arbre de nou un cop.

<a id="markdown-242-cerca-delements-simplegetelementsbyclassname" name="242-cerca-delements-simplegetelementsbyclassname"></a>
### 2.4.2. Cerca d`elements simple:`getElementsByClassName`,

`getElementsByTagName` i `getElementById`

Aquests mètodes permeten fer cerques d'elements al document. Cal recalcar que es tracta d'elements (implementen la interfície `Elements`) i no de qualsevol node.

És a dir, es poden cercar tots els paràgrafs d'una pàgina però no els nodes de text que contingui.

Els mètodes `getElementsByClassName` i `getElementsByTagName` retornen una llista de nodes de tipus element, mentre que `getElementById` retorna sempre un únic node de tipus element.

Cadascun realitza la cerca segons un aspecte diferent:

- `getElementsByClassName` : nodes de tipus element que continguin la
  classe passada com a argument.

- `getElementsByTagName` : nodes de tipus element amb l'etiqueta passada com a argument; per exemple: `p`, per obtenir una llista de paràgrafs, o `h1` per obtenir totes les capçaleres de primer nivell.

- `getElementById` : node de tipus element amb l'atribut `id` que coincideix amb el valor passat com a argument. Permet accedir de forma més directa a qualsevol element, però requereix afegir, abans, l'atribut `id` als elements que s'han de manipular.

```html
<h1>Primera capçalera</h1>
<ul>
  <li>Primer element de la primera llista</li>
  <li>Segon element de la primera llista</li>
  <li>Tercer element de la primera llista</li>
</ul>
<h1 class="secundari">Segona capçalera</h1>
<p id="contingut" class="secundari paragraf">Un paràgraf</p>
<ul>
  <li>Primer element de la segona llista</li>
  <li>Segon element de la segona llista</li>
  <li>Tercer element de la segona llista</li>
</ul>

<script>

  var elementsSecundaris = document.getElementsByClassName(`secundari`);

   console.log(`Contingut textual dels elements amb classe="secundari":`);
   for (var i = 0; i <elementsSecundaris.length; i ++) {
   console.log(elementsSecundaris[ i ].textContent);
   }

   var elementsLlista = document.getElementsByTagName(` li `);
   console.log(`Contingut textual dels elements de la llista (<li></li>):`);
   for (i = 0; i <elementsLlista.length; i ++) {
   console.log(elementsLlista[ **i** ].textContent);

   }

  var elementContingut = document.getElementById(`contingut`);

  console.log(`Contingut textual **del** element amb **id ="contingut":` + elementContingut.textContent);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/NRWwZx?editors=1011.

Fixeu-vos que el mètode `getElementsByClassName` retorna dos elements, ja que comprova totes les classes de cada element, de manera que tant secundari com secundari paràgraf són coincidències vàlides.

També cal destacar que en el cas de `getElementsByTagName` es retornen tots els elements amb l'etiqueta `li` del document, és a dir, inclou tant els elements de la primera llista com els de la segona.

Com és d'esperar, és possible fer modificacions sobre aquests nodes, per exemple per moure'ls o eliminar-los. En cas de voler eliminar-los, es pot presentar un problema inesperat: com que en eliminar el node canvia la seva posició a la llista, es produirà un error en intentar accedir als elements posteriors. Una possible solució seria la següent: fer servir un bucle amb while que elimini el primer element de la llista i es repeteixi fins que la longitud de la llista sigui 0.

```html
<h1>Primera capçalera</h1>
<ul>
  <li>Primer element de la primera llista</li>
  <li>Segon element de la primera llista</li>
  <li>Tercer element de la primera llista</li>
</ul>
<h1 class="secundari">Segona capçalera</h1>
<p id="contingut" class="secundari paragraf">Un paràgraf</p>
<ul>
  <li>Primer element de la segona llista</li>
  <li>Segon element de la segona llista</li>
  <li>Tercer element de la segona llista</li>
</ul>
<script>
  var elementsLlista = document.getElementsByTagName(`li`);
  while (elementsLlista.length > 0) {
    elementsLlista[0].parentNode.removeChild(elementsLlista[0]);
  }
</script>
```

Podeu veure aquest exemple en l'enllaç següent:
codepen.io/ioc-daw-m06/pen/XjWVWE?editors=1011. **Selectors CSS** Podeu trobar
informació detallada sobre els selectors CSS en l'enllaç següent: goo.gl/o8ELvX.

```
Un element és descendent directe d`un altre quan el seu pare és aquest element.
```

<a id="markdown-243-cerca-delements-amb-selectors-queryselector-i-queryselectorall" name="243-cerca-delements-amb-selectors-queryselector-i-queryselectorall"></a>
### 2.4.3. Cerca d'elements amb selectors ('querySelector' i 'querySelectorAll')

`querySelectorAll`

Aquests mètodes permeten fer una cerca específica d'elements, passant com a argument una cadena de text amb un selector CSS. La diferència entre tots dos és que el primer només retorna el primer element coincident, mentre que el segon retorna una llista amb totes les coincidències.

Entre els selectors que es poden utilitzar hi ha:

- __`#identificador`__: que contingui id="identificador".

- __`.nom_classe`__: que contingui class="nom_classe".

- __`element`__: que sigui un element amb l'etiqueta element.

- __`element1 element2`__: que sigui un element amb l'etiqueta element2 descendent d'un element amb l'etiqueta element1. Cal destacar que no cal que sigui descendent directe.

- __`element1>element2`__: que sigui un element amb el tagelement2 descendent directe d'un element amb l'etiqueta element1.

- __`[type="button"]`__: elements que tinguin l'atributtypei el seu valor sigui 
exactament button.

- __`:first-child`__ (exemple de pseudoclasse): elements que siguin el primer fill
de qualsevol altre element.

- __`element:first-child`__ (exemple de pseudoclasse): elements que siguin el primer fill de l'element pare.

Cal remarcar que el nombre de possibles selectors i les seves combinacions és molt gran i el seu estudi queda fora de l'abast d'aquest mòdul.

A continuació podeu veure un exemple d'ús del mètode `querySelectorAll`:

```html
<h1>Primera capçalera</h1>
<ul>
  <li>Primer element de la primera llista</li>
  <li>Segon element de la primera llista</li>
  <li>Tercer element de la primera llista</li>
</ul>
<h1 class="secundari">Segona capçalera</h1>
<p id="contingut" class="secundari paragraf">Un paràgraf</p>
<ul>
  <li>Primer element de la segona llista</li>
  <li>Segon element de la segona llista</li>
  <li>Tercer element de la segona llista</li>
</ul>
<script>
console.log('-- Capçaleras h1 amb classe secundari --');
var elementsTitols = document.querySelectorAll('h1.secundari');
for (var i=0; i<elementsTitols.length; i++) {
  console.log(elementsTitols[i].textContent);
}

console.log('-- Tots els elements de la primera llista --');
var elementsLlista = document.querySelectorAll('li');
for (var i=0; i<elementsLlista.length; i++) {
  console.log(elementsLlista[i].textContent);
}

console.log('-- Primers elements de les llistes --');
var elementsPrimers = document.querySelectorAll('li:first-child');
for (var i=0; i<elementsPrimers.length; i++) {
  console.log(elementsPrimers[i].textContent);
}
</script>
```
Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/XjWVky?editors=1011.

Com es pot apreciar, en el primer cas se seleccionen tots els elements amb l'etiqueta `h1` amb la classe `secundari`. Així doncs, només troba una coincidència, ja que tot i que hi ha dos elements amb l'etiqueta `h1` i dos elements amb la classe `secundari`, només hi ha un element que compleixi les dues condicions.

En el segon cas s'han seleccionat tots els elements amb l'etiqueta li, de manera que el seu efecte resultat és idèntic al que retornaria el mètode `documentgetElementsByTagName('li');`.

A l'últim cas, en canvi, s'ha afegit al selector:first-child, de manera que en lloc de retornar tots els elements de les llistes, només retorna el primer element de cadascuna.

<a id="markdown-244-lextensió-htmldocument" name="244-lextensió-htmldocument"></a>
### 2.4.4. L'extensió `HTMLDocument`

En el cas dels documents HTML, a banda de totes les propietats i mètodes de la interfícieDocument, s'aplica l'extensióHTMLDocument, que afegeix algunes propietats i mètodes extres que no es troben quan es treballa amb documents XML o SVG. Entre les més destacables es troben:

- __`activeElement`__ : referència a l'element enfocat.

- __`cookie`__ : cadena de text que permet consultar o modificar les galetes del document.

- __`forms`__ (només lectura): llista d'elements de tipusform(formularis).

- __`images`__ (només lectura): llista d'elements de tipusimg(imatges).

- __`getElementsByName(String name)`__ : retorna una llista d'elements amb el nom (atributname, habitualment utilitzat en formularis) passat com a argument.

- __`getSelection()`__ : retorna el text seleccionat al document.

- __`write(String text)`__ : escriu el text al document.

- __`writeln(String text)`__ : escriu el text al document i afegeix un salt de línia.

<a id="markdown-245-altres-propietats-body-documentelement-i-forms" name="245-altres-propietats-body-documentelement-i-forms"></a>
### 2.4.5. Altres propietats: `body`, `documentElement` i `forms`

La interfície `document` ofereix també dues propietats que permeten accedir directament als elements `body` i `html`: `body` i `documentElement` respectivament.

L'accés a l'element `body` és especialment útil per afegir la detecció de l'event `load`, ja que això permet detectar quan s'ha acabat de carregar el DOM. En cas contrari, es poden produir errors, per exemple si es volen realitzar modificacions
al DOM abans que aquest s'hagi acabat de carregar completament.

```js

document.body.onload = function() {
console.log("DOM carregat");
}

```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/rrVmgb?editors=0012.

Fixeu-vos queonloadés una drecera per l' event load, així doncs es podria haver fet servir també el mètode `addEventListener` per afegir la detecció de l'event.

Per altra banda, l'extensióHTMLDocumentafegeixforms a la propietat, que permet accedir a una llista d'objectes que conté la informació de tots els formularis del document i, al seu torn, cadascun d'aquests formularis permet accedir als seus elements:

```html

<form id ="primer">
  <input type ="text" />
</form>
<form id ="segon">
  <input type ="text" />
</form>
<script>
   console.log(`Nombre de formularis al document:`, document.forms.length);

   for (var i = 0; i <document.forms.length; i ++) {
     console.log(`id del formulari amb índex` + i + `:`, document.forms[i]. id );
   }
 </script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/WGQERN?editors=1011.

Tot i que en determinats casos pot ser útil accedir a aquesta propietat per recórrer tots els formularis del document, és poc habitual. Per una banda, els documents no acostumen a contenir múltiples formularis i, per altra banda, quan s'ha de treballar amb múltiples formularis s'acostuma a requerir un control més precís (s'obtenen a través del seu id).

<a id="markdown-25-la-interfície-element" name="25-la-interfície-element"></a>
## 2.5. La interfície `Element`

Aquesta interfície, com també `Document`, és herència de `Node` i d``EventTarget`, per tant, permet manipular els elements i gestionar esdeveniments. A més a més, afegeix mètodes per enregistrar i desenregistrar observadors del mateix element.

Mentre que `Document` facilita la creació i manipulació del document que es mostra al navegador, la interfície `Element` permet manipular els elements concrets, manipulant les classes que els afecten, la llista d'atributs i afegint o eliminant detectors d' events específics.

<a id="markdown-251-informació-bàsica-dels-elements-tagname-classname-classlist-i-id" name="251-informació-bàsica-dels-elements-tagname-classname-classlist-i-id"></a>
### 2.5.1. Informació bàsica dels elements: 'tagName', 'className', 'classList' i 'id'

`classList` i `id`

Aquestes propietats permeten conèixer la informació bàsica d'un element. Fixeu-vos que aquesta és la que ens permet fer una cerca simple des del document, a través de la seva etiqueta, de les classes o de l'id. Vegem-les detingudament:

- `tagName` (només lectura): nom de l'etiqueta d'aquest element.

- `className` : cadena de caràcters separats per espais que inclou tots els noms
de classes que afecten l'element (per exemple, en aplicar un full d'estils CSS). Es pot modificar, per tant, permet afegir noves classes i establir una nova cadena de text com a valor.

- `classList` (només lectura): llista amb el nom de les classes que es pot recórrer com un array.

- `id`: identificador únic de l'element dintre del document.

Com es pot apreciar a la llista anterior, no es pot modificar ni eltagNameni la llista
de classes, però aquesta darrera pot modificar-se amb dos mètodes que aquesta proporciona:

- `add(String classe)`: afegeix a l'element la classe indicada pel paràmetre. Si ja hi era a l'element, no fa res. Té una versió que admet diferents classes, separades per comes, i que fa exactament el mateix, però per a cada classe que rep com a paràmetre.

- `remove(String nomClasse)` : suprimeix de l'element la classe indicada pel paràmetre. Si l'element no té la classe que es demana suprimir, no fa res.

Té també una versió que admet diferents classes, separades per comes, i que suprimeix de l'element cadascuna de les classes rebudes com a paràmetre de la mateixa manera que es feia amb una.

```
Propietats d”Element`
Podeu trobar més informació sobre la interfície Element en l'enllaç següent: goo.gl/0bCjXA.
```

Podem veure com utilitzar-les al següent exemple:

```html

<style>
.vermell{
  color:red;
}

.negreta{
  font-weight:bold;
}
</style>
<p id="para">paràgraf de prova</p>


<script>

var paragraf=document.getElementById("para");

paragraf.classList.add("vermell");
paragraf.classList.add("negreta");

alert("Hem afegit els estils vermell i negreta.\n\n Ara eliminarem l'estil vermell.\n\n Prem una tecla per continuar");

paragraf.classList.remove("vermell");

alert("Hem suprimit l'estil vermell.\n\n Ara eliminarem també negreta.\n\n Prem una tecla per continuar.");

paragraf.classList.remove("negreta");
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/NwEMmJ.

El següent exemple treballa amb les propietats `tagName` i `className`:

```html
<h1 class="principal">Primera capçalera</h1>
<p id="contingut" class="principal paragraf" title="Aqui va un paràgraf">Un paràgraf</p>
<script>
var elementH1 = document.getElementsByTagName('h1')[0];
var elementP = document.getElementsByTagName('p')[0];

elementH1.tagName = 'H2';

console.log('-- Tag dels elements --');
console.log(elementH1.tagName);
console.log(elementP.tagName);

console.log('-- Classes dels elements --');
console.log(elementH1.className);
console.log(elementP.className);

console.log('-- Modificació de els classes dels elements --');
elementH1.className = elementH1.className + ' ampliat';
elementP.className = 'canvi per noves classes ';

console.log('-- Classes dels elements ampliats--');
console.log(elementH1.className);
console.log(elementP.className);

console.log('-- Llista de classes del paràgraf --');
for (var i = 0; i < elementP.classList.length; i++) {
  console.log("Classe " + i + ":" + elementP.classList[i]);
}

console.log('-- Identificadors dels elements --');
console.log('Capçalera: ' + elementH1.id);
console.log('Paràgraf: ' + elementP.id);
elementH1.id = 'actualitzat';
elementP.id = elementP.id + ' actualitzat';

console.log('-- Identificadors dels elements actualitzats--');
console.log('Capçalera: ' + elementH1.id);
console.log('Paràgraf: ' + elementP.id);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/xExYXV?editors=1012.

Fixeu-vos que tant en el cas de `className` com aides pot assignar com a valor una cadena de text, sigui una de nova o concatenant el valor anterior. En tots dos casos el valor per defecte que prenen és una cadena buida, de manera que es poden concatenar sense fer cap consideració especial.


Relació entre `className` i `classList`

El següent exemple mostra com, tal com és d'esperar, en modificar `className` també es modifica `classList`. Concretament, implementa els mètodes `afegirClasse` i `eliminarClasse`, que fan el mateix, respectivament, que classList.add i `classList`.remove, però sense utilitzar aquests. En la pràctica, aquest codi només té utilitat si es fa una aplicació per navegadors antics, que no proporcionen la propietat `classList`.


Una opció seria dividir la cadena de caràcters assignada a `className` fent servir el mètode split, i seguidament recórrer l'arraygenerat per fer l'acció desitjada, però això no és necessari perquè la propietat `classList` ja conté aquest array:

```html
 <style>
 .principal {
  background-color: grey;
}

.vermell {
  color: red;
}

.important {
  font-weight: bold;
}
 </style>
<h1 class="principal">Primera capçalera</h1>
<p id="contingut" class="principal paragraf" title="Aquí hi va un paràgraf">Un paràgraf</p>
 <script>
 var afegirClasse = function(element, classe) {
  var trobada = false;
  for (var i=0; i<element.classList.length; i++) {
    if (element.classList[i] == classe) {
      trobada = true; // Ja es troba a l'element, no cal afegir-la
    }
  }
  if (!trobada) {
    element.className += ' ' + classe;
  }
}

var eliminarClasse = function(element, classe) {
  var nouClassName = '';
  for (var i=0; i<element.classList.length; i++) {
    if (element.classList[i] != classe) {
      nouClassName += element.classList[i] + ' ';
    }
  }
  element.className = nouClassName;
}

var elementH1 = document.getElementsByTagName('h1')[0];
var elementP = document.getElementsByTagName('p')[0];

afegirClasse(elementH1, 'vermell');
afegirClasse(elementH1, 'vermell');
console.log(elementH1.className); // No es duplica

eliminarClasse(elementH1, 'principal');
 </script>

```

Podeu veure aquest exemple en l`enllaç següent: codepen.io/ioc-daw-m06/pen/VKwQGz?editors=1111.


Com es pot comprovar, la funció `afegirClasse` afegeix la classe i evita possibles
repeticions, i la funció `eliminarClasse` elimina la classe sense haver d`editar manualment la cadena de text i crea una nova cadena de text a partir de la llista de classes que no coincideixin amb la que es vol eliminar.

Per simplificar més la utilització d'aquestes funcions es poden afegir al prototipus d'Element, d'aquesta manera són accessibles directament per tots els elements. Modifiqueu el codi JavaScript de l`exemple anterior pel següent:


```js
Element.prototype.afegirClasse = function(classe) {
  var trobada = false;
  for (var i = 0; i < this.classList.length; i++) {
    if (this.classList[i] == classe) {
      trobada = true; // Ja es troba a l'element, no cal afegir-la
    }
  }
  if (!trobada) {
    this.className += ' ' + classe;
  }
}

Element.prototype.eliminarClasse = function(classe) {
  var nouClassName = '';
  for (var i = 0; i < this.classList.length; i++) {
    if (this.classList[i] != classe) {
      nouClassName += this.classList[i] + ' ';
    }
  }
  this.className = nouClassName;
}

var elementH1 = document.getElementsByTagName('h1')[0];
var elementP = document.getElementsByTagName('p')[0];

elementH1.afegirClasse('vermell');
elementH1.afegirClasse('vermell');
console.log(elementH1.className); // No es duplica

elementH1.eliminarClasse('principal');

```

Podeu veure aquest exemple en l`enllaç següent: http://codepen.io/ioc-daw-m06/pen/yaLvWL?editors=1111.


Fixeu-vos que la funcionalitat és idèntica, però en lloc d'haver d'invocar una
funció i passar cada vegada l'element que s`ha de modificar i la classe, ara es
poden invocar directament a partir de l'element concret que es vulgui manipular: `elementH1.afegirClasse(`vermell');`.

<a id="markdown-252-obtenció-dels-descendents-com-html-innerhtml" name="252-obtenció-dels-descendents-com-html-innerhtml"></a>
### 2.5.2. Obtenció dels descendents com HTML: `innerHTML`

Aquesta propietat és molt interessant perquè permet obtenir i establir el codi HTML dels nodes descendents de l'element. És a dir, en lloc de crear una branca d'un arbre i afegir-la com a nodes, és possible assignar a aquesta propietat el codi HTML que correspondria:

```html

 <div id ="contingut"></div>

 <script>
 var contingut = document.getElementById(`contingut`);
 contingut.innerHTML = `<h1>Això és una capçalera</h1>`;
 </script>
```

Podeu veure aquest exemple en l'enllaç següent: http://codepen.io/ioc-daw-m06/pen/VKwdGz?editors=1010.

Com es pot apreciar, és fàcil de fer servir, però la cadena de codi HTML es pot complicar ràpidament si s'hi han d'afegir múltiples elements:

```html

 <div id ="contingut"></div>

 <script>
 var contingut = document.getElementById(`contingut`);
 contingut.innerHTML = `<h1>Això és una capçalera</h1><p>I això un paràgraf amb un <a href ="#">enllaç</a>.</p>`;
 </script>

```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/NRWzJJ?editors=1010.

Fixeu-vos que només s'ha afegit un paràgraf amb un enllaç a continuació de la capçalera, però el codi és molt menys entenedor i és més difícil detectar els errors.

Per altra banda, com que es tracta d'una cadena de text, es pot manipular de la mateixa manera, per exemple: fent servir expressions regulars per fer canvis al text o concatenant valors per generar la cadena i seguidament assignant-la com a propietat:

```html
 <div id ="contingut">Carregant dades...</div>

 <script>
var estudiants = ['Josep', 'Maria', 'Carles', 'Montserrat'];
var codiHtml = '';

codiHtml += '<ul>';

for (var i = 0; i < estudiants.length; i++) {
  codiHtml += '<li>' + estudiants[i] + '</li>';
}

codiHtml += '</ul>';

var contingut = document.getElementById('contingut');
contingut.innerHTML = codiHtml;
 </script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/yaLEdL?editors=1010.

Cal destacar que tot el contingut de l'element és reemplaçat, per aquesta raó no es mostra el text "Carregant dades": és reemplaçat per la llista de noms una vegada s'executa el codi JavaScript.

Per descomptat, és possible consultar la propietat per obtenir el codi HTML corresponent als descendents del node:

```html

<div id="contingut">
  <ul>
    <li>Josep</li>
    <li>Maria</li>
    <li>Carles</li>
    <li>Montserrat</li>
  </ul>
</div>
<script>

document.getElementById('contingut');
console.log(contingut.innerHTML);

</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/mAdKNK?editors=1011.

<a id="markdown-253-atributs-attributtes-getattribute-removeattribute-setattribute" name="253-atributs-attributtes-getattribute-removeattribute-setattribute"></a>
### 2.5.3. Atributs: `attributtes`, `getAttribute`, `removeAttribute`, `setAttribute`

La interfícieElementsofereix una propietat per consultar la llista completa d'atributs i tres mètodes per afegir, actualitzar o eliminar un atribut complet.

La propietat `attributes` (de només lectura) permet consultar la llista completa d'atributs. Els atributs es retornen com un objecte que es pot recórrer com si es tractés d'un array. Per consultar el nom i el valor de cadascun d'aquests atributs
es pot consultar la propietat `name`i `value` respectivament:

```html

<h1 id ="titol" class ="vermell principal">Aquesta és la capçalera</h1>
<script>
var titol = document.getElementById('titol');
for (var i = 0; i <titol.attributes.length; i ++) {
console.log(titol.attributes[ i ]. name + `:` + titol.attributes[ i ]. value );
}
</script>

```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/WGNKAV?editors=1011.

Per altra banda, a diferència de la llista de noms de classes, amb els atributs no cal fer una implementació pròpia dels mètodes d'addició i eliminació, ja que la mateixa interfície els inclou:

- `getAttribute` : retorna el valor de l'atribut.

- `removeAttribute` : elimina l'atribut.

- `setAttribute` : estableix el valor de l'atribut.

```html

<style>
 .vermell {
 color:red;
 }
</style>
<h1 id ="titol" class ="vermell principal">Aquesta és la capçalera</div>
<script>
var titol = document.getElementById('titol');

titol.setAttribute('title', 'Això es mostra en posar el cursor a sobre');
titol.removeAttribute('class');
console.log('L\'identificador és: ' + titol.getAttribute('id'));
 </script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/QKWBvw?editors=1111.

Cal destacar que a HTML5 es va afegir la possibilitat de definir atributs personalitzats; d'aquesta manera és possible, per exemple, emmagatzemar identificadors de productes o tipus especials d'elements:

```html
<div data−id−producte="42">...</div>
```

Tot i que els navegadors admeten la definició d'atributs amb qualsevol nom l'especificació requereix que incloguin el prefix data-i que no continguin majúscules, per exemple:data-id-producte. Aquests nous atributs es poden fer servir després per obtenir el seu valor o per seleccionar els elements fent servir selectors.

<a id="markdown-254-modificar-estils-css-style" name="254-modificar-estils-css-style"></a>
### 2.5.4. Modificar estils CSS: `style`

A HTML és possible modificar els estils concrets d'un element a través de l'atribut style. Normalment els estils aplicats d'aquesta forma tenen prioritat sobre qualsevol altre que afecti l'element.

Tot i així, quan es vol tractar amb aquest atribut des de JavaScript no és tan simple com caldria esperar, perquè s'han de tenir en compte dos aspectes fonamentals:

- El valor final de la propietat no és l'indicat a l'atribut, sinó el calculat, que pot estar modificat per altres regles de diferents orígens (fulls d'estil, navegador...).

```
Propietat 'style' Podeu trobar més informació sobre la propietat style en l'enllaç següent: goo.gl/BYa2IC.
```

- En consultar el valor de l'atribut style d'un element des de JavaScript, s'obté una col·lecció i no una cadena de text.

Per altra banda, si es vol treballar amb el contingut textual de la propietat es pot
fer o bé fent servir el mètode `setAttribute` o modificant la propietat `cssText` de la col·lecció retornada per `style`:

```html
<p id="paragraf1" style="color: red; font-weight: bold">Paràgraf 1</p>
<p id="paragraf2" style="color: red; font-weight: bold">Paràgraf 2</p>

<script>

var paragraf1 = document.getElementById('paragraf1');
var paragraf2 = document.getElementById('paragraf2');

paragraf1.setAttribute('style', 'color:green;');
paragraf2.style.cssText = 'color: blue';

console.log(paragraf1.style.cssText);
console.log(paragraf2.style.cssText);

</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/zKKNwa?editors=1011.

Com es pot apreciar, tant fent servir el mètode `setAttribute` com assignant el valor directament a la propietat `cssText`, el valor de la propietat és substituït; per aquesta raó cap dels dos textos es mostra en negreta.

És a dir, en cas de voler modificar alguna de les propietats d'estil CSS s'hauria de crear una nova cadena de text amb el contingut correcte i reemplaçar el valor de la propietat `style.cssText`.

Una manera més adequada de treballar amb els estils concrets és fer-ho a través de la col·lecció. Fixeu-vos en l'exemple següent, partint d'un element HTML que conté dos estils (canvi de color a vermell i font gruixuda), s'elimina el color, es modifica el gruix de la font i s'afegeix un nou estil per augmentar-ne la mida. Per facilitar la reutilització i fer-lo més entenedor s'ha aplicat el disseny descendent i s'ha creat una funció per a cada acció:

```html

<p id ="paragraf" style ="color: red; font−weight: bold">Paràgraf</p>

<script>
var mostrarEstils = function (element) {
  var estil = element.style;
  var css = window.getComputedStyle(paragraf, null);
  for (var i=0; i<estil.length; i++) {
    console.log (estil[i] + ':' +css[estil[i]] + ";");
  }
}

var afegirEstil = function (element, clau, valor) {
  element.style[clau] = valor;
}

var eliminarEstil = function (element, clau) {
  afegirEstil(element, clau, null)
}

var actualitzarEstil = function (element, clau, valor) {
  afegirEstil(element, clau, valor);
}

var paragraf = document.getElementById('paragraf');

console.log("-- Estil original --");
mostrarEstils(paragraf);
afegirEstil(paragraf, 'font-size', '30px');
eliminarEstil(paragraf, 'color');
actualitzarEstil(paragraf, 'font-weight', 'lighter');

console.log("-- Estil modificat --");
mostrarEstils(paragraf);

</script>
```

Podeu veure aquest exemple en el següent enllaç: codepen.io/ioc-daw-m06/pen/dprOEx?editors=1011.

El primer que us cridarà l'atenció és la complexitat que té mostrar els estils, ja 
que s'ha d'invocar el mètode `window.getComputedStyle` per obtenir un objecte amb la informació de tots els valors calculats per l'objecte.

S'ha de tenir en compte que no només s'apliquen els estils de la propietat, sinó que s'apliquen també els propis del navegador i els dels fulls d'estil carregats. És possible obtenir només els valors aplicats al propi estil, però aquests valors no són
finals: pot ser que una altra regla CSS ho hagi sobreescrit, per exemple, si s'ha
aplicat el modificador `!important` a una regla que l'afecti.

Una vegada s'ha obtingut la llista de propietats calculades, es recorren els noms dels estils establerts a la propietatstylecom si es tractés d'un array , ja que la propietat `style` és una col·lecció que té una propietat `length`, i cada element es
troba referenciat per un enter que es fa servir com a índex.

D'aquesta manera, combinant els valors calculats amb els estils aplicats a l'element, es pot mostrar una llista dels valors reals aplicats a l'element.

<a id="markdown-255-relacions-entre-elements-previouselementsibling-nextelementsibling-firstelementchild-i-lastelementchild" name="255-relacions-entre-elements-previouselementsibling-nextelementsibling-firstelementchild-i-lastelementchild"></a>
### 2.5.5. Relacions entre elements: `previousElementSibling`, `nextElementSibling`, `firstElementChild` i `lastElementChild`

Tot i que la interfície `Element` deriva de `Node` i, consegüentment, disposa de les propietats `previousSibling` i `nextSibling`, aquestes no retornen els elements, sinó els nodes. És a dir, inclouen tot tipus de nodes, com per exemple els nodes de tipus text que es generen en afegir un salt de línia o un tabulador.

En canvi, gràcies a `previousElementSibling` i `nextElementSibling`(totes dues propietats són de només lectura), es poden consultar els nodes anterior i posterior directament:

```html

<ul>
<li>Primer element de la llista</li>
<li id ="central">Segon element de la llista</li>
<li>Tercer element de la llista</li>
</ul>
<script>
var central = document.getElementById('central');
  
console.log('El contingut de l\'element anterior és: ', central.previousElementSibling.textContent);
  
console.log('El contingut de l\'element següent és: ', central.nextElementSibling.textContent);
</script>
```
Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/rrVydz?editors=1011.

Com es pot comprovar, a la consola es mostra correctament el contingut textual del primer i el tercer element, ignorant els nodes de tipus text.

De la mateixa manera, es pot accedir al primer i l'últim element a través de les
propietats `firstElementChild` i `lastElementChild`:

```html

<ul id ="llista">
  <li>Primer element de la llista</li>
  <li>Segon element de la llista</li>
  <li>Tercer element de la llista</li>
</ul>
<script>
var central = document.getElementById('llista');

console.log('El contingut del primer element és: ', central.firstElementChild.textContent);

console.log('El contingut del darrer element és: ', central.lastElementChild.textContent);
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/xEGqWa?editors=1011.

<a id="markdown-256-cerca-delements-descendents-simplegetelementsbyclassname-getelementsbytagname" name="256-cerca-delements-descendents-simplegetelementsbyclassname-getelementsbytagname"></a>
### 2.5.6. Cerca d`elements descendents simple:`getElementsByClassName`, `getElementsByTagName`

La funcionalitat dels mètodes `getElementsByClassName` i `getElementsByTagName` és idèntica a la que proporciona la interfície `Document` amb la peculiaritat que la cerca només es fa entre els descendents del mateix element.

Cal destacar que no s'inclou un mètode `getElementById`, ja que els identificadors són únics i no és rellevant si és o no descendent d'un element concret, com es pot comprovar en l'exemple següent:

```html

<ul>
  <li>Primer element de la llista</li>
  <li id ="central">
    <ul>
      <li>Primer element de la subllista</li>
      <li>Segon element de la subllista</li>
    </ul>
  </li>
  <li>Tercer element de la llista</li>
</ul>

<script>
var central = document.getElementById('central');
var elementsSubLlista = central.getElementsByTagName('li');

for (var i=0; i<elementsSubLlista.length; i++) {
  console.log(elementsSubLlista[i].textContent);
}
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/RGwBxE?editors=1011.

Cal destacar que tot i que inicialment s'invoca `getElementById` per obtenir la referència a l'element amb identificador `central`, a continuació se cerquen els elements a partir d'aquest i no pas dedocument. Així doncs, es limita la cerca als seus descendents i el resultat obtingut són els elements de la subllista.

<a id="markdown-257-cerca-delements-descendents-amb-selectors-queryselector-queryselectorall" name="257-cerca-delements-descendents-amb-selectors-queryselector-queryselectorall"></a>
### 2.5.7. Cerca d'elements descendents amb selectors: 'querySelector', 'querySelectorAll'

`querySelectorAll`

Igual que els mètodes `getElementsByTagName` i `getElementsByClassName`, la funcionalitat d'aquests és molt similar a la dels mètodes amb el mateix nom de la interfícieDocument, però en aquest cas la cerca també es limita als elements descendents del mateix element.

En l'exemple següent podeu comprovar com es fa una selecció a partir d'un element, de manera que només retorna la llista d'elements descendents i no pas totes les coincidències del document:

```html

<ul>
<li>Primer element de la llista</li>
<li id ="central">
<ul data −quantaitat="0">
<li data −quantitat="0">Primer element de la subllista</li>
<li data −quantitat="19">Segon element de la subllista</li>
<li data −quantitat="0">Tercer element de la subllista</li>
</ul>
</li>
 <li data −quantitat="0">Tercer element de la llista</li>
 </ul>

<script>
var central = document.getElementById('central');
var elementsSubLlista = central.querySelectorAll('li[data-quantitat="0"]');

for (var i = 0; i < elementsSubLlista.length; i++) {
  console.log(elementsSubLlista[i].textContent + ' (data-quantitat=' + elementsSubLlista[i].getAttribute('data-quantitat') + ')');
}
</script>

```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/gwOjBN?editors=1011.

Fixeu-vos que s'ha fet servir un atribut propi, `data-quantitat`, i que el selector `li[data-quantitat='0']` ha filtrat els resultats de manera que només es mostren a la consola el primer i tercer element de la subllista, sense incloure ni l'element `ul` ni el segon element, que té com a valor de l'atribut 19. A més a més, com és d'esperar, tampoc no s'hi ha inclòs el tercer element de la llista, ja que no és descendent de l'element central.

<a id="markdown-26-integració-de-la-detecció-devents-amb-el-dom" name="26-integració-de-la-detecció-devents-amb-el-dom"></a>
## 2.6. Integració de la detecció d'events amb el DOM

La programació d' events permet interactuar amb l'aplicació web i afegeix la detecció d' events als elements (o al mateix document), de manera que l'aplicació pot reaccionar de diferents maneres, per exemple: afegint files a una taula, eliminant-les, modificant les classes CSS per canviar-ne els colors o aplicar efectes...

S'ha de tenir en compte que quan es dispara un event en un element fill, si no s'especifica el contrari, aquest travessa tots els nodes pare, de manera que finalment són rebuts pel node arrel, que és `document`.

És a dir, si s'implementa la gestió de l'esdeveniment `submit` al document, quan
s'enviï un formulari (es dispara l' event `submit`) contingut en un element fill, el
document detectarà aquest event.

A continuació podeu trobar una llista dels events més destacables a l'hora de tractar
amb un document o element:

- __`blur`__ : es dispara quan es perd el focus.

- __`focus`__ : es dispara quan l'element rep el focus.

- __`click`__ : es dispara quan es produeix un clic sobre el document.

- __`dblclick`__ : es dispara quan es produeix un doble clic sobre el document.

- __`keydown`__ , __`keypress`__ , __`keyup`__ : es disparen quan es detecta que s'ha premut una tecla.

- __`load`__ : es dispara quan es completa la càrrega del document.

- __`scroll`__ : es dispara quan es desplaça verticalment o horitzontalment el document.

- __`submit`__ : es dispara quan s'envia un formulari.

- __`input`__ : es dispara quan es modifica el valor d'un camp d'entrada (per exemple, un quadre de text).

- __`change`__ : es dispara quan es modifica el valor d'un camp d'entrada però, a diferència d`input, no es dispara l' event per cada canvi produït, només es dispara en determinades circumstàncies, com per exemple en canviar el focus a un altre element.

Això permet, per exemple, controlar quan es fa clic sobre qualsevol element d'una pàgina web, sense haver de gestionar aquest event en cadascun dels elements que formen la pàgina.

La interfície ofereix mètodes per "escoltar" quan es dispara un event (`addEventListener`), per deixar d'escoltar-lo (r`emoveEventListener`) i tot un seguit de dreceres en forma de mètodes que permeten realitzar les dues accions
per events concrets.


```

Quan es parla d`events, el terme ‘escoltar` (listening en anglès) fa referència a la
detecció de l`event al document o element.

```

La utilització de les dreceres comporta més limitacions, ja que no es pot afegir més d'una funció per a cada event , però pot simplificar el codi en casos molt simples (per exemple, per controlar la càrrega de documents o imatges).

<a id="markdown-261-afegir-detecció-desdeveniments-addeventlistener" name="261-afegir-detecció-desdeveniments-addeventlistener"></a>
### 2.6.1. Afegir detecció d'esdeveniments: 'addEventListener'

El mètode `addEventListener` permet enregistrar una funció que serà invocada quan es dispari l' event passat com a argument a l'element, per exemple quan es faci un doble clic sobre ell o es detecti un canvi en un camp del formulari.

En l'exemple següent podeu veure com s'ha afegit un comptador de caràcters que indica el nombre de caràcters introduït en una àrea de text i que, a més a més, en modifica el color segons els següents paràmetres:

- Menys de 100 caràcters o més de 156: text en vermell, el text és massa curt o massa llarg.

- Menys de 150 caràcters: text en taronja, el text és curt.

- Entre 150 i 156: text en verd, text amb llargària òptima.

```html
<style>
label,
small {
  display: block;
}

.massa-curt-o-llarg {
  color: red;
}

.curt {
  color: orange;
}

.correcte {
  color: green;
}
</style>
<div>
  <label>Introduex el contingut de la descripció meta</label>
  <textarea name="meta-description" id="meta-description" placeholder="Introdueix fins a 156 caràcters" / cols="80" rows="3"></textarea>
  <small>Nombre de caràcters: <span id="comptador" className="curt">0</span></small>
</div>
<script>
var camp = document.getElementById('meta-description'),
  comptador = document.getElementById('comptador');

var actualitzarComptador = function() {
  var llargaria = camp.value.length
  comptador.textContent = llargaria;
  if (llargaria > 156 || llargaria < 100) {
    comptador.className = 'massa-curt-o-llarg';
  } else if (llargaria < 150) {
    comptador.className = 'curt';
  } else {
    comptador.className = 'correcte';
  }
}

camp.addEventListener('input', actualitzarComptador);

</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/NddQWZ.

Com podeu apreciar, afegir un detector d' events és molt senzill, ja que només cal invocar el mètode `addEventListener` passant com a arguments el nom de l' event al qual es vol reaccionar i la funció que s'ha d'executar quan es dispari:
`camp.addEventListener('input', actualitzarComptador);`.

A continuació podeu comprovar, modificant el mateix exemple, la diferència més
important entre els events `input` i `change`. Mentre que el primer es dispara cada vegada que es modifica el contingut del `textarea`, el segon només es dispara en canviar el focus (per exemple, fent clic en un altre punt del document):

```js
camp.addEventListener(`change`, actualitzarComptador);
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/Xjbddo.

Alternativament, es podria fer servir la dreceraoninput, modificant la línia en què s'afegeix la detecció d' events per la següent:

```js
camp.oninput = actualitzarComptador;
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/jrPWvm.

Aquest format és més concís, però podria provocar errors si es fes servir aquest codi en un projecte més avançat en el qual s'haguessin de fer diferents accions quan es detectessin canvis (per exemple, guardar un esborrany): si s'ha fet servir aquest format en tots dos casos, només s'executaria la funció afegida en darrer lloc.

Per altra banda, les dreceres permeten incrustar el codi JavaScript directament al codi HTML com si es tractés d'un atribut:

```html
 <button onclick ="escriureMissatge();">Escriure missatge a la consola</button>

 <button onclick ="alert('Alerta!');">Mostra una alerta</button>

 <script>
 var escriureMissatge=function() {
 console.log(`Aquesta funció ha estat invocada des del botó`)
 }
 </script>
```

```
L'etiqueta `meta-description`

L'etiqueta meta-description conté el text que mostren els cercadors a tall de resum quan surt el llistat de pàgines trobades.
La llargària màxima recomanada de l'etiqueta per millorar el SEO és de 156 caràcters.
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/vXOKJd?editors=1011.

Com es pot apreciar, es poden invocar tant funcions pròpies com funcions predefinides de JavaScript.

<a id="markdown-262-eliminar-detecció-desdeveniments-removeeventlistener" name="262-eliminar-detecció-desdeveniments-removeeventlistener"></a>
### 2.6.2. Eliminar detecció d'esdeveniments: 'removeEventListener'

En alguns casos pot interessar-vos eliminar un detector d' events , per exemple, per deshabilitar un botó d'enviar formulari si els camps de text són buits o no s'ha passat la validació.

En el següent exemple podeu veure com s'afegeixen i eliminen els detectors dinàmicament, de manera que només es pot clicar sobre el quadre blau:

```html
<style>
  div {
    width: 100px;
    height: 100px;
    background-color: grey;
    float: left;
    margin: 5px;
  }

  span {
    padding: 0 3px;
  }

  .seleccionat {
    background-color: green;
    color: white;
  }

  .proper {
    background-color: blue;
    color: white;
  }
</style>
<p>
  El quadre clicable es mostra de color <span class="proper">blau</span> i
  l'últim quadre clicat de color <span class="seleccionat">verd</span>
</p>
<div id="a"></div>
<div id="b"></div>
<div id="c"></div>
<script>
  var quadreA = document.getElementById("a");
  var quadreB = document.getElementById("b");
  var quadreC = document.getElementById("c");

  var seleccionarA = function() {
    quadreA.className = "seleccionat";
    quadreB.className = "proper";
    quadreC.className = "";

    quadreA.removeEventListener("click", seleccionarA);

    quadreB.addEventListener("click", seleccionarB);
    console.log(this);
  };

  var seleccionarB = function() {
    quadreB.className = "seleccionat";
    quadreC.className = "proper";
    quadreA.className = "";
    quadreB.removeEventListener("click", seleccionarB);
    quadreC.addEventListener("click", seleccionarC);
  };

  var seleccionarC = function() {
    quadreC.className = "seleccionat";
    quadreA.className = "proper";
    quadreB.className = "";
    quadreC.removeEventListener("click", seleccionarC);
    quadreA.addEventListener("click", seleccionarA);
  };

  var inicialitzar = function() {
    quadreA.className = "proper";
    listenerA = quadreA.addEventListener("click", seleccionarA);
  };

  inicialitzar();
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/gwpAKx.

Com es pot apreciar, només cal indicar el nom de l' event (el seu tipus) i la funció que s'ha d'eliminar. És a dir, en cas que hi hagués múltiples funcions lligades al mateix event , només s'eliminaria la indicada.

En cas de fer servir dreceres, per eliminar un detector només cal assignar el valor nul al mètode:

```js
var quadreA = document.getElementById("a");
var quadreB = document.getElementById("b");
var quadreC = document.getElementById("c");

var seleccionarA = function() {
  quadreA.className = "seleccionat";
  quadreB.className = "proper";
  quadreC.className = "";
  quadreA.onclick = null;
  quadreB.onclick = seleccionarB;
};

var seleccionarB = function() {
  quadreB.className = "seleccionat";
  quadreC.className = "proper";
  quadreA.className = "";
  quadreB.onclick = null;
  quadreC.onclick = seleccionarC;
};

var seleccionarC = function() {
  quadreC.className = "seleccionat";
  quadreA.className = "proper";
  quadreB.className = "";
  quadreC.onclick = null;
  quadreA.onclick = seleccionarA;
};

var inicialitzar = function() {
  quadreA.className = "proper";
  quadreA.onclick = seleccionarA;
};

inicialitzar();
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/LRVNwR.

Com es pot veure, independentment de si es fan servir dreceres o no, crear una funció per a cada element que cal detectar no és gens pràctic. A l'exemple anterior si és volgués augmentar el nombre de quadres, caldria modificar les tres funcions existents i afegir-n'hi una altra. A més a més, totes les funcions són pràcticament idèntiques. Aquest és un senyal molt clar que cal refactoritzar el codi.

Una opció és aprofitar les relacions entre nodes: en aquest cas el proper node sempre és el següent, i un cop no n'hi ha més es pot navegar directament al primer fill del node pare:

```html
<style>
  div#quadres div {
    width: 100px;
    height: 100px;
    background-color: grey;
    float: left;
    margin: 5px;
  }

  span {
    padding: 0 3px;
  }

  #quadres div.seleccionat {
    background-color: green;
    color: white;
  }

  #quadres div.proper {
    background-color: blue;
    color: white;
  }
</style>
<p>
  El quadre clicable es mostra de color <span class="proper">blau</span> i
  l'últim quadre clicat de color <span class="seleccionat">verd</span>
</p>
<div id="quadres">
  <div></div>
  <div></div>
  <div></div>
  <div></div>
  <div></div>
  <div></div>
</div>
<script>
  var quadres = document.getElementById("quadres");
  var seleccionat;
  var proper;

  var seleccionar = function() {
    // S'elimina l'estil i el detector del seleccionat anterior
    console.log(seleccionat, proper);
    seleccionat.className = "";
    seleccionat.removeEventListener("click", seleccionar);

    // S'actualitza el seleccionat al proper quadre
    seleccionat = proper;
    seleccionat.className = "seleccionat";

    // Es determina el proper quadre i s'afegeix el detector
    proper = seleccionat.nextElementSibling;
    if (!proper) {
      proper = quadres.firstElementChild;
    }
    proper.className = "proper";
    proper.addEventListener("click", seleccionar);
  };

  var inicialitzar = function() {
    seleccionat = quadres.firstElementChild;
    proper = seleccionat.nextElementSibling;
    seleccionar();
  };

  inicialitzar();
</script>
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/KgprwE.

Com es podeu veure, s'ha modificat el codi HTML per afegir un element contenidor (quadres); ja no cal fer servir unidper a cada quadre i s'ha refinat el codi CSS perquè els estils només han d'afectar els elements `div` descendents de quadres.

Ara bé, si no es poden fer servir les relacions entre elements, es pot aprofitar el context en el qual s'invoquen les funcions. S'ha de tenir en compte que dintre de la funció invocada, el seu context és el node al qual s'ha lligat el detector. Així doncs, és possible generalitzar aquestes funcions per fer servir el node com a context.

En l'exemple següent podeu comprovar com es genera aleatòriament quin serà el proper element, només cal reemplaçar el codi JavaScript pel següent:

```js
var quadres = document.getElementById("quadres");
var darrerSeleccionat;

var seleccionar = function() {
  var proper;

  // S'elimina l'estil i el detector del seleccionat anterior
  if (darrerSeleccionat) {
    darrerSeleccionat.className = "";
  }

  // S'actualitza l'element actual
  this.removeEventListener("click", seleccionar);
  this.className = "seleccionat";
  darrerSeleccionat = this;

  // Es determina el proper quadre i s'afegeix el detector
  proper = seleccionarQuadreAleatori();
  proper.className = "proper";
  proper.addEventListener("click", seleccionar);
};

var seleccionarQuadreAleatori = function(noIncloure) {
  var maxIndex = quadres.childNodes.length - 1;

  // S'han de descartar el darrer node seleccionat per no repetir i els nodes de text
  do {
    index = Math.floor(Math.random() * (maxIndex + 1));
    proper = quadres.childNodes[index];
  } while (proper.nodeName != "DIV" || proper === darrerSeleccionat);
  return proper;
};

seleccionar();
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/VKLPxQ.

Fixeu-vos que en aquest exemple no cal controlar quin és l'element actual ni el proper globalment, només es guarda la referència al darrer seleccionat per poder esborrar-lo quan es cliqui el següent element i evitar que el mateix element es repeteixi. També s'ha eliminat la funció d'inicialització: no cal inicialitzar cap variable, només cal invocar `seleccionar`.

Per altra banda, s'ha afegit la funció `seleccionarQuadreAleatori`, que genera un nombre entre 0 i el nombre de nodes descendents de l'element pare menys 1 (recordeu que els índexs dels arrays es compten començant per 0) i es van comprovant els nodes fins que se'n troba un que sigui de tipus **DIV** i no sigui el darrer seleccionat. Heu de tenir en compte que `childNodes` retorna una llista de nodes i, consegüentment, s'inclouen també els nodes amb text que es troben
entre els elements: salts de línia i tabulacions.

<a id="markdown-27-cas-pràctic-generador-de-factures" name="27-cas-pràctic-generador-de-factures"></a>
## 2.7. Cas pràctic: generador de factures

A continuació trobareu un exemple pràctic, un generador de factures. Hi podeu veure com s'integren les característiques principals de les interfícies del DOM, com pot ser la cerca, la consulta, la creació i l'eliminació d'elements.

Primerament, afegiu el següent codi HTML i CSS en un nou document per crear l'estructura del generador de factures, que està dividit en dues seccions:

• Una àrea d'entrada de dades formada per 3 quadres de text i un botó.

• Una taula que contindrà les línies de la factura i el peu que mostra els totals.

```html
<style>
  div {
    margin-bottom: 15px;
  }

  label {
    width: 100px;
    display: inline-block;
  }

  input {
    width: 100px;
  }

  th {
    width: 136px;
  }

  td {
    text-align: right;
  }

  td:first-child {
    text-align: left;
  }

  tfoot th {
    text-align: left;
  }

  tfoot th:last-child {
    text-align: right;
  }

  tfoot,
  thead,
  tbody,
  table {
    border: 1px solid black;
  }

  thead,
  tfoot {
    background-color: grey;
  }

  tbody tr:hover {
    background-color: #2897e8;
  }
</style>
<div>
  <h3>Introducció de productes a la factura</h3>
  <label for="producte">Producte:</label>
  <input type="text" id="producte" />
  <label for="quantitat">Quantitat:</label>
  <input type="number" id="quantitat" value="0" />
  <label for="preu-unitari">Preu unitari:</label>
  <input type="number" id="preu-unitari" value="0" />
  <button id="afegir">Afegir</button>
</div>

<table rules="groups">
  <thead>
    <tr>
      <th>Producte</th>
      <th>Quantitat</th>
      <th>Preu unitari</th>
      <th>Preu total</th>
      <th>Accions</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <th colspan="4">Base imposable</th>
      <th><span id="base-imposable">0</span>€</th>
    </tr>
    <tr>
      <th colspan="4" data-iva="0.21">IVA 21%</th>
      <th><span id="iva">0</span>€</th>
    </tr>
    <tr>
      <th colspan="4">Total factura</th>
      <th><span id="total">0</span>€</th>
    </tr>
  </tfoot>
  <tbody></tbody>
</table>
```

Quant al codi HTML, cal destacar que s'ha afegit la propietat id per als següents elements:

- Entrada de text `producte` per introduir el nom del producte.

- Entrada de text `quantitat` per introduir la quantitat de productes facturats.

- Entrada de text `preu-unitari` per introduir el preu unitari del producte.

- Botó `afegir` per afegir la nova línia a la factura.

- Element `base-imposable` per mostrar la base imposable total.

- Element `iva` per mostrar el total calculat per l'IVA.

- Element `total` per mostrar el total a pagar.

Addicionalment, s'ha afegit l'atribut propi `data-iva` amb el valor 0.21 de manera que és possible modificar el percentatge d'IVA que s'ha d'aplicar a la factura modificant, directament, aquest atribut. Així doncs, és possible modificar aquest valor per aplicar, per exemple, un 7% d'IVA (0.07).

El codi CSS només s'utilitza per donar estil al document. S'ha aplicat un fons de color gris a la capçalera i al peu de la taula. A més a més, per destacar quina és la fila a la qual afectaran les accions, aquesta canvia de color quan el cursor és a sobre.

El codi JavaScript, tot i que a primera vista pot semblar complicat, és força senzill.

No és res més que l'aplicació de les funcionalitats i l'accés a les propietats dels elements i el document.

Primer de tot hi ha la funció `inicialitzar`, que és l'encarregada d'inicialitzar tots els elements necessaris de l'aplicació. Aquesta funció és invocada automàticament quan es completa la càrrega del DOM:

```js
var inicialitzar = function() {
  var boto = document.getElementById("afegir");
  boto.onclick = afegirLinia;
};

// Inicialització de l'aplicació quan es carregui el DOM
document.body.onload = inicialitzar;
```

Dins de la funció `inicialitzar` se cerca l'element amb identificador `afegir`, que correspon al botó i assigna a l' event `click` la funció `afegirLinia`, fent servir la drecera `onclick`. Seguidament, s'assigna aquesta funció a l' event `load` de `document.body`, de manera que aquesta funció s'executa una vegada s'acaba de carregar el DOM.

Fixeu-vos que si en canvieu l'ordre, l'aplicació no funcionarà correcta
ment. Primer s'ha de declarar la funció o el valor que s'assignarà a
`document.body.onload`, que serà null.

La següent funció és `afegirLinia`, que és invocada quan es fa clic al botó `afegir`:

```js
var afegirLinia = function() {
  var nomProducte = document.getElementById("producte").value;
  var quantitatProducte = document.getElementById("quantitat").value;
  var preuUnitari = document.getElementById("preu-unitari").value;
  var totalProducte = quantitatProducte * preuUnitari;

  afegirFilaTaula(nomProducte, quantitatProducte, preuUnitari, totalProducte);
  recalcularTotal();
  netejarLinia();
};
```

Com es pot apreciar, en la implementació d'aquest programa s'ha aplicat el disseny descendent, de manera que s'ha dividit el codi en múltiples funcions específiques.

En primer lloc, s'obté el valor dels tres camps de text. Com que no cal guardar la referència a l'element, s'accedeix directament a la seva propietat `value`:

`document.getElementById('producte').value`. Així, doncs, `nomProducte`
contindrà el valor de l'element amb identificador `producte`. Una manera menys concisa d'implementar-lo seria la següent:

```js
var elementNomProducte = document.getElementById(`producte`);
var nomProducte = elementNomProducte.value;
```

Una vegada s'han obtingut laquantitatProductei elpreuUnitari, es calcula el preu total i es passen aquests quatre valors a la funció `afegirFilaTaula` per afegir les dades a la taula. Seguidament s'invocare `calcularTotal` (que recalcula la base imposable, l'IVA i l'import total), i finalment `netejarLinia`, per eliminar les dades de l'entrada de text.

La funció `afegirFilaTaula`, tot i que és la més llarga de 'aplicació, és molt simple: bàsicament es repeteix el mateix codi per a cada columna. Es podria haver fet servir un array alternativament, però per simplificar el codi i fer-lo més entenedor s'ha optat per duplicar-lo:

```js
var afegirFilaTaula = function(
  nomProducte,
  quantitatProducte,
  preuUnitari,
  totalProducte
) {
  var cosTaula = document.querySelector("tbody");

  var fila = document.createElement("tr");

  var col1 = document.createElement("td");
  var col2 = document.createElement("td");
  var col3 = document.createElement("td");
  var col4 = document.createElement("td");
  var col5 = document.createElement("td");

  col1.innerHTML = nomProducte + " (detall)";
  col2.innerHTML = quantitatProducte;
  col3.innerHTML = preuUnitari + "€";
  col4.innerHTML = totalProducte + "€";
  col5.innerHTML = "(eliminar)";

  col1.addEventListener("click", mostrarDetall);
  col5.addEventListener("click", eliminarFila);

  fila.appendChild(col1);
  fila.appendChild(col2);
  fila.appendChild(col3);
  fila.appendChild(col4);
  fila.appendChild(col5);

  cosTaula.appendChild(fila);
};
```

Primer de tot, s'obté la referència al cos de la taula (l'element `tbody`) amb el mètode `document.querySelector`, perquè aquest permet accedir directament a l'element com si fos un selector CSS i sempre retorna un únic element (al contrari de `document.getElementsByTagName`, que retorna un array ).

A continuació, es creen els nous elements que s'afegiran:

- Una nova fila: `document.createElement('tr')`.

- Cinc noves cel·les, una per a cada columna: `document.createElement('td')`.

Una vegada s'han creat les columnes (recordeu que es tracta de nodes de tipus `element`) s'assigna el contingut corresponent a cadascuna d'elles, i s'estableix la seva propietat `innerHTML`.

Tot seguit, s'afegeix la detecció de l' event click a les columnes 1 i 5, de manera que en clicar sobre les columnes s'invoca les funcions `mostrarDetall` o `eliminarFila`, respectivament.

Amb els continguts i la detecció d' events afegida, només resta afegir les columnes a la fila (`fila.appendChild(col1)`) i, seguidament, la fila a la taula (`cosTaula.appendChild(fila)`).

El següent mètode, recalcularTotal, és l'encarregat de recalcular els totals que es mostren al peu de la taula. Aquest mètode és més complex, perquè es treballa amb selectors, accés als elements descendents i germans i s'accedeix a propietats.

```js
var recalcularTotal = function() {
  var files = document.querySelectorAll("tbody tr");
  var valorBase = 0;

  for (var i = 0; i < files.length; i++) {
    var columnaUltima = files[i].lastElementChild;
    var columnaPenultima = columnaUltima.previousElementSibling;
    var valorTotalFila = parseFloat(columnaPenultima.textContent);
    valorBase += valorTotalFila;
  }

  var elementBase = document.getElementById("base-imposable");
  elementBase.innerHTML = valorBase;

  var elementPercentatgeIVA = document.querySelector("[data-iva]");
  var valorPercentatgeIVA = elementPercentatgeIVA.getAttribute("data-iva");
  var valorIVA = parseFloat(valorPercentatgeIVA * valorBase);

  var elementIVA = document.getElementById("iva");
  elementIVA.innerHTML = valorIVA;

  var elementTotal = document.getElementById("total");
  elementTotal.innerHTML = valorBase + valorIVA;
};
```

Fixeu-vos que per obtenir totes les files s'invoca `document.querySelectorAll('tbody tr')`, de manera que s'obtenen totes les files (elements de `tipustr`) que es trobin dins de l'element `tbody`. És a dir, s'exclouen les files de la capçalera i del peu de la taula. Cal destacar que a diferència de `querySelector`, que retorna només un únic element, `querySelectorAll` retorna una col·lecció d'elements.

Seguidament es recorre aquesta col·lecció per extreure la informació de cada línia de la factura i calcular-ne el valor base total. Com que la columna que interessa és la cinquena, s'ha optat per accedir a l'últim element descendent de la fila (`files[i].lastElementChild`) i a continuació a l'element anterior (`columnaUltima.previousElementChild`).

Per assegurar que el valor que s'afegeix és un nombre real (és a dir, no s'interpreta com una cadena de text), s'invoca la funcióparseFloati aquest valor s'afegeix a la variable `valorBase`. Una vegada acaba l'execució del bucle, la variable `valorBase` correspondrà al total de la base imposable que s'afegeix al document a través de la propietat `innerHTML` de l'element amb l'identificador base-imposable.

El següent pas és calcular l'IVA. Per fer-ho primer s'obté la referència a l'element que conté la propietat data-iva invocant `document.querySelector('[data-iva]')`. Seguidament, s'invoca `elementPercentatgeIVA.getAttribute(`data-iva')`per obtenir el valor d'aquest atribut que indica el percentatge que s'ha d'aplicar. Una vegada s'ha calculat, s'afegeix al document assignant-lo a la propietat`innerHTML`de l'element`iva`.

Amb tots dos valors calculats, només queda sumar-los i afegir-los al document com a contingut de l'element `total`.

La funció `netejarLinia` és molt més simple que l'anterior. De la mateixa manera com s'obtenen els valors a la funció `afegirLinia`, s'estableixen els valors per defecte de les entrades de text: una cadena buida per al producte i 0 per a la quantitat i el preu unitari.

```js
var netejarLinia = function() {
  document.getElementById(`producte`).value = "";
  document.getElementById(`quantitat`).value = 0;
  document.getElementById(`preu−unitari`).value = 0;
};
```

Seguidament es troba el codi que s'invoca en detectar-se l' event `click` sobre la primera i l'última columna. En el primer cas només cal destacar que s'obtenen tots els elements amb l'etiquetat `d` del node pare, i després es recorre aquesta llista per construir el text que es mostrarà com a detall:

```js
var mostrarDetall = function() {
  var missatge = `Detall de la factura:\n`;
  var elementsFila = this.parentNode.getElementsByTagName(`td`);
  var etiquetes = [`Producte`, `Quantitat`, `Preu unitari`, `Preu total`];
  for (var i = 0; i < elementsFila.length; i++) {
    missatge += `\t` + etiquetes[i] + `: ` + elementsFila[i].textContent + `\n`;
  }
  alert(missatge);
};
```

Fixeu-vos que es fa servir `this` per accedir a les propietats pròpies de l'element clicat. Tot i que totes les cel·les de la primera columna criden aquesta funció, el context en el qual s'executen sempre és l'element concret on s'ha disparat l' event.
Per acabar, hi ha el codi de la funció `eliminarFila`. En primer lloc s'elimina la mateixa fila i per fer-ho s'accedeix al node pare del pare. És a dir, es travessa el node ascendentment fins a l'element `tr` (la fila), seguidament, fins a l'element `tbody` que la conté, i a partir d'aquest, s'elimina. Seguidament, s'invoca la funció `recalcularTotal()` per actualitzar els valors del peu de la taula.

```js
var eliminarFila = function() {
  this.parentNode.parentNode.removeChild(this.parentNode);
  recalcularTotal();
};
```

A continuació podeu trobar el codi JavaScript complet del generador de factures:

```js
var inicialitzar = function() {
  var boto = document.getElementById(`afegir`);
  boto.onclick = afegirLinia;
};
// Inicialització de l`aplicació quan es carregui el DOM
document.body.onload = inicialitzar;
var afegirLinia = function() {
  var nomProducte = document.getElementById(`producte`).value;
  var quantitatProducte = document.getElementById(`quantitat`).value;
  var preuUnitari = document.getElementById(`preu−unitari`).value;
  var totalProducte =
    quantitatProductequantitatProductequantitatProductequantitatProducte\ *
    preuUnitari;
  afegirFilaTaula(nomProducte, quantitatProducte, preuUnitari, totalProducte);
  recalcularTotal();
  netejarLinia();
};
var afegirFilaTaula = function(
  nomProducte,
  quantitatProducte,
  preuUnitari,
  totalProducte
) {
  var cosTaula = document.querySelector(`tbody`);

  var fila = document.createElement(`tr`);

  var col1 = document.createElement(`td`);
  var col2 = document.createElement(`td`);
  var col3 = document.createElement(`td`);
  var col4 = document.createElement(`td`);
  var col5 = document.createElement(`td`);

  col1.innerHTML = nomProducte + `(detall)`;
  col2.innerHTML = quantitatProducte;
  col3.innerHTML = preuUnitari + `AC`;
  col4.innerHTML = totalProducte + `AC`;
  col5.innerHTML = `(eliminar)`;

  col1.addEventListener(`click`, mostrarDetall);
  col5.addEventListener(`click`, eliminarFila);

  fila.appendChild(col1);
  fila.appendChild(col2);
  fila.appendChild(col3);
  fila.appendChild(col4);
  fila.appendChild(col5);

  cosTaula.appendChild(fila);
};

var recalcularTotal = function() {
  var files = document.querySelectorAll(`tbody tr`);
  var valorBase = 0;

  for (var i = 0; i < files.length; i++) {
    var columnaUltima = files[i].lastElementChild;
    var columnaPenultima = columnaUltima.previousElementSibling;
    var valorTotalFila = parseFloat(columnaPenultima.textContent);
    valorBase += valorTotalFila;
  }
  var elementBase = document.getElementById(`base−imposable`);
  elementBase.innerHTML = valorBase;

  var elementPercentatgeIVA = document.querySelector(`[data−iva]`);
  var valorPercentatgeIVA = elementPercentatgeIVA.getAttribute(`data−iva`);
  var valorIVA = parseFloat(
    valorPercentatgeIVAvalorPercentatgeIVAvalorPercentatgeIVAvalorPercentatgeIVA\ *
      valorBase
  );

  var elementIVA = document.getElementById(`iva`);
  elementIVA.innerHTML = valorIVA;

  var elementTotal = document.getElementById(`total`);
  elementTotal.innerHTML = valorBase + valorIVA;
};

var netejarLinia = function() {
  document.getElementById(`producte`).value = 0;
  document.getElementById(`quantitat`).value = 0;
  document.getElementById(`preu−unitari`).value = 0;
};
var mostrarDetall = function() {
  var missatge = `Detall de la factura:\n`;
  var elementsFila = this.parentNode.getElementsByTagName(`td`);
  var etiquetes = [`Producte`, `Quantitat`, `Preu unitari`, `Preu total`];
  for (var i = 0; i < elementsFila.length; i++) {
    missatge += `\t` + etiquetes[i] + `:` + elementsFila[i].textContent + `\n`;
  }
  alert(missatge);
};
var eliminarFila = function() {
  this.parentNode.parentNode.removeChild(this.parentNode);
  recalcularTotal();
};
```

Podeu veure aquest exemple en l'enllaç següent: codepen.io/ioc-daw-m06/pen/XjbooE.
