# Projet Démonstrateur — Fouad Ait Ouahmad

> Projet personnel démontrant mes compétences en cybersécurité et développement.

---

## 🎯 Objectif

Ce projet sert de démonstration pratique pour :
- Mes compétences en Python et Bash
- Ma compréhension des concepts de sécurité offensive
- Ma capacité à documenter et structurer un projet

## 📋 Contenu

### Module 1 — Scanner de ports
Un scanner de ports simple en Python avec détection de services.

```python
# Exemple d'utilisation
python port_scanner.py --target 192.168.1.1 --ports 1-1000
```

### Module 2 — Générateur de rapports
Génération de rapports de pentest en Markdown/HTML.

```bash
python report_generator.py --input scan_results.json --output report.md
```

### Module 3 — Automatisation CTF
Scripts d'automatisation pour les challenges CTF (extraction, analyse, exploitation).

## 🛠️ Stack

- Python 3.12+
- Bash
- Docker (pour l'isolation)

## 📦 Installation

```bash
git clone https://github.com/fao241/projet-demonstrateur.git
cd projet-demonstrateur
pip install -r requirements.txt
```

## 🚀 Utilisation

```bash
# Lancer le scanner
python -m src.scanner --target <IP> --ports <RANGE>

# Générer un rapport
python -m src.reporter --input <FILE> --output <FILE>
```

## 📄 Licence

MIT License — voir [LICENSE](LICENSE) pour plus de détails.

---

## ⚠️ Avertissement

Ce projet est destiné à des fins éducatives uniquement. Ne l'utilisez que sur des systèmes que vous possédez ou avez l'autorisation de tester.
