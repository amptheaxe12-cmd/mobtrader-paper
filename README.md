# Mob Trader

Right-click almost any mob in Minecraft and the normal trading screen opens. Each
mob pays out in its own loot, and takes payment in whatever it eats or drops.
Sheep want wheat and hand over wool. Endermen want ender pearls and hand over
blocks they'd have stolen anyway.

Paper, Minecraft 26.2. Works in single player and on servers.

## How it works

- Every mob has a pool of possible trades. Three get picked at random.
- Amounts roll inside a range, so prices differ from one animal to the next.
- The roll is seeded from the mob's UUID: one particular cow always offers the
  same deal, but the cow beside it offers something else.
- Villagers and wandering traders are left alone with their vanilla trading.

## Enchanted gear

Combat and tool mobs sell one piece of gear, enchanted the way an enchanting
table would at the listed level. Higher level, better odds. Always one use only,
and always expensive.

| Mob | Pays with | Gear | Table level |
| --- | --- | --- | --- |
| Zombie | Rotten flesh | Iron sword, iron shovel | 10–30 |
| Husk | Rotten flesh | Iron hoe | 10–30 |
| Drowned | Rotten flesh | Fishing rod | 12–30 |
| Skeleton | Bones | Bow | 10–30 |
| Stray | Bones | Bow | 15–30 |
| Wither skeleton | Bones | Stone sword | 20–30 |
| Blaze | Blaze rods | Golden sword | 20–30 |
| Piglin | Gold ingots | Golden axe | 15–30 |
| Zombified piglin | Gold ingots | Golden sword | 15–30 |
| Pillager | Emeralds | Crossbow | 15–30 |
| Vindicator | Emeralds | Iron axe | 20–30 |
| Iron golem | Iron ingots | Iron pickaxe | 15–30 |
| Guardian | Prismarine shards | Fishing rod | 20–30 |
| Elder guardian | Prismarine crystals | Trident | 20–30 |
| Enderman | Ender pearls | Diamond pickaxe | 20–30 |
| Phantom | Phantom membrane | Elytra | 15–30 |
| Witch | Glass bottles | Enchanted book | 25–30 |
| Sheep | Wheat | Shears | 5–20 |
| Warden | Echo shards | Netherite sword | 30 |

Because the roll is tied to the mob, the sword a given zombie is holding out is
always that same sword. Walk away and come back, it hasn't changed.

## Ordinary trades

Roughly forty mobs have their own tables. A sample:

| Mob | Pays with | Gets you |
| --- | --- | --- |
| Cow | Wheat | Leather, beef, milk |
| Sheep | Wheat | Wool, mutton, black wool |
| Chicken | Seeds | Eggs, feathers, raw chicken |
| Pig | Carrots, potatoes, beetroot | Porkchops, a saddle |
| Bee | Poppies, dandelions | Honeycomb, honey bottles, honey block |
| Wolf | Bones, beef | Leather, string, bone meal |
| Fox | Sweet berries | Glow berries, emeralds |
| Panda | Bamboo | Slime balls, cake |
| Turtle | Seagrass | Kelp, sand, scute |
| Strider | Warped fungus | String, blaze rods, lava |
| Creeper | Gunpowder | Fireworks, TNT, flint and steel |
| Spider | String | Spider eyes, cobwebs |
| Slime | Slime balls | Sticky pistons, leads |
| Ghast | Ghast tears | Fire charges, gunpowder, soul sand |
| Piglin | Gold ingots | The real barter table |
| Shulker | Ender pearls | Shulker shells, purpur, chorus fruit |
| Evoker | Emeralds | Totem of undying, enchanted golden apple |
| Warden | Echo shards | Sculk, sculk catalyst, diamonds |

Anything without its own table falls back to a generic emerald list.

## Install

1. Fabric Loader 0.19.5 or newer for Minecraft 26.2
2. Fabric API 0.161.0+26.2
3. Drop the mod jar in your `mods` folder

## Config

Written to `config/mobtrader.json` the first time the mod loads.

```json
"minecraft:zombie": [
  { "buy": "minecraft:rotten_flesh", "buyCount": 20, "buyCountMax": 48,
    "sell": "minecraft:iron_sword", "sellCount": 1, "maxUses": 1,
    "enchantLevels": 10, "enchantLevelsMax": 30 }
]
```

| Field | What it does |
| --- | --- |
| `buy` / `buyCount` / `buyCountMax` | What you hand over, and the range |
| `buyB` / `buyBCount` / `buyBCountMax` | Optional second cost item |
| `sell` / `sellCount` / `sellCountMax` | What you get, and the range |
| `maxUses` | How many times before the trade locks |
| `enchantLevels` / `enchantLevelsMax` | Enchanting-table level to roll at; leave out for a plain item |

Top-level settings:

| Setting | Default | What it does |
| --- | --- | --- |
| `tradesPerMob` | 3 | How many trades to pick from each pool. 0 shows the whole pool |
| `sameTradesPerMob` | true | Lock each mob's trades. Set false to reroll on every right-click |
| `requireSneak` | false | Require sneak + right-click, so you don't open trades while shearing or feeding |

Any entity id works, modded ones included. Restart the game after editing.
Delete the file to regenerate the defaults.

## Building from source

Needs JDK 25 and Gradle 9.5.1 or newer. The repo also builds on GitHub Actions;
the jar comes out as a downloadable artifact on every push.

```
gradle build
```

<img width="818" height="482" alt="Screenshot 2026-10-31 215244" src="https://github.com/user-attachments/assets/a80dccfd-c5d9-45d5-a02b-e535a8b327e5" />
<img width="816" height="478" alt="Screenshot 2026-10-31 215637" src="https://github.com/user-attachments/assets/19e22143-7cc6-4e0b-92f0-067d6e598854" />
<img width="813" height="481" alt="Screenshot 2026-10-31 215523" src="https://github.com/user-attachments/assets/2cc9401a-8534-4ade-9828-64873ddb7155" />

You name it you can trade with it 

## Notes

- Hostile mobs keep attacking while the trade screen is open.
- A mob's own right-click action is pre-empted when it has a trade table.
  Turn on `requireSneak` to get shearing, feeding and horse riding back.
- Stock resets when you close the screen.
- This is a plugin not a mod
