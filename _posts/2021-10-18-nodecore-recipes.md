---
title: Nodecore Recipes
description: Recipe book for the Minetest game Nodecore
tags: nodecore
---

<style>
    article tr.border-on-top {
        border-top: 1px solid grey;
    }

    article td {
        padding: 0.5em 0;
        vertical-align: top;
    }

    article table ul {
        margin: 0;
        margin-left: 1rem;
    }

    @media only screen and (min-width: 800px) {
        article ul {
            width: max-content;
        }
    }
</style>

The last time I checked, [the official wiki](https://nodecore.mine.nu/wiki/index.php/Main_Page) was very broken, so my brother and I brute-forced our way through the game, and wrote this recipe book while we were at it. This page is incomplete.

Recipes tested on [NodeCore](https://content.minetest.net/packages/warr1024/nodecore) release 5310 (game.conf) with a few mods:

-   [nc_light](https://content.minetest.net/packages/Winter94/nc_light)
-   [nc_stucco](https://content.minetest.net/packages/Avicennia_g/nc_stucco)
-   [nc_ziprunes](https://content.minetest.net/packages/Warr1024/nc_ziprunes)

<table style="border-collapse:collapse"><tbody><tr><th>Required by</th><th>Name</th><th>Requires</th><th>Instructions</th></tr><tr id="adobe" class="border-on-top"><td rowspan="1"><ul></ul></td><td rowspan="1">Adobe</td><td><ul><li>1
<span style="color:red">Ash</span></li><li>1
<a href="#loosedirt">Loose Dirt</a></li><li>1
<a href="#woodenmallet">Wooden Mallet</a></li></ul></td><td>Place a loose dirt on an ash. Pummel with a mallet</td></tr><tr id="aggregate" class="border-on-top"><td rowspan="1"><ul></ul></td><td rowspan="1">Aggregate</td><td><ul><li>1
<span style="color:red">Ash</span></li><li>1
<span style="color:red">Loose Gravel</span></li><li>1
<a href="#woodenmallet">Wooden Mallet</a></li></ul></td><td>Place a loose gravel on an ash. Pummel with a mallet</td></tr><tr id="charcoal" class="border-on-top"><td rowspan="1"><ul><li><a href="#charcoallump">Charcoal Lump</a></li></ul></td><td rowspan="1">Charcoal</td><td><ul><li>1
<a href="#fire">Fire</a></li></ul></td><td>Create a fire. Put out the fire by surrounding it with non-combustible material</td></tr><tr id="charcoalblock" class="border-on-top"><td rowspan="1"><ul><li><a href="#charcoallump">Charcoal Lump</a></li></ul></td><td rowspan="1">Charcoal Block</td><td><ul><li>8
<a href="#charcoallump">Charcoal Lump</a></li><li>1
<a href="#woodenmallet">Wooden Mallet</a></li></ul></td><td>Drop 8 charcoal lump. Pummel them with a mallet</td></tr><tr id="charcoallump" class="border-on-top"><td rowspan="2"><ul><li><a href="#charcoalblock">Charcoal Block</a></li><li><a href="#torch">Torch</a></li></ul></td><td rowspan="2">Charcoal Lump</td><td><ul><li>1
<a href="#charcoalblock">Charcoal Block</a></li><li>1
<a href="#woodenhatchet">Wooden Hatchet</a></li></ul></td><td>Pummel a charcoal block with a hatchet [makes 8]</td></tr><tr><td><ul><li>1
<a href="#charcoal">Charcoal</a></li><li>1
<a href="#woodenhatchet">Wooden Hatchet</a></li></ul></td><td>Pummel a charcoal with a hatchet</td></tr><tr id="chromaticglass" class="border-on-top"><td rowspan="1"><ul></ul></td><td rowspan="1">Chromatic Glass</td><td><ul><li>1
<a href="#moltenglass">Molten Glass</a></li><li>1
<a href="#water">Water</a></li></ul></td><td>Cool a still (not flowing) molten glass with water</td></tr><tr id="cleanglass" class="border-on-top"><td rowspan="1"><ul></ul></td><td rowspan="1">Clean Glass</td><td><ul><li>1
<a href="#moltenglass">Molten Glass</a></li></ul></td><td>Let a molten glass cool while still (not flowing)</td></tr><tr id="crudeglass" class="border-on-top"><td rowspan="1"><ul></ul></td><td rowspan="1">Crude Glass</td><td><ul><li>1
<a href="#moltenglass">Molten Glass</a></li></ul></td><td>Let a molten glass cool while flowing</td></tr><tr id="dirt" class="border-on-top"><td rowspan="2"><ul><li><a href="#loosedirt">Loose Dirt</a></li></ul></td><td rowspan="2">Dirt</td><td><ul></ul></td><td>A naturally occurring resource. Discover as part of the grassy ground</td></tr><tr><td><ul><li>1
<a href="#loosedirt">Loose Dirt</a></li><li>1
<a href="#woodenmallet">Wooden Mallet</a></li></ul></td><td>Pummel a loose dirt with a mallet</td></tr><tr id="eggcorn" class="border-on-top"><td rowspan="1"><ul><li><a href="#plantedeggcorn">Planted Eggcorn</a></li></ul></td><td rowspan="1">Eggcorn</td><td><ul><li>1
<a href="#leaves">Leaves</a></li></ul></td><td>Mine a leaves with your hand. There is a chance of it turning into an eggcorn. The closer to the tree trunk the higher the chance</td></tr><tr id="fire" class="border-on-top"><td rowspan="1"><ul><li><a href="#charcoal">Charcoal</a></li><li><a href="#moltenglass">Molten Glass</a></li></ul></td><td rowspan="1">Fire</td><td><ul><li>1
<a href="#littorch">Lit Torch</a></li><li>1
<span style="color:red">group:Burnable</span></li></ul></td><td>Place a lit torch beside a group:burnable</td></tr><tr id="leaves" class="border-on-top"><td rowspan="1"><ul><li><a href="#eggcorn">Eggcorn</a></li><li><a href="#looseleaves">Loose Leaves</a></li><li><a href="#stick">Stick</a></li></ul></td><td rowspan="1">Leaves</td><td><ul><li>1
<a href="#tree">Tree</a></li></ul></td><td>A natural resource. Discover as part of a tree</td></tr><tr id="littorch" class="border-on-top"><td rowspan="1"><ul><li><a href="#fire">Fire</a></li></ul></td><td rowspan="1">Lit Torch</td><td><ul><li>1
<a href="#staff">Staff</a></li><li>1
<a href="#torch">Torch</a></li></ul></td><td>Pummel a torch with a staff</td></tr><tr id="log" class="border-on-top"><td rowspan="2"><ul><li><a href="#woodenplank">Wooden Plank</a></li></ul></td><td rowspan="2">Log</td><td><ul><li>1
<a href="#treetrunk">Tree Trunk</a></li><li>1
<a href="#woodenhatchet">Wooden Hatchet</a></li></ul></td><td>Mine a tree trunk with a hatchet</td></tr><tr><td><ul><li>1
<a href="#treetrunk">Tree Trunk</a></li></ul></td><td>Mine a tree trunk with your hand. This takes a very long time</td></tr><tr id="loosedirt" class="border-on-top"><td rowspan="2"><ul><li><a href="#adobe">Adobe</a></li><li><a href="#dirt">Dirt</a></li><li><a href="#plantedeggcorn">Planted Eggcorn</a></li></ul></td><td rowspan="2">Loose Dirt</td><td><ul><li>1
<a href="#dirt">Dirt</a></li><li>1
<a href="#woodenspade">Wooden Spade</a></li></ul></td><td>Mine a dirt with a spade</td></tr><tr><td><ul><li>1
<a href="#dirt">Dirt</a></li></ul></td><td>Mine a dirt with your hand</td></tr><tr id="looseleaves" class="border-on-top"><td rowspan="1"><ul><li><a href="#peat">Peat</a></li></ul></td><td rowspan="1">Loose Leaves</td><td><ul><li>1
<a href="#leaves">Leaves</a></li></ul></td><td>Mine a leaves with your hand. Leaves may turn into a stick or an eggcorn when mined</td></tr><tr id="loosesand" class="border-on-top"><td rowspan="2"><ul><li><a href="#moltenglass">Molten Glass</a></li><li><a href="#render">Render</a></li></ul></td><td rowspan="2">Loose Sand</td><td><ul><li>1
<a href="#sand">Sand</a></li><li>1
<a href="#woodenspade">Wooden Spade</a></li></ul></td><td>Mine a sand with a spade</td></tr><tr><td><ul><li>1
<a href="#sand">Sand</a></li></ul></td><td>Mine a sand with your hand</td></tr><tr id="moltenglass" class="border-on-top"><td rowspan="1"><ul><li><a href="#chromaticglass">Chromatic Glass</a></li><li><a href="#cleanglass">Clean Glass</a></li><li><a href="#crudeglass">Crude Glass</a></li></ul></td><td rowspan="1">Molten Glass</td><td><ul><li>2
<a href="#fire">Fire</a></li><li>1
<a href="#loosesand">Loose Sand</a></li></ul></td><td>Place a loose sand and 2 fire at 2 corners of the sand. Wait</td></tr><tr id="peat" class="border-on-top"><td rowspan="1"><ul></ul></td><td rowspan="1">Peat</td><td><ul><li>8
<a href="#looseleaves">Loose Leaves</a></li><li>1
<a href="#woodenadze">Wooden Adze</a></li></ul></td><td>Drop 8 loose leaves. Pummel them with an adze</td></tr><tr id="plantedeggcorn" class="border-on-top"><td rowspan="1"><ul><li><a href="#tree">Tree</a></li></ul></td><td rowspan="1">Planted Eggcorn</td><td><ul><li>1
<a href="#eggcorn">Eggcorn</a></li><li>1
<a href="#loosedirt">Loose Dirt</a></li></ul></td><td>Place an eggcorn 1 block down in the ground. Place a loose dirt on the eggcorn</td></tr><tr id="render" class="border-on-top"><td rowspan="1"><ul></ul></td><td rowspan="1">Render</td><td><ul><li>1
<span style="color:red">Ash</span></li><li>1
<a href="#loosesand">Loose Sand</a></li><li>1
<a href="#woodenmallet">Wooden Mallet</a></li></ul></td><td>Place a loose sand on an ash. Pummel with a mallet</td></tr><tr id="sand" class="border-on-top"><td rowspan="1"><ul><li><a href="#loosesand">Loose Sand</a></li></ul></td><td rowspan="1">Sand</td><td><ul></ul></td><td>A naturally occurring resource. Discover as part of the ground near a river or sea</td></tr><tr id="staff" class="border-on-top"><td rowspan="1"><ul><li><a href="#littorch">Lit Torch</a></li><li><a href="#torch">Torch</a></li><li><a href="#woodenadze">Wooden Adze</a></li><li><a href="#woodenframe">Wooden Frame</a></li><li><a href="#woodenhatchet">Wooden Hatchet</a></li><li><a href="#woodenmallet">Wooden Mallet</a></li><li><a href="#woodenspade">Wooden Spade</a></li></ul></td><td rowspan="1">Staff</td><td><ul><li>2
<a href="#stick">Stick</a></li></ul></td><td>Place a stick on the top of a stick</td></tr><tr id="stick" class="border-on-top"><td rowspan="2"><ul><li><a href="#staff">Staff</a></li><li><a href="#woodenadze">Wooden Adze</a></li></ul></td><td rowspan="2">Stick</td><td><ul><li>1
<a href="#leaves">Leaves</a></li></ul></td><td>Mine a leaves with your hand. There is a chance of it turning into a stick. The closer to the tree trunk the higher the chance</td></tr><tr><td><ul><li>1
<span style="color:red">Stone-Tipped Mallet</span></li><li>1
<a href="#woodenplank">Wooden Plank</a></li></ul></td><td>Pummel the top of a wooden plank with a stone-tipped mallet or better [makes 8]</td></tr><tr id="torch" class="border-on-top"><td rowspan="1"><ul><li><a href="#littorch">Lit Torch</a></li></ul></td><td rowspan="1">Torch</td><td><ul><li>1
<a href="#charcoallump">Charcoal Lump</a></li><li>1
<a href="#staff">Staff</a></li></ul></td><td>Place a charcoal lump on the top of a staff</td></tr><tr id="tree" class="border-on-top"><td rowspan="1"><ul><li><a href="#leaves">Leaves</a></li><li><a href="#treetrunk">Tree Trunk</a></li></ul></td><td rowspan="1">Tree</td><td><ul><li>1
<a href="#plantedeggcorn">Planted Eggcorn</a></li></ul></td><td>A natural structure. Grows from a planted eggcorn</td></tr><tr id="treetrunk" class="border-on-top"><td rowspan="1"><ul><li><a href="#log">Log</a></li></ul></td><td rowspan="1">Tree Trunk</td><td><ul><li>1
<a href="#tree">Tree</a></li></ul></td><td>A natural resource. Discover as part of a tree</td></tr><tr id="water" class="border-on-top"><td rowspan="1"><ul><li><a href="#chromaticglass">Chromatic Glass</a></li></ul></td><td rowspan="1">Water</td><td><ul></ul></td><td>A natural resource. Discover as part of a river or sea</td></tr><tr id="woodenadze" class="border-on-top"><td rowspan="1"><ul><li><a href="#peat">Peat</a></li><li><a href="#woodenhatchethead">Wooden Hatchet Head</a></li><li><a href="#woodenmallethead">Wooden Mallet Head</a></li><li><a href="#woodenplank">Wooden Plank</a></li><li><a href="#woodenspadehead">Wooden Spade Head</a></li></ul></td><td rowspan="1">Wooden Adze</td><td><ul><li>1
<a href="#staff">Staff</a></li><li>1
<a href="#stick">Stick</a></li></ul></td><td>Place a stick on the top of a staff</td></tr><tr id="woodenframe" class="border-on-top"><td rowspan="1"><ul><li><a href="#woodenshelf">Wooden Shelf</a></li></ul></td><td rowspan="1">Wooden Frame</td><td><ul><li>2
<a href="#staff">Staff</a></li></ul></td><td>Place a staff on the side of a staff</td></tr><tr id="woodenhatchet" class="border-on-top"><td rowspan="1"><ul><li><a href="#charcoallump">Charcoal Lump</a></li><li><a href="#log">Log</a></li><li><a href="#woodenhatchethead">Wooden Hatchet Head</a></li><li><a href="#woodenmallethead">Wooden Mallet Head</a></li><li><a href="#woodenplank">Wooden Plank</a></li><li><a href="#woodenspadehead">Wooden Spade Head</a></li></ul></td><td rowspan="1">Wooden Hatchet</td><td><ul><li>1
<a href="#staff">Staff</a></li><li>1
<a href="#woodenhatchethead">Wooden Hatchet Head</a></li></ul></td><td>Place a wooden hatchet head on a staff</td></tr><tr id="woodenhatchethead" class="border-on-top"><td rowspan="2"><ul><li><a href="#woodenhatchet">Wooden Hatchet</a></li></ul></td><td rowspan="2">Wooden Hatchet Head</td><td><ul><li>1
<a href="#woodenhatchet">Wooden Hatchet</a></li><li>1
<a href="#woodenspadehead">Wooden Spade Head</a></li></ul></td><td>Pummel a wooden spade head with a hatchet</td></tr><tr><td><ul><li>1
<a href="#woodenadze">Wooden Adze</a></li><li>1
<a href="#woodenspadehead">Wooden Spade Head</a></li></ul></td><td>Pummel a wooden spade head with an adze</td></tr><tr id="woodenmallet" class="border-on-top"><td rowspan="1"><ul><li><a href="#adobe">Adobe</a></li><li><a href="#aggregate">Aggregate</a></li><li><a href="#charcoalblock">Charcoal Block</a></li><li><a href="#dirt">Dirt</a></li><li><a href="#render">Render</a></li></ul></td><td rowspan="1">Wooden Mallet</td><td><ul><li>1
<a href="#staff">Staff</a></li><li>1
<a href="#woodenmallethead">Wooden Mallet Head</a></li></ul></td><td>Place a wooden mallet head on a staff</td></tr><tr id="woodenmallethead" class="border-on-top"><td rowspan="2"><ul><li><a href="#woodenmallet">Wooden Mallet</a></li><li><a href="#woodenspadehead">Wooden Spade Head</a></li></ul></td><td rowspan="2">Wooden Mallet Head</td><td><ul><li>1
<a href="#woodenhatchet">Wooden Hatchet</a></li><li>1
<a href="#woodenplank">Wooden Plank</a></li></ul></td><td>Pummel a wooden plank with a hatchet</td></tr><tr><td><ul><li>1
<a href="#woodenadze">Wooden Adze</a></li><li>1
<a href="#woodenplank">Wooden Plank</a></li></ul></td><td>Pummel a wooden plank with an adze</td></tr><tr id="woodenplank" class="border-on-top"><td rowspan="2"><ul><li><a href="#stick">Stick</a></li><li><a href="#woodenmallethead">Wooden Mallet Head</a></li><li><a href="#woodenshelf">Wooden Shelf</a></li></ul></td><td rowspan="2">Wooden Plank</td><td><ul><li>1
<a href="#log">Log</a></li><li>1
<a href="#woodenhatchet">Wooden Hatchet</a></li></ul></td><td>Pummel a log with a hatchet</td></tr><tr><td><ul><li>1
<a href="#log">Log</a></li><li>1
<a href="#woodenadze">Wooden Adze</a></li></ul></td><td>Pummel a log with an adze</td></tr><tr id="woodenshelf" class="border-on-top"><td rowspan="1"><ul></ul></td><td rowspan="1">Wooden Shelf</td><td><ul><li>4
<a href="#woodenframe">Wooden Frame</a></li><li>1
<a href="#woodenplank">Wooden Plank</a></li></ul></td><td>Place 4 wooden frames in a diamond arrangement, then place a wooden plank in the centre [makes 4]</td></tr><tr id="woodenspade" class="border-on-top"><td rowspan="1"><ul><li><a href="#loosedirt">Loose Dirt</a></li><li><a href="#loosesand">Loose Sand</a></li></ul></td><td rowspan="1">Wooden Spade</td><td><ul><li>1
<a href="#staff">Staff</a></li><li>1
<a href="#woodenspadehead">Wooden Spade Head</a></li></ul></td><td>Place a wooden spade head on a staff</td></tr><tr id="woodenspadehead" class="border-on-top"><td rowspan="2"><ul><li><a href="#woodenhatchethead">Wooden Hatchet Head</a></li><li><a href="#woodenspade">Wooden Spade</a></li></ul></td><td rowspan="2">Wooden Spade Head</td><td><ul><li>1
<a href="#woodenhatchet">Wooden Hatchet</a></li><li>1
<a href="#woodenmallethead">Wooden Mallet Head</a></li></ul></td><td>Pummel a wooden mallet head with a hatchet</td></tr><tr><td><ul><li>1
<a href="#woodenadze">Wooden Adze</a></li><li>1
<a href="#woodenmallethead">Wooden Mallet Head</a></li></ul></td><td>Pummel a wooden mallet head with an adze</td></tr></tbody></table>
