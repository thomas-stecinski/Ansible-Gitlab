# Infrastructure Automatisée avec Docker, PostgreSQL et GitLab

Ce projet configure une infrastructure automatisée avec une base de données PostgreSQL et un serveur GitLab. Il utilise **Ansible** pour la configuration et **Docker Compose** pour orchestrer les services.

---

## Structure du Projet
```bash
.
├── docker
│   └── docker-compose.yml
├── inventory.yml
├── README.md
├── roles
│   ├── bdd
│   │   └── tasks
│   │       └── main.yml
│   ├── common
│   │   └── tasks
│   │       └── main.yml
│   └── gitlab
│       └── tasks
│           └── main.yml
├── site.yml
└── stop_services.yml
```

---
## Configuration

Dans le fichier "inventory.yml" ne pas oublié de modifié les addresse ip de la machine hôte et machine cliente (gitlab)
```bash
<192.168.255.131>  
```

## Commandes Essentielles

### Déployer l'Infrastructure avec Docker

Pour déployer les services PostgreSQL et GitLab via Docker Compose :

```bash
# Étape 1 : Construire les conteneurs Docker
docker-compose -f docker/docker-compose.yml build

# Étape 2 : Lancer les conteneurs Docker
docker-compose -f docker/docker-compose.yml up -d
```

### Déployer l'Infrastructure avec une Seconde VM

Pour déployer le projet sur une seconde machine sans Docker :
```bash
ansible-playbook -i inventory.yml site.yml
```
### Arrêter les Services
Pour arrêter tous les services, quelle que soit la méthode utilisée (Docker ou Ansible) :
Stoper sur docker : 
```bash
docker-compose -f docker/docker-compose.yml down
```
Stoper sur la VM Ansible :
```bash
ansible-playbook -i inventory.yml stop_services.yml
```

