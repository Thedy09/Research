# Analyse Technique Web3 – Fonctionnement des Hooks dans Uniswap V4

**Auteur** : Yao Théodore DORVI (Thedy)  
**Date** : Août 2025

---

## ✨ Contexte
Uniswap V4 introduit les "Hooks", une innovation majeure qui transforme chaque pool en module programmable. Contrairement aux versions précédentes (notamment V3), cette version permet d'injecter du code personnalisé à des moments précis de la vie d'une pool.

---

## ⚙️ Qu'est-ce qu'un Hook ?
Un *Hook* est un contrat externe que l'on associe à une pool au moment de sa création. Son adresse encode quels "points d'accroche" sont activés (ex. avant ou après un swap). Le *PoolManager* d'Uniswap V4 appelle ensuite ces fonctions au bon moment, en toute sécurité.

### ▶️ Points d’accroche disponibles :
- `beforeInitialize` / `afterInitialize`
- `beforeAddLiquidity` / `afterAddLiquidity`
- `beforeRemoveLiquidity` / `afterRemoveLiquidity`
- `beforeSwap` / `afterSwap`
- `beforeDonate` / `afterDonate`

Un seul Hook peut être associé à une pool, mais il peut implémenter plusieurs de ces callbacks.

---

## 🧪 Cas d’usage pratiques
### 1. **Frais dynamiques**
Les Hooks permettent de calculer des frais adaptés aux conditions de marché (volatilité, volume, etc.) en renvoyant un `lpFeeOverride` dans `beforeSwap`.

### 2. **Oracles internes personnalisés**
On peut définir des oracles on-chain plus robustes que ceux de V3, comme des oracles tronqués qui limitent les variations de prix par bloc.

### 3. **Ordres limites & TWAMM**
Les Hooks permettent d'exécuter des swaps en plusieurs fois (TWAMM) ou de simuler des ordres limites basés sur des ticks précis.

### 4. **Gouvernance native et incentives**
Hooks peuvent vérifier l'état d'un vote on-chain avant de permettre un swap, ou distribuer automatiquement des récompenses aux LPs.

### 5. **Gestion de liquidité dynamique**
Auto-compounding, stratégies multi-position, distribution de frais : les possibilités sont immenses.

---

## 🔐 Enjeux techniques et risques
- **Complexité élevée** : les Hooks doivent être auditable et correctement configurés. Une erreur dans les flags ou les retours peut bloquer une transaction.
- **Surface d'attaque augmentée** : chaque Hook est un contrat externe avec ses propres risques (reentrance, gas, centralisation, etc.)
- **Contrainte d'adresse** : les callbacks activés sont codés dans l'adresse du Hook via CREATE2, ce qui demande un minage d'adresse spécifique.

---

## 🧠 Limites actuelles
- **Un seul Hook par pool** : pas de combinaison dynamique de modules, ce qui limite la composaibilité.
- **Adoption progressive** : les pools avec Hook doivent être promues pour attirer du volume (ex. via UniswapX).
- **Interface dév encore technique** : pas d'interface friendly pour les non-devs pour créer ou auditer des Hooks.

---

## 🔗 Ressources officielles
- [GitHub Uniswap V4](https://github.com/Uniswap/v4-core)
- [Docs Uniswap V4](https://docs.uniswap.org/)
- [Blog de lancement V4](https://uniswap.org/blog/uniswap-v4)

---

> “Avec les Hooks, Uniswap V4 devient un OS pour AMMs” – Vitalik Buterin (indirectement)

---

**Contact** : TG:@Thedy09 | [LinkedIn](https://www.linkedin.com/in/thedy09/) 

