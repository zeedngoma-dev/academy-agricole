# ACADEMY AGRICOLE — projet source complet (socle applicatif)

Ce dépôt fournit un socle Next.js/TypeScript structuré pour développer Academy Agricole : site public, catalogue filtrable, fiches formation, inscription/connexion Supabase, espace apprenant, endpoint serveur de tracking Meta CAPI et schéma SQL de départ.

## Démarrage local
1. Installer Node.js 20+.
2. Copier `.env.example` vers `.env.local`.
3. Créer un projet Supabase et renseigner `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY` et `SUPABASE_SERVICE_ROLE_KEY` (la clé service role reste strictement côté serveur).
4. Exécuter `supabase/schema.sql` dans l'éditeur SQL Supabase.
5. `npm install`
6. `npm run dev` puis ouvrir `http://localhost:3000`.

## Important — état réel des fonctionnalités
Ce projet est un socle de développement, pas une plateforme déjà prête à encaisser de vrais paiements. Les pages publiques et le catalogue sont utilisables. L'authentification nécessite la configuration Supabase. Le schéma SQL fournit les tables de départ. Le tracking Meta CAPI est câblé côté serveur si les variables secrètes sont renseignées, mais doit encore être relié aux événements métier et testé dans Meta Events Manager.

Les paiements réels, la validation de signature du webhook, l'activation des inscriptions après paiement, le back-office complet, les rôles formateur/admin, l'éditeur LMS, les fichiers vidéo privés, les factures, les certificats PDF/QR, les affiliés et les autres pixels restent à implémenter et valider avec les prestataires et identifiants réels. Le webhook de paiement répond volontairement 501 tant que la vérification de signature spécifique au prestataire n'est pas codée. Aucun paiement n'est simulé.

## Avant mise en production
- Choisir un prestataire de paiement contractuellement disponible en République du Congo et intégrer sa documentation officielle.
- Implémenter la vérification cryptographique des webhooks et une logique idempotente de fulfillment.
- Ajouter policies RLS complètes pour administrateurs et formateurs, tests d'autorisation et migrations.
- Stocker vidéos et supports dans un bucket privé, servir des URL signées à durée courte.
- Ajouter validation/assainissement, limitation de débit, journalisation, sauvegardes, monitoring et tests automatisés.
- Implémenter consentement cookies avant activation des pixels marketing.
- Ajouter CAPI deduplication : même `event_id` côté navigateur et serveur; ne pas envoyer d'informations personnelles sans base légale/consentement requis.
- Configurer domaine, HTTPS, emails transactionnels et pages CGV/confidentialité.

## Arborescence
- `src/app`: pages et routes API
- `src/lib`: données de catalogue et clients Supabase
- `supabase/schema.sql`: structure relationnelle initiale
