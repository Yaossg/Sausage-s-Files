# ManaCraft

> This tutorial is for version 1.0

> Mana is the power of nature!

## General

`ManaCraft` is a mod developed by Yaossg, Thanks to fly25 for providing some of texture. the English version tutorial is proofread by switefaster.

JEI is well supported by this mod, which is highly recommended to be installed, for you can look up most recipes, some blocks' and items' instructions, which is never metioned by this tutorial.

In 1.1, the mod supported tinkers' construct

For api, you can download [HERE](./api)

## World Generations

### Ore Generations

arguments about ore generations can be found or edited in the config, so never metioned here

![](./ores.png)

the left one is mana ore and mana (block)
the right one is orichalcum ore and orichalcum ingot (block)

![](./ores-overview.png)

ore generations of vanilla (minecraft) with only mana_craft

there's only 3 types of veins in the mod

![](./ores-mana.png)

the mana vein

![](./ores-orichalcum.png)

the orichalcum vein

![](./ores-mixture.png)

the mixture vein, which is mixed by mana ore and orichalcum ore

#### Others

you can also get mana by harvesting grasses in a low chance

orichalcum can be made of gold and mana, see  JEI for more information

### The Village

![](./mana-priest.png)

the mana priest, 

who has following 4 careers:

- Mana Magician

|level|buy|sell|
|:-:|:-:|:-:|
|1|mana |mana glass, mana apple|
|2|mana prok|machine frame|

- Mana Tool Magician

|level|buy|sell|
|:-:|:-:|:-:|
|1|mana |mana shears, enchanted mana shovel|
|2|orichalcum ingot|enchanted mana hoe|
|3|mana diamond|enchanted mana pickaxe|

- Mana Weapon Magician

|level|buy|sell|
|:-:|:-:|:-:|
|1|mana |mana shears, mana ball|
|2|orichalcum ingot|enchanted mana wand|
|3|mana diamond|enchanted mana sword|

- Mana Armorer

|level|buy|sell|
|:-:|:-:|:-:|
|1|mana |mana shears, enchanted mana boots|
|2|orichalcum ingot|enchanted mana helmet, enchanted mana leggings|
|3|mana diamond|enchanted mana chestplate|

- Mana Summoner

|level|buy|sell|
|:-:|:-:|:-:|
|1|mana |mana dust|
|2|orichalcum ingot|mana foot, mana body|
|3|mana diamond|mana head|

![](./v-l.png)

the mana lantern

![](./v-p.png)

the mana producer in a village, 2 mana priest are spawned in this structure

![](./mv-p.png)

the mana producer in a village in mana biome

### Biomes

there's 4 biomes added, there the ores of this mod is multipled

common mana terrian, including plains and hills, double ores of this mod, special village can be found here

![](./b-mana.png)

the plain mana 

![](./mana-village.png)

the mana vilage

chaos mana terrian,including plains and hills, three times ores of this mod

![](./b-mana-chaos.png)

the chaos mana 

## Multi-Block Structure

### mana producer

the most important machine in this mod

![](./materials.png)

the materials, building steps are:

![](./p-1.png)
![](./p-2.png)
![](./p-3.png)
![](./p-4.png)
![](./p-5.png)
![](./p-6.png)

especially, mana producer's core is put in finally

you can also generate a mana producer by the generator

### mana shooter

![](./shooter.png)

especially, mana head should be set finally

you can also spawn this entity by the egg

mana shooter can attack monsters by mana balls, or self-explode while dying

## Mana Ball

mana ball can be thrown by hand, but flies slowly

dispenser can launch mana ball as well, and files a little faster

certainly, the most important way is by mana wand, which launches fastest

After shooting, unless meeting block, it can fly forever even through entities

especially, mana ball is an important crafting material

## Enchantment

### floating

mana wand's enchantment cause mana ball without no gravity but slower

especially, floating ball get slower as time goes by, and it disappers when slow enough

### mana evoker

mana armor shoot balls while getting hurt

higher level it has, more mana balls appear

### mana recycler

even if without enchantment, all mana weapon, tool, armor drops mana when its durability consumed

and after enchanting this, mana it drops get more

higher level it has, more mana it drops

## Potions

### mana evoker

he who has this effect will be surrounded by balls that appear around

higher level it has, more mana balls appear

## Machines

about machines' recipes' and fuels' registries, see [API](#api)

### mana producer

introduced above, for recipes, please see JEI

special note: though mana producer support I/O, as producer is put inside the frame, which makes it unable to connect to transfer pipes, so please keep looking forward to my another mod called Sausage's Factory, which provide a I/O device that can transfer remotely even if you cannot touch the machine itself

### mana booster

speed up for mana producer, or other machine, support vanilla furnace and brewing stand, see [API](#api) to learn how to register

for mana producers, you need to put in a radius that depends on config to speed up

for others, you need to put it aside to speed up

## Loot Tables

some loots have been added by this mod, see [here](https://github.com/Yaossg/ManaCraft/tree/master/src/main/resources/assets/mana_craft/loot_tables/inject)

## Config and Customize Recipes/Fuels

in the config folder, you can see 2 ManaCraft config file(ManaCraft.cfg and ManaCraft OreGens.cfg) and a config folder(mana_craft_machines)

the first one define general settings in ManaCraft

the second one define settings about ore generations.

the folder includes customize mana producer recipes and mana booster fuels, for a standard format, see [HERE](https://github.com/Yaossg/ManaCraft/tree/master/src/main/resources/assets/mana_craft/machines) for detail

## API

ManaCraft's API, allows you:

- custom mana tool
- register mana producer recipe
- register mana booster fuel
- register mana booster's boostable machines

most API has javadoc, so no more info here



