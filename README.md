# Ressources — Parcours IA G2

> Repo `ia-g2-ressources` — ressources transverses, partagées entre tous les
> briefs du parcours **« Concevoir et implémenter une solution d'IA »**
> (CISIA / OPCO ATLAS, Parcours 2 — Professionnels IT).

Ce repo est complémentaire des repos de briefs `ia-g2-parcours-*`, qui
contiennent chacun le squelette de code et les mini-cours d'un brief.

> 📌 Ce repo grandit **au rythme des modules**. Ce qui est présent ci-dessous
> couvre le **socle transverse + la transition M0 → M1**. Les fiches-patterns,
> cheatsheets et étagères async de chaque module seront ajoutés **quand la
> promo ouvrira le module concerné**. Fais `git pull` au début de chaque module.

---

## 📁 Contenu

| Fichier | Quand le mobiliser ? |
|---|---|
| [`00_competences_referentiels.md`](./00_competences_referentiels.md) | **Source de vérité des compétences** — 9 C techniques (CISIA) + 9 CT transversales (OPCO ATLAS) avec intitulés officiels, niveaux Simplon et mapping par module. À garder sous la main pendant tout le parcours. |
| [`glossaire_IA.md`](./glossaire_IA.md) | **Glossaire vivant** — vocabulaire data/IA démystifié (1-2 lignes/terme), tagué par module, 🎓 sur les termes du questionnaire C1/C2/C4. À garder ouvert dès M0. |
| [`recap_M0_vers_M1.md`](./recap_M0_vers_M1.md) | **Pont entre M0 et M1** — cycle ML, technos vues vs à venir, compétences cochées. À lire entre la fin de M0 et le démarrage de M1. |
| [`decouverte_pandas.ipynb`](./decouverte_pandas.ipynb) | **Découverte express (~20 min, hands-on)** — lire et explorer un tableau : `read_csv`, `head`/`info`, `describe`, `value_counts`, `groupby`, une visu. Données FastIA (tickets support). À *faire tourner* avant le premier jour de M1. |
| [`decouverte_scikit_learn.ipynb`](./decouverte_scikit_learn.ipynb) | **Découverte express (~15 min, hands-on)** — la grammaire scikit-learn `fit`/`predict`/`score` sur un petit dataset embarqué. À *faire tourner* une fois avant M1 si tu n'as jamais entraîné de modèle, **après** le notebook pandas. Ne fait **pas** la vraie démarche (ça, c'est M1-B1). |
| [`conventions_commit.md`](./conventions_commit.md) | **Format des messages de commit** — type, scope, description + exemples. À garder ouvert pendant les briefs avec rendu Git. |
| [`cheatsheet_git_template_workflow.md`](./cheatsheet_git_template_workflow.md) | **Workflow « Use this template »** — le cycle repo template → repo perso → clone → commits, puis le travail à deux (une branche par personne, fusion dans `main` par pull request, seul `main` est corrigé). Dès **M0**. |
| [`aide_memoire_M1.pdf`](./aide_memoire_M1.pdf) | **Aide-mémoire M1 (une page) — entraîner & évaluer proprement** — workflow en 7 étapes (EDA → split scellé → pipeline → fit → predict → métrique → verdict), règle d'or « on n'apprend que sur le train », métriques, fuite de données, pièges. À garder sous les yeux pendant M1. |
| [`fiche_pattern_ML_supervise.md`](./fiche_pattern_ML_supervise.md) | **Fiche-pattern du geste ML supervisé** — les étapes d'un pipeline d'apprentissage supervisé (split → entraînement → évaluation), le geste C5 travaillé dès **M1-B1**. Référence de consolidation post-brief. |
