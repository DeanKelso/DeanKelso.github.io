Title: Timberfall
Type: Game dev / Gameplay systems + 3D art
For: Personal (2-person team)
Tools: Unreal Engine 5 (Blueprints, Chaos, Niagara, PCG), Blender (Geometry Nodes), Substance Painter, Photoshop
Year: 2025
Role: Everything the player touched or could see: the tree-cutting system, axes, movement, 3D art and the world. My dev partner handled a lot of the backend.
Time: About 6 months (June to December 2025)
Next time: Lock the scope and set a performance budget before building the world.
Section: work
Play: no
Cover: HighresScreenshot00001.png
OK to show: yes

Description:
Timberfall was a first-person lumberjack game in Unreal Engine 5, made with a friend. The fantasy was simple: be a lumberjack, cut down bigger and stranger trees, get cooler axes, and explore a world that keeps pulling you further in. In the middle of the map stood the Elder Tree, a tree so big its roots blocked off whole parts of the world. Cutting it down was the long-term goal.

My partner did a lot of the backend. I built everything the player touched or could see: the tree-cutting system, the axes, the movement, the 3D art and the world.

- **Short loop:** cut a tree, sell the logs, level up
- **Medium loop:** buy new axes, unlock new trees and new areas
- **Long loop:** cut down the Elder Tree

## Chop down the biggest tree first
One of my notes from the project says to start with the biggest problem, not a pile of small ones. In a game about cutting trees, the biggest tree was literally the tree. So before towns, quests or anything else, I built one tree that felt great to cut down, then made it work for every tree in the game.

## Building a tree
Every tree starts with reference. I look at how the leaves are built, how the branches spread, and what the trunk is doing: thick or slim, tall, wavy or straight. Then I decide how many variations I need so the forest doesn't look copy-pasted.

In Blender I either use my own version of a free Geometry Nodes tree generator, or hand-model the trunk and branches with the Skin modifier plus subdivision. Each part gets a low-poly version (around 200 verts, cut down by removing loops and triangulating where it makes sense) and a high-poly version I sculpt for the normal map.

Then I build full trees out of linked copies of those parts, stretched and rotated for variety. Because they're linked, changing one branch updates every tree, so I could see my changes in real time.

- **Leaves are cards, not geometry.** Nanite at the time wasn't the right call for a game full of forests that had to run well on low-to-mid PCs.
- **Normals from a sphere.** A Data Transfer modifier copies a sphere's normals onto the leaves, so the canopy shades softly like one shape instead of hundreds of flat cards.
- **Two materials per tree** in Unreal: one for bark, one for leaves.

## Cutting it up
A finished tree isn't done yet. It gets split into the parts the cutting system needs:

- **Stump:** what stays in the ground
- **Pill cover, pill top, pill bottom:** the section the axe actually chops through
- **Cut trunk:** split up and down and across, so when the tree hits the ground it breaks open like a peanut and shows the logs inside
- **Logs:** cut to follow the shape of the trunk (once you pick one up it becomes a standard log; remembering every shape wasn't worth the dev time)

## Breaking it
In Unreal, the pill parts become Chaos geometry collections. I fractured them until the chips looked and felt right when the axe bit in: radial cuts around the trunk, a grid inside the pill, and anchors at the bottom so the stump stays put. Then I tuned the physics on the falling tree (mass, center of mass, damping, max spin speed) so it tips over with weight instead of flying off.

## How the code fits together
The code works like a chain: one event calls the next, and each step checks a condition before it keeps going. Every tree is a child of one Master Tree blueprint, so a new tree only sets its own meshes, health, the axe level it needs, hitboxes, grapple spots and where its logs spawn.

**1. One swing:** attack input → pick the next swing animation → an animation notify starts the axe trace → the trace hits a tree and calls Chop → camera shake, hit-stop, a tiny slow-mo and hit effects → the axe pulls back out.

**2. The tree takes the hit:** Chop → is the axe a high enough level? → was it a big-damage hit? → take away health and reset the despawn timer → health hits 0 → start the falling logic (and tell the quest system).

**3. Timber:** turn on physics and push the tree away from the player → branches follow the trunk every frame → a floor trace looks for the ground → when it lands, swap to the broken trunk, spawn the logs, hide the branches → spawn the stump and start the regrow timer. If a tree gets stuck and never lands, it cleans itself up.

## Hundreds of trees, one real one
Running all that code on hundreds of trees would kill the frame rate. So every tree in the world is a cheap instanced mesh. The axe carries a Foliage Swap trigger: when it touches a tree, it looks that mesh up by name in a data table, spawns the matching choppable blueprint in its place, and removes the instance. Trees you leave alone swap back. Because the names all match, adding a new tree to the game is one new row in the table.

## The axe
I modeled, sculpted and textured the starter axe myself: blockout, sculpt, then hand-painted textures baked into normal, color and RMA maps. In code it's a Master Axe, so every new axe reuses the swing, trace and hit logic and only changes its damage, speed and effects.

I planned 30 to 40 axes across four zones: light and heavy axes, double heads, throwing axes, a fire axe that burns trees over time, a gravity axe, and a "domino" axe that knocks trees into each other.

## Movement
The world was big, so moving around had to be fun on its own: sprint, crouch, slide and slide-jump, with camera shake and FOV changes to sell the speed. There was also a grapple hook.

## The world
The art style was hand-painted and stylized: hard edges and flat planes instead of smooth surfaces, strong contrast, painted highlights and shadows, and mostly hard color transitions. I built the foliage, fog cards and lighting, and checked scenes in Unreal's optimization view modes (shader complexity, overdraw, shadow caching) to keep the frame rate up.

## How it changed
From a grey test grid to a stylized world with a town in about six months. These are in order.

## Why it stopped
Scope creep. The idea list kept growing: towns, shrines, a fishing quest, boss trees that fight back, a forest that turns on you if you cut too much. At the same time I was spending more and more of my time optimizing, fighting the engine and testing assets instead of making the game more fun. I burned out, and we stopped.

## What I learned
- **Lock the scope early.** Every cool idea went into my notes, and the notes turned into a second game.
- **Set the performance budget first.** Pick the frame rate and target PCs before building the world, not after.
- **Biggest tree first still works.** Building the core system first is why the tree cutting feels good, and it's the part I'm proudest of.
- **Build it modular.** The Master Tree and Master Axe made new trees and axes quick to add.
- **Take breaks before you burn out.** I wrote that one down during the project. I should have listened to it.

Images:
## Chop down the biggest tree first
TreeSystem/Final_TreeVideo_web.mp4 {full wide} - (CHOP. CHOP. TIMBER.) The full tree system: chips fly, the tree falls, and it breaks open into logs.
HighresScreenshot00001.png {full wide} - (The forest) Every tree here is cheap until you swing at it.
## Building a tree
TreeSystem/Screenshot_7.png {tall} - (Trunk) Low-poly trunk next to a person for scale.
TreeSystem/Screenshot_8.png {half} - (Low + high poly) A low-poly version for the game, a high-poly version to sculpt.
TreeSystem/Screenshot_10.png {half} - (Branches) Built with the Skin modifier.
TreeSystem/Screenshot_11.png {tall} - (Leaf normals) Leaves inside a sphere. Its normals get copied onto them.
TreeSystem/Screenshot_12.png {half} - (Data Transfer) The modifier that does it.
TreeSystem/Screenshot_13.png {tall} - (Checking in engine) Import and check early, every time.
## Cutting it up
TreeSystem/Screenshot_14.png {big} - (Stump)
TreeSystem/Screenshot_15.png {half} - (Pill cover)
TreeSystem/Screenshot_16.png {half} - (Pill top)
TreeSystem/Screenshot_17.png {half} - (Pill bottom)
## Breaking it
TreeSystem/Screenshot_21.png {full wide} - (Fracturing) The pill turned into a Chaos geometry collection.
TreeSystem/Screenshot_22.png {big} - (Fracture pieces) Every color is a piece that can break off.
TreeSystem/Tree_Hit_Demo.mov {half} - (Hit)
TreeSystem/Tree_Falling_Demo.mov {half} - (Falling)
TreeSystem/Tree_Ground_Demo.mov {wide} - (Hitting the ground) Breaks open like a peanut.
## How the code fits together
TreeSystem/Screenshot_18.png {full wide} - (Master Tree) Hitboxes, grapple spots, log spawn points, all set per tree.
TreeSystem/Screenshot_19.png {tall} - (Tree settings) Health, XP, axe level needed, big-damage threshold.
AxeSystem+Model/Axe_System (2).png {full wide} - (1. Swing) Attack input: block double swings, slow the player, play the animation.
AxeSystem+Model/Axe_System (5).png {full wide} - (1. Axe trace) An animation notify turns the hit trace on and off.
AxeSystem+Model/Axe_System (7).png {full wide} - (1. Hit feel) Camera shake, hit-stop, slow-mo, effects.
TreeSystem/Screenshot_24.png {full wide} - (2. Chop) Is the axe strong enough? Was it a big hit?
TreeSystem/Screenshot_26.png {full wide} - (2. Health) Health hits 0 → start falling, tell the quest system.
TreeSystem/Screenshot_27.png {full wide} - (3. Timber) Physics on, push it away from the player, add XP.
TreeSystem/Screenshot_29.png {full wide} - (3. Follow) Branches follow the trunk; check for the ground.
TreeSystem/Screenshot_31.png {full wide} - (3. Landing) When it hits the ground, break it.
TreeSystem/Screenshot_33.png {full wide} - (3. Stump) Spawn the stump and start the regrow timer.
## Hundreds of trees, one real one
AxeSystem+Model/Axe_System (1).png {wide} - (Foliage Swap trigger) Lives on the axe.
TreeSystem/Screenshot_39.png {full wide} - (The swap) Look up the mesh, spawn the real tree, remove the instance.
TreeSystem/Screenshot_38.png {full wide} - (Data table) One row per tree type.
TreeSystem/Screenshot_36.png {full wide} - (Swap back) Untouched trees go back to cheap instances.
## The axe
AxeSystem+Model/Blender_Screenshots (2).png {tall} - (Blockout)
AxeSystem+Model/Blender_Screenshots (3).png {tall} - (Sculpt)
AxeSystem+Model/Blender_Screenshots (4).png {tall} - (Textured)
AxeSystem+Model/Blender_Screenshots (1).png {big} - (Axe head) Hand-painted scratches and highlights.
AxeSystem+Model/Blender_Screenshots (8).png {tall} - (Handle)
AxeSystem+Model/RGB+A.png {half} - (Color map)
AxeSystem+Model/Normal.png {half} - (Normal map)
AxeSystem+Model/FirstPerson_Hit_Swing.mov {wide} - (Swing + hit)
AxeSystem+Model/ThirdPersonSwing.mov {half} - (Third person)
## Movement
Movement/Sprinting+Sliding_Demo.mov {wide} - (Sprint + slide)
Movement/Slide+Jumping_Demo.mov {half} - (Slide jump)
Movement/Long_Sliding_Demo.mov {half} - (Long slide)
Movement/MovementVideo.mkv {full wide} - (Through town)
## The world
Folliage/Screenshot_1.png {full wide} - (Lit) The final look.
Folliage/Screenshot_3.png {half} - (Base color)
Folliage/Screenshot_4.png {half} - (Lighting only)
Folliage/Screenshot_2.png {half} - (Wireframe) Leaf cards, not real leaves.
Folliage/Screenshot_7.png {half} - (Shader complexity) Checking what costs the most.
## How it changed
ProgressPictures/ScreenShot00003.png {third} - (Start) A grey grid.
ProgressPictures/ScreenShot00007.png {third} - (First ground)
ProgressPictures/ScreenShot00011.png {third} - (First forest)
ProgressPictures/ScreenShot00017.png {half} - (Trying a new look)
ProgressPictures/ScreenShot00029.png {half} - (Autumn birches)
ProgressPictures/ScreenShot00045.png {half} - (Roads + the truck)
ProgressPictures/ScreenShot00054.png {half} - (The first town)
ProgressPictures/ScreenShot00057.png {big} - (Stylized)
ProgressPictures/ScreenShot00065.png {big} - (Last version)
