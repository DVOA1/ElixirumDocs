# Ars Elixirum Datapack Guide

## ⚖️ Legal Stuff

This guide ain’t official. Not made by or endorsed by the **Obscuria Team**, the creators of Ars Elixirum.
They own all rights to the mod, its content, names, and assets.

This doc is just to help you make datapacks that work with it. Personal, non-commercial use only. Don’t be a dumbass and try to sell it or claim it as your own.

---

## 🔑 Key Concepts

> These are the most relevant things to know. Not all-inclusive, just what you need to get started fast.

* [Adding Custom Essences](#essence-folder)
* [Manually Setting Ingredients](#ingredient-preset-folder)
* [Tags](#tags)

  * [Filter Ingredients](#filter-ingredients)
  * [Add Heat Sources](#adding-new-heat-sources)

---

## 📂 Folder Structure

```bash
data/
└── elixirum/
    ├── elixirum/
    │   ├── configured_elixir
    │   ├── elixir_prefix
    │   ├── essence
    │   └── ingredient_preset
    └── tags/
        ├── block/
        │   └── heat_sources.json
        └── item/
            ├── essence_blacklist.json
            ├── essence_whitelist.json
            └── potion_shelf_placeable.json
```

---

## 🌍 Elixirum Folder

Create a folder named `elixirum` inside the main `elixirum` directory. That’s where everything custom goes.

### Configured Elixir

Defines effect variants using a pre-made essence. You only set `amplifier` and `duration`.

**File name = essence name**

```json
{
  "variants": [
    [
      {
        "amplifier": 0,
        "duration": 60,
        "essence": "elixirum:health_boost"
      }
    ],
    [
      {
        "amplifier": 2,
        "duration": 180,
        "essence": "elixirum:health_boost"
      }
    ],
    [
      {
        "amplifier": 5,
        "duration": 360,
        "essence": "elixirum:health_boost"
      }
    ]
  ]
}
```

---

### Elixir Prefix

Adds a random prefix from the lang file (like "Devastating elixir of strength").

```json
{
  "key": "effect_prefix.elixirum.absorption_assimilating",
  "source": "minecraft:absorption"
}
```

---

### Essence Folder

This one matters most. Essences define the effect part of the elixir.

* `category`: "NONE", "OFFENSIVE", "DEFENSIVE", "ENHANCING", "DIMINISHING"
* `max_amplifier`: max amplifier (starts at 0)
* `max_duration`: max duration in ticks
* `mob_effect`: the effect ID
* `required_ingredients`: how many ingredients needed to not be pale
* `required_quality`: how much quality needed to not be weak

**File name = effect name (no namespace)**

```json
{
  "category": "enhancing",
  "max_amplifier": 3,
  "max_duration": 1200,
  "mob_effect": "farmersdelight:comfort",
  "required_ingredients": 1,
  "required_quality": 10
}
```

---

### Ingredient Preset Folder

Overrides ingredient generation completely. You set items or tags manually with weights.

> Almost every item has randomly generated effects unless overridden here.

* `essences`: keys are essence IDs, values are weights
* `target`: the item ID

**File name = item name**

```json
{
  "essences": {
    "elixirum:saturation": 20
  },
  "target": "minecraft:blue_orchid"
}
```

---

## 📅 Tags

Tags let you control ingredient filtering, shelf placement, and cauldron heat sources.

### Filter Ingredients

* Blacklist an item from ingredient gen: `#elixirum:essence_blacklist`
* Whitelist: `#elixirum:essence_whitelist` *(ignored if also blacklisted)*

> Blacklist **always** wins.

---

### Potion Shelf Placement

To make an item placeable on potion shelves, tag it with:

```
#elixirum:potion_shelf_placeable
```

---

### Add Heat Sources

Make a block a heat source for cauldrons by tagging it:

```
#elixirum:heat_sources
```

Default values:

```json
{
  "values": [
    { "id": "#minecraft:fire", "required": false },
    { "id": "#minecraft:campfires", "required": false },
    "minecraft:magma_block"
  ]
}
```

---

## 🔄 Datapack Override Order

This is how the mod resolves overrides:

```
Essence Whitelist > Ingredient Preset > Essence Blacklist > Ingredient Generation
```

---

*Written by DVOA1 | 2025*
