# stonemart.github.io
BerryQuest Task List
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quest Log — UE5 RPG Dev</title>
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600;700&family=Crimson+Text:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --ink: #1a1208;
    --parchment: #f2e8c9;
    --parchment-dark: #e8d9a8;
    --parchment-mid: #ede0bc;
    --stone: #2c2416;
    --stone-light: #3d3221;
    --gold: #c89a2e;
    --gold-light: #e8be55;
    --gold-dim: #7a5e1a;
    --ember: #c0440a;
    --ember-light: #e05a18;
    --sage: #4a6741;
    --sage-light: #6a8f60;
    --mist: #6b7d8c;
    --complete: #4a6741;
    --xp-bar: #c89a2e;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--stone);
    font-family: 'Crimson Text', Georgia, serif;
    color: var(--parchment);
    min-height: 100vh;
    background-image:
      radial-gradient(ellipse at 20% 0%, #4a3520 0%, transparent 50%),
      radial-gradient(ellipse at 80% 100%, #3a2810 0%, transparent 50%),
      repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.03) 2px, rgba(0,0,0,0.03) 4px);
  }

  .page-wrap {
    max-width: 760px;
    margin: 0 auto;
    padding: 24px 16px 60px;
  }

  /* Header */
  .header {
    text-align: center;
    padding: 32px 24px 28px;
    position: relative;
  }
  .header::before, .header::after {
    content: '';
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    width: 80%;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--gold-dim), var(--gold), var(--gold-dim), transparent);
  }
  .header::before { top: 0; }
  .header::after { bottom: 0; }

  .header-rune {
    font-size: 28px;
    margin-bottom: 8px;
    display: block;
    filter: drop-shadow(0 0 8px rgba(200,154,46,0.5));
  }
  .header h1 {
    font-family: 'Cinzel', serif;
    font-size: 28px;
    font-weight: 700;
    color: var(--gold-light);
    letter-spacing: 0.08em;
    text-shadow: 0 0 20px rgba(200,154,46,0.3), 0 2px 4px rgba(0,0,0,0.5);
    margin-bottom: 4px;
  }
  .header p {
    font-size: 15px;
    color: rgba(242,232,201,0.6);
    font-style: italic;
    letter-spacing: 0.04em;
  }

  /* Adventurer Panel */
  .adventurer {
    margin: 24px 0;
    background: rgba(0,0,0,0.3);
    border: 1px solid var(--gold-dim);
    border-radius: 4px;
    padding: 16px 20px;
    display: flex;
    align-items: center;
    gap: 20px;
    position: relative;
    overflow: hidden;
  }
  .adventurer::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(200,154,46,0.05) 0%, transparent 60%);
    pointer-events: none;
  }
  .avatar {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    background: radial-gradient(circle at 35% 35%, var(--stone-light), var(--stone));
    border: 2px solid var(--gold-dim);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 26px;
    flex-shrink: 0;
    position: relative;
  }
  .avatar::after {
    content: '';
    position: absolute;
    inset: -3px;
    border-radius: 50%;
    border: 1px solid rgba(200,154,46,0.2);
  }
  .adventurer-info { flex: 1; min-width: 0; }
  .adventurer-name {
    font-family: 'Cinzel', serif;
    font-size: 16px;
    color: var(--gold-light);
    font-weight: 600;
    margin-bottom: 2px;
  }
  .adventurer-title {
    font-size: 13px;
    color: rgba(242,232,201,0.55);
    font-style: italic;
    margin-bottom: 10px;
  }
  .xp-track {
    position: relative;
    height: 8px;
    background: rgba(0,0,0,0.4);
    border-radius: 4px;
    border: 1px solid rgba(200,154,46,0.25);
    overflow: hidden;
  }
  .xp-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--gold-dim), var(--gold-light));
    border-radius: 4px;
    transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
  }
  .xp-fill::after {
    content: '';
    position: absolute;
    right: 0;
    top: 0;
    bottom: 0;
    width: 4px;
    background: white;
    opacity: 0.4;
    border-radius: 0 4px 4px 0;
    animation: shimmer 2s ease-in-out infinite;
  }
  @keyframes shimmer { 0%,100%{opacity:0.3} 50%{opacity:0.7} }
  .xp-label {
    display: flex;
    justify-content: space-between;
    margin-top: 5px;
    font-size: 11px;
    color: rgba(242,232,201,0.45);
    font-family: 'Cinzel', serif;
    letter-spacing: 0.05em;
  }
  .stat-chips {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 4px;
    flex-shrink: 0;
  }
  .level-badge {
    font-family: 'Cinzel', serif;
    font-size: 11px;
    color: var(--gold);
    background: rgba(200,154,46,0.12);
    border: 1px solid var(--gold-dim);
    padding: 4px 10px;
    border-radius: 2px;
    letter-spacing: 0.1em;
    white-space: nowrap;
  }
  .tasks-done-chip {
    font-size: 11px;
    color: rgba(242,232,201,0.5);
    white-space: nowrap;
  }

  /* Chapter */
  .chapter {
    margin-bottom: 10px;
    border: 1px solid rgba(200,154,46,0.2);
    border-radius: 3px;
    overflow: hidden;
    background: rgba(0,0,0,0.2);
    transition: border-color 0.2s;
  }
  .chapter.completed { border-color: rgba(74,103,65,0.5); }

  .chapter-header {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 13px 16px;
    cursor: pointer;
    user-select: none;
    background: rgba(0,0,0,0.15);
    transition: background 0.15s;
    position: relative;
  }
  .chapter-header:hover { background: rgba(200,154,46,0.06); }
  .chapter-icon {
    font-size: 18px;
    width: 32px;
    text-align: center;
    flex-shrink: 0;
  }
  .chapter-meta { flex: 1; min-width: 0; }
  .chapter-title {
    font-family: 'Cinzel', serif;
    font-size: 13px;
    font-weight: 600;
    color: var(--gold);
    letter-spacing: 0.06em;
    margin-bottom: 3px;
  }
  .chapter.completed .chapter-title { color: var(--sage-light); }
  .chapter-subtitle {
    font-size: 12px;
    color: rgba(242,232,201,0.45);
    font-style: italic;
  }
  .chapter-progress-wrap {
    display: flex;
    align-items: center;
    gap: 8px;
    flex-shrink: 0;
  }
  .chapter-mini-bar {
    width: 60px;
    height: 4px;
    background: rgba(0,0,0,0.4);
    border-radius: 2px;
    overflow: hidden;
  }
  .chapter-mini-fill {
    height: 100%;
    background: var(--gold);
    border-radius: 2px;
    transition: width 0.4s ease;
  }
  .chapter.completed .chapter-mini-fill { background: var(--sage-light); }
  .chapter-pct {
    font-size: 11px;
    color: rgba(242,232,201,0.4);
    font-family: 'Cinzel', serif;
    min-width: 30px;
    text-align: right;
  }
  .chapter-chevron {
    font-size: 10px;
    color: var(--gold-dim);
    transition: transform 0.2s;
    margin-left: 4px;
  }
  .chapter-header.open .chapter-chevron { transform: rotate(90deg); }

  /* Quests */
  .quest-list {
    display: none;
    padding: 6px 0 10px;
    border-top: 1px solid rgba(200,154,46,0.1);
  }
  .quest-list.open { display: block; }

  .quest-item {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    padding: 9px 16px 9px 20px;
    cursor: pointer;
    transition: background 0.12s;
    position: relative;
  }
  .quest-item:hover { background: rgba(200,154,46,0.04); }
  .quest-item.done { opacity: 0.55; }

  .quest-check {
    width: 18px;
    height: 18px;
    border: 1.5px solid var(--gold-dim);
    border-radius: 2px;
    flex-shrink: 0;
    margin-top: 2px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s;
    background: rgba(0,0,0,0.2);
  }
  .quest-item.done .quest-check {
    background: var(--sage);
    border-color: var(--sage-light);
  }
  .quest-checkmark {
    width: 9px;
    height: 6px;
    border-left: 2px solid var(--parchment);
    border-bottom: 2px solid var(--parchment);
    transform: rotate(-45deg) translateY(-1px);
    display: none;
  }
  .quest-item.done .quest-checkmark { display: block; }

  .quest-content { flex: 1; }
  .quest-name {
    font-size: 14px;
    color: var(--parchment);
    line-height: 1.35;
    transition: color 0.2s;
  }
  .quest-item.done .quest-name {
    text-decoration: line-through;
    color: rgba(242,232,201,0.4);
  }
  .quest-detail {
    font-size: 12px;
    color: rgba(242,232,201,0.38);
    font-style: italic;
    margin-top: 1px;
  }
  .quest-xp {
    font-family: 'Cinzel', serif;
    font-size: 10px;
    color: var(--gold-dim);
    background: rgba(200,154,46,0.08);
    border: 1px solid rgba(200,154,46,0.18);
    padding: 2px 7px;
    border-radius: 2px;
    white-space: nowrap;
    flex-shrink: 0;
    margin-top: 2px;
    transition: all 0.2s;
  }
  .quest-item.done .quest-xp {
    color: var(--sage-light);
    background: rgba(74,103,65,0.12);
    border-color: rgba(74,103,65,0.25);
  }

  /* AI badge */
  .ai-tag {
    display: inline-block;
    font-size: 9px;
    font-family: 'Cinzel', serif;
    letter-spacing: 0.08em;
    color: var(--mist);
    background: rgba(107,125,140,0.12);
    border: 1px solid rgba(107,125,140,0.25);
    padding: 1px 6px;
    border-radius: 2px;
    margin-left: 6px;
    vertical-align: middle;
  }

  /* Level up toast */
  .toast {
    position: fixed;
    bottom: 24px;
    left: 50%;
    transform: translateX(-50%) translateY(80px);
    background: var(--stone);
    border: 1px solid var(--gold);
    border-radius: 3px;
    padding: 12px 24px;
    text-align: center;
    z-index: 100;
    transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
    box-shadow: 0 0 30px rgba(200,154,46,0.3), 0 8px 24px rgba(0,0,0,0.6);
    pointer-events: none;
    min-width: 220px;
  }
  .toast.show { transform: translateX(-50%) translateY(0); }
  .toast-title {
    font-family: 'Cinzel', serif;
    font-size: 14px;
    color: var(--gold-light);
    letter-spacing: 0.1em;
    margin-bottom: 3px;
  }
  .toast-msg {
    font-size: 13px;
    color: rgba(242,232,201,0.7);
    font-style: italic;
  }

  /* Footer divider */
  .footer-line {
    text-align: center;
    margin-top: 32px;
    font-size: 12px;
    color: rgba(242,232,201,0.25);
    font-style: italic;
    letter-spacing: 0.06em;
  }
  .ornament {
    display: block;
    text-align: center;
    color: var(--gold-dim);
    font-size: 14px;
    letter-spacing: 8px;
    margin: 10px 0 6px;
    opacity: 0.6;
  }

  @keyframes xpPop {
    0% { transform: scale(1); }
    40% { transform: scale(1.07); }
    100% { transform: scale(1); }
  }
  .xp-pop { animation: xpPop 0.4s ease; }
</style>
</head>
<body>
<div class="page-wrap">

  <div class="header">
    <span class="header-rune">⚔️</span>
    <h1>Quest Log</h1>
    <p>The Chronicles of the Dungeon Forge — UE5 RPG Development</p>
  </div>

  <div class="adventurer">
    <div class="avatar">🧙</div>
    <div class="adventurer-info">
      <div class="adventurer-name">The Game Maker</div>
      <div class="adventurer-title" id="adventurer-title">Apprentice Dungeon Architect</div>
      <div class="xp-track">
        <div class="xp-fill" id="xp-fill" style="width: 0%"></div>
      </div>
      <div class="xp-label">
        <span id="xp-label-left">0 XP earned</span>
        <span id="xp-label-right">0 / 46 quests</span>
      </div>
    </div>
    <div class="stat-chips">
      <div class="level-badge" id="level-badge">LEVEL 1</div>
      <div class="tasks-done-chip" id="tasks-done-chip">0 tasks done</div>
    </div>
  </div>

  <div id="chapters-container"></div>

  <span class="ornament">· · ✦ · ·</span>
  <div class="footer-line">Tasks marked <em>AI</em> can be delegated to an AI assistant. Check them off as you forge your world.</div>
</div>

<div class="toast" id="toast">
  <div class="toast-title" id="toast-title">⚔ LEVEL UP!</div>
  <div class="toast-msg" id="toast-msg">You have grown in power.</div>
</div>

<script>
const CHAPTERS = [
  {
    id: 'c1',
    icon: '📜',
    title: 'Chapter I — The Scroll of Design',
    subtitle: 'Game Design Phase · Lay the foundation before a single line of code',
    quests: [
      { id: 't1', name: 'Write your Game Design Document (GDD)', detail: 'Core loop, scope, target feel', xp: 40, ai: true },
      { id: 't2', name: 'Define the crafting system rules', detail: 'Recipe trees, ingredient categories, station types', xp: 30, ai: true },
      { id: 't3', name: 'Design biome & dungeon themes', detail: 'At least 3 biomes — art direction + enemy flavour', xp: 25, ai: true },
      { id: 't4', name: 'Create item & lore bible', detail: 'Weapons, materials, consumables, lore flavour text', xp: 30, ai: true },
      { id: 't5', name: 'Define enemy types & behaviour briefs', detail: 'Names, roles, attack patterns, AI intent', xp: 20, ai: true },
      { id: 't6', name: 'Finalize scope & cut list', detail: 'Decide what ships in v1.0 vs. post-launch', xp: 20, ai: false },
    ]
  },
  {
    id: 'c2',
    icon: '🏗️',
    title: 'Chapter II — The Runic Foundation',
    subtitle: 'UE5 Setup Phase · Build your forge before you craft',
    quests: [
      { id: 't7', name: 'Install UE5 and create project', detail: 'Use the top-down starter template', xp: 15, ai: false },
      { id: 't8', name: 'Set up Git + version control', detail: 'Git LFS for large assets, .gitignore for UE5', xp: 20, ai: true },
      { id: 't9', name: 'Learn UE5 Blueprint fundamentals', detail: 'Variables, functions, event graphs — 4–6 hrs', xp: 50, ai: false },
      { id: 't10', name: 'Configure folder structure', detail: 'Art, Blueprints, Maps, Sound, UI folders', xp: 10, ai: true },
      { id: 't11', name: 'Set up input mapping', detail: 'WASD / controller, mouse click-to-move, attack key', xp: 20, ai: false },
    ]
  },
  {
    id: 'c3',
    icon: '🌍',
    title: 'Chapter III — The World Engine',
    subtitle: 'Procedural Generation · Make the world build itself',
    quests: [
      { id: 't12', name: 'Learn UE5 PCG Framework basics', detail: 'PCG graph editor, point actors, surface samplers', xp: 45, ai: false },
      { id: 't13', name: 'Build dungeon/room tile set rules', detail: 'Floor, wall, door, corner tile variants', xp: 35, ai: false },
      { id: 't14', name: 'Write dungeon generation algorithm', detail: 'BSP or room-and-corridor approach in C++/Blueprint', xp: 50, ai: true },
      { id: 't15', name: 'Implement weighted loot table system', detail: 'DataTable-driven rarity tiers', xp: 30, ai: true },
      { id: 't16', name: 'Build enemy spawn manager', detail: 'Spawn points tied to room types + difficulty scaling', xp: 30, ai: true },
      { id: 't17', name: 'Tune generation seeds', detail: 'Playtest 20+ seeds until outputs feel fun', xp: 25, ai: false },
    ]
  },
  {
    id: 'c4',
    icon: '⚙️',
    title: 'Chapter IV — The Codex of Systems',
    subtitle: 'Gameplay Code · The mechanical heart of your world',
    quests: [
      { id: 't18', name: 'Learn Gameplay Ability System (GAS) basics', detail: 'Attributes, abilities, effects — 6–8 hrs', xp: 60, ai: false },
      { id: 't19', name: 'Build player stat system', detail: 'Health, stamina, strength, speed via GAS attributes', xp: 40, ai: true },
      { id: 't20', name: 'Build inventory system', detail: 'Item slots, stacking, drag-drop, persistence', xp: 45, ai: true },
      { id: 't21', name: 'Build crafting system', detail: 'Recipe matching, ingredient consumption, output spawn', xp: 40, ai: true },
      { id: 't22', name: 'Create enemy AI behaviour trees', detail: 'Idle → patrol → chase → attack → flee', xp: 40, ai: true },
      { id: 't23', name: 'Build top-down combat system', detail: 'Melee hitboxes, projectiles, dodge roll', xp: 50, ai: false },
      { id: 't24', name: 'Implement save/load system', detail: 'Player stats, inventory, dungeon seed persistence', xp: 35, ai: true },
    ]
  },
  {
    id: 'c5',
    icon: '🎨',
    title: 'Chapter V — The Artisan\'s Workshop',
    subtitle: 'Art & Visuals · Dress your world in stone and shadow',
    quests: [
      { id: 't25', name: 'Source character asset pack (Fab.com)', detail: 'Top-down hero + enemy meshes with animations', xp: 20, ai: false },
      { id: 't26', name: 'Source environment & dungeon pack', detail: 'Modular walls, floors, props, chests', xp: 20, ai: false },
      { id: 't27', name: 'Generate UI icon set with AI', detail: 'Item sprites, skill icons, material icons', xp: 25, ai: true },
      { id: 't28', name: 'Build HUD in UMG', detail: 'Health bar, stamina, minimap placeholder, hotbar', xp: 35, ai: false },
      { id: 't29', name: 'Build inventory UI in UMG', detail: 'Grid layout, item tooltips, crafting panel', xp: 35, ai: false },
      { id: 't30', name: 'Set up Lumen lighting per biome', detail: 'Torch flicker, ambient color per dungeon theme', xp: 30, ai: false },
    ]
  },
  {
    id: 'c6',
    icon: '🔊',
    title: 'Chapter VI — The Sound Forge',
    subtitle: 'Audio · Give your world a voice',
    quests: [
      { id: 't31', name: 'Generate biome ambience tracks (AI)', detail: 'Cave, forest, fire dungeon, ice dungeon', xp: 20, ai: true },
      { id: 't32', name: 'Generate SFX pack (AI)', detail: 'Combat hits, item pickup, crafting sounds', xp: 20, ai: true },
      { id: 't33', name: 'Generate adaptive music layers (AI)', detail: 'Calm, combat, boss — stems that blend', xp: 25, ai: true },
      { id: 't34', name: 'Implement audio via MetaSounds', detail: 'Wire all sounds to gameplay events in UE5', xp: 35, ai: false },
      { id: 't35', name: 'Set up adaptive music system', detail: 'Transition between calm/combat based on proximity', xp: 25, ai: false },
    ]
  },
  {
    id: 'c7',
    icon: '🔥',
    title: 'Chapter VII — The Final Trial',
    subtitle: 'Polish & Ship · Prove your creation is worthy',
    quests: [
      { id: 't36', name: 'Profile with Unreal Insights', detail: 'Find and fix top 3 frame-time offenders', xp: 40, ai: false },
      { id: 't37', name: 'Optimise PCG generation cost', detail: 'Generation must complete under 500ms', xp: 30, ai: false },
      { id: 't38', name: 'Complete a full playtest run', detail: 'Start → 3 dungeons → boss → crafted gear → win', xp: 35, ai: false },
      { id: 't39', name: 'Bug bash — fill issue tracker', detail: 'Log every crash, softlock, and broken system', xp: 25, ai: false },
      { id: 't40', name: 'Fix critical bugs from playtest', detail: 'P0/P1 issues only for launch', xp: 30, ai: false },
      { id: 't41', name: 'Write Steam / itch.io page copy (AI)', detail: 'Hook, feature list, 3 tagline options', xp: 20, ai: true },
      { id: 't42', name: 'Create trailer script & structure (AI)', detail: 'Narration beats, gameplay moments to capture', xp: 20, ai: true },
      { id: 't43', name: 'Capture and edit gameplay trailer', detail: 'Record, edit, add music, export', xp: 30, ai: false },
      { id: 't44', name: 'Set up store page, pricing, metadata', detail: 'Screenshots, tags, age rating, price', xp: 20, ai: false },
      { id: 't45', name: 'Package and submit build', detail: 'Packaged shipping build, platform review submit', xp: 50, ai: false },
      { id: 't46', name: 'Launch! 🎉', detail: 'Click the button. You made a game.', xp: 100, ai: false },
    ]
  }
];

const LEVELS = [
  { min: 0,    max: 199,  name: 'LEVEL 1', title: 'Apprentice Dungeon Architect' },
  { min: 200,  max: 499,  name: 'LEVEL 2', title: 'Journeyman Blueprint Weaver' },
  { min: 500,  max: 899,  name: 'LEVEL 3', title: 'Adept World Forger' },
  { min: 900,  max: 1399, name: 'LEVEL 4', title: 'Skilled Dungeon Architect' },
  { min: 1400, max: 1899, name: 'LEVEL 5', title: 'Expert System Crafter' },
  { min: 1900, max: 2399, name: 'LEVEL 6', title: 'Master Lore Weaver' },
  { min: 2400, max: 2999, name: 'LEVEL 7', title: 'Grand Artificer of Realms' },
  { min: 3000, max: Infinity, name: 'LEVEL MAX', title: 'Legendary Game Maker' },
];

const TOTAL_XP = CHAPTERS.flatMap(c => c.quests).reduce((a, q) => a + q.xp, 0);
const TOTAL_TASKS = CHAPTERS.flatMap(c => c.quests).length;

let state = {};
try { state = JSON.parse(localStorage.getItem('rpg-quest-state') || '{}'); } catch(e) {}

let openChapters = {};
try { openChapters = JSON.parse(localStorage.getItem('rpg-open-chapters') || '{}'); } catch(e) {}

function save() {
  try {
    localStorage.setItem('rpg-quest-state', JSON.stringify(state));
    localStorage.setItem('rpg-open-chapters', JSON.stringify(openChapters));
  } catch(e) {}
}

function getStats() {
  let xp = 0, done = 0;
  CHAPTERS.forEach(c => c.quests.forEach(q => {
    if (state[q.id]) { xp += q.xp; done++; }
  }));
  return { xp, done };
}

function getLevel(xp) {
  for (let i = LEVELS.length - 1; i >= 0; i--) {
    if (xp >= LEVELS[i].min) return LEVELS[i];
  }
  return LEVELS[0];
}

let prevLevel = null;

function updateHeader() {
  const { xp, done } = getStats();
  const lvl = getLevel(xp);
  const pct = Math.round((xp / TOTAL_XP) * 100);

  const fill = document.getElementById('xp-fill');
  fill.style.width = pct + '%';
  fill.classList.remove('xp-pop');
  void fill.offsetWidth;
  fill.classList.add('xp-pop');

  document.getElementById('xp-label-left').textContent = xp + ' XP earned';
  document.getElementById('xp-label-right').textContent = done + ' / ' + TOTAL_TASKS + ' quests';
  document.getElementById('level-badge').textContent = lvl.name;
  document.getElementById('adventurer-title').textContent = lvl.title;
  document.getElementById('tasks-done-chip').textContent = done + ' tasks done';

  if (prevLevel && prevLevel.name !== lvl.name) {
    showToast('⚔ ' + lvl.name + '!', lvl.title);
  }
  prevLevel = lvl;
}

function showToast(title, msg) {
  const t = document.getElementById('toast');
  document.getElementById('toast-title').textContent = title;
  document.getElementById('toast-msg').textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3000);
}

function toggleQuest(qid, xp) {
  state[qid] = !state[qid];
  save();
  const el = document.getElementById('quest-' + qid);
  if (el) el.classList.toggle('done', state[qid]);
  updateChapterProgress(el);
  updateHeader();
}

function updateChapterProgress(questEl) {
  if (!questEl) return;
  const chapter = questEl.closest('.chapter');
  if (!chapter) return;
  const cid = chapter.dataset.cid;
  const ch = CHAPTERS.find(c => c.id === cid);
  if (!ch) return;
  const done = ch.quests.filter(q => state[q.id]).length;
  const pct = Math.round((done / ch.quests.length) * 100);
  const fill = chapter.querySelector('.chapter-mini-fill');
  const pctEl = chapter.querySelector('.chapter-pct');
  if (fill) fill.style.width = pct + '%';
  if (pctEl) pctEl.textContent = pct + '%';
  chapter.classList.toggle('completed', done === ch.quests.length);
}

function toggleChapter(cid, headerEl) {
  openChapters[cid] = !openChapters[cid];
  save();
  const body = document.getElementById('body-' + cid);
  if (body) body.classList.toggle('open', openChapters[cid]);
  headerEl.classList.toggle('open', openChapters[cid]);
}

function render() {
  const container = document.getElementById('chapters-container');
  container.innerHTML = '';

  CHAPTERS.forEach(ch => {
    const done = ch.quests.filter(q => state[q.id]).length;
    const pct = Math.round((done / ch.quests.length) * 100);
    const isOpen = !!openChapters[ch.id];
    const isComplete = done === ch.quests.length;

    const div = document.createElement('div');
    div.className = 'chapter' + (isComplete ? ' completed' : '');
    div.dataset.cid = ch.id;

    div.innerHTML = `
      <div class="chapter-header${isOpen ? ' open' : ''}" onclick="toggleChapter('${ch.id}', this)">
        <div class="chapter-icon">${ch.icon}</div>
        <div class="chapter-meta">
          <div class="chapter-title">${ch.title}</div>
          <div class="chapter-subtitle">${ch.subtitle}</div>
        </div>
        <div class="chapter-progress-wrap">
          <div class="chapter-mini-bar"><div class="chapter-mini-fill" style="width:${pct}%"></div></div>
          <span class="chapter-pct">${pct}%</span>
        </div>
        <span class="chapter-chevron">▶</span>
      </div>
      <div class="quest-list${isOpen ? ' open' : ''}" id="body-${ch.id}">
        ${ch.quests.map(q => `
          <div class="quest-item${state[q.id] ? ' done' : ''}" id="quest-${q.id}" onclick="toggleQuest('${q.id}', ${q.xp})">
            <div class="quest-check"><div class="quest-checkmark"></div></div>
            <div class="quest-content">
              <div class="quest-name">${q.name}${q.ai ? '<span class="ai-tag">AI</span>' : ''}</div>
              <div class="quest-detail">${q.detail}</div>
            </div>
            <div class="quest-xp">+${q.xp} XP</div>
          </div>
        `).join('')}
      </div>
    `;
    container.appendChild(div);
  });

  prevLevel = getLevel(getStats().xp);
  updateHeader();
}

render();
</script>
</body>
</html>
