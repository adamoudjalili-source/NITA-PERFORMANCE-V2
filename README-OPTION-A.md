# Option A — Aperçu en temps réel (Codespaces/Gitpod + Devtools)

## Étapes Codespaces
1. Pousse ce dossier `.devcontainer` à la racine de ton repo.
2. Dans GitHub > Settings > Codespaces > Secrets, ajoute :
   - SUPABASE_URL
   - SUPABASE_ANON_KEY
   - SUPABASE_SERVICE_ROLE_KEY
3. Ouvre **Create codespace on main**.
4. Dans le terminal Codespaces :
   ```bash
   mvn spring-boot:run -Dspring-boot.run.profiles=dev
   ```
5. Dans l’onglet **Ports**, mets le port 8080 en **Public** (si non auto).
6. Ouvre l’URL 8080 dans un **navigateur externe** (plus simple pour l’extension LiveReload).

## LiveReload
- Ajoute la dépendance Devtools (voir `pom-devtools-snippet.xml`).
- Installe l’extension navigateur **LiveReload** (Chrome/Edge).
- Chaque fois que tu modifies un template Thymeleaf, un contrôleur ou des assets,
  la page se rafraîchit automatiquement.
  *Remarque :* le rafraîchissement complet (restart) se produit lors de changements de classes Java.

## Étapes Gitpod (alternative)
1. Pousse `.gitpod.yml` à la racine du repo.
2. Dans Gitpod > Variables, déclare SUPABASE_URL / SUPABASE_ANON_KEY / SUPABASE_SERVICE_ROLE_KEY.
3. Ouvre le workspace : il lancera automatiquement `mvn spring-boot:run -P dev` et exposera un URL public.

## Commandes utiles
- Profil dev :
  ```bash
  mvn spring-boot:run -Dspring-boot.run.profiles=dev
  ```
- Forcer le redémarrage automatique :
  ```bash
  mvn spring-boot:run -Dspring-boot.run.profiles=dev -Dspring-boot.run.jvmArguments="-Dspring.devtools.restart.enabled=true"
  ```

## Pièges fréquents & solutions
- **Pas de refresh Thymeleaf** : vérifie `spring.thymeleaf.cache=false` et que le profil `dev` est actif.
- **Pas de LiveReload** : l’extension navigateur doit être installée et la page ouverte en externe (pas seulement l’aperçu intégré).
- **Port non public** : dans Codespaces, mets 8080 en *Public*.
- **Changements Java non vus** : Devtools redémarre l’app; si pas d’effet, supprime `target/` et relance.
- **Variables Supabase** : ne pas les hardcoder; utilise les secrets d’environnement de la plateforme.
