# CLAUDE.md - Umbra Sapiens Development Guide

## Project Overview

**Project Name:** Umbra Sapiens
**Version:** 0.17d Istanbul (Not Constantinople)
**Type:** Crusader Kings II Total Conversion/Expansion Mod
**Repository Size:** 641 MB (14,222 files)
**Last Updated:** November 23, 2025

Umbra Sapiens is a comprehensive expansion mod for Crusader Kings II that extends the game world to include historically underrepresented regions including Asia, Africa, the Americas, Oceania, and Arctic territories. The mod adds hundreds of new cultures, dynasties, religions, and gameplay mechanics focused on world history beyond the base game's Europe-centric coverage.

## Technology Stack

### Language and Format
This project does NOT use traditional programming languages. Instead it uses:

- **Paradox Interactive Script Format** (.txt files) - 9,383 files
  - Key-value pair structure with nested blocks
  - Conditions, triggers, and effects for game logic
  - Comments using `#` symbol
  - No compilation or build step required

- **Graphics Formats:**
  - `.dds` - DirectDraw Surface (compressed textures) - 248 files
  - `.tga` - Targa (uncompressed images) - 4,321 files
  - `.gfx` - Graphics definition files
  - `.gui` - UI layout files

- **Localization:** `.csv` files for translations (77 files)

### Dependencies
- **Crusader Kings II** (base game required)
- **Umbra Spherae-Reborn** (mod dependency)

## Repository Structure

```
Umbra_Sapiens2/
├── umbra_sapiens.mod          # Mod configuration/manifest
├── .gitattributes             # Git LF normalization
│
└── umbra_sapiens/             # Main mod directory (524 MB)
    ├── common/                # Game definitions & rules (171 files)
    ├── history/               # Historical data (9,124 files)
    ├── events/                # Scripted events (45 files)
    ├── decisions/             # Player decisions (24 files)
    ├── localisation/          # Translations (77 CSV files)
    ├── gfx/                   # Graphics & UI (4,800+ files)
    ├── map/                   # Map data (11 files)
    └── interface/             # UI definitions (2 files)
```

## Key Directories Explained

### `/umbra_sapiens/common/` - Game Mechanics & Definitions

This is the core logic directory. All game rules, content definitions, and mechanical systems are defined here:

| Directory | Files | Purpose | Example Files |
|-----------|-------|---------|---------------|
| **cultures/** | 9 | Cultural groups and individual cultures | `japan.txt`, `korea.txt`, `africa.txt`, `north_america.txt` |
| **dynasties/** | 72 | Noble houses and family lines | `korean.txt`, `japan.txt`, `kongo.txt`, `maya.txt` |
| **landed_titles/** | 33 | Kingdom/Empire/County hierarchies | `US_China.txt`, `US_Japan.txt`, `US_Brazil.txt` |
| **religions/** | 3 | Faith systems and religious mechanics | `00_religions.txt`, `crusade.info` |
| **buildings/** | 2 | Constructible structures | `castle.txt`, `CastleCulture.txt` |
| **cb_types/** | 3 | Casus belli (war justifications) | - |
| **decisions/** | - | Player-triggered actions | - |
| **governments/** | - | Government types (feudal, republic, etc.) | - |
| **laws/** | - | Succession and realm laws | - |
| **traits/** | - | Character trait definitions | - |
| **bloodlines/** | - | Inheritable dynasty bonuses | `00_bloodlines.txt` |
| **societies/** | - | Secret societies and organizations | - |
| **scripted_triggers/** | - | Reusable condition checks | - |
| **scripted_effects/** | - | Reusable effect libraries | - |

**Key File:** `defines.txt` - Sets game timeline:
- Start date: 1066.9.15 (High Medieval)
- Last playable date: 1640.12.1 (Early Modern)

### `/umbra_sapiens/history/` - Historical Data (9,124 files)

Historical starting states for the game:

- **characters/** (224 files) - Character definitions with genealogies
- **provinces/** (3,405 files) - Province-level data (culture, religion, holdings)
- **titles/** (5,473 files) - Title ownership and succession history
- **technology/** - Regional tech levels
- **offmap_powers/** - Off-map realm history (e.g., distant empires)

### `/umbra_sapiens/events/` - Scripted Events (45 files)

Trigger-based narrative content:
- `jd_chinese_war_events.txt` - Chinese warfare system
- `reformation_events.txt` - Religious reformation mechanics
- `portuguese_events.txt` - Portuguese-specific content
- Regional/cultural event chains

### `/umbra_sapiens/decisions/` - Player Decisions (24 files)

Player-triggered actions:
- `china_decisions.txt` - Chinese administration
- `japan_decision.txt` - Japanese feudalism
- `colonial_decisions.txt` - Colonial mechanics
- `forming_countries_decisions.txt` - Nation formation
- `banking_decisions.txt` - Economic systems

### `/umbra_sapiens/localisation/` - Translations (77 files)

CSV-formatted text localization:
- Format: `KEY;English;French;German;Spanish;...`
- Files named by region: `0_US_Portugal.csv`, `0_US_Indonesia.csv`
- **customizable_localisation/** - Dynamic text generation

### `/umbra_sapiens/gfx/` - Graphics Assets (4,800+ files)

Visual content organized by type:

- **flags/** (4,175 files) - Realm and character flags (.dds format)
- **characters/** - Portrait components:
  - `amerindian_male/`, `amerindian_female/`
  - `japanese_male/`, `japanese_female/`
  - `merina_male/`, `merina_female/` (Madagascar)
  - `tuniq_male/` (Arctic cultures)
  - `shared/` - Universal portrait elements
- **interface/** - UI graphics and definitions
  - `portraits/` (15+ ethnic portrait sets)
  - `coat_of_arms/` - Heraldry graphics
  - `portrait_properties/` - Portrait configuration
- **FX/** - Visual effects
- **models/** - 3D assets:
  - `Settlements/`, `Shields/`, `animation/`
- **traits/** - Trait icon graphics
- **coats_of_arms/** - Dynamic heraldry definitions

## File Format Conventions

### Paradox Script Syntax

All `.txt` files in this mod use Paradox Interactive's proprietary scripting format:

```paradox
# Comments use hash symbol
key = value                    # Simple assignment
key = { value1 value2 }       # List
nested_key = {                # Block
    inner_key = value
    another_key = { ... }
}
```

#### Common Patterns

**Culture Definition:**
```paradox
culture_group = {
    graphical_cultures = { culture_gfx }

    specific_culture = {
        color = { 0.3 0.55 0.8 }  # RGB values 0-1

        male_names = {
            Name1_LocalizedForm Name2 Name3_Alt
        }
        female_names = {
            Name1 Name2_LocalizedForm
        }

        male_patronym = "sson"     # Patronymic suffix
        female_patronym = "sdotter"

        modifier = culture_modifier_name
    }
}
```

**Character Definition:**
```paradox
character_id = {
    name = "CharacterName"
    dynasty = dynasty_id

    birth_date = 1050.1.15
    death_date = 1100.6.23

    culture = culture_name
    religion = religion_name

    father = parent_character_id
    mother = parent_character_id

    trait = trait_name
    trait = another_trait
}
```

**Province Data:**
```paradox
# province_id - Province Name
province_id = {
    culture = culture_name
    religion = religion_name

    # Holdings
    b_barony_name = castle  # or city, temple

    # History changes
    1066.1.1 = {
        culture = new_culture
    }
}
```

### Naming Conventions

#### File Naming
- Prefix `00_` indicates master/override files: `00_cultures.txt`, `00_dynasties.txt`
- Prefix `US_` indicates Umbra Sapiens-specific content: `US_China.txt`, `US_Japan.txt`
- Regional grouping: `north_america.txt`, `east_africa.txt`
- Culture-specific: `japan.txt`, `korean.txt`, `indonesia.txt`

#### ID Conventions
- IDs use lowercase with underscores: `japanese_culture`, `shinto_religion`
- Dynasty IDs are numeric: `1000001`, `2034567`
- Character IDs are numeric: `1234567`
- Province IDs are numeric: `1` to `3405`

#### Localization Keys
- Format: `PREFIX_identifier` (e.g., `culture_japanese`, `religion_shinto`)
- Names with alternate forms use underscore: `Erik_Eric`, `Catherine_Katarina`

## Geographic Coverage

The mod expands CK2 to cover:

### Asia
- **Japan** - Complete cultural and political systems
- **Korea** - Full Korean peninsula
- **China** - Extended Chinese regions with off-map mechanics
- **Indonesia** - Island nations and cultures
- **Indochina** - Southeast Asian mainland
- **Central Asia** - Steppe and Silk Road regions

### Americas
- **North America** - Indigenous cultures (Algonquian, Iroquoian, Arctic, etc.)
- **Mesoamerica** - Aztec, Maya, and related cultures
- **South America** - Amazon, Andes, Patagonia regions
- **Caribbean** - Island cultures

### Africa
- **West Africa** - Kongo, Mali, etc.
- **East Africa** - Swahili coast, Ethiopia
- **Madagascar** - Merina and other cultures
- **North Africa** - Enhanced coverage

### Other
- **Oceania** - Australia, Pacific islands
- **Arctic** - Inuit, Siberian cultures
- **Atlantis** - Fictional content

## Development Workflows

### Making Changes

#### 1. Modifying Existing Content

**Adding a New Culture:**
1. Navigate to `umbra_sapiens/common/cultures/`
2. Find the appropriate cultural group file (e.g., `japan.txt` for Japanese cultures)
3. Add culture definition following the established format
4. Update localisation in `umbra_sapiens/localisation/`

**Adding New Characters:**
1. Navigate to `umbra_sapiens/history/characters/`
2. Find the appropriate regional file
3. Add character with unique numeric ID
4. Link to existing dynasty or create new one

**Creating New Titles:**
1. Define title in `umbra_sapiens/common/landed_titles/`
2. Create title history in `umbra_sapiens/history/titles/`
3. Assign starting holder if needed
4. Add localisation entry

#### 2. Adding New Events

1. Create or edit file in `umbra_sapiens/events/`
2. Define event with unique namespace and ID
3. Set trigger conditions
4. Define effects and options
5. Add localization for event text

#### 3. Creating New Decisions

1. Edit appropriate file in `umbra_sapiens/decisions/`
2. Define decision with:
   - Potential (who can see it)
   - Allow (requirements to take it)
   - Effect (what happens)
   - AI will do (AI decision logic)
3. Add localization

### Testing Changes

There is no automated testing framework. Test by:
1. Loading the mod in Crusader Kings II
2. Starting a game with relevant bookmark/character
3. Testing in-game behavior
4. Checking for syntax errors (game will show errors on load)
5. Verifying localization displays correctly

### Version Control

#### Git Workflow
- **Main branch:** Production-ready code
- **Feature branches:** Named with `claude/` prefix for AI development
- **Current working branch:** `claude/claude-md-mibkrv6fjiy04jnn-013wf1M8C8AnVzpHcNTSov6N`

#### Committing Changes
```bash
# Stage your changes
git add umbra_sapiens/path/to/changed/file.txt

# Commit with descriptive message
git commit -m "Add new Japanese clans to dynasties

- Added 5 new historical clans to japan.txt
- Updated localization for new dynasty names"

# Push to feature branch
git push -u origin claude/claude-md-mibkrv6fjiy04jnn-013wf1M8C8AnVzpHcNTSov6N
```

#### Commit Message Style
Based on repository history, use clear descriptive messages:
- "Add [feature]" - New content
- "Fix [issue]" - Bug fixes
- "Update [system]" - Modifications
- Include date references when relevant (e.g., "23.11.2025")

## Common Tasks for AI Assistants

### 1. Adding New Historical Characters

**Steps:**
1. Research historical accuracy (dates, relationships, titles)
2. Find appropriate character file in `history/characters/`
3. Assign unique numeric character ID (check for next available)
4. Define character with all attributes:
   - Name, birth/death dates
   - Dynasty, culture, religion
   - Family relationships (father, mother, spouse, children)
   - Traits if notable
5. If creating new dynasty, add to `common/dynasties/`
6. Update title history if character held titles
7. Add name localization if not already present

### 2. Expanding Geographic Coverage

**Adding a New Region:**
1. Define cultures in `common/cultures/[region].txt`
2. Create dynasties in `common/dynasties/[region].txt`
3. Define landed titles in `common/landed_titles/US_[Region].txt`
4. Set up provinces in `history/provinces/`
5. Assign characters in `history/characters/`
6. Create title history in `history/titles/`
7. Add appropriate flags in `gfx/flags/`
8. Configure portrait graphics in `gfx/characters/`
9. Localize all new content in `localisation/`

### 3. Creating New Game Mechanics

**Adding a Decision:**
1. Create decision in `decisions/[category]_decisions.txt`
2. Define triggers and effects using scripted_triggers/effects
3. Add AI logic
4. Localize decision text, tooltips
5. Test edge cases

**Adding an Event Chain:**
1. Create event file in `events/[theme]_events.txt`
2. Use consistent namespace
3. Link events with event IDs
4. Add mean_time_to_happen or triggers
5. Localize all event text and options

### 4. Maintaining Consistency

**Always check:**
- ID uniqueness (characters, dynasties, events)
- Localization coverage (no missing text keys)
- Historical accuracy for date ranges (1066-1640)
- Graphics references exist in `gfx/`
- Parent/child culture relationships
- Dynasty continuity in character definitions

## Important Conventions

### Do's ✓
- **Research first:** Read existing similar files before creating new content
- **Follow patterns:** Match existing file structure and formatting
- **Be historically accurate:** Use proper dates within game timeframe (1066-1640)
- **Localize everything:** Every visible text needs localization entry
- **Use unique IDs:** Never reuse character, dynasty, or event IDs
- **Comment your code:** Use `#` for explanatory comments
- **Group logically:** Keep regional content together
- **Test incrementally:** Load and test after each major change

### Don'ts ✗
- **Don't break syntax:** Paradox script is strict about braces and formatting
- **Don't duplicate IDs:** Results in unpredictable game behavior
- **Don't ignore localisation:** Missing keys show as raw text in-game
- **Don't create orphans:** Characters need dynasties, titles need holders
- **Don't exceed date range:** Game timeline is 1066-1640
- **Don't mix cultural graphics:** Keep portrait sets consistent
- **Don't forget dependencies:** Reference existing game objects correctly
- **Don't skip testing:** Broken mods can crash the game

## File Size Considerations

- Total repository: 641 MB
- Individual graphics can be large (.tga files especially)
- History files with thousands of characters can be large
- Watch for file duplication
- Compress graphics where possible (.dds preferred over .tga)

## Localization Guidelines

### CSV Format
```csv
KEY;English;French;German;Spanish;...
culture_japanese;Japanese;Japonais;Japanisch;Japonés;...
```

### Best Practices
- Always provide English at minimum
- Use semicolons as delimiters
- Escape semicolons in text with `\;`
- Keep keys descriptive: `event_name_123` better than `e123`
- Group related keys together
- Use alternate name forms with underscore: `Erik_Eric`

## Graphics Integration

### Adding Character Portraits
1. Create sprites in appropriate ethnic folder: `gfx/characters/[ethnicity]_[gender]/`
2. Reference in `.gfx` file: `gfx/interface/umbra_sapiens.gfx`
3. Define portrait properties: `interface/portrait_properties/`
4. Link to culture in culture definition

### Adding Flags
1. Create `.dds` file for flag graphic
2. Place in `gfx/flags/`
3. Name matching title: `c_province_name.tga` or `k_kingdom_name.tga`
4. Flag auto-loads based on title ID

### Coat of Arms
- Define in `interface/coat_of_arms/`
- Reference in title definition
- Use heraldry patterns from base game

## Performance Considerations

- Minimize trigger complexity in events (they check frequently)
- Use scripted_triggers for reused conditions (more efficient)
- Avoid creating excessive characters in history (game loads all)
- Compress graphics appropriately
- Don't create circular dependencies in title hierarchies

## Debugging Tips

### Common Errors

**Missing Localization:**
- Symptom: Raw keys display in-game (e.g., `culture_japanese`)
- Fix: Add entry to appropriate CSV in `localisation/`

**Invalid Syntax:**
- Symptom: Game error log on launch
- Fix: Check brace matching, key-value pairs, use `#` for comments

**Broken Character References:**
- Symptom: Missing characters, broken dynasties
- Fix: Verify character IDs exist, check father/mother references

**Missing Graphics:**
- Symptom: Blank portraits, missing flags
- Fix: Check file paths, verify `.gfx` definitions

**Trigger Errors:**
- Symptom: Decisions/events don't appear
- Fix: Review trigger logic, check scope context

## Contact and Resources

### Project Information
- **Repository:** LuqP2/Umbra_Sapiens2
- **Main Contributors:**
  - Leiferson (lead developer)
  - tsf4 (contributor)
  - tannerflick4 (maintainer)
  - Lucas Pierri (contributor)

### Useful References
- Crusader Kings II Wiki (for base game mechanics)
- Paradox Modding Forum
- Existing mod files (best documentation source)

## Current State (November 23, 2025)

**Branch:** `claude/claude-md-mibkrv6fjiy04jnn-013wf1M8C8AnVzpHcNTSov6N`
**Status:** Clean working directory
**Recent Updates:**
- Merged PR #1 from Leiferson/main
- Fixed duplicates in some files
- Regular maintenance updates

## Quick Reference Card

| Task | Primary Files | Secondary Files |
|------|---------------|-----------------|
| Add culture | `common/cultures/` | `localisation/`, `gfx/characters/` |
| Add character | `history/characters/` | `common/dynasties/`, `history/titles/` |
| Add title | `common/landed_titles/` | `history/titles/`, `gfx/flags/` |
| Add event | `events/` | `localisation/` |
| Add decision | `decisions/` | `localisation/`, `common/scripted_*` |
| Add religion | `common/religions/` | `localisation/`, `gfx/interface/` |
| Add graphics | `gfx/[category]/` | `gfx/interface/*.gfx` |
| Add province | `history/provinces/` | `map/`, `common/landed_titles/` |

---

**Last Updated:** November 23, 2025
**For AI Assistants:** This document provides comprehensive context for working with the Umbra Sapiens mod codebase. Always read existing files before making changes, maintain consistency with established patterns, and test changes in-game before committing.
