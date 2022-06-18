---
title: Portée
slug: Glossary/Scope
tags:
  - Encodage
  - Glossaire
translation_of: Glossary/Scope
original_slug: Glossaire/Portée
---
Le contexte d'{{glossary("exécuter","exécution")}} courant. Le contexte dans lequel les {{glossary("Value","valeurs")}} et **expressions** sont "visibles," ou peuvent être référencées. Si une **{{glossary("variable")}}** ou autre expression n'est pas "dans la portée actuelle", alors son utilisation ne sera pas possible. Les portées peuvent aussi être empilées hiérarchiquement de manière à ce que les portées enfants puissent accéder aux portées parentes, mais pas l'inverse.

Une **{{glossary("fonction")}}** sert de **fermeture** en {{glossary("JavaScript")}}, et crée ainsi une portée, pour cette raison, par exemple, une variable définie exclusivement à l'intérieur de la fonction ne sera pas accessible en dehors de celle-ci ni depuis d'autres fonctions.

## Exemple d'accès à une variable
Imaginons que nous souhaitons accéder à une variable avant sa déclaration. Dans ce cas précis, la une erreur sera retournée.

```js 
console.log(a):
let a;

// error : cannot access 'a' before initialization
``` 
Dans l'exemple ci-dessus, le même phénomène se produit. En effet la variable est accessible dans le bloc de la fonction et non en dehors de celle-ci.

```js
function myFunction() {
 let a = 2;
}

console.log(a)
// Uncaught ReferenceError: a is not defined
```
Le scope est une source d'erreur fréquente qui demande une certaine vigilance lors de l'écriture de votre code.

## Pour approfondir

### Culture générale

- {{Interwiki("wikipedia", "Portée (informatique)")}} sur Wikipédia
