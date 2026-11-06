# Orchestrateur ou integration continue ? (TP06)

| Critere | Prefect (orchestrateur) | GitHub Actions (CI) |
|-----------------------------------|-------------------------|---------------------|
| Ce qui declenche l'execution | Planification temporelle (cron, intervalle avec `serve`), webhook, ou appel manuel | Evenement Git (`push`, `pull_request`), tag, ou declenchement manuel (`workflow_dispatch`) |
| Ou s'execute le traitement | Machine locale ou worker dedie sur un work pool (VM locale, cluster Kubernetes, serveur de calcul) | Runners GitHub dans le cloud (`ubuntu-latest`, Windows, macOS) ou self-hosted runners |
| Qui surveille, et ou | Prefect Server ou Prefect Cloud (dashboard web dedie, port 4200 en local) | GitHub Actions (interface web dans l'onglet Actions du depot Git) |
| Ce qui se passe en cas d'echec | Reessais automatiques configurables (`retries`), alertes (Slack, email), mise en pause ou echec du flow | Arret immediat du job (code de retour != 0), rejet ou blocage de la PR, notification GitHub |
| Type de tache adapte | Pipelines de donnees (ETL), reentrainement periodique lourd de modeles ML, workflows distribues | Tests unitaires, validation de la qualite/metriques, linting, build et deploiement CI/CD |
| Ce qui est versionne dans Git | Code des flows (`flow_mlops.py`), configuration de deploiement (`prefect.yaml`), scripts | Fichiers de workflows YAML (`.github/workflows/ci.yml`), scripts de test et dependances CI |

## Conclusion (5 lignes)
Prefect et GitHub Actions sont deux outils complementaires au sein d'une demarche MLOps industrielle.
Prefect orchestre les flux de donnees et le reentrainement des modeles sur des infrastructures de calcul dediees avec planification et reprise sur erreur.
GitHub Actions securise l'integration continue en validant automatiquement le code, l'execution du pipeline et les seuils de qualite a chaque push.
L'orchestrateur pilote le cycle de vie de la donnee et du modele, tandis que la CI automatise la conformite et le cycle de vie du code applicatif.
Leur articulation garantit un developpement reproductible, des deploiements fiables et des modeles continuellement a jour en production.

