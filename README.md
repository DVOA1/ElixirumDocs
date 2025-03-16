# Ars Elixirum Documentation

---

<a id="legal-notice"></a>

## Legal Notice

This documentation is provided for **informational purposes only** and is not affiliated with or endorsed by the creators of Ars Elixirum. Ars Elixirum is the intellectual property of **Obscuria Team**, and all rights to the mod and its contents are reserved by them.

The guide provided here explains how to create a datapack that interacts with Ars Elixirum, but the mod itself is not my work. All **trademarks, logos, and copyrighted content** related to Ars Elixirum **belong to their respective owners.**

This documentation is intended for **personal, non-commercial use** and is meant to help users create custom content for the Ars Elixirum mod in compliance with the mod's terms and conditions.

---

## Key Concepts

> NOTE: These key points are not the only things this guide provides. These are only the most important concepts to make more relevant things in the datapack.

- [Adding Custom Essences](#add-essence)
- [Tags](#tags)

## Folders Structure

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

<a id="elixirum"></a>

## Elixirum Folder

Inside the `elixirum` folder, create another `elixirum` folder, which will contain everything we will make.

### Configured Elixir Folder

Contains an effect (referencing a pre-made essence) that can have multiple variants. You can only modify *amplifier* and *duration*.

The file name must be the essence name.

**Template (taken from the mod code):**

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

### Elixir Prefix Folder

Applies a random prefix to the essence (e.g., "Devastating elixir of strength"). It takes a lang key from the lang file and applies it as a prefix.

**Template (taken from the mod code):**

```json
{
  "key": "effect_prefix.elixirum.absorption_assimilating",
  "source": "minecraft:absorption"
}
```

---

<a id="add-essence"></a>

### Essence Folder

The most important folder. Here you will add your effects with the following parameters:

- **category**: can be "NONE", "OFFENSIVE", "DEFENSIVE", "ENHANCING", "DIMINISHING". This determines how the essence behaves with affixes.
- **max_amplifier**: sets the maximum amplifier (starting from 0) the essence can have. The essence can have any amplifier below this number.
- **max_duration**: sets the maximum duration the essence can have. The essence can have any duration below this number.
- **mob_effect**: the ID of the effect you want to generate (e.g., "farmersdelight:comfort").
- **required_ingredients**: minimum amount of ingredient to make this essence non-pale.
- **required_quality**: minimum amount of quality to make this essence non-weak.

The file name must be the effect name (without namespace).

**Template (generated by my code):**

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

Contains every ingredient with a set effect and weight.
> **Note**: Almost every item in the game will have a randomly generated effect based on the seed.

**Parameters:**

- **essences**: contains every essence that the set item will have
  - **ESSENCE_ID** (using "elixirum:" as namespace): weight
- **target**: contains the item ID

The file name must be the item name.

**Template (taken from the mod code):**

```json
{
  "essences": {
    "elixirum:saturation": 20
  },
  "target": "minecraft:blue_orchid"
}
```

---

<a id="tags"></a>

## Tags

With tags you can filter ingredients, make items placeable on shelves and make heat sources compatible with cauldrons.

Here's how:

---

### Filter Ingredients

To add an item to the ingredient gen blacklist, you add the tag `#elixirum:essence_blacklist`. This will **ALWAYS** override the whitelist

You can also add item to a whitelist by adding the tag `#elixirum:essence_whitelist`. Does nothing if the item is in the blacklist.

---

### Making Items Placeable On Shelves

You can make item placeable on shelves by adding the tag `#elixirum:potion_shelf_placeable`

---

### Adding New Heat Sources

You can make an heat source compatible with Ars Elixirum's cauldrons by adding the tag `#elixirum:heat_sources`

By default the compatible heat sources are the following:

> heat_sources.json

```json
{
  "values": [
    {
      "id": "#minecraft:fire",
      "required": false
    },
    {
      "id": "#minecraft:campfires",
      "required": false
    },
    "minecraft:magma_block"
  ]
}
```

---

<<<<<<< HEAD
=======
## Legal Notice

This documentation is provided for informational purposes only and is not affiliated with or endorsed by the creators of Ars Elixirum. Ars Elixirum is the intellectual property of Obscuria Team, and all rights to the mod and its contents are reserved by them.

The guide provided here explains how to create a datapack that interacts with Ars Elixirum, but the mod itself is not my work. All trademarks, logos, and copyrighted content related to Ars Elixirum belong to their respective owners.

This documentation is intended for personal, non-commercial use and is meant to help users create custom content for the Ars Elixirum mod in compliance with the mod's terms and conditions.

---

>>>>>>> 5211c36 (add logo)
##### Documentation written by DVOA1 | 2025
