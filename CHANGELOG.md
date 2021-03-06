# Changelog
## Portainer Manager


- [Changelog](#changelog)
  - [Portainer Manager](#portainer-manager)
  - [v1.2.1 (11/02/2022)](#v121-11022022)
    - [Enhancements:](#enhancements)
    - [Fixed :](#fixed-)
    - [Known Issues :](#known-issues-)
    - [Future apps](#future-apps)
  - [v1.2.0 (23/11/2021)](#v120-23112021)
    - [Enhancements:](#enhancements-1)
    - [Fixed :](#fixed--1)
    - [Known Issues :](#known-issues--1)
    - [Future apps](#future-apps-1)
    - [Future features](#future-features)
  - [v1.1.0 (19/11/2021)](#v110-19112021)
    - [Enhancements:](#enhancements-2)
    - [Fixed :](#fixed--2)
    - [Known Issues :](#known-issues--2)
    - [Future apps](#future-apps-2)
    - [Future features](#future-features-1)
  - [v1.0.0 (29/10/2021)](#v100-29102021)
    - [Enhancements:](#enhancements-3)
    - [Fixed :](#fixed--3)
    - [Known Issues :](#known-issues--3)
    - [Future apps](#future-apps-3)
    - [Future features](#future-features-2)

## v1.2.1 (11/02/2022)
### Enhancements:

- Add supports of Alpine Linux

---

### Fixed :

- Remove comment-line in playbooks which occurs playbooks crash

---

### Known Issues :

- Flatcar Container Linux needs specific bootstrap (see [README](README.md) )
  - Can't install docker-compose using pip
  - Locksmithd auto update is disabled

---

### Future apps

- Traefik (builtin)
- OpenLDAP
- Gitlab
- Nexus
- SonarQube
- Jenkins

---
## v1.2.0 (23/11/2021)
### Enhancements:

- Docker-slaves endpoints using portainer_agent

---

### Fixed :

- Duplicated installation of docker-compose

---

### Known Issues :

- Flatcar Container Linux needs specific bootstrap (see [README](README.md) )
  - Can't install docker-compose using pip
  - Locksmithd auto update is disabled

---

### Future apps

- Traefik (builtin)
- OpenLDAP
- Gitlab
- Nexus
- SonarQube
- Jenkins

---

### Future features

- Safe method to generate/store/pass secrets --> target version: unknown

## v1.1.0 (19/11/2021)
### Enhancements:

- Welcome to [Flatcar Container Linux](https://www.flatcar-linux.org/) supports - [v2983.2.0](https://www.flatcar-linux.org/releases/#release-2983.2.0)

---

### Fixed :

- N/A

---

### Known Issues :

- Flatcar Container Linux needs specific bootstrap (see [README](README.md) )
  - Can't install docker-compose using pip
  - Locksmithd auto update is disabled

---

### Future apps

- Traefik (builtin)
- OpenLDAP
- Gitlab
- Nexus
- SonarQube
- Jenkins

---

### Future features

- Safe method to generate/store/pass secrets --> target version: unknown


## v1.0.0 (29/10/2021)
### Enhancements:

- **First version**

- **Supported OS:**
  - Alpine Linux 3.14.x
  - Debian 10 and Ubuntu 20.04
  - RHEL and CentOS 8
- **Applications:**
  - Portainer (builtin)
- **Security:**
  - N/A

### Fixed :

- N/A

---

### Known Issues :

- N/A

---

### Future apps

- Traefik (builtin)
- OpenLDAP
- Gitlab
- Nexus
- SonarQube
- Jenkins

---

### Future features

- Safe method to generate/store/pass secrets --> target version: unknown
