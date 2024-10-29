# projet-ci-cd

exemple opti : https://nicolas-poste.medium.com/optimisations-de-gitlab-ci-5-minutes-pour-en-gagner-beaucoup-plus-ae33b31717de

Solution pour améliorer le build et le déploiement de la CI :

- **Optimisés les tests :**
    - Utilisation de `parallel` pour exécuter les tests en parallèle.
    - Effectué des tests ciblés par module ou par fonctionnalité.
    - Identifier et corriger les tests "flakys" (tests intermittents) pour éviter les erreurs fantômes qui ralentissent la pipeline.

- **Optimisations de la pipeline :**
    - Séparer les étapes de build, tests et déploiement, et configurer des conditions pour que certaines étapes ne se déclenchent que si nécessaire.
    - Configurer le cache pour les dépendances (comme dans notre CI, avec `cache: npm` pour Node.js), pour éviter de les recharger à chaque build.
    - Exécuter uniquement les pipelines pour les branches pertinentes (ex. : main, dev) ou les commits avec certaines balises.

- **Quand on utilise des containers :**
    - Privilégier les images de base plus petites (comme alpine pour Linux) afin de réduire le temps de build et de téléchargement.
    - Utiliser le multistage build pour diviser les étapes de build en plusieurs étapes, et ainsi réduire la taille des images finales.

- **Gestion Efficace des Dépendances :**
    - Utiliser des gestionnaires de dépendances comme yarn ou npm.
    - Utiliser un fichier de verrouillage (package-lock.json, Gemfile.lock) pour assurer la cohérence des dépendances entre les builds.
    - Intégrer des outils (comme Dependabot et Renovate) pour suivre les mises à jour de dépendances et identifier celles qui pourraient accélérer les builds.

- **Utilisation d'artefacts :**
    - Stocker les artefacts générés lors des builds pour les réutiliser entre les étapes ou pour des tests ultérieurs.