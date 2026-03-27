


# TP CI/CD

Nicolas PATINO - Jean PAUL LALANDE

## Questions et réponses: 

* Pourquoi `latest` n’est pas une version ?
Parce que latest est un tag mouvant : il pointe simplement vers la dernière image poussée. Il n’identifie donc pas une version précise, immuable et traçable.

* Différence tag vs digest ?
Un tag est un nom lisible par un humain, comme latest ou v1.0.0, mais il peut être déplacé.
Un digest est un identifiant unique basé sur le contenu exact de l’image, donc immuable.

* Pourquoi séparer staging/prod ?
Parce que cela permet de valider les changements dans un environnement proche de la production avant de les exposer aux utilisateurs. On réduit ainsi le risque de déployer directement des erreurs en production.

* Pourquoi une version `vX.Y.Z` ne doit jamais être reconstruite ?
Parce qu’une version doit rester strictement identique dans le temps. La reconstruire pourrait produire une image différente sous le même numéro de version, ce qui casse la reproductibilité et la traçabilité.

* Citez les avantages d'une PR gate.
Elle permet de bloquer l’intégration d’un code non validé, d’imposer le passage des tests avant merge, d’améliorer la qualité du code, de faciliter la revue entre développeurs et de garder une trace claire des changements validés.

* Qu’est-ce qui garantit la traçabilité ici ?
La traçabilité est assurée par les commits Git, les pull requests, les tags de version comme v1.0.0, les tags Docker comme le SHA du commit, et les digests d’images qui identifient de manière unique chaque build.

