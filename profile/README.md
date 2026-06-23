# Intention

0/ Permettre à des non-informaticiennes

- de créer un petit site rapidement / facilement
- avoir une relation saine et sereine avec son contenu

1/ Liste des dépots de code

- [Scribouilli](https://github.com/Scribouilli/scribouilli) code source de l'atelier (client)
- [toctoctoc](https://github.com/Scribouilli/toctoctoc) outil d'authentification github, gitlab et scribougit (serveur)
- [site-template](https://github.com/Scribouilli/site-template) base de scribouilli pour démarrer un site
- [mimoza](https://github.com/Scribouilli/mimoza) thème de base pour le site généré par Scribouilli
- [documentation](https://github.com/Scribouilli/documentation) page du site explicatif de scriboulli (https://scribouilli.org/)
- [.github](https://github.com/Scribouilli/.github) le dépot où est enregistré ce fichier README.md

Il y aussi des dépots spécifique pour Framalibre
- [site-template-framalibre](https://github.com/Scribouilli/site-template-framalibre)
- [kabusin](https://github.com/Scribouilli/kabusin)

Et pour la campagne legislative de 2024
- [roz-aer](https://github.com/Scribouilli/roz-aer)
- [Scribouilli2024](https://github.com/Scribouilli/scribouilli2024)
- [site-template-2024](https://github.com/Scribouilli/site-template-2024)
- [toctoctoc2024](https://github.com/Scribouilli/toctoctoc2024)

2/ Schéma d'interaction des composants de Scribouilli

```mermaid
graph TB

    subgraph ServeurPasANous
    Github
    Gitlab
    ScribouGit
    end

    subgraph Client
    Atelier
    end

    subgraph Github
    API-Github("API")
    Git-Github("git")
    end
    subgraph Gitlab
    API-Gitlab("API")
    Git-Gitlab("git")
    end
    subgraph ScribouGit
    API-ScribouGit("API")
    Git-ScribouGit("git")
    end
    
    subgraph Atelier
    IsomorphicGit
    end

    IsomorphicGit-->ProxyIsomorphic-git
    ProxyIsomorphic-git-->|🔑| Git-Github("git");
    ProxyIsomorphic-git-->|🔑| Git-Gitlab("git");
    ProxyIsomorphic-git-->|🔑| Git-ScribouGit("git");
    Atelier-->Toctoctoc("Toctoctoc")-->|🔑|Atelier;
    Atelier-->|🔑| API-Github("API");
    Atelier-->|🔑| API-Gitlab("API");
    Atelier-->|🔑| API-ScribouGit("API");

    style Client fill:#fff,stroke:#f66,stroke-width:2px
    style ServeurPasANous fill:#fff,stroke:#f66,stroke-width:2px
```

3/

```mermaid
graph LR
  SiteScribouilli["Sites Scribouillis"] --> Monsite@{ shape: procs, label: "Mon petit site"} -- est une copie de --> site-template;
  site-template -- importe le thème --> mimoza;
  site-template o--o deploy("github/workflows/build-and-deploy.yml dans le repo site-tempalte build avec Jekyll")
```



