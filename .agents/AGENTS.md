# Convention de codage personnel pour le langage : Python

Ce document rassemble mes règles, standards et garde-fous de développement pour **Python**. L'objectif est de maintenir une base de code propre, modulaire, prévisible et hautement maintenable.

---

## 1.1 Commentaires & Documentation
* **Commentaires en fin de ligne :** Utiliser un seul symbole `#`.
* **Lignes de commentaires / Blocs :** Utiliser deux symboles `##`.
* **Docstrings :** Une docstring par fonction sans exception. Les fonctions et méthodes dont la portée s'étend au-delà du fichier doivent impérativement suivre les conventions de style **Google Docstrings**.

## 1.2 Normes de Nommage & Visibilité
* **Variables, Fonctions & Méthodes :** Strictement en `snake_case`.
* **Classes :** En `PascalCase` / `CamelCase`.
* **Privatisation :** Utiliser un préfixe `_` pour usage interne.

## 1.3 Taille du Code & Modularité
* **Longueur des fonctions :** < 15 lignes (20 max).
* **Densité par fichier :** < 4 fonctions par fichier (6 max).
* **Classes par fichier :** 1 seule classe par fichier (exceptions: modèles Pydantic/dataclasses).

## 1.4 Imports
* **Imports de modules :** Si utilisé dans 2 blocs, au sommet. Sinon au sommet du bloc.
* **Imports locaux :** Au sommet, séparés par une ligne vide des modules standard.
* **From :** Max 5 éléments par `from`.

## 1.5 Bonnes pratiques
* **Type hints obligatoires.**
* **Exceptions explicites.**
* **Pas de valeurs par défaut mutables.**
* **Fonctions pures si possible.**
* **Constantes :** `MA_CONSTANTE`.
* **Entrée de test :** `if __name__ == "__main__":` pour les modules.
* **Pas de print en prod :** utiliser `logging`.
* **Tests obligatoires** pour la logique non triviale.
