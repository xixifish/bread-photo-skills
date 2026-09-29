---
name: photo-set
description: Write Gemini prompts for a set of four matching bread photos in a calm, bright Japanese–Nordic café style (like the film Kamome Diner) — the whole bread in a café setting, the same bread with no background, a cross-section in the same setting, and the cross-section with no background. Use this when the user wants photos of a bread for a café or bakery website, menu or portfolio, or names a bread and asks for its photos.
argument-hint: "[bread name] [square | portrait | landscape]"
---

# Bread Photo Set

For one bread, write the prompts for four matching photos:

| Photo | Background | File name |
|---|---|---|
| Whole bread | café table by a window | `<bread>-whole.png` |
| Whole bread | plain white | `<bread>-whole-white.png` |
| Cross-section | the same café table | `<bread>-cross-section.png` |
| Cross-section | plain white | `<bread>-cross-section-white.png` |

All four must show the **same loaf**, so the user makes them in **one Gemini chat**, each photo an edit of an earlier one.

If the user typed only the command, show two examples with the bread name after the command (for example `shokupan` and `shokupan portrait`) and ask which bread they want.

## The style

A small, quiet neighborhood café on an ordinary morning, inspired by the Japanese film *Kamome Diner* (かもめ食堂) and the drama *Pan to Soup to Neko Biyori* (パンとスープとネコ日和): bright window light, a white plaster wall, pale wood, undyed linen, and simple, honest homemade bread. Don't name these titles in prompts; describe the look instead.

Use this exact scene and style text for every bread, so all the photos on the website look like one set.

**Scene** (for photo 1):

> on a honey-toned pale oak cutting board on a warm pale oak table by a window, a folded undyed linen cloth beside it and nothing else on the table, a warm white plaster wall softly out of focus behind

**Style text** (end of photo 1's prompt):

> Soft, gently warm morning daylight from a window on the left, bright and airy, bright exposure, lifted soft shadows, no blown-out highlights. Calm, cozy, quiet everyday morning mood of a small neighborhood café. Warm, muted natural palette of cream, warm white and honey-toned pale wood, with the warm browns of the bread as the main color. Simple, uncluttered composition with generous empty space. Realistic photograph, 50mm lens, camera about 35 degrees above the table, bread centered, moderate depth of field, soft contrast, true-to-life colors, very subtle fine grain.

**Avoid** (end of photo 1's prompt):

> Avoid: dark or moody lighting, dark background, cool blue or grey color cast, grey weathered wood, dramatic spotlight, orange golden-hour glow, heavy blur, oversaturated colors, glossy advertising look, steam, flying flour, extra props, text, logos, watermarks, people, distorted bread shapes.

## Photo shape

The user can add a shape after the bread name. Default to square if they don't.

| Shape | Words that ask for it | Prompt opening | Good for |
|---|---|---|---|
| Square (default) | square, 1:1 | "A square photo of" | menus, social media, grids |
| Portrait | portrait, vertical, tall, 4:5, 2:3 | "A vertical portrait photo of" | phones, tall menu cards |
| Landscape | landscape, horizontal, wide, banner, 16:9, 3:2 | "A wide landscape photo of" | website banners |

Only photo 1 states the shape. The edits in photos 2–4 keep its framing, so all four come out the same shape. For a landscape photo, add "with generous empty space on both sides" after the scene, so the bread doesn't fill the whole width.

For a square photo, center the bread. Add this sentence at the end of the prompt in every step, 1 to 4:

> The bread sits in the exact center of the square frame, with equal empty space on the left and right, and above and below.

In step 2, it applies to the whole arrangement: the loaf and its cut pieces together stay centered. The style text's "bread centered" alone wasn't enough: with the camera looking down at the table, Gemini tended to place the bread low or off to one side, and the cut step shifted it further. Tested with a baguette: centered in all four photos.

Gemini's chat can't produce an exact pixel size. If the user asks for one (for example 1200 × 1500), use the closest shape and tell them to resize afterwards (on a Mac: open the image in Preview → Tools → Adjust Size). Making an image smaller works well; making it bigger makes it blurry.

## Describing the bread

Describe the bread's **shape and crust** concretely. Vague names get generic bread; for example, "shokupan" alone came out as a small, round, floury loaf. Examples:

- **Shokupan (Japanese milk bread):** baked in a rectangular tin, tall and boxy with straight sides and square corners, two or three rounded humps on top, a thin smooth crust that's glossy golden-brown on top and paler on the sides, no flour, no scoring.
- **Country sourdough:** a round boule with a deep-brown, crackly, blistered crust, a light dusting of flour, and one curved raised ear where it was scored.
- **Anpan (Japanese sweet red bean buns):** round, slightly flattened buns about the size of a palm, smooth domed tops, a thin soft crust that is evenly glossy golden-brown on top and paler at the sides, a small cluster of black sesame seeds pressed into the center of each top, no flour, no scoring.

Don't describe the **crumb texture** in words. In testing, every wording made the crumb look fake (craters, cotton strands or foam). The texture comes from a real photo instead (see below).

**Do describe a filling** in words, in step 2: what it is, its color, its shape and where it sits, for example "The smooth koshian red bean filling shows in the cut as one even, glossy dark reddish-brown oval in the center of each half, with no whole bean pieces, surrounded by soft white crumb." The photo gives the texture of the dough; the words make sure the filling is the right kind and in the right place. In testing with anpan, the crumb photo alone gave a filling that ran off the edge like a wedge; adding this sentence gave a natural result.

## The crumb photo

The cross-section needs a real photo of this bread's crumb for Gemini to copy. Look in the `crumb-photos/` folder of the user's project for a file named after the bread (any image format). If there isn't one, ask the user for a photo of the inside of this kind of bread: their own bread is best, or a free Unsplash or Pexels photo.

**The photo should show the whole cut face and little else:** the cut surface of a slice or half-loaf, seen straight on, filling most of the frame, with only a thin edge of crust and as little background as possible. Gemini copies whatever the photo shows, not just the texture. Testing found both extremes fail:

- **Too much:** a whole slice with its crust, background and props made Gemini copy the slice's outline and pale crust, which didn't match the loaf.
- **Too little:** a zoomed-in patch from the middle made the holes come out too large and evenly spread, and the cut face looked flat, like a sticker.
- **The whole cut face** kept a natural hole size and the real structure (tighter near the crust, more open in the middle), and looked real.

If the user's photo shows much more than the cut face, tell them to crop it to the cut face before using it.

**Exception: a whole photo can work better when the reference bread has the same simple shape as the user's.** For shokupan, an uncropped photo (a cut loaf and slices of the same kind of tin loaf, lit from the side) gave a softer, more natural cut surface than a cropped flat slice seen from above. A tin loaf's slices are plain rectangles, so there was no unusual outline for Gemini to copy, and the side light gave the crumb depth. If a cropped photo gives a flat-looking cut surface, suggest trying the whole photo instead.

**Match the cut and the recipe, too.** For breads with layers, spirals or fillings, the crumb photo should be cut the same way step 2 cuts the bread: for rolls, a roll standing upright, cut straight down through the center, seen from the front. It should also contain only what the bread contains, with no icing, nuts, zest or other extras the user's bread doesn't have. Crop off toppings the bread does have too (sesame, seeds, sugar): Gemini copies their pattern and position from the photo. Crop off hands and fingers as well: Gemini may add them to the scene. In testing, a strip of sesame along the reference anpan's crust appeared on both cut halves. In testing, a blurry photo of a tipped-over cinnamon roll gave holes that were too large and a stringy texture. A sharp photo of an upright roll, cut straight through, with the icing cropped off, looked real.

## How to cut it

Choose the cut by the bread's shape. The less Gemini has to invent, the more real the result looks. Always say exactly where each piece rests (on the board, beside or behind which piece), so nothing floats or hangs over an edge.

- **Tin loaves** (shokupan, sandwich loaves): "Cut one thick slice straight across the loaf from its left short end, so the slice shows the loaf's full square cross-section. The loaf stays where it was, lying the same way, just one slice shorter, with its new cut end facing left. Stand the slice upright on the board in front of the loaf's left end, turned so its cut face faces the camera. The long side of the loaf stays uncut crust." Always name the short end: in testing, "cut a slice from the front of the loaf" on a loaf lying side-on made Gemini cut into the long side, which is impossible for a tin loaf. With the short end named and an uncropped crumb photo of a cut shokupan loaf, shokupan looked real.
- **Round or oval loaves** (country sourdough, rye, boules): "Cut the loaf in half through the middle. Stand one half on the board with its cut face toward the camera. Place the other half on the board just behind and to the side of it, cut face down, so both halves rest fully on the board. Lit from the side by the window." Don't cut a slice from the end. In testing, a sourdough end slice came out too big, with a paler crust than the loaf. And "the other half behind it" alone left the back half half-off the board, not clearly resting on anything.
- **Long loaves** (baguette): "Cut the loaf in half at an angle and place the two pieces side by side, cut faces toward the camera."
- **Rolls** (cinnamon rolls): "Cut one roll in half through the middle and place the two halves in front of the others on the board, cut faces toward the camera, both halves resting fully on the board." Tested with cinnamon rolls: looked real, but only with a well-chosen crumb photo (see "The crumb photo").
- **Small filled buns** (anpan, cream buns, curry bread): "Cut one bun in half through the middle and place the two halves in front of the others on the board, cut faces toward the camera, both halves resting fully on the board. Keep the cut one's size the same as before, do not make it bigger or smaller." Then describe the filling (see "Describing the bread"). Tested with anpan: looked real. Without the size sentence, Gemini made the halves 10–60% bigger than the whole bun in every try.

If a cross-section looks off, one more try can help, since results vary. But resending the same prompt in the same chat often returns an almost identical image. Instead, send a direct edit that names what to change ("Edit the image above. Change only the cut faces: …"), or start a new chat with the saved step 1 image attached.

## Output

Reply with a one-line plan, then these four steps. Prompts are in English; everything else is in the language the user writes in (English if they only typed the command).

````markdown
### <Bread> — photo set (<shape>)

Open a **new Gemini chat** and send these one at a time. Download each image at full size before moving on.

**1. Whole bread — café** (nothing attached) → save as `<bread>-whole.png`
```
<shape opening> one whole, uncut homemade <bread>: <shape and crust>, <scene>. <style text> <centering sentence, square only> <avoid>
```

**2. Cross-section — café** (attach `crumb-photos/<file>`) → save as `<bread>-cross-section.png`
```
Edit the first image. Keep the bread's shape and crust, the board, cloth, wall, light and framing exactly the same, and add nothing new to the scene. <how to cut it, from "How to cut it" below> <for a filled bread: the filling sentence> Every cut piece keeps the same crust as the loaf, the same color and texture. The attached photo is a real photo of <bread> crumb, for texture reference only: make the cut faces match its crumb exactly — the same texture, softness, small irregularities and color. Do not copy anything else from it. <centering sentence, square only> Avoid: round crater-like holes, stringy or fibrous crumb, foam-like or cake-like crumb.
```

**3. Cross-section — no background** → save as `<bread>-cross-section-white.png`
```
Edit the image above. Keep the bread exactly the same — its shape, crust, crumb, color, size, and the light on it. Remove everything else: no board, table, cloth, knife, crumbs or wall. Place the bread alone on a plain, smooth, evenly lit pure white background. Same framing. <centering sentence, square only>
```

**4. Whole bread — no background** (attach your saved `<bread>-whole.png`) → save as `<bread>-whole-white.png`
```
Edit the attached image. Keep the bread exactly the same — its shape, crust, color, size, and the light on it. Remove everything else: no board, table, cloth, knife, crumbs or wall. Place the bread alone on a plain, smooth, evenly lit pure white background. Same framing. <centering sentence, square only>
```

**Optional — transparent background:** Gemini can't make a real transparent image, so photos 3 and 4 come out on plain white. If you need a transparent PNG, remove the white yourself: in Finder, right-click the image → Quick Actions → Remove Background.
````

After the steps, add one line: if any photo looks wrong, share it and say what's off.

## Why it works this way

These rules come from testing, so keep them:

- **Gemini, not ChatGPT.** ChatGPT's cross-sections looked artificial even with a crumb photo; Gemini's looked real.
- **One chat, whole bread first.** Editing one image keeps the loaf identical across all four photos. Photo 4 re-attaches photo 1 because the chat has moved on to the cross-section by then.
- **A white background, not a transparent one.** Asking Gemini for a "transparent background" gives a fake checkerboard drawn into the picture, so photos 3 and 4 ask for plain white.
- **"Size" in the keep sentence of steps 3 and 4.** Without it, removing the background sometimes made the bread bigger or smaller, so the no-background photos didn't match the café ones.
- **Brightness words in the style text.** Without them, Gemini's café photos came out darker and moodier than this style. With "bright exposure, lifted soft shadows" they came out bright and airy.
- **Warmth words in the scene and style text.** "Pale wood" and "clean white walls" once gave grey, weathered wood and a cold white wall, which felt cool rather than cozy. "Honey-toned pale oak", "warm white" and "gently warm morning daylight" keep the warmth without turning orange.
