# ColorHarmony: WCAG 2.1 Compliant 60-30-10 Palette Generator

Un utilitaire frontend sans dépendances (Vanilla JS) conçu pour générer des palettes de couleurs harmonieuses basées sur la règle de design 60-30-10. Contrairement aux générateurs aléatoires standard, cet outil s'appuie sur des calculs mathématiques stricts dans l'espace colorimétrique HSL et garantit l'accessibilité typographique via la norme WCAG 2.1.



## 🛠 Problématiques Techniques Résolues

Ce micro-projet démontre la résolution de plusieurs défis d'ingénierie front-end standard :

### 1. Calcul de Luminance Relative (Accessibilité)
L'outil n'utilise pas la formule YIQ obsolète. Il implémente la spécification mathématique exacte du W3C (WCAG 2.1) pour calculer la luminance relative (linéarisation des canaux sRGB) et déterminer dynamiquement si le texte superposé doit être clair ou sombre (ratio de contraste > 4.5:1).

### 2. Algorithmes d'Harmonie Chromatique
Génération de couleurs non pas par randomisation pure, mais par contraintes angulaires sur le cercle chromatique (Modulo 360).
- **Split-Complémentaire / Complémentaire / Analogue :** Verrouillage de la saturation et de la luminosité pour éviter les teintes illisibles, tout en décalant la teinte (`Hue`) selon des degrés mathématiques précis (ex: +150° / +210°).

### 3. Gestion d'État Asymétrique (State Locking)
Implémentation d'un système de verrouillage UI. Lorsqu'une couleur (Dominante, Secondaire ou Accent) est verrouillée par l'utilisateur, l'algorithme recalcule le `baseHue` à partir de la couleur verrouillée et génère le reste de la palette de manière déterministe pour maintenir l'harmonie.

### 4. API Presse-papier Robuste (Fallback Mechanism)
La fonction d'exportation utilise l'API moderne asynchrone `navigator.clipboard`. Pour prévenir les échecs silencieux sur les environnements locaux (`file://`) ou non sécurisés (HTTP), un mécanisme de repli (fallback) synchrone via `document.execCommand('copy')` avec un nœud `<textarea>` éphémère est implémenté.

## 🚀 Stack Technique

- **Logique :** Vanilla JavaScript (ES6+)
- **Interface :** HTML5, Tailwind CSS (via CDN pour un prototypage rapide)
- **Architecture :** Monofichier, gestion d'état centralisée via un objet `state` constant.

## 📦 Utilisation

Aucun build step requis. 
1. Cloner le dépôt.
2. Ouvrir le fichier `index.html` dans n'importe quel navigateur moderne.
3. Appuyer sur la touche `Espace` pour générer de nouvelles palettes mathématiquement contraintes.

## 📋 Exportations Supportées

Le générateur compile dynamiquement la palette générée dans plusieurs formats prêts pour la production :
- Variables CSS natives (`:root`)
- Fichier de configuration Tailwind CSS (`tailwind.config.js`)
- Variables SCSS
