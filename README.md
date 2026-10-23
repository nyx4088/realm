# The Realm

A first-person 3D pixel-art exploration game. Ten connected biomes in one open
world, built entirely from procedural low-poly geometry and instancing - no
external assets, no HUD, no combat, no fail states. Just walk.

## The ten lands (west to east, one continuous walk)

1. **Moss Golem Forest** - a ~60 m stone golem with moss, vines and flowers,
   pulsing cyan eyes, sunbeams, deer and birds
2. **Great Tree Village** - a 100 m tree with lit treehouses, rope bridges,
   spiral stairs and root waterfalls feeding a stream
3. **Glow Mushroom Forest** - giant purple mushrooms with glowing cyan gills,
   pink mist, floating spores, mushroom-hat creatures
4. **White Mountain City** - tiered white city, central tower, aqueducts, a
   waterfall through the city, turquoise river, sailboats, snow peaks
5. **Flower Valley** - 400+ swaying flowers, winding stream, crystal spire,
   sunset sky, butterflies and fireflies
6. **Night Swamp Village** - stilt houses, walkable boardwalks, weeping
   willows, glowing frogs on lily pads, a rowboat with a lantern
7. **Dragon Lake** - turquoise lake, shimmering mountain reflection, a giant
   sleeping blue dragon and three smaller dragons
8. **Sky Castle** - castle on a rock spire above a sea of clouds, a long
   staircase to a barred gate, waterfalls falling into the clouds
9. **Fishing Dock** - wooden dock on a teal lake, a huge carved-face cliff
   with a ruined tower. Press **E** at the dock to cast a fishing line
10. **Dragon Over Farmland** - a red dragon circling overhead, its shadow
    sweeping over patchwork fields, villages, a river and a distant castle

## Controls

- **Desktop:** click to lock the pointer, WASD to move, mouse to look,
  Shift to run, Space for a small jump, E to fish at the dock
- **Mobile:** left virtual joystick to move, drag the right side to look,
  on-screen JUMP / RUN / E buttons
- Eye height 1.7 m, walk speed 3 m/s, gentle head-bob, Rapier physics for
  ground and collision

## Look

- RenderPixelatedPass (pixel size 4), nearest-neighbour upscale
- Posterized colour pass plus ordered dithering on gradients (final pass)
- Bloom on emissive objects, volumetric light shafts, soft per-biome fog
  that blends as you cross borders, one dominant warm light per biome
  against cool shadows, no outlines
- Procedural wind audio per biome (WebAudio, starts on first click)
- InstancedMesh throughout, distance culling via fog + biome visibility,
  pixel ratio capped at 2 - targets 60 fps on mid-range phones

## Run

```bash
cd realm
npm install
npm run dev        # dev server
```

## Build and deploy

```bash
npm run build      # static output in dist/, base path /realm/
npm run preview    # preview the production build
```

Deploy the contents of `dist/` to any static host. For GitHub Pages, serve
it from a `/realm/` path (the Vite base is set to `/realm/` in
`vite.config.js`). If you need it under a different subpath, rebuild with
`npx vite build --base=./` for relative asset paths.

## QA shortcuts

- `?preview&biome=0` .. `?preview&biome=9` - teleport to a biome with the
  start overlay hidden (no pointer lock), plus `&yaw=` and `&pitch=`
- `window.__realm` in the console exposes `{ scene, camera, body }`

## Layout

- `index.html` - start overlay, mobile controls, styles
- `src/main.js` - engine (renderer, composer chain, Rapier player), all ten
  biome builders, particles, creatures, fishing and procedural audio
- `vite.config.js` - base `/realm/`, output `dist/`

A prebuilt copy also lives in the StampQuest site at
`philately-passport/site/realm/` (relative-base build), linked from
Settings, About this app, "Enter The Realm". It is not pushed live until
you say ship.
