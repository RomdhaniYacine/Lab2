# Lab 2 — SAST avec Semgrep

**Durée :** 1h &nbsp;|&nbsp; **Stack :** Python / Flask &nbsp;|&nbsp; **Outil :** Semgrep

---

## Contexte

L'API interne `freemobile-netops-api` (gestion d'équipements réseau NOC) va passer en production.
Un audit SAST est requis. L'application contient **6 vulnérabilités** à identifier, comprendre et corriger.

---

## Prérequis

- Docker
- Semgrep — [docs.semgrep.dev](https://docs.semgrep.dev)

---

## Lancer l'application

```bash
git clone https://github.com/RomdhaniYacine/Lab2.git
cd Lab2
docker compose up
```

---

## Étape 1 — Scanner avec Semgrep

Utilisez Semgrep pour analyser `app.py` et détecter les vulnérabilités présentes.

> Référence : [docs.semgrep.dev/getting-started](https://docs.semgrep.dev/getting-started/)

**Questions :**
- Combien de vulnérabilités Semgrep a-t-il détectées ?
- Lesquelles n'ont **pas** été détectées ? Pourquoi ?
- Que signifie l'exit code retourné par Semgrep ?

---

## Étape 2 — Corriger le code

Les 6 vulnérabilités présentes dans `app.py` :

| # | Type | Impact |
|---|---|---|
| 1 | SQL Injection | Extraction de toutes les données |
| 2 | OS Command Injection | Exécution de commandes sur le serveur |
| 3 | Weak Cryptography (MD5) | Compromission des mots de passe |
| 4 | Insecure Deserialization (pickle) | Remote Code Execution |
| 5 | Code Injection (eval) | Exécution de code Python arbitraire |
| 6 | Insecure Random | Token de session prévisible |

Corrigez chaque vulnérabilité. Après correction, relancez Semgrep — le résultat doit être **0 finding**.

---

## Étape 3 — Pipeline CI GitHub Actions

Activez le pipeline Semgrep dans `.github/workflows/security.yml` (bloc `TODO`), committez et poussez.

Vérifiez que :
- Le pipeline **échoue** sur le code vulnérable
- Le pipeline **passe** sur le code corrigé

> Référence : [semgrep.dev/docs/semgrep-ci](https://semgrep.dev/docs/semgrep-ci/running-semgrep-ci-with-a-third-party-ci-provider/)

---

## Checklist de réussite

```
[ ] Semgrep installé et fonctionnel
[ ] Vulnérabilités identifiées et comprises
[ ] 0 finding après correction
[ ] Pipeline CI vert sur GitHub
```

---

## Solution

Dans `solution/` — à consulter uniquement après avoir terminé.
