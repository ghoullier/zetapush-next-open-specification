

### <a name="P04-SUPPR01"></a> [P04-SUPPR01] ETQ dev je supprime mon application (front et backend) en production
*GIVEN*
  - J'ai une application en production
  - J'ai l'identifiant de mon application 'my-first-app'

*WHEN*
  - J'exécute la commande : ```zeta delete ```

*THEN
  - J'ai une demande de confirmation : ```Your application 'my-first-app' will be deleted. Are you sur Y/n ?```
  - Si je répond oui alors l'application y compris le frontend sont supprimés


---

### <a name="P04-SUPPR02"></a> [P04-SUPPR02] ETQ dev je supprime mon front en production
*GIVEN*
  - J'ai une application en production
  - J'ai l'identifiant de mon application 'my-first-app'

*WHEN*
  - J'exécute la commande : ```zeta delete --front-only```

*THEN
  - J'ai une demande de confirmation : ```Your frontend 'my-first-app' will be deleted. Are you sur Y/n ?```
  - Si je répond oui alors le frontend est supprimé


---

### <a name="P04-SUPPR03"></a> [P04-SUPPR03] ETQ dev je supprime mon backend en production

*GIVEN*
  - J'ai une application en production
  - J'ai l'identifiant de mon application 'my-first-app'

*WHEN*
  - J'exécute la commande : ```zeta delete --worker-only```

*THEN
  - J'ai une demande de confirmation : ```Your backend 'my-first-app' will be deleted. Are you sur Y/n ?```
  - Si je répond oui alors le backend est supprimé

