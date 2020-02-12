# Conventions d'écriture

Afin d'améliorer la lisibilité du code et de faciliter le refactoring, le présent document définit les conventions d'écriture du projet _Blog Coddity_. A l'intention des développeurs, il est conseillé de lire ce document et d'en adopter les principes.

# Sommaire

1. [Style d'écriture du code](#style-code)
    1. [Soft-wrap et retours à la ligne](#soft-wrap)
    2. [Démarcation au sein d'un composant](#demarcation-code)
    3. [Bindings de fonctions](#binding)
2. [Gestion du dépôt Git](#git)

# [Style d'écriture du code](#style-code)

## [Soft-wrap et retours à la ligne](#soft-wrap)

## [Démarcation au sein d'un composant](#demarcation-code)

Il est recommandé de scinder un composant trop large et peu spécifique en plusieurs sous-composants courts et spécifiques, conformément au [principe de responsabilité unique](https://fr.wikipedia.org/wiki/Principe_de_responsabilit%C3%A9_unique). Cette habitude rend le code plus lisible et mieux construit. Toutefois, lorsque le composant est déjà court ou spécifique, cet exercice n'est pas nécessaire. Dans ce cas, le code source du composant peut être simplement démarqué en plusieurs sous parties, afin d'en améliorer la lisibilité et la compréhension. Veillez à ce que la démarcation de vos fichiers ait un sens et qu'elle soit en harmonie avec le reste du projet. Evitez d'abuser des sous-parties : cela rendrait le code indéchiffrable.

```javascript

// --------------------------------------------------
// Librairies

import React from 'react';

// --------------------------------------------------
// Composant

class Composant extends React.Component
{
    render() {
        return null;
    }
}

```

## [Bindings de fonctions](#binding)

Il est courant d'utiliser la valeur `this` au sein des event handlers pour faire référence aux composants où ils sont définis. Cependant, lorsque l'on passe un event handler par le biais d'un prop à un sous composant React, sa valeur `this` est altérée. Elle ne correspond plus au composant de définition de l'event handler, mais plutôt au composant recevant ledit handler. En Javascript, il s'agit d'un **binding implicite** ; [voir l'article suivant pour plus de détails sur la gestion du `this` en JS](). Dans un cas précis comme celui des event handlers, ce comportement est indésirable et peut être contourné par un **binding explicite**.

Il existe plusieurs méthodes pour "binder" une fonction (excusez-moi pour cet anglicisme). [La méthode recommandée par la documentation React est le binding au sein du constructeur](https://reactjs.org/docs/handling-events.html#___gatsby). Cette méthode a le mérite d'être explicite ; toutefois, elle est verbeuse.

```javascript
import React from 'react';

class MagicButton extends React.Component
{
    constructor() {
        super(props);
        
        this.state = {
            clicked: false
        };

        // Ici, on bind l'event handler
        this.handleClickEvent = this.handleClickEvent.bind(this);
    }

    handleClickEvent() {
        this.setState({
            clicked: true
        });
    }

    render() {
        return <button onClick={this.handleClickEvent}>Cliquez-moi !</button>;
    }
}
```

# [Gestion du dépôt Git](#git)

