# Convention de codage personnel pour le language : Python

Ce document rassemble mes règles, standards et garde-fous de développement pour **Python**. L'objectif est de maintenir une base de code propre, modulaire, prévisible et hautement maintenable.

---

## 1.1 Commentaires & Documentation
* **Commentaires en fin de ligne :** Utiliser un seul symbole `#`.

    ````python
    valeur_ajustee = valeur + 1  # Ajustement de l'index suite au décalage
    ````
* **Lignes de commentaires / Blocs :** Utiliser deux symboles `##`.
    ````python
    ## Vérification globale des prérequis système et de l'état
    ## du stockage local avant d'amorcer le traitement distribué.
    if not infrastructure.is_ready():
        raise SystemError("Infrastructure non initialisée")
    ````
* **Docstrings :** Une docstring par fonction sans exception. Les fonctions et méthodes dont la portée s'étend au-delà du fichier (fonctions publiques ou exportées) doivent impérativement suivre les conventions de style **Google Docstrings**.
    ````python
    from pathlib import Path
    from typing import Any, Optional, Union
    import json

    def _pretty_print(obj, indent=2, sort_keys=False, max_width=120):
        """
        Affiche proprement un dict ou un objet sérialisable en JSON.
        Si l'objet n'est pas JSON-serialisable, utilise pprint en secours.
        """
        try:
            s = json.dumps(obj, ensure_ascii=False, indent=indent, sort_keys=sort_keys)
            print(s)
        except (TypeError, ValueError):
            from pprint import pprint
            pprint(obj, indent=indent, width=max_width, sort_dicts=sort_keys)


    def load_json(path: Union[str, Path], default: Optional[Any] = None,
                encoding: str = "utf-8", *, raise_on_error: bool = False) -> Any:
        """Load a JSON file from disk, returning a default on error.

        Attempts to read and parse JSON from `path`. If the file is missing,
        unreadable, or contains invalid JSON, the function returns `default`
        unless `raise_on_error` is True, in which case the original exception
        is propagated.

        Args:
            path (str | Path): Path to the JSON file to read.
            default (Any, optional): Value to return on error. Defaults to None.
            encoding (str, optional): File encoding to use. Defaults to "utf-8".
            raise_on_error (bool, optional): If True, re-raise exceptions instead
                of returning `default`. Defaults to False.

        Returns:
            Any: Parsed JSON data (usually dict or list), or `default` on error.
        """
        p = Path(path)
        try:
            with p.open("r", encoding=encoding) as f:
                return json.load(f)
        except Exception:
            if raise_on_error:
                raise
            return default
    ````

## 1.2 Normes de Nommage & Visibilité
* **Variables, Fonctions & Méthodes :** Strictement en `snake_case` (ex: `calculer_metrique()`, `flux_donnees`).
* **Classes :** En `PascalCase` / `CamelCase` avec initiale majuscule (ex: `OrchestrateurSysteme`).
* **Privatisation :** Utiliser un préfixe avec un simple underscore `_` pour indiquer visuellement qu'une fonction, une variable ou une classe est à usage strictement interne au fichier/module (ex: `_configurer_socket`).

## 1.3 Taille du Code & Modularité
* **Longueur des fonctions :** Moins de 15 lignes de code par fonction (20 lignes grand maximum). Si une fonction nécessite davantage de lignes pour accomplir sa tâche, elle doit être extraite et isolée dans son propre fichier dédié.
* **Densité par fichier :** Moins de 4 fonctions par fichier (6 au grand maximum).
* **Classes par fichier :** Une seule classe par fichier. Les seules exceptions tolérées concernent les structures de données pures, légères et sans logique complexe (ex: modèles Pydantic, petites classes utilitaires d'usage local).

## 1.4 Imports :
* **Imports de modules :** si un module est utilisé dans au moins deux bloc, il doit être importé au sommet du fichier, sinon, il doit-être importé au somme du bloc

* **Imports d'autres fichier :** si on importe un autre fichier du projet, c'est au sommet du fichier et séparé des imports de module par une ligne vide

* **Utilisation de from :** utiliser un from pour importer au plus 5 éléments d'un même sous module

## 1.5 Bonnes pratiques additionnelles
* **Annotations de type :** Utiliser des type hints sur les signatures de fonctions, les retours et les structures de données importantes. Cela rend le code plus lisible et plus robuste.
* **Gestion explicite des erreurs :** Éviter les `except Exception` généraux quand c'est possible. Privilégier les exceptions spécifiques et lever des erreurs claires avec un message utile.
* **Valeurs par défaut immuables :** Éviter les objets mutables comme valeur par défaut (`[]`, `{}`) ; préférer `None` puis initialiser à l'intérieur de la fonction.
* **Fonctions pures et prévisibles :** Une fonction doit idéalement faire une seule chose, sans effets de bord cachés. Si elle modifie l'état global, le faire explicitement.
* **Constantes :** Mettre les constantes en majuscules avec underscores (`MA_CONSTANTE`).
* **entrée de tests :** tous packages le permettant doit offrir un point d'entrée de demonstration sous un `if __name__ == "__main" :`
* **Logs et sorties :** placeres `print()` de debug hors production ; les remplacer par `logging` en production ou par un compertement "verbose".
* **Tests :** Pour toute logique non triviale, ajouter des tests unitaires ou au moins un scénario de validation reproductible.
