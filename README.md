
## Lancer le projet

1. Cloner le dépôt
2. Ouvrir le projet dans IntelliJ IDEA
3. Lancer la classe `JwtdemoApplication`
4. L'API est disponible sur `http://localhost:8080`

## Endpoints

| Méthode | URL | Accès | Description |
|---|---|---|---|
| POST | `/auth/register` | Public | Créer un compte |
| POST | `/auth/login` | Public | Obtenir un token JWT |
| GET | `/api/hello` | Token requis | Message de bienvenue |
| GET | `/api/profile` | Token requis | Utilisateur connecté |

## Exemple d'utilisation (PowerShell)

```powershell
# 1. Inscription
Invoke-RestMethod -Method Post -Uri http://localhost:8080/auth/register -ContentType "application/json" -Body '{"email":"test@mail.com","password":"1234"}'

# 2. Connexion
$r = Invoke-RestMethod -Method Post -Uri http://localhost:8080/auth/login -ContentType "application/json" -Body '{"email":"test@mail.com","password":"1234"}'

# 3. Accès protégé
Invoke-RestMethod -Uri http://localhost:8080/api/profile -Headers @{Authorization = "Bearer $($r.token)"}
```

## Fonctionnement

1. Le client envoie email + mot de passe à `/auth/login`.
2. Le serveur vérifie les identifiants et renvoie un token JWT signé.
3. Le client envoie ce token dans l'en-tête `Authorization: Bearer <token>`.
4. `JwtFilter` valide le token et authentifie l'utilisateur.
5. Sans token valide, l'accès à `/api/**` est refusé (403).

## Console H2

`http://localhost:8080/h2-console`
JDBC URL : `jdbc:h2:mem:securitydb` | User : `sa` | Mot de passe : vide

## Auteur

Projet réalisé dans le cadre du cours de sécurité (ENSET).
