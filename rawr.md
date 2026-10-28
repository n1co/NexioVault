  **Robustesse produit (invisible mais décisif)**

  

  - **Décodage RAW dans un Web Worker** : aujourd'hui LibRaw tourne sur le thread principal — pendant un gros décodage, l'UI a des micro-gels. C'est le chantier perf le plus rentable qui reste, et il bénéficie aussi à l'iPad.

  - **Auto-update** de l'app desktop (electron-updater branché sur tes releases GitHub) — sinon personne n'aura jamais tes correctifs.

  - **Onboarding première ouverture** : un écran vide avec 15 boutons, c'est intimidant ; trois étapes guidées (créer le catalogue → importer → développer) changent la rétention.

  - **Rapport de crash local** (fichier de log exportable, pas de télémétrie — cohérent avec le positionnement).