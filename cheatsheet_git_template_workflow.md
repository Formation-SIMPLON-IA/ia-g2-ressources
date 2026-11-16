# Cheatsheet — workflow Git « Use this template » (individuel, à deux, seul·e sur un brief à deux)

> **Ressource transverse — à garder ouverte sur chaque brief de code (dès M0).**
> Réf rapide du **workflow** : du repo template à ta livraison, seul·e ou à deux.
>
> Complète [`conventions_commit.md`](./conventions_commit.md) (qui couvre les
> **messages** de commit). Ici on couvre **le cycle** : créer ton repo, démarrer
> proprement, collaborer, et ce qu'on commit (ou pas).

---

## 1. Le cycle « Use this template » (à chaque brief de code)

```
   Repo TEMPLATE du brief (ia-g2-parcours-mX-bY)
        │  clic « Use this template » (bouton vert, GitHub)
        ▼
   TON repo perso : <MX-BY>-<thème>-<prénom>     (sur TON compte GitHub)
        │  git clone
        ▼
   Ton dossier local  ──►  venv (Python 3.11) + install  ──►  tu travailles  ──►  commits
        │
        ▼
   git push  (chez toi) ──► lien du repo déposé sur Simplonline
```

> 💡 **« Use this template » ≠ fork.** Le template te crée un repo **neuf et
> indépendant** (pas d'historique lié), sur **ton** compte. Tes commits restent chez
> toi.

> ⚠️ **Seul `main` est corrigé.** Un travail resté sur une autre branche
> n'existe pas pour la correction : ce que tu veux rendre doit être dans `main`.

---

## 2. Démarrer proprement (les 4 commandes)

> Ces 4 commandes valent pour les briefs dont le `requirements.txt` est à la racine du repo
> (M0-B1, M1-B1, M1-B2). **M0-B2 démarre par `docker compose`** : voir le README de son
> repo template. **M1-B1 n'a pas de dossier `tests/`** : il a un `contract_test.py` (voir son README).

```bash
git clone git@github.com:<toi>/<MX-BY>-<thème>-<prénom>.git
cd <MX-BY>-<thème>-<prénom>
python3.11 -m venv .venv && source .venv/bin/activate   # un venv par repo
pip install -r requirements.txt
```

Puis lance le test fourni (`pytest -q`, quand le repo a un dossier `tests/`) ou le squelette
pour vérifier que tout tourne **avant** de coder.

> Variante HTTPS (sans clé SSH) :
> `git clone https://github.com/<toi>/<MX-BY>-<thème>-<prénom>.git`

> 💡 **Identité git** (une fois par machine, si pas déjà fait) :
> ```bash
> git config --global user.name "Ton Prénom Nom"
> git config --global user.email "ton.email@exemple.fr"
> ```
> Sinon tes commits sont mal attribués sur GitHub.
>
> Avec `uv` : `uv venv --python 3.11`, puis `uv pip install -r requirements.txt`
> (un `uv venv` n'embarque pas `pip`).

---

## 3. Trois cas, trois règles

| Cas | Brief | Règle |
|---|---|---|
| **(a) Brief individuel** | M0-B1, M1-B1, M1-B2 | Commits **directement sur `main`**. C'est permis et c'est la règle. |
| **(b) Brief à deux** | M0-B2 | **Une branche par personne** (`<prenom>`), **pull request vers `main`**, **jamais de commit direct sur `main`**. |
| **(c) Seul·e sur un brief prévu à deux** | M0-B2 | **Mêmes règles que (b)** : ta branche `<prenom>`, pull request vers `main`, tu fusionnes ta propre pull request, livrables dans `rendu/<prenom>/`. |

> ⚠️ **Seul `main` est corrigé.** Un travail resté sur une autre branche n'existe pas
> pour la correction : en (b) et (c), il ne compte qu'une fois **fusionné dans `main`
> par pull request**.

Pour le détail de M0-B2 (création du repo, invitation de l'autre personne, README commun,
conflits de fusion, dossier `rendu/<prenom>/`), **suis le README du repo template
`ia-g2-parcours-m0-b2`** : il fait foi.

### Cas (b) et (c) : les commandes

```bash
git switch -c <prenom>                 # ta branche
git add <fichiers> && git commit -m "feat(api): add /score endpoint"
git push -u origin <prenom>
# GitHub : Pull Request base = main <- compare = <prenom>, puis « Merge pull request »
git switch main && git pull            # récupérer ce qui a été fusionné
git switch <prenom> && git merge main  # remettre ta branche à jour avant la PR suivante
```

- Une pull request vers `main` au minimum à la fin de chaque séance et avant le rendu.
- À deux (b) : l'autre personne relit avant de fusionner. Seul·e (c) : tu fusionnes ta propre pull request.

### Facultatif (non demandé par le brief M0-B2)

Ces pratiques sont possibles, **aucune n'est exigée** :

| Pratique | Comment |
|---|---|
| `Co-authored-by` | en pair-coding, ajouter la ligne `Co-authored-by: Prénom Nom <email@exemple.fr>` (précédée d'une ligne vide) dans le message de commit |
| Message Discord à la fusion | un message dans le fil Discord du brief quand tu fusionnes dans `main` |
| Test croisé | avant de livrer, l'un clone et lance le repo de l'autre |
| Échange des rôles | décider qui fait quoi au démarrage, échanger en cours de route |

---

## 4. Ce qu'on commit — ce qu'on ne commit JAMAIS

Le `.gitignore` du template gère déjà l'essentiel. À retenir :

| ✅ On commit | 🚫 On ne commit pas |
|---|---|
| code (`src/`, `app/`, `tests/`) | `.venv/`, `__pycache__/`, `*.pyc` |
| `requirements.txt`, `Dockerfile`, `.gitignore` | `.env` et tout **secret** (clé API, mot de passe) |
| README, docs, notebooks (**avec leurs sorties** si c'est le notebook de rendu) | `.ipynb_checkpoints/` |
| données **toy** (< 1 Mo) | gros datasets → **script de téléchargement** |
| modèle `.joblib` **léger** (< 10 Mo, `compress=3`) | gros modèles → **script `train.py`** |

> 💡 **`git add .` à l'aveugle = piège n°1.** Tu finis par committer ton `.venv` ou
> un `.env`. Préfère `git status -s` puis `git add <fichiers ciblés>`.
>
> ⚠️ Un **secret commité reste dans l'historique** même après suppression. Si ça
> arrive : préviens, on régénère la clé (ne te contente pas d'un `git rm`).

---

## 5. Taguer une release

Quand un livrable est prêt, pose un **tag** (souvent demandé dans les briefs) :

```bash
git tag v2.0.0             # ex. M1-B1 -> v2.0.0 ; M1-B2 -> v0.1.0-api ; M5 -> v1.0.0-prod
git push origin v2.0.0
```

---

## 6. Le filet quotidien

```bash
git status -s                          # voir ce qui a changé
git add src/preprocess.py              # stager ciblé (pas git add .)
git commit -m "refactor(training): ..."  # message : cf. conventions_commit.md
git push
git log --oneline -5                   # relire ses derniers commits
```

Vise des **commits explicites et fréquents** (un par intention) — les briefs en
demandent en général **au moins 3-4** (ex. `eda` / `training` / `verdict`).

---

## 7. Pièges fréquents

| Piège | Conséquence | Réflexe |
|---|---|---|
| `git add .` à l'aveugle | `.venv`/`.env` committés | `git status -s` + add ciblé |
| Secret dans un commit | fuite persistante dans l'historique | régénérer la clé, prévenir |
| Identité git non configurée | commits « inconnus » sur GitHub | `git config user.name/email` |
| Commits `WIP` / vagues dans `main` | historique illisible | 1 intention = 1 commit clair |
| Travail resté sur une branche | rien à corriger dans `main` | fusionner dans `main` par pull request (M0-B2) avant le rendu |
| Gros modèle/dataset committé | repo lourd, clone lent | `.gitignore` + script de téléchargement |
| Sorties de notebook effacées dans le notebook de rendu | le correcteur ne voit pas les graphiques | conserve les sorties dans un notebook de rendu (le correcteur doit voir les graphiques) |

---

## 8. À retenir

- **« Use this template » → ton repo perso** (pas un fork), tu travailles chez toi.
- **Démarrer = 4 commandes** (clone, venv Python 3.11, install, test) **avant** de coder, pour les briefs avec `requirements.txt` à la racine ; M0-B2 : `docker compose` (voir son README).
- **Brief individuel** : commits directement sur `main`, **seul `main` est corrigé**.
- **Brief à deux, ou seul·e sur un brief prévu à deux (M0-B2)** : une branche `<prenom>`, pull request vers `main`, jamais de commit direct sur `main`.
- **Jamais** committer `.venv`, `.env`, secrets, gros datasets/modèles — `git add`
  **ciblé**, pas `.` à l'aveugle.
- Pour les **messages**, voir [`conventions_commit.md`](./conventions_commit.md).
