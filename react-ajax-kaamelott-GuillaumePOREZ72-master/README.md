# Ajax Kaamelott

Avant toute chose, pense à bien analyser le projet.  

L'objectif final est d'avoir le logo de Kaamelott et une citation générée au chargement de la page, puis une nouvelle chaque fois que l'on clique sur un bouton.  

Pour cela on veux se servir d'une API qui recense les différentes blagues présentes dans la série. Voici la [documentation ici](https://github.com/A3lfyr/kaamelott-api).  
On se servira de la route suivante pour recevoir une nouvelle citation: https://kaamelott.reiter.tf/quote/random

Pour démarrer le projet actuel, il suffit de faire `yarn`, puis `yarn start`.

Dans cet exercice, tu pourras écrire tout le code directement à l'intérieur du composant `App`.

Si tu veux tenter sans indice supplémentaire, tu peux t'arrêter là dans les consignes et essayer par toi-même.

Si tu préfères être guidé, voici les différentes étapes qui t'amèneront vers l'objectif final.

## Étape 1: Gérer le state de la citation

- Importe le hook `useState` de React.
- Utilise `useState` pour déclarer un state `quote` avec la valeur initiale `null`.

Le state `quote` agira comme un conteneur pour la citation qui permet une gestion dynamique et conditionnelle, la persistance des données, et une interaction élégante avec le reste du système de composants de React.  
Dis plus vulgairement, on est entrain de dire à React qu'il faut surveiller cette valeur et mettre à jour notre composant chaque fois qu'elle est modifiée

## Étape 2: Création de la fonction getQuote

- Déclarer une fonction asynchrone `getQuote` dans le composant.
- Utiliser `fetch` pour faire une requête à l'API de citations.
- Transformer la réponse en JSON et utiliser `setQuote` pour mettre à jour le state quote.
- Gérer les erreurs en faisant apparaître une `alert` sur le site

<details>
  <summary>Indices</summary>
  
  ```js
  const getQuote = async () => {
    try {
      const response = await fetch("https://api.chucknorris.io/jokes/random");
      const data = await response.json();
      setQuote(data.value);
    } catch (error) {
      console.error(error);
      alert('Erreur de récupération');
    }
  }
  ```

L'url de l'API pour récuperer une nouvelle citation de Kaamelott est: https://kaamelott.reiter.tf/quote/random

Pense a bien vérifier la forme de l'objet que tu récupères avec un `console.log`

</details>

## Étape 3: Utilisation de useEffect

- Importer le hook `useEffect` de React.
- Ajouter un `useEffect` qui appelle la fonction getQuote lors du chargement initial du composant.

⚠️Attention: Si tu as une fonction asynchrone a l'intérieur de useEffect, il faut l'entourer d'une autre fonction. Exemple, si getQuote est asynchrone, il faudra écrire:

```js
useEffect(() => {
    getQuote();
  }, [])
```

<details>
  <summary>Indices</summary>  
  
La fonction useEffect dans React prend deux arguments :

1. La Fonction d'Effet : C'est une fonction qui contient le code à exécuter chaque fois que l'effet est déclenché. Cela peut inclure divers effets de bord, comme les appels réseau, les abonnements, les mises à jour manuelles du DOM, etc.

2. Le Tableau de Dépendances : C'est un tableau optionnel qui peut être passé comme second argument. Les valeurs dans ce tableau sont surveillées, et si l'une d'entre elles change, l'effet est déclenché à nouveau. Si vous passez un tableau vide [], l'effet ne sera déclenché lors du chargement initial du composant (et lors de sa disparition).

```js
  useEffect(maFonction, []);
```

</details>

## Étape 4: Structurer le JSX

- Remplacer le texte `Ma citation` par le state `quote.citation` dans le JSX uniquement si `quote.citation` n'est pas `null`. Tu devrais voir la citation apparaître sur la page.
- Modifier le bouton pour qu'il appelle `getQuote` lors d'un clic.
- Importer l'image `Kaamelott_Logo.png` depuis le répertoire approprié.
- Ajouter l'image avec la classe `logo` et l'attribut `alt` approprié.
- Ajouter un paragraphe en dessous de la citation qui liste les infos concernant le personnage, l'épisode et la saison
- Ajouter les classes `widget-content` et `cite` au paragraphe fraichement crée

## Étape 5: Tester son code

- S'assurer que le composant fonctionne comme prévu et que les citations sont bien affichées à partir de l'API.
- S'assurer également que les erreurs remontent correctement si j'appelle une API defectueuse.

## Bonus

- Explorer d'autres fonctionnalités de l'API (tu peux par exemple récuperer que les citations de ton personnage préféré)
- Ajouter des animations et transitions CSS.
- Ajouter un filtre pour lister les citations par personnage ou saison
