# 💰 Gestion_Dépense

Application web complète de gestion des dépenses personnelles avec authentification JWT sécurisée et interface moderne.

![ExpenseTracker](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)
![Next.js](https://img.shields.io/badge/Frontend-Next.js%2016-black)
![NestJS](https://img.shields.io/badge/Backend-NestJS-ea2845)
![License](https://img.shields.io/badge/License-MIT-blue)

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   Frontend (Next.js)                    │
│  • Dashboard Responsive                                 │
│  • Login/Signup Moderne                                 │
│  • Gestion des Paramètres                               │
└────────────────────┬────────────────────────────────────┘
                     │ Axios + JWT
                     ▼
┌─────────────────────────────────────────────────────────┐
│                   Backend (NestJS)                      │
│  • API RESTful                                          │
│  • Authentification JWT                                 │
│  • Gestion des Dépenses & Catégories                    │
│  • Réinitialisation de Mot de Passe                     │
└────────────────────┬────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│                  PostgreSQL + Prisma                    │
│  • Base de données relationnelle                        │
│  • ORM type-safe                                        │
└─────────────────────────────────────────────────────────┘
```

---

## 🖥️ Frontend — Next.js

### 🚀 Fonctionnalités

- ✅ **Authentification Sécurisée**
  - Login / Signup / Logout
  - JWT stocké en cookie httpOnly
  - Protection des routes privées

- ✅ **Dashboard Responsive**
  - Statistiques en temps réel
  - Gestion des dépenses
  - Gestion des catégories
  - Filtrage par catégorie

- ✅ **Paramètres Utilisateur**
  - Modification du profil
  - Changement de mot de passe
  - Suppression de compte
  - Préférences de notifications

- ✅ **Design Moderne**
  - Interface responsive (mobile, tablette, desktop)
  - Animations fluides
  - Mode sombre compatible
  - Accessibilité optimisée

### 🛠️ Stack Technologique

| Technologie | Version | Usage |
|------------|---------|-------|
| **Next.js** | 16 | Framework React |
| **Tailwind CSS** | Latest | Styling responsive |
| **Axios** | Latest | HTTP Client |
| **React Hook Form** | Latest | Gestion des formulaires |
| **Lucide React** | Latest | Icônes |

### 📦 Installation Frontend

#### 1. Cloner le repository

```bash
git clone https://github.com/Sylvano96/gestion_depense_front.git
cd front
```

#### 2. Installer les dépendances

```bash
npm install
# ou
yarn install
# ou
pnpm install
```

#### 3. Configurer les variables d'environnement

Créer un fichier `.env.local` à la racine du projet :

```env
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

#### 4. Lancer le serveur de développement

```bash
npm run dev
```

L'application sera disponible sur [http://localhost:3000](http://localhost:3000)

```

---

## 🛡️ Backend — NestJS

### 🚀 Fonctionnalités Principales

- ✅ **Authentification JWT**
  - Login / Logout
  - JWT stocké en cookie httpOnly
  - Refresh token automatique
  - Protection des routes via JwtAuthGuard

- ✅ **Gestion des Utilisateurs**
  - Inscription avec validation
  - Modification du profil
  - Changement de mot de passe
  - Suppression de compte

- ✅ **Réinitialisation de Mot de Passe**
  - Code temporaire par email
  - Validation du token
  - Template email professionnel
  - Expiration de 30 minutes

- ✅ **Gestion des Dépenses**
  - CRUD complet
  - Filtrage par catégorie
  - Statistiques mensuelles
  - Tri par date

- ✅ **Gestion des Catégories**
  - Création / Modification / Suppression
  - Validation des données
  - Relations avec les dépenses

- ✅ **Sécurité**
  - Hash des mots de passe (bcrypt)
  - Validation des entrées
  - CORS configuré
  - Rate limiting optionnel

## 🐳 Docker Compose Configuration

Le projet inclut une configuration Docker Compose pour PostgreSQL et pgAdmin.

### Fichier docker-compose.yml

Créer un fichier `docker-compose.yml` à la racine du projet backend :

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:15-alpine
    container_name: gestion_depense_postgres
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: password123
      POSTGRES_DB: gestion_depense
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - gestion_depense_network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U admin -d gestion_depense"]
      interval: 10s
      timeout: 5s
      retries: 5

  pgadmin:
    image: dpage/pgadmin4:latest
    container_name: gestion_depense_pgadmin
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: admin
    ports:
      - "5050:80"
    depends_on:
      - postgres
    networks:
      - gestion_depense_network
    volumes:
      - pgadmin_data:/var/lib/pgadmin

volumes:
  postgres_data:
  pgadmin_data:

networks:
  gestion_depense_network:
    driver: bridge
```

### Commandes Docker Compose

```bash
# Démarrer les services
docker-compose up -d

# Voir les logs
docker-compose logs -f

# Arrêter les services
docker-compose down

# Arrêter et supprimer les volumes
docker-compose down -v

# Voir l'état des services
docker-compose ps

# Redémarrer les services
docker-compose restart

# Reconstruire les images
docker-compose up -d --build
```

### Accès à pgAdmin

Une fois les services démarrés :

1. Accédez à `http://localhost:5050`
2. Connectez-vous avec :
   - **Email** : `admin@admin.com`
   - **Mot de passe** : `admin`

3. Ajouter le serveur PostgreSQL :
   - **Host name/address** : `postgres`
   - **Port** : `5432`
   - **Username** : `admin`
   - **Password** : `password123`
   - **Database** : `gestion_depense`

---

### 📦 Installation Backend

#### 1. Cloner le repository

```bash
git clone https://github.com/Sylvano96/gestion_depense_back.git
cd back
```

#### 2. Installer les dépendances

```bash
npm install
# ou
yarn install
```

#### 3. Configurer PostgreSQL avec Docker Compose

Un fichier `docker-compose.yml` est fourni pour faciliter la configuration de PostgreSQL et pgAdmin.

Démarrer les services :

```bash
docker-compose up -d
```

Services disponibles :
- **PostgreSQL** : `localhost:5432`
- **pgAdmin** : `http://localhost:5050`
  - Email : `admin@admin.com`
  - Mot de passe : `admin`

Pour arrêter les services :
```bash
docker-compose down
```

Pour voir les logs :
```bash
docker-compose logs -f
```

#### 4. Mettre à jour le fichier .env

Créer un fichier `.env` à la racine :

```env
# Base de données (Docker Compose)
DATABASE_URL="postgresql://admin:password123@localhost:5432/gestion_depense"

# Authentification
JWT_SECRET=your_super_secret_key_change_in_production_12345
JWT_EXPIRES_IN=24h
COOKIE_NAME=access_token

# Email (Gmail)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_SECURE=false
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password

# URLs
APP_URL=http://localhost:3000
FRONTEND_URL=http://localhost:3000

# Environnement
NODE_ENV=development
PORT=3001
```

#### 5. Initialiser Prisma

```bash
npx prisma migrate dev --name init
```

#### 6. Lancer le serveur

```bash
npm run start:dev
```

L'API sera disponible sur [http://localhost:3001](http://localhost:3001)

---

## 🔧 Configuration Complète

### 1. Démarrer Docker Compose (Backend)

```bash
cd back
docker-compose up -d
```

**Services lancés :**
- PostgreSQL sur `localhost:5432`
- pgAdmin sur `http://localhost:5050`

### 2. Variables d'environnement Frontend (.env.local)

Créer le fichier à la racine de `gestion_depense_front` :

```env
# API
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXT_PUBLIC_APP_URL=http://localhost:3000

# Optionnel
NEXT_PUBLIC_ENV=development
```

### 3. Variables d'environnement Backend (.env)

Créer le fichier à la racine de `gestion_depense_back` :

```env
# Base de données PostgreSQL (Docker Compose)
DATABASE_URL="postgresql://admin:password123@localhost:5432/gestion_depense"

# Authentification
JWT_SECRET=your_super_secret_key_change_in_production_12345
JWT_EXPIRES_IN=24h
COOKIE_NAME=access_token

# Email (Gmail)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_SECURE=false
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password

# URLs
APP_URL=http://localhost:3000
FRONTEND_URL=http://localhost:3000

# Environnement
NODE_ENV=development
PORT=3001
```

### 4. Configuration Gmail pour Nodemailer

1. Activer 2FA sur votre compte Google
2. Générer un [mot de passe d'application](https://myaccount.google.com/apppasswords)
3. Utiliser ce mot de passe dans `SMTP_PASS`

### 5. Accès à pgAdmin

- URL : `http://localhost:5050`
- Email : `admin@admin.com`
- Mot de passe : `admin`

Pour ajouter le serveur PostgreSQL dans pgAdmin :
- **Host** : `postgres`
- **Port** : `5432`
- **User** : `admin`
- **Password** : `password123`
- **Database** : `gestion_depense`

---

## 🚀 Utilisation

### Lancer le projet complet

#### 1. Démarrer Docker Compose (Backend)

```bash
cd back
docker-compose up -d
```

#### 2. Terminal 1 - Backend

```bash
cd back
npm install
npm run start:dev
```

#### 3. Terminal 2 - Frontend

```bash
cd front
npm install
npm run dev
```

### Accès à l'application

- **Frontend** : [http://localhost:3000](http://localhost:3000)
- **Backend** : [http://localhost:3001](http://localhost:3001)
- **Swagger API** : [http://localhost:3001/api](http://localhost:3001/api) (si configuré)

### Premier usage

1. Créer un compte → Cliquer sur "Créer un compte"
2. Se connecter → Email et mot de passe
3. Ajouter des catégories → Bouton "+" dans la section Catégories
4. Ajouter des dépenses → Bouton "Ajouter" dans Mes dépenses
5. Consulter les statistiques → Dashboard

---

## 🎯 Fonctionnalités Détaillées

### Dashboard

Le dashboard affiche en temps réel :
- **Total des dépenses** - Somme de toutes les dépenses
- **Dépenses du mois** - Somme du mois en cours
- **Nombre de catégories** - Total des catégories créées
- **Liste des dépenses** - Filtrable par catégorie
- **Catégories** - Avec action rapide de filtrage

### Système de Catégories

- Créer des catégories personnalisées
- Supprimer les catégories
- Filtrer les dépenses par catégorie
- Affichage du nombre de dépenses par catégorie

### Gestion des Dépenses

- Ajouter une dépense avec titre, montant et catégorie
- Supprimer une dépense (avec confirmation)
- Affichage de la date de création
- Montants avec format monétaire (€)

### Paramètres Utilisateur

#### Profil
- Modifier le nom
- Modifier l'email
- Sauvegarder les modifications

#### Sécurité
- Changer le mot de passe
- Affichage/masquage du mot de passe
- Confirmation du nouveau mot de passe

#### Zone de Danger
- Supprimer le compte définitivement

---

## 🔐 Sécurité

### Frontend
- ✅ JWT en cookie httpOnly (non accessible via JavaScript)
- ✅ Middleware d'authentification
- ✅ Redirection automatique vers login
- ✅ Validation des formulaires
- ✅ Gestion des erreurs sensibles

### Backend
- ✅ Hash des mots de passe avec bcrypt (10 rounds)
- ✅ JwtAuthGuard sur les routes protégées
- ✅ Validation des DTOs
- ✅ CORS configuré
- ✅ Cookies httpOnly et Secure
- ✅ Rate limiting (optionnel)
- ✅ Tokens temporaires avec expiration

---

## 🧪 Tests

### Test du Backend

```bash
# Tests unitaires
npm run test

# Tests e2e
npm run test:e2e

# Couverture
npm run test:cov
```

### Tester l'API avec cURL

```bash
# Inscription
curl -X POST http://localhost:3001/auth/signup \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"Password123","name":"John Doe"}'

# Connexion
curl -X POST http://localhost:3001/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"Password123"}'

# Créer une catégorie
curl -X POST http://localhost:3001/categories \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -d '{"name":"Alimentation"}'
```

---

## 🐛 Dépannage

### Erreur de connexion à PostgreSQL

```bash
# Vérifier si les containers Docker sont en cours d'exécution
docker-compose ps

# Voir les logs
docker-compose logs postgres

# Redémarrer les services
docker-compose restart

# Vérifier la connexion
psql -h localhost -U admin -d gestion_depense
```

### pgAdmin n'est pas accessible

```bash
# Vérifier le statut
docker-compose ps

# Redémarrer pgAdmin
docker-compose restart pgadmin
```

### Base de données non trouvée

```bash
# Recréer les volumes
docker-compose down -v
docker-compose up -d

# Réinitialiser Prisma
npx prisma migrate dev --name init
```

### Erreur CORS

Vérifier dans le backend (`main.ts`) :
```typescript
app.enableCors({
  origin: 'http://localhost:3000',
  credentials: true,
});
```

### Erreur d'email non reçu

- Vérifier les variables SMTP dans `.env`
- Vérifier les logs : `console.log(info.messageId)`
- Pour Gmail : utiliser un mot de passe d'application

### Token expiré

Le frontend rafraîchit automatiquement le token. Si le problème persiste :
- Vérifier `JWT_EXPIRES_IN` dans `.env`
- Vider les cookies du navigateur
- Se reconnecter

---

## 📦 Dépendances Principales

### Frontend
```json
{
  "next": "^16.0.0",
  "react": "^19.0.0",
  "axios": "^1.7.0",
  "react-hook-form": "^7.52.0",
  "tailwindcss": "^3.4.0",
  "lucide-react": "^0.394.0"
}
```

### Backend
```json
{
  "@nestjs/core": "^10.0.0",
  "@nestjs/common": "^10.0.0",
  "@nestjs/jwt": "^12.0.0",
  "@nestjs/passport": "^10.0.0",
  "prisma": "^5.8.0",
  "@prisma/client": "^5.8.0",
  "bcrypt": "^5.1.0",
  "nodemailer": "^6.9.0",
  "cookie-parser": "^1.4.6",
  "class-validator": "^0.14.0",
  "dayjs": "^1.11.0"
}
```

---

## 📝 Scripts Disponibles

### Frontend

```bash
npm run dev       # Démarrage développement
npm run build     # Build de production
npm run start     # Démarrer la build production
npm run lint      # Vérifier le linting
```

### Backend

```bash
npm run start           # Production
npm run start:dev       # Développement avec hot reload
npm run build          # Compiler TypeScript
npm run test           # Tests unitaires
npm run test:e2e       # Tests e2e
npm run prisma:migrate # Migration Prisma
```

---

## 🤝 Contribution

Les contributions sont les bienvenues ! Pour contribuer :

1. Fork le projet
2. Créer une branche (`git checkout -b feature/AmazingFeature`)
3. Commit les changements (`git commit -m 'Add AmazingFeature'`)
4. Push la branche (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

---

## 📄 License

Ce projet est sous licence MIT - voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

## 👨‍💻 Auteur

**Sylvano** - [@Sylvano96](https://github.com/Sylvano96)

---

## 📞 Support

Pour toute question ou issue :
- Contactez : eliasvano78@gmail.com

---

## 🙏 Remerciements

- NestJS pour l'excellent framework backend
- Next.js pour le framework frontend moderne
- Prisma pour l'ORM type-safe
- Tailwind CSS pour le styling responsive

---

**Dernière mise à jour** : 2025 | **Version** : 1.0.0
