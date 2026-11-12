GOAL
Build a short walkable browser game in a thick oil-painting style, based on my 7 attached images (in story order). The reference project is "Oil paint" by blendi at patch.gg/blendi/oil-paint (code MIT, art CC0). If you can't open it, use the technique below. Build it the same way he did.

HOW THE REFERENCE WAS BUILT (follow this approach)
- Stack: three.js (0.186) with WebGLRenderer on WebGL2 only. Rapier for physics. Vite or similar for the build. Not WebGPU.
- Nothing is filtered after rendering. Everything is a "dab": one brush stroke in one mixed colour, pinned to a point in the 3D world and turned to lie along a direction in the world (the grain of a trunk, the fall of a cloak). The paint stays on objects as the camera moves.
- Dabs are GPU-instanced. Position and attributes go in buffers, and colour and direction are decided in GLSL in a function called makeDab.
- Colour is paint, not light. Each object has three colour mixes (light, half-tone, shade). Each dab picks one based on how lit its spot is, with a little random variation (jitter) so colour looks broken like real paint. No tone-mapping, so colours look on screen as chosen.
- The brush is a sheet of 8 marks generated in code: where paint is, how thick it stands, and a streak of a second colour. A light from the upper left rakes across the thickness.
- Distance simplifies: dabs keep a minimum and maximum on-screen size, so far things use fewer, larger strokes.
- The ground is built from flat dabs, each belonging to a fixed small square, so strokes never crawl when the camera moves.
- Strokes must never be sorted by camera position, or the paint shimmers. Near things get a fixed depth each. Far things (mountains, mist, sky) are layered in a fixed far-to-near order.
- Shadows for the still world are baked once from the sun. A moving character's shadow is a soft glaze over the ground.
- Glowing things (my feathers, the chariot, lanterns, sunrise) use additive strokes instead of covering ones.
- Mist is used to separate rows of things.
- Characters and objects get paint through "pins": points spread over a mesh's surface and carried with it as it moves.
- Textures on models are ignored. Colour comes only from the palettes.
- Everything in the scenes is made in code. Only the character model and animation clips were free CC0 assets.

PERFORMANCE
- Add a quality=low mode (fewer pixels, fewer strokes, less mist). It must run acceptably on a mid-range laptop.

MY GAME
Hero: a tiny round chicken (cream feathers, red comb, amber wings, small teal-green shoulder bag). Build it from simple shapes in code, painted with pins. It waddles, flaps when jumping, and has a "cluck" button.
Controls: WASD, Space to jump, mouse to look. Gamepad optional.

SCENES (image numbers)
1. Dawn village: red-earth path, white houses with tiled roofs, palms, hibiscus, paddy fields, temple in mist.
2. Stone path uphill with 3 glowing feathers to collect.
3. Broken cliff. After collecting all 3 feathers, a golden lotus-shaped flying chariot arrives. It has no wheels, with flowing cloth and lanterns.
4. Automatic ~20 second ride over painted clouds.
5. Summit reveal: a giant stone eagle statue lying with wings spread and one claw raised. My own design, a tribute inspired by a Kerala hill landmark. This is the main shot: make it huge and dramatic.
6. Ending: the chicken places 3 feathers at the claw, the sky bursts into golden strokes, and the text "For my little one." appears.

COLOURS (light / mid / shade)
- Red earth: #C2573A / #8F3A2A / #5A2A25
- Palms and leaves: #B9C25A / #6E8A3A / #2F4A2A
- Rocks and path: #C9936A / #8A6048 / #4E3A34 (moss #7F8F3A)
- Chicken: #F6E3B0 / #E5B96A / #B98A55 (comb #D83A2B, bag #3F6F63)
- Gold chariot: #FFD86A / #E0A030 / #A0601E (cushion #B8282E)
- Statue stone: #E8C9A0 / #B89574 / #6E5545
- Sky: pale gold, orange, lavender-pink. Mist: #C9B8C8

RULES
- Original designs only. Nothing copied from any film or existing artwork.
- No sound needed.
- Treat the statue and the story with respect. It is a tribute.

BUILD ORDER
1. Set up the renderer, dab system, brush sheet and ground first. Show me a screenshot.
2. Then scenes 1, 2 and 5 only. Stop and show me.
3. I will ask for scenes 3, 4 and 6 afterwards.

DELIVER
A project I can run with npm install and npm run build, with the demo in dist/. Include a short README listing what each file does.

REFERENCE IMAGES
The 7 images are in this repo (github.com/FerrorBeta33/Little-Chicken-Quest), in the root folder.
In story order:
1. "01 A Chicken’s Journey to Jatayu.png": scene 1, dawn village
2. "02 Golden Feather Trail Through Kerala Hills.png": scene 2, stone path with 3 glowing feathers
3. "03 Chicken and Lotus Chariot at Dawn.png": scene 3, broken cliff, chariot arriving
4. "04 Chicken’s Golden Lotus Chariot Above Clouds.png": scene 4, chariot ride over clouds
5. "05 Reclining Jatayu at Golden Dawn.png": scene 5, summit reveal with the giant eagle statue (the main shot)
6. "06 Three Golden Feathers at Dawn.png": scene 6, ending, with the text "For my little one."
7. "07 Cheerful Chicken Beside Jatayu’s Toes.png": close-up of the chicken's face and body. Use it as the main character reference.

Open and study all 7 before building. Use them only as visual reference for composition, colours and mood. Do not use them as textures.
Note: file names contain spaces and curly apostrophes, so quote the paths. Wheels on the chariot in image 5 are a mistake. The chariot has no wheels, as in images 3 and 4.
