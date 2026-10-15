---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Module 3 - Anatomie d'un Agent IA
info: |
  ## Cours Agentic AI 
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
pdf: true
export: true
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable Comark Syntax: https://comark.dev/syntax/markdown
comark: true
download: true
# duration of the presentation
duration: 35min
---

# Module 3 : Anatomie d'un Agent IA
## Décomposition des composants internes d'un système agentique

<div class="pt-12">
  <span class="px-3 py-1 rounded bg-teal-600/60 text-sm font-mono">Architecture logicielle & Design Patterns</span>
  <p class="mt-4 text-gray-300 text-sm">Cerveau, mains, mémoire, but et boucle de rétroaction</p>
</div>

---
layout: default
---

# 1. Vue d'ensemble : Les 5 piliers de l'agent

Un agent n'est pas un bloc monolithique, mais un assemblage de 5 composants interconnectés :

<div class="mt-4 flex justify-center">

```mermaid {scale: 0.75}
graph LR
    subgraph AGENT ["Système Agentique"]
        G[🎯 But / Objectif] --> B[🧠 Cerveau : LLM]
        M[(💾 Mémoire)] <--> B
        B <--> T[🛠️ Outils / Tools]
    end
    T <--> E[🌍 Monde Extérieur / APIs / OS]
    
    style B fill:#0d9488,stroke:#14b8a6,stroke-width:2px,color:#fff
    style AGENT fill:#f8fafc,stroke:#cbd5e1,stroke-width:1px
    style G fill:#f1f5f9,stroke:#94a3b8,color:#000
    style M fill:#f1f5f9,stroke:#94a3b8,color:#000
    style T fill:#f1f5f9,stroke:#94a3b8,color:#000
    style E fill:#e2e8f0,stroke:#64748b,color:#000
```

</div>

<div class="grid grid-cols-5 gap-2 mt-6 text-center text-xs">
  <div class="p-2 border rounded bg-gray-50 dark:bg-gray-800"><b>1. Le But</b><br/>La mission & ses critères de succès</div>
  <div class="p-2 border rounded bg-teal-50 dark:bg-teal-950 font-bold border-teal-500">2. Le Cerveau<br/>Raisonnement & planification</div>
  <div class="p-2 border rounded bg-gray-50 dark:bg-gray-800"><b>3. Les Outils</b><br/>Capacité d'agir et d'observer</div>
  <div class="p-2 border rounded bg-gray-50 dark:bg-gray-800"><b>4. La Mémoire</b><br/>Court terme vs Long terme</div>
  <div class="p-2 border rounded bg-gray-50 dark:bg-gray-800"><b>5. La Boucle</b><br/>Percevoir ➔ Décider ➔ Agir</div>
</div>

---
layout: two-cols
---

# 2. Le Cerveau : Le LLM comme moteur cognitif

Dans l'agent, le LLM n'est pas utilisé pour sa "culture", mais comme **machine à états sémantique**.

::left::
### Ses responsabilités :
- **Compréhension d'intention :** Traduire un besoin flou en action précise.
- **Planification (Task Planning) :** Décomposer un problème complexe en étapes séquentielles.
- **Sélection d'outils :** Choisir *quel* outil appeler avec *quels* paramètres formels.
- **Auto-évaluation :** Juger si l'observation reçue résout le problème ou s'il faut changer de stratégie.

::right::
<div class="ml-4 p-4 rounded-xl border border-teal-500/30 bg-teal-50 dark:bg-teal-950">
  <div class="font-bold text-teal-600 mb-2">Le bon modèle pour le bon rôle</div>
  <p class="text-xs text-gray-600 dark:text-gray-300 leading-relaxed">
    Tous les modèles ne font pas de bons "cerveaux" d'agents :
  </p>
  <ul class="text-xs mt-2 space-y-2">
    <li>• <b>Modèles rapides (ex. Haiku, GPT-4o-mini) :</b> très bons pour les sous-tâches simples (extraction, résumé d'un outil).</li>
    <li>• <b>Modèles de raisonnement (ex. o1, R1, Sonnet) :</b> indispensables pour l'orchestration principale, le backtracking et la détection d'erreurs d'exécution.</li>
  </ul>
</div>

---
layout: default
---

# 3. Les Mains et les Sens : Les Outils (Tools)

Sans outils, un LLM n'a aucun effet de bord. Les outils transforment une intention en calcul déterministe.

<div class="grid grid-cols-4 gap-4 mt-6 text-xs">
  <div class="p-3 border rounded bg-gray-50 dark:bg-gray-800">
    <div class="font-bold text-teal-600 text-sm mb-1">🌐 Recherche Web & Scraping</div>
    Accès à l'information en temps réel, documentation technique fraîche, vérification de faits.
    <div class="mt-2 text-gray-400 font-mono text-[10px]">Tavily, Perplexity API, Playwright</div>
  </div>
  <div class="p-3 border rounded bg-gray-50 dark:bg-gray-800">
    <div class="font-bold text-teal-600 text-sm mb-1">💻 Interpréteur de code</div>
    Exécution sandboxée de code généré pour faire des calculs précis, manipuler des fichiers ou tracer des graphes.
    <div class="mt-2 text-gray-400 font-mono text-[10px]">Python REPL, E2B, Docker sandbox</div>
  </div>
  <div class="p-3 border rounded bg-gray-50 dark:bg-gray-800">
    <div class="font-bold text-teal-600 text-sm mb-1">🗄️ Accès Données / SQL</div>
    Interrogation de bases relationnelles ou d'APIs métiers internes (CRM, ERP, Jira).
    <div class="mt-2 text-gray-400 font-mono text-[10px]">Text-to-SQL, GraphQL, REST connectors</div>
  </div>
  <div class="p-3 border rounded bg-gray-50 dark:bg-gray-800">
    <div class="font-bold text-teal-600 text-sm mb-1">🔌 Connecteurs Système</div>
    Intéraction directe avec le système de fichiers, git, ou l'envoi d'e-mails.
    <div class="mt-2 text-gray-400 font-mono text-[10px]">MCP Servers, Bash CLI, GitHub API</div>
  </div>
</div>

<div class="mt-6 p-3 bg-amber-50 dark:bg-amber-950 border border-amber-400 rounded text-xs">
  ⚠️ <b>Règle de conception :</b> Plus vous donnez d'outils à un agent, plus son taux d'erreur de sélection explose. Visez moins de 10-15 outils bien documentés par agent.
</div>

---
layout: default
---

# Zoom Protocole : MCP (Model Context Protocol)

Comment éviter l'enfer d'intégration des $N$ modèles avec les $M$ outils ?

<div class="grid grid-cols-2 gap-6 items-center mt-2">

<div>

### Le standard ouvert (Anthropic, 2024)
- **Le problème historique :** Chaque framework (LangChain, LlamaIndex, CrewAI) réécrivait ses propres connecteurs Jira, GitHub, Postgres...
- **La solution MCP :** Le « port USB-C » de l'IA. Un protocole universel basé sur **JSON-RPC 2.0**.
- **Les 3 primitives exposées par un serveur MCP :**
  - 🛠️ **Tools :** Fonctions exécutables par le modèle (*actions*)
  - 📄 **Resources :** Données en lecture seule (*contexte, logs, fichiers*)
  - 💬 **Prompts :** Modèles d'instructions pré-paramétrés

</div>

<div>

```mermaid
graph TD
    subgraph CLIENT ["Hôte / Client Agent"]
        LLM[Agent / IDE / Claude Desktop]
    end

    subgraph PROTOCOL ["Protocole MCP (JSON-RPC)"]
        direction TB
        LLM <-->|Découverte & Appels| S1[Serveur MCP GitHub]
        LLM <-->|Découverte & Appels| S2[Serveur MCP Postgres]
        LLM <-->|Découverte & Appels| S3[Serveur MCP Fichiers Locaux]
    end

    style CLIENT fill:#f8fafc,stroke:#94a3b8
    style PROTOCOL fill:#f0fdfa,stroke:#0d9488
    style LLM fill:#0d9488,color:#fff
```

<div class="mt-2 p-2 bg-teal-50 dark:bg-teal-950 border border-teal-500/40 rounded text-[11px] text-gray-600 dark:text-gray-300">
  💡 <b>Bénéfice :</b> Vous développez un serveur MCP pour votre outil interne <i>une seule fois</i>, et il devient instantanément utilisable par n'importe quel agent ou IDE compatible.
</div>

</div>

</div>


---
layout: default
---

# 4. Zoom outillage : L'interpréteur de code comme super-outil

Pourquoi l'accès à un environnement Python (Sandbox) décuple-t-il la puissance de l'agent ?

<div class="grid grid-cols-2 gap-6 mt-4">
<div>

### Les LLMs échouent sur les opérations exactes :
- Calcul arithmétique complexe (`17.43 * 849.21`)
- Comptage exact de caractères / lignes
- Algèbre linéaire ou inversion de matrices

### L'approche agentique :
Au lieu de deviner le résultat, **le LLM écrit le script et le fait exécuter** par un interpréteur dédié.

</div>

<div class="p-3 bg-gray-900 text-gray-100 rounded-lg font-mono text-xs">
  <div class="text-gray-400">// Ce que l'agent génère et exécute :</div>
  <div class="text-emerald-400 mt-2">```python</div>
  import pandas as pd<br/>
  df = pd.read_csv("ventes_2025.csv")<br/>
  result = df[df['zone'] == 'Europe']['chiffre'].sum()<br/>
  print(f"Total Europe : {result} EUR")<br/>
  <div class="text-emerald-400">```</div>
  <div class="text-gray-400 mt-2">// Sortie capturée et renvoyée au LLM :</div>
  <div class="text-amber-300">Total Europe : 14820492 EUR</div>
</div>
</div>

<div class="mt-4 text-xs text-gray-500">
  🔒 <b>Impératif de sécurité :</b> L'exécution de code doit toujours tourner dans un bac à sable isolé (Sandbox gVisor / microVM type E2B / conteneur éphémère sans privilèges).
</div>



---
layout: default
---

# 5. La Mémoire (1/2) : Mémoire de travail (Court terme)

Comment l'agent conserve-t-il le fil de sa pensée pendant l'exécution ?

<div class="grid grid-cols-3 gap-4 mt-6">
  <div class="p-4 border rounded bg-gray-50 dark:bg-gray-800">
    <div class="font-bold text-sm text-teal-600 mb-1">1. Le Scratchpad</div>
    <div class="text-xs text-gray-500 mb-2">L'ardoise temporaire</div>
    <p class="text-xs">
      Le buffer de contexte accumule la trace d'exécution : <i>Pensée ➔ Outil ➔ Résultat</i>.
    </p>
  </div>
  <div class="p-4 border rounded bg-gray-50 dark:bg-gray-800">
    <div class="font-bold text-sm text-teal-600 mb-1">2. La Saturation</div>
    <div class="text-xs text-gray-500 mb-2">Le piège du contexte</div>
    <p class="text-xs">
      Après 5 appels d'outils renvoyant du JSON volumineux, le contexte explose, coûte cher et noie l'attention.
    </p>
  </div>
  <div class="p-4 border-2 border-teal-500 rounded bg-teal-50 dark:bg-teal-950">
    <div class="font-bold text-sm text-teal-600 mb-1">3. Compression & Élagage</div>
    <div class="text-xs text-gray-500 mb-2">Le pattern de synthèse</div>
    <p class="text-xs">
      Résumer dynamiquement les étapes intermédiaires passées pour ne garder que les conclusions utiles.
    </p>
  </div>
</div>

<div class="mt-6 p-4 rounded bg-gray-100 dark:bg-gray-800 font-mono text-[11px]">
  <b>Prompt d'élagage typique :</b><br/>
  "Résume les 4 dernières actions et leurs résultats en 3 lignes maximum. Supprime les JSONs bruts de l'historique avant de décider de la prochaine étape."
</div>

---
layout: default
---

# 6. La Mémoire (2/2) : Mémoire persistante (Long terme)

Permet à l'agent d'apprendre au fil des sessions ou de partager des données entre plusieurs exécutions :

<div class="mt-4 flex justify-center">

```mermaid  {scale: 0.7}
graph TD
    subgraph LT_MEMORY ["Types de Mémoire à Long Terme"]
        A[Mémoire Épisodique] -->|Rappels d'actions passées| V[(Base Vectorielle)]
        B[Mémoire Sémantique] -->|Faits & Documents métiers| R[(RAG / Knowledge Base)]
        C[Mémoire Procédurale] -->|Profil utilisateur / Règles| KV[(Store Clé-Valeur / Graph)]
    end
    
    style LT_MEMORY fill:#f8fafc,stroke:#cbd5e1
    style V fill:#ccfbf1,stroke:#0d9488,color:#000
    style R fill:#ccfbf1,stroke:#0d9488,color:#000
    style KV fill:#ccfbf1,stroke:#0d9488,color:#000
```

</div>

<div class="grid grid-cols-3 gap-4 mt-6 text-xs">
  <div>
    <b>Épisodique :</b> <i>« La semaine dernière, cette même requête SQL avait échoué avec l'erreur X ; j'utilise plutôt la syntaxe Y. »</i>
  </div>
  <div>
    <b>Sémantique :</b> Connaissances métier injectées à la volée via recherche vectorielle ou graphe de connaissances.
  </div>
  <div>
    <b>Procédurale :</b> Préférences stables de l'utilisateur (ex. <i>« Cet utilisateur préfère les réponses en TypeScript strict »</i>).
  </div>
</div>

---
layout: two-cols
---

# 7. Le But : Cadrage et Décomposition de la tâche

Un agent sans but borné dérive rapidement vers des actions infinies.

::left::
### Définir un bon objectif :
- **Spécifique et mesurable :** 
  - ❌ *"Améliore la sécurité du serveur"*
  - ✅ *"Identifie les ports ouverts non standard et génère un script UFW pour les bloquer"*
- **Critères d'arrêt stricts (Stop Conditions) :**
  - Nombre maximal d'itérations
  - Format de réponse final imposé
  - Déclencheur d'arrêt explicite : `FINAL_ANSWER`

::right::
<div class="ml-4">

### Patterns de décomposition :
1. **Plan-and-Solve :**
   Le LLM génère d'abord un plan en 4 étapes, puis s'y tient rigoureusement en cochant les cases.
2. **Re-planning dynamique :**
   Après chaque outil exécuté, l'agent met à jour son plan restant :
   - *Étape 1 : Faite*
   - *Étape 2 : Échouée ➔ Plan de secours B*
   - *Étape 3 : En attente*

</div>

---
layout: default
---

# 8. La Boucle d'Interaction : Perceive ➔ Reason ➔ Act ➔ Observe

C'est le cycle d'horloge de tout système agentique (Pattern ReAct) :

<div class="mt-4 center flex justify-center">

```mermaid {scale: 0.5}
sequenceDiagram
    autonumber
    participant U as Utilisateur / Env
    participant B as Cerveau (LLM)
    participant T as Outil (Tool/API)
    
    U->>B: 1. Perceive : Objectif ou événement entrant
    Note over B: 2. Reason : Analyse de l'état & choix de l'outil
    B->>T: 3. Act : Appel JSON de la fonction (ex: execute_sql)
    Note over T: Exécution locale déterministe
    T-->>B: 4. Observe : Retour de résultat brut
    Note over B: 5. Reason : Évaluation (But atteint ?)
    B->>U: 6. Réponse finale ou nouvelle itération
```

</div>

<div class="mt-4 text-center text-xs text-gray-500">
  Si le but n'est pas atteint à l'étape 5, la boucle repart immédiatement à l'étape 2 avec la nouvelle observation en mémoire.
</div>

---
layout: default
---

# 9. Trace d'exécution pas-à-pas (Sous le capot)

Exemple réel de la boucle ReAct lors d'un audit de production :

<div class="p-3 bg-gray-900 text-gray-100 rounded-lg font-mono text-[11px] leading-relaxed">
  <div class="text-teal-400 font-bold">▶ OBJECTIF INITIAL : "Vérifie l'espace disque du serveur web et alerte si > 85%"</div>
  
  <div class="text-purple-400 mt-2">THOUGHT 1:</div>
  <div>Je dois exécuter une commande système pour lire l'occupation disque du point de montage racine.</div>
  
  <div class="text-amber-400 mt-1">ACTION 1:</div>
  <div>Call tool: <code class="text-red-400">exec_ssh(host="web-prod-01", cmd="df -h /")</code></div>
  
  <div class="text-blue-400 mt-1">OBSERVATION 1:</div>
  <div><code class="text-red-400">Filesystem Size Used Avail Use% Mounted on /dev/sda1 50G 46G 4G 92% /</code></div>
  
  <div class="text-purple-400 mt-2">THOUGHT 2:</div>
  <div>L'utilisation est de 92%, ce qui est supérieur au seuil de 85%. Je dois envoyer une alerte Slack à l'équipe Infra.</div>
  
  <div class="text-amber-400 mt-1">ACTION 2:</div>
  <div>Call tool: <code class="text-red-400">send_slack(channel="#alerts-infra", msg="⚠️ Alerte disque web-prod-01 à 92%")</code></div>
  
  <div class="text-blue-400 mt-1">OBSERVATION 2:</div>
  <div><code class="text-red-400">{"status": "ok", "timestamp": "14:02:11"}</code></div>
  
  <div class="text-emerald-400 mt-2">FINAL ANSWER:</div>
  <div>Vérification effectuée : le serveur web-prod-01 est saturé à 92%. Une alerte a été publiée sur Slack #alerts-infra.</div>
</div>

---
layout: default
---

# 10. Les points de rupture architecturaux

Où un agent en production casse-t-il le plus souvent ?

<div class="grid grid-cols-2 gap-6 mt-4 text-xs">
<div class="p-3 border rounded bg-gray-50 dark:bg-gray-800">

### 1. Parsing & Schéma d'outils
- Le LLM génère un JSON syntaxiquement invalide ou avec un nom d'argument erroné (`city_name` au lieu de `city`).
- **Parade :** Validation stricte via Pydantic + message d'erreur explicite réinjecté dans la boucle pour auto-correction.

### 2. Dérive de but (Goal Drift)
- Après 4 ou 5 étapes infructueuses, l'agent perd de vue l'objectif initial et explore des sous-problèmes sans rapport.
- **Parade :** Rappeler le but initial dans le *System Prompt* à chaque nouvelle itération.

</div>
<div class="p-3 border rounded bg-gray-50 dark:bg-gray-800">

### 3. Effet "Bavardage" (Ping-pong infini)
- Deux outils ou deux agents se renvoient la balle sans converger vers une solution.
- **Parade :** `max_iterations = 6` et retour gracieux avec journalisation de l'échec.

### 4. Débordement de fenêtre de contexte
- Un outil renvoie une page web de 50 000 mots ou un dump de base complet.
- **Parade :** Tronquer ou résumer systématiquement les sorties d'outils avant réinjection.

</div>
</div>



---
layout: default
---

# Le Harnais (Harness) : L'armure de l'agent

<div class="text-teal-600 font-semibold mb-4">
  « On ne lâche jamais un LLM nu dans la nature : on l'enferme dans un harnais logiciel strict. »
</div>

Le **harnais** est le cadre logiciel déterministe qui pilote, bride et surveille l'agent pendant son cycle de vie. Il remplit deux fonctions vitales :

<div class="grid grid-cols-2 gap-6 mt-4 text-xs">

<div class="p-4 border-2 border-teal-500 rounded-xl bg-teal-50 dark:bg-teal-950">
  <div class="font-bold text-sm text-teal-600 mb-2">🛡️ 1. Le Harnais d'Exécution (Runtime)</div>
  <div class="text-gray-500 mb-3 italic">Garantir la sécurité et la stabilité en production</div>

  <ul class="space-y-2">
    <li>• <b>Garde-fous de budget :</b> Plafond strict de tokens ($) et timeout temporel par session.</li>
    <li>• <b>Interception des actions critiques :</b> Bloquer les commandes destructrices (<code>DROP TABLE</code>, <code>rm</code>) et forcer une validation humaine (*Human-in-the-loop*).</li>
    <li>• <b>Isolation d'environnement :</b> Exécution du code dans une sandbox étanche (MicroVM / Docker éphémère).</li>
    <li>• <b>Télémétrie & Tracing :</b> Capture pas-à-pas (OpenTelemetry) pour rejouer les runs en cas de bug.</li>
  </ul>
</div>

<div class="p-4 border rounded-xl bg-gray-50 dark:bg-gray-800">
  <div class="font-bold text-sm text-indigo-500 mb-2">🧪 2. Le Harnais d'Évaluation (Eval)</div>
  <div class="text-gray-500 mb-3 italic">Mesurer scientifiquement la performance</div>

  <ul class="space-y-2">
    <li>• <b>Banc d'épreuve reproductible :</b> Rejouer l'agent sur 50 scénarios figés (ex. benchmarks style SWE-bench).</li>
    <li>• <b>Détection de régressions :</b> Vérifier qu'un changement de prompt ou de modèle ne casse pas 15% des cas passants.</li>
    <li>• <b>Asserters automatisés :</b> Vérifier l'état final du système plutôt que le texte produit (ex: <i>« le test unitaire du repo passe-t-il au vert ? »</i>).</li>
  </ul>
</div>

</div>

<div class="mt-6 p-2 bg-gray-100 dark:bg-gray-800 rounded text-center text-xs font-mono">
  👉 <b>Retenez cette règle d'ingénieur :</b> L'intelligence est dans le modèle, mais la fiabilité industrielle est dans le <u>harnais</u>.
</div>
```



---
layout: default
---

# 11. Synthèse du Module 3

<div class="p-5 bg-teal-50 dark:bg-teal-950 border border-teal-500 rounded-xl space-y-3">
  <div class="font-bold text-teal-600 text-lg">L'anatomie complète d'un Agent :</div>
  <ul class="text-sm space-y-2">
    <li>🔹 <b>Cerveau :</b> Le LLM orchestre et prend les décisions de transition ; il ne doit pas faire de calcul direct.</li>
    <li>🔹 <b>Outils :</b> Des fonctions typées rigoureuses (APIs, Code Sandbox, SQL) qui fournissent l'exactitude factuelle.</li>
    <li>🔹 <b>Mémoire :</b> Court terme (Scratchpad/contexte élagué) pour l'exécution en cours, Long terme (Vector/Key-Value) pour la persistance.</li>
    <li>🔹 <b>But :</b> Décomposé en sous-étapes avec des conditions d'arrêt impératives.</li>
    <li>🔹 <b>Cycle :</b> Une boucle déterministe <code>Percevoir ➔ Raisonner ➔ Agir ➔ Observer</code>.</li>
    <li>🔹 <b>Le harnais :</b> Un cadre logiciel pour vérifier le travail de l'agent.</li>

  </ul>
</div>

<div class="mt-6 text-center text-sm text-gray-500">
  👉 <i>Module 4 à suivre :  Les 4 patrons de conception agentiques.</i>
</div>

---
layout: end
class: text-center
---

# Fin du Module 3
### Place aux échanges & questions !
