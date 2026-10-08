# LOG
Aquest document és la bitàcola del projecte: serveix per registrar el que s'ha fet i quins prompts d'IA s'han fet servir per fer-ho.

## Eina i model d'IA utilitzat
- **Eina**: Google Gemini
- **Model**: Gemini 3.6 Flash

## Registre d'usos de la IA

### Ús 1
**Prompt literal:**
"Com puc afegir un nou camp anomenat publisher a un formulari reactiu existent a Angular?"

**Resposta de la IA:** Va explicar que s'ha d'afegir el camp dins de la definició de `this.fb.group({})` passant el valor inicial i les validacions si calguessin, tipus `publisher: ['']`.

**Incoherències detectades:** Cap incoherència.

**Solució/adaptació manual:** Es va adaptar al formulari de llibres existent deixant-lo com un camp opcional inicialitzat amb un string buit.

---

### Ús 2
**Prompt literal:**
"Com carrego un valor per defecte a l'input publisher quan estic editant un llibre que ja en té un?"

**Resposta de la IA:** Va mostrar l'ús de `this.form.patchValue({})` dins del mètode que carrega les dades per actualitzar el valor del control.

**Incoherències detectades:** La IA no va tenir en compte que el camp podia ser `undefined` a la interfície si el llibre no el tenia.

**Solució/adaptació manual:** Es va afegir l'operador Nullish Coalescing per passar una cadena buida si no n'hi ha: `publisher: book.publisher ?? ''`.

---

### Ús 3
**Prompt literal:**
"Quin codi HTML necessito per connectar un input text amb el camp de formulari reactiu d'Angular?"

**Resposta de la IA:** Va donar l'estructura del `<input type="text" formControlName="publisher">`.

**Incoherències detectades:** Cap incoherència.

**Solució/adaptació manual:** Es va embolcallar dins d'un `<label>` seguint els mateixos estils que ja tenia l'arxiu `book-form.html` al projecte i afegint-hi un `placeholder`.

---

### Ús 4
**Prompt literal:**
"Com puc fer que la barra de cerca de la meva llista filtri també per l'editorial a part del títol i descripció?"

**Resposta de la IA:** Va indicar com modificar el mètode `.filter()` per encadenar una altra condició `|| book.publisher.includes(text)`.

**Incoherències detectades:** La IA va assumir que l'editorial sempre seria un string vàlid, però en el nostre cas el camp és opcional.

**Solució/adaptació manual:** Es va afegir una comprovació prèvia d'existència per evitar errors si el llibre no té editorial: `(book.publisher && book.publisher.toLowerCase().includes(text))`.

---

### Ús 5
**Prompt literal:**
"Com afegeixo una columna nova a una taula HTML i hi poso valors amb el nou control flow d'Angular 17?"

**Resposta de la IA:** Va explicar com posar el `<th>` a la capçalera i, dins del `<td>` de cada fila (que s'itera amb `@for`), utilitzar la sintaxi `@if (condició) { ... } @else { ... }` per mostrar condicionalment l'editorial o un guionet.

**Incoherències detectades:** Cap incoherència.

**Solució/adaptació manual:** Es va crear el condicional de manera que si el llibre no tenia editorial mostrés un guionet gris (`<span class="muted">—</span>`) per mantenir la consistència del disseny.

---

### Ús 6
**Prompt literal:**
"Per què la fila que diu 'No hay resultados' ja no ocupa tota la taula després d'haver afegit la columna d'editorial?"

**Resposta de la IA:** Va explicar que s'havia de modificar l'atribut `colspan` del `<td>` d'aquesta fila perquè coincidís amb el nombre total de columnes que ara té la taula.

**Incoherències detectades:** Cap incoherència.

**Solució/adaptació manual:** Es va canviar el valor de `colspan="9"` a `colspan="10"` al HTML del component `books-list`.

---

### Ús 7
**Prompt literal:**
"Com puc mostrar l'editorial només si existeix a les targetes HTML (mode grid) amb la nova sintaxi d'Angular?"

**Resposta de la IA:** Va donar el codi `@if (book.publisher) { <p>{{ book.publisher }}</p> }`.

**Incoherències detectades:** Cap incoherència.

**Solució/adaptació manual:** Es va adaptar amb la classe que feien servir la resta de targetes (`class="card-text"`) i posant la paraula "Editorial:" en negreta al davant.

---

### Ús 8
**Prompt literal:**
"Què necessito per poder construir (fer build) del projecte d'Angular sense errors un cop afegit tot això?"

**Resposta de la IA:** Va explicar que cal córrer la comanda `npm run build` o `ng build` i assegurar-se que no hi hagi errors de TypeScript en els canvis recents.

**Incoherències detectades:** Cap incoherència.

**Solució/adaptació manual:** En intentar fer-ho, es va haver d'usar `npx ng build` o executar primer `npm install` ja que localment no estaven instal·lats els `node_modules` en l'entorn de treball inicial, finalitzant amb un build net.
