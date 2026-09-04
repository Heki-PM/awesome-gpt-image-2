> [Back to README](../README.md) | [Full gallery overview](./gallery.md) | [Disclaimer & WeChat account](./disclaimer.md)

*(Unofficial English translation of `docs/templates.md`, translated for easier navigation. Original Chinese file is authoritative.)*

<a name="section-templates"></a>

## 🧩 Industrial-Grade Prompt Templates & Pitfall Guide

> Hi everyone, I'm your merciless reverse-engineering machine. To make these templates truly "open the box and use," I dug through all 393 cases from top to bottom and distilled 21 **industrial-grade prompt templates** out of them.
> Honestly, organizing these rules nearly broke me, but once they worked it was extremely satisfying! Every template comes with its own "pitfall guide" — just copy, fill in the blanks, and stop relying on random luck.

<a name="tpl-ui"></a>

### UI & Interfaces

**Standard template**

```text
Generate a [platform, e.g. iOS/Android/Web] interface image for a [product type].
Core features: [feature A], [feature B], [feature C].
Visual style: [minimalist/tech/skeuomorphic], primary color [color], accent color [color].
Layout: [top navigation/two-column/card feed], clear information hierarchy, ample whitespace.
Output: high-fidelity UI screenshot, clearly readable text, ratio [9:16/16:9].
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "UI Screenshot",
  "platform": "iOS",
  "product": "Fitness App",
  "layout": "Card-based feed with bottom tab bar",
  "style": {
    "theme": "Dark Mode",
    "primary_color": "Neon Green",
    "typography": "Clean sans-serif"
  },
  "content": {
    "header": "Today's Activity",
    "cards": [
      {"title": "Running", "data": "5.2 km", "button": "Start"},
      {"title": "Calories", "data": "340 kcal"}
    ]
  },
  "constraints": "High fidelity, readable text, 9:16 aspect ratio"
}
```

**Screenshot generation template**

```text
Generate a [platform, e.g. X/Douyin/Xiaohongshu/WeChat Moments] content screenshot, [dark/light] mode.
Overall ratio: [9:16 / 3:4 / 1:1], phone-screenshot style.

Core content:
- Account info: [avatar description / username / verification badge]
- Body text: [specific text content, including any required text in the target language]
- Engagement stats: [like/comment/share/save counts]

UI elements:
- Top: [status bar/nav bar/search bar]
- Bottom: [action bar/tab bar/input field]
- Extras: [floating window/danmaku/gift effect/shopping-cart card]

Constraints: text must accurately display the specified wording, no garbled characters or placeholder text, fixed ratio.
Output: convincing social-platform screenshot, clearly readable text.
```

**Livestream interface template**

```text
Generate a [platform, e.g. Douyin/Kuaishou/Bilibili] livestream interface screenshot.
Host: [person description/name], pose: [sitting/standing/action], outfit: [outfit description].
Background: [livestream room background description], lighting: [warm/cool/mixed].

UI overlay:
- Top: host avatar + follow button + viewer count + rank/popularity score
- Bottom left: danmaku/comment list ([N] items, example content)
- Bottom right or center: product card / gift effect / PK progress bar
- Bottom: input field + function icons (share/like/gift/shopping cart)

Style: [realistic livestream screenshot/high-fidelity UI/dark theme/pastel theme], ratio 9:16.
Constraints: text clearly readable, danmaku content plausible, UI elements must not cover the host's face.
Output: convincing livestream-screenshot image.
```

**Pitfall guide**

- **Don't give vague instructions**: specify "platform + ratio + layout" explicitly, or the model will lay things out like a clueless intern.
- **Force text lock-in**: require "text must be absolutely readable, must display the specified wording," to avoid garbled buttons and meaningless placeholder text.
- **Distinguish platform features in screenshots**: X (Twitter) has blue-check verification and retweet/quote distinctions; Douyin has a spinning music disc and like animations; Xiaohongshu has a two-column waterfall layout. Specify the platform before generating, or the model will mix styles together.
- **Lock the livestream scenario first**: e-commerce livestreams and talent-show livestreams have very different UI layouts (e-commerce has a product list in the top right, talent shows lean on danmaku interaction) — decide the livestream type before filling in details.
- **Lock unusual screen ratios**: special screens like car dashboards or smart-home displays have fixed ratios (e.g. 21:9) — this must be stated up front, or the model defaults to a 9:16 phone ratio.

<a name="tpl-infographic"></a>

### Charts & Infographics

**Standard template**

```text
Generate an infographic on [topic: be clear and specific, avoid being broad — e.g. "a daily health-management guide for seniors" rather than just "health"], targeting [audience: detail audience traits such as age group, occupation, interests].
Structure: title area + [3-5] modules (each module has an icon, short title, 1-2 sentence explanation; connect modules logically using arrows, color-coding, or connecting lines to suggest information flow or relationships as appropriate).
Chart type: [flowchart/comparison chart/relationship diagram/timeline].
Style: [professional report/pop-science illustration/children's educational, etc.], primary color [color], background [light/dark].
Output: infographic with a clear information hierarchy and high readability, in [specified language, e.g. Chinese].
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "Infographic",
  "topic": "Urban Metabolism",
  "audience": "General Public",
  "structure": {
    "title_area": "Urban Life-System Atlas",
    "layout": "Isometric cutaway, 12 numbered panels",
    "modules": [
      {"title": "Energy", "icon": "lightning", "text": "Power flows"},
      {"title": "Water Cycle", "icon": "water_drop", "text": "Water flows"}
    ]
  },
  "style": {
    "aesthetic": "Scientific atlas",
    "colors": "Low saturation, color-coded flows",
    "background": "Light paper texture"
  },
  "constraints": "No cyberpunk, no gibberish text, strict structural layout"
}
```

**Scale-zoom scientific infographic template**

```text
Generate a scientific scale-zoom infographic for [topic].
Structure: 6-8 circular or hexagonal frames, arranged in ascending scale from microscopic to macroscopic.
Each frame contains: the scale's name, a 3-5 word insight, unit of measurement or magnification factor, and a highly detailed 3D render at that scale.
Connect the scales with thin lines, avoid repeating levels. Title uses "[TOPIC]: AT EVERY SCALE" or "ZOOM: THE WORLD OF [TOPIC]".
Style: scientific editorial infographic, precise macro lighting, clear hierarchy, short and readable text.
Constraints: no generic magnifying-glass icon, don't draw every scale at the same size, don't cram in long paragraphs of body text.
```

**Pitfall guide**

- **Control the module count**: explicitly fixing the "number of modules" and "chart type" greatly reduces visual clutter and information overload.
- **Keep copy minimal**: for chart scenes, prefer short-sentence copy — never cram large paragraphs of body text into the image; the model isn't a typesetter.

<a name="tpl-poster"></a>

### Posters & Typography

**Standard template**

```text
Design a poster for [an event/product/movie], theme: [theme keyword].
Key visual: [main element], headline: [title], subheading: [subtitle].
Layout: [centered/left-aligned/diagonal composition], style: [retro/futuristic/minimalist].
Colors: [primary + secondary color], mood: [mood keywords].
Output: high-resolution poster suitable for social media distribution.
```

**Sports commercial campaign template**

```text
Design a commercial campaign poster for [a sport/fitness category].
Subject: [athlete/model/product prop], pose: [seated/sprinting/swinging/power move].
Key prop: [racket/dumbbell/sneaker/jersey], made a visual anchor via exaggerated proportion or diagonal composition.
Layout: [single strong key-visual/triptych/data-doodle poster].
Large headline: "[main title]", supporting copy: "[short phrase/stat/slogan]".
Visual style: high-end sports-brand advertising, strong light and shadow, reflective floor, clean composition, brand color palette [primary + secondary].
Constraints: subject must be clear, text readable, tone consistent, no messy collage, no incorrectly-rendered sports equipment.
Output: 1:1 or 4:5, sports-commercial visual suitable for social media.
```

**Concept typography poster template**

```text
Create ONE finished premium conceptual typography poster for the exact title:

"[title/word/phrase]"

Single poster only. No moodboard, grid, presentation board, mockup, captions, prompt text, process sheet, or sample labels.

The title must be the dominant visual structure of the poster: huge, readable, powerful, and spelled exactly. Do not translate, shorten, replace, or misspell it. Do not add other large readable text.

Silently interpret the title's meaning, mood, cultural aura, symbolic associations, psychological tension, and visual rhythm. Turn that interpretation into one strong visual metaphor.

Typography is the hero. Design custom-looking letterforms whose weight, width, contrast, spacing, rhythm, distortion, negative space, edge quality, and ink texture express the temperament of the title. The type should feel intentionally designed, not like a default font.

If the title refers to a widely known person, make a large editorial portrait or half-body figure a major visual presence, occupying roughly 40%-70% of the composition. The figure should interact with the typography: overlapping the letters, emerging from them, being framed by them, casting shadows on them, breaking through them, or being partially hidden behind them.

For abstract or non-person titles, use a human figure, landscape, object, or atmospheric setting only when it strengthens the meaning. It must interact with the typography and deepen the concept, not decorate it.

Use a restrained 4-6 color system matched to the theme: dominant background color, primary typography color, figure / landscape tone, emotional accent color, muted support color, and subtle paper / ink texture tone.

Composition style: high-end editorial poster, museum-quality graphic design, dramatic scale, strong hierarchy, few elements, intelligent whitespace, bold flat color areas, sharp cropping, silkscreen / lithograph / risograph grain, paper fibers, subtle ink imperfections, refined visual tension.

Avoid generic word art, glossy 3D lettering, random icons, stock-photo realism, cluttered collage, excessive grunge, tourist clichés, official logos, copied slogans, copied campaign aesthetics, unrelated text, and misspelled typography.
```

**Multi-style signature selection poster template**

> Source reference: [signature-image-prompts-gpt-image-2.md](https://github.com/zaizhi-1112/ai-image-extension-playbook/blob/main/signature-image-prompts-gpt-image-2.md) / [@liyue_ai](https://x.com/liyue_ai)

```text
You are a high-end signature design system + style-persona visual system.

Input:
Name: [name/nickname]

Task:
Based on the name, automatically generate a 9:16 vertical "multi-style signature selection poster."
The goal is to translate the name into 6 signature options, each with its own stroke feel, temperament, and sense of power.

Hidden analysis (do silently):
1. Analyze the character shapes of the name: density, horizontal/vertical proportion, center of gravity, room for connecting strokes, room for cursive style.
2. Infer a temperament: cool/aloof, expressive, restrained, businesslike, artistic, relaxed, sharp, refined.
3. For each signature, first define the writing behavior: stroke start, connecting strokes, rhythm, structural distortion, stroke ending.

Layout:
- Pure white or very light gray gradient background, at least 40% whitespace
- Large title at top: [Name] · Signature Style Selection
- Subtitle: Different stroke styles, different presence
- Middle section: 2-column × 3-row card grid
- Bottom small text: "Pick one as your signature."

Card specs:
- Uniform size, uniform spacing, overall alignment for every card
- Slight rounded corners, 8-16px
- Very thin outline or no border
- Very subtle shadow
- Subtle off-white, very light gray, rice-paper or matte texture
- Visual target close to high-end magazine layout, avoid a strong "UI" feel

6 signature styles:
1. Minimalist & rational: close to a brand signature, restrained strokes, clear whitespace
2. Wild & tense: strong connecting strokes, strong sense of speed, stretched final stroke
3. Relaxed & casual: clearly handwritten feel, naturally flowing, approachable and light
4. Eastern running/cursive script: dry-brush strokes, ink feel, pronounced rhythmic variation
5. Sharp & structural: geometric cut corners, a sense of breakage, calm and restrained
6. Experimental: partially illegible, restructured form, avant-garde personality

Each card must include:
- A number
- The style name
- A large-size rendering of the signature
- One short sentence describing its temperament
- One very subtle accent color

Lighting & texture:
High-end studio lighting, soft ambient light, delicate shadows, clean airy feel.
Overall palette mainly black, gray, and white, with restrained accent color.

Prohibited:
No font collage, no ordinary calligraphy characters, no messy colors, no signature too small, no loose/sloppy layout, no lack of stroke feel, no template-collage look.
```

**Single signature extraction template**

```text
From the [position/number/style name] signature in the input image, extract that signature's core stroke style and generate a pure signature image.

Requirements:
- Keep only the signature itself — no poster card, title, subtitle, or caption text
- Preserve the original signature's stroke start, connecting strokes, structural slant, dry-brush strokes, and stroke-ending rhythm
- Background: pure white or very light off-white
- Signature centered, sized generously, clean whitespace at the edges
- Ink color deep black or ink-black, with natural brush tension, slight ink marks, and realistic handwriting pressure variation
- Output a high-resolution, pure signature image suitable for tracing practice, collecting, or further design

Avoid:
Do not add multiple additional signatures, do not turn it into a font showcase, do not add a border, do not add decorative elements, do not weaken the original stroke style.
```

**Signature practice breakdown diagram template**

```text
Based on the input [signature image/signature style], generate a signature-practice breakdown diagram.

Goal:
Help the user practice this signature with a pen on paper, by breaking down each stroke's writing path, order, pressure, and rhythm.

Layout structure:
- Vertical teaching diagram or horizontal practice board
- Final signature thumbnail at the top
- Middle section breaks down key strokes into 8-12 steps
- Each step shows: the current stroke, a direction-of-motion arrow, the starting point, pause points, and the ending point
- Below: the full connected stroke path plus 3-5 lines of practice tips

Breakdown requirements:
- Every stroke must correspond to the real stroke style in the original signature
- Mark fast strokes, slow strokes, heavy pressure, light lift, turns, hooks-back, dry-brush strokes, and long trailing strokes
- Show the progressive process from basic skeleton to the finished signature
- Explain the connection logic between characters and how the overall center of gravity shifts

Visual style:
White paper background, black handwritten lines, red or blue teaching arrows, clear numbering, workbook texture.

Avoid:
Do not show only the finished result, do not omit key strokes, do not turn the steps into random doodles, do not generate an unrelated calligraphy copybook.
```

**Chinese-language version: Concept typography poster template**

```text
Generate one extremely polished, high-end conceptual typography poster for the following title. Only one poster is needed.

Title: "[title/word/phrase]"

Only one poster is needed. No moodboard, no grid layout, no presentation board, no mockup, no caption text, no process draft, no sample label.

The title must be the dominant visual structure of the poster: huge, readable, powerful, and spelled exactly correctly. Do not translate, shorten, replace, or misspell the title. Do not add other large blocks of readable text.

Deeply understand the title's meaning, mood, cultural atmosphere, symbolic associations, psychological tension, and visual rhythm. Turn this understanding into one powerful visual metaphor.

Typography is the star. Design custom letterforms whose weight, width, contrast, spacing, rhythm, distortion, negative space, edge texture, and ink texture must express the title's temperament. The type should look carefully designed, not like a default font.

If the title points to a widely known person, let a large editorial portrait or half-body figure become the main visual presence, occupying 40%-70% of the composition. The figure must interact with the type: overlapping letters, emerging from letters, framed by letters, casting shadows on letters, breaking through letters, or partially hidden behind letters.

For abstract or non-person titles, only use a portrait, landscape, object, or atmospheric scene when it strengthens the meaning. It must interact with the type and deepen the concept, not just decorate it.

Use a restricted 4-6 color palette matched to the theme: main background color, main type color, figure/landscape tone, emotional accent color, soft supporting color, subtle paper/ink texture color.

Composition style: high-end editorial poster, museum-grade graphic design, dramatic scale, strong hierarchy, few elements, intelligent whitespace, bold flat color areas, sharp cropping, screen-print/lithograph/riso-print grain, paper fiber texture, subtle ink imperfections, refined visual tension.

Avoid: generic text effects, glossy 3D lettering, random icons, stock-photo realism, messy collage, excessive grunge, tourist-postcard clichés, official logos, plagiarized slogans, plagiarized campaign aesthetics, unrelated text, and misspelled type.
```

**Ink-wash double-exposure portrait poster template**

```text
Generate an ink-wash double-exposure portrait poster of [a person/character/brand founder/athlete].
Format: 9:16 vertical, high-end cinematic poster composition.
Subject structure:
- Upper zone: an enlarged head, facial contour, or half-body silhouette of the person — the strongest recognition anchor.
- Middle-lower zone: a full-body or half-body shot of the same person, pose: [standing/action pose/gazing at camera].
- Inside the silhouette: blend in [a key scene], [a symbolic object], [a narrative fragment], [environmental texture] to form a double-exposure narrative.
Visual connection: use mist, ink diffusion, dry-brush edges, negative space, and soft light/shadow transitions to link the upper silhouette, the inner collage, and the lower subject into one continuous top-to-bottom visual flow.
Style: Eastern ink-wash aesthetic + realistic cinematic feel, restrained, high-end, generous whitespace, layered but not cluttered.
Text: may include [title/name/short phrase], must be minimal, readable, feel like a poster inscription rather than infographic captioning.
Constraints: no hard collage, don't fill the whole background, no cheap wuxia-style effects, don't copy an existing real poster's layout, don't let the silhouette and the main subject compete for focus.
Output: poster-quality finished image, subject clear, ink edges natural, narrative elements strongly tied to the person's identity.
```

**Nature science-education poster template**

```text
You are a high-end nature science-education poster generation system, whose goal is to create Apple-keynote-style premium educational visual posters for rare animals, insects, reptiles, mammals, or other lesser-known creatures.

Overall visual direction:
Generate a 9:16 vertical, premium science poster using a minimalist, pure-white, clean, modern, Apple-style product-launch poster language. The background should be pure white or a very light gray-white gradient, keeping generous whitespace. The overall design should feel premium, restrained, visually striking, and scientific in presentation.

Core design principles:
1. The subject animal must be dramatically enlarged, becoming the strongest visual center of the image.
2. The subject should have a strong sense of dimensionality, realistic texture, high-definition detail, and soft studio lighting.
3. Poster information should be minimal and precise, avoiding crowding.
4. Do not use traditional infographic elements like cards, rounded-corner frames, complex background patterns, aged-yellow paper texture, or decorative borders.
5. The bottom info area should use only a four-column minimalist layout of icon + title + short caption, separated by thin vertical lines.
6. Typography should feel like a premium keynote visual: huge headline, restrained subheading, small and clear body text.
7. Style keywords: Apple-inspired, premium editorial, pure white background, hero subject, clean typography, minimal infographic, high-end science poster.

Layout structure:
Top-left title area:
Large headline in the target language: {species name}
Subheading in the target language: {one attention-grabbing tagline about the species}
Thin short divider line
English name: {English species name}
Distribution info: Primary range: {distribution area}

Middle and lower-middle: main visual:
Generate an ultra-HD, realistic, strongly three-dimensional {species name}.
The subject should occupy 50%-70% of the visual area.
The subject's pose should be display-worthy, powerful, or highly recognizable.
Keep the white background, don't add a complex natural environment.
A small amount of necessary supporting elements may remain, such as a branch, rock, snow, sand, or bark — but must stay minimal.
The subject should cast realistic shadows so it stands in the frame like high-end product photography.

Bottom info area:
Use four minimalist info columns to present educational facts.
Each column contains:
- A thin-line icon
- A small colored title
- 1-3 lines of short text
Columns separated by very thin light-gray vertical lines.
No card frames, no rounded-corner backgrounds, no large blocks of color.

Four info columns:
Column 1:
Title: {feature 1 title}
Caption: {feature 1 short caption}

Column 2:
Title: {feature 2 title}
Caption: {feature 2 short caption}

Column 3:
Title: {feature 3 title}
Caption: {feature 3 short caption}

Column 4:
Title: {feature 4 title}
Caption: {feature 4 short caption}

Bottom summary line:
At the very bottom, centered, place one small gray-text summary line:
{one premium, restrained, memorable educational summary sentence}

Fonts & typography:
Main title: large, black, premium, solid, powerful font.
Subtitle: gray, medium size, slightly wider letter spacing.
English name: small, gray, clean and modern.
Body text: clear, modern font, kept readable.
All text must have enough breathing room.

Color rules:
Background: pure white, very light gray, subtle soft-light gradient.
Main title: black or dark graphite.
Subtitle and body: neutral gray.
The four bottom info titles may use low-saturation accent colors:
warm brown, cool blue, teal, purple, orange.
Color should be used only for icons and small titles — never as large color fills.

Image quality:
2K HD quality, clear detail, sharp subject, realistic lighting.
Subject texture must be believable — fur, scales, shell, skin folds, feathers, or markings.
Avoid distortion, incorrect limbs, incorrect anatomy, blurry subject, low-quality textures, plastic look, cartoonish look.

Prohibited:
Do not use an aged-yellow paper background.
Do not use a complex infographic grid.
Do not use rounded-corner cards.
Do not use thick borders.
Do not use large decorative graphics.
Do not add unrelated logos.
Do not add unnecessary small text.
Do not make the subject too small.
Do not let text overlap the subject.
Do not overcrowd the bottom info area.
Do not produce a childish, cartoonish, or cheap-display-board look.

Final output:
Generate one 9:16 vertical, premium, clean, high-visual-impact, Apple-style nature science-education poster.
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "Movie Poster",
  "theme": "Interstellar Journey",
  "typography": {
    "headline": "BEYOND STARS",
    "subheading": "A New Era Begins",
    "layout": "Centered, bold cinematic font, bottom heavy"
  },
  "visuals": {
    "subject": "Silhouette of an astronaut looking at a glowing nebula",
    "style": "Cinematic lighting, high contrast, dramatic shadows",
    "color_palette": "Deep space blue, glowing orange accents"
  },
  "vibe": "Epic, mysterious, vast"
}
```

**Pitfall guide**

- **Don't be lazy**: spell out exactly "what the key visual actually is" — don't just say "make a poster" and expect a masterpiece.
- **Hard-code the copy**: write out the headline and subheading explicitly, or the model will improvise and add random, meaningless text.
- **Lock the structure first for sports posters**: sports campaigns easily turn into messy collages — decide "single key visual / triptych / data-doodle" first, before writing the subject and copy.
- **Props are the compositional skeleton**: for props like rackets, dumbbells, sneakers, specify their angle, scale, and position, or the model tends to render them as generic background decoration.
- **Lock the title first for typography posters**: for concept typography posters, explicitly require that "the title must be spelled exactly correctly and be the dominant visual," or you'll easily end up with a pretty but unreadable text-effect image.
- **The image must interact with the type**: the person, object, or scene must be embedded in, overlapping, passing through, or supporting the letterforms — placing it just alongside them will look like decorative stock art.
- **Ban moodboard-style results**: explicitly require "single poster only" to avoid the model generating a multi-option display board, a process draft, or a sample collage.
- **Enlarge the subject**: in nature science-education posters, the subject animal must be dramatically enlarged, occupying 50%-70% of the visual area, to ensure it's the strongest visual center.
- **Keep information minimal**: follow the "few but precise" principle — the bottom info area should use only a four-column minimalist layout, avoiding crowding and visual clutter.
- **Keep the style consistent**: strictly follow the Apple-style minimalist look — pure white background, clean typography, soft studio lighting — avoiding traditional infographic elements like cards or rounded-corner frames.

<a name="tpl-product"></a>

### Products & E-commerce

**Standard template**

```text
Generate a main e-commerce image for [product name], with selling points [selling point 1] and [selling point 2].
Scene: [solid-color studio shot/lifestyle scene], shot: [close-up/half-body/full view].
Material detail: [material keywords], lighting: [soft light/side light/rim light].
Extra elements: [price badge/selling-point icon/promo text].
Output: product-display image ready to use directly on an e-commerce platform.
```

**Personalized beauty-recommendation report template**

```text
You are a professional beauty consultant + facial-analysis system + brand visual-design system.
Goal: based on [a user selfie] and [a lipstick brand], generate a vertical lipstick-recommendation report infographic that includes "analysis + recommendation + swatch test + occasion suggestions."

Input parameters:
User image: [user selfie]
Brand: [Dior / YSL / Armani / Chanel / TF / other brand]
Style preference (optional): [work-appropriate / soft / statement / mood / brightening priority]
Number of recommendations: [3-5]

Analysis layer:
- Determine skin tone: cool / warm / neutral (including value/brightness)
- Determine temperament: cool & aloof / gentle / vivid / clean / mature
- Determine lip baseline: natural lip color depth, lip shape, suitable intensity
- Output one summary sentence: "Better suited to [color family] + [saturation] + [texture] lipstick direction"

Recommendation layer:
From [brand], select [3-5] differentiated shades, each including:
- Shade name
- Color-family tag
- On-face effect
- Recommended occasion

Brand visual layer:
Automatically generate a visual tone based on [brand], using only a small amount of brand accent color for titles, thin lines, small icons, and local accents.
Example: YSL — high-contrast black and gold; Dior — French soft-focus gray-white; Armani — low-saturation matte; Chanel — minimalist black and white; TF — dark cinematic feel.

Layout structure:
Top-left: user input image + skin-tone analysis
Top-right: one analysis conclusion sentence
Middle: a 3-5 column lip-swatch matrix on the same face, one shade per column
Bottom: a decisive personal recommendation

Visual requirements:
High-end beauty-editorial visual, structured information-visualization layout, realistic skin texture, precise lip color, consistent lighting, 9:16 vertical, 8K.
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "E-commerce Hero Image",
  "product": {
    "name": "Noise Cancelling Headphones",
    "material": "Matte black finish with metallic accents",
    "angle": "3/4 profile, floating slightly"
  },
  "setting": {
    "background": "Minimalist studio setup, soft gray gradient",
    "lighting": "Softbox overhead, sharp rim light on edges"
  },
  "copywriting": {
    "badges": ["NEW", "$299"],
    "slogan": "Silence the World"
  },
  "constraints": "Commercial photography quality, hyper-realistic textures"
}
```

**Pitfall guide**

- **Material and lighting are everything**: always stack material keywords (e.g. "matte texture") and lighting keywords (e.g. "rim light") — a product shot with no light-and-shadow instantly looks like a flea-market photo.
- **Don't cover the whole image with promo text**: give only 1-2 core lines of copy (e.g. "New Arrival") — too much text ruins the image.
- **Analyze before rendering**: for beauty-recommendation content, don't let the model jump straight to shades — first require it to analyze skin tone, temperament, and lip baseline, then map that conclusion to shade recommendations.
- **Brand should only be an accent**: brand tone should show up in thin lines, accent colors, font character, and lighting — don't fill the frame with a logo or large color blocks.
- **Lock the same face for the swatch matrix**: explicitly state "same face, only lip color changes," or the model tends to render a different person for each shade.

<a name="tpl-brand"></a>

### Brand & Logos

**Standard template**

```text
Design a brand-visual concept for [brand name].
Brand keywords: [keyword 1], [keyword 2], [keyword 3].
Include: logo direction [geometric/wordmark/pictorial], supporting graphics, primary/secondary colors, application mockups.
Style: [modern/premium/approachable], industry: [industry], audience: [audience].
Output: a consistent-style brand-identity visual.
```

**Full brand-identity-kit template**

```text
You are a top-tier brand agency creative director. The goal is to deliver a complete brand-identity system for [business/product], covering logo, color palette, typography, tone of voice, and application touchpoints.

Input info:
Business name: [business name]
Business description: [one-sentence description]
Industry: [industry]
Target audience: [detailed description]
Competitors: [3-5]
Brand personality: [5 keywords]
Feelings it should evoke: [trust / excitement / luxury / closeness / power / other]
Visual identities you like: [3 references]
Visual identities you dislike: [3 counter-examples]
Design budget: [free / paid]

Please output:
1. Brand strategy foundation: brand archetype, core promise, positioning, differentiation, and one unique keyword.
2. Logo concepts: generate 3-5 completely different logo directions, each explaining the core visual concept, shape language, symbolism, typography direction, first-glance emotion, and applicable touchpoints.
3. Color system: primary color, secondary colors, accent color, neutrals, HEX codes, psychological rationale, usage rules, and forbidden combinations.
4. Typography system: headline font, body font, accent font, size hierarchy, letter spacing, line height, and free alternatives.
5. Application touchpoints: business card, app icon, website homepage, social-media template, billboard or packaging mockups.
6. Brand rules: 3 core brand rules that should never be broken.

Output format:
A structured brand book that any designer, developer, or AI tool can understand and reuse within 10 minutes.
```

**Brand touchpoint-system visual board template**

```text
Generate a high-end brand touchpoint-system visual board for [brand name] — not a single poster, but a complete set of brand-application showcases.

Brand positioning: [industry/lifestyle/product category]
Core temperament: [keyword 1], [keyword 2], [keyword 3]
Key-visual scene: [core product/service/experience], placed on [material surface/spatial scene], shown with [lighting] and [lens].

The touchpoint system must include:
- A main product hero shot
- Brand materials: packaging box / tote bag / cup / label / sticker / seal, etc.
- Menu card / price list / small typography sample
- A lifestyle scene or a snippet of the user experience
- Consistent application of color, type, and graphic language across the different touchpoints

Design language:
[modern minimalist/Japanese-style whitespace/luxury editorial/tech brand], primary color [color], secondary color [color], generous whitespace, refined materials, realistic shadows, small text clearly readable.

Composition requirements:
Like a top design agency's pitch page — all touchpoints neat but not rigid, the main visual most prominent, supporting materials clearly hierarchical, overall feel of a coherent, implementable brand system.

Constraints:
Do not generate only a single logo; do not cram all the materials into a messy collage; do not use random gibberish text; do not let the packaging, menu, and stickers feel stylistically disconnected from each other.
```

**Brand-wrapped product-ad template**

```text
Input: [product image], [brand identity], [output format]

PHASE 1 / ANCHOR: describe [brand identity] in 2 lines, including palette, materials, lighting, and mood.
PHASE 2 / INJECT: place [product] into this brand world — the product must follow the brand's temperament and environmental language.
PHASE 3 / FORMAT: specify [output format], e.g. hero image, square ad, vertical story, or e-commerce header.
PHASE 4 / SIGNATURE: add [brand elements], e.g. grain, shadow, overlay texture, packaging symbol, or graphic border.

Variables:
[brand identity] / [product] / [output format] / [brand elements]

Goal: when swapping in different products under the same brand, the visual world stays consistent, and the ad image still has a clear hero subject and commercial polish.
```

**Brand-personality comic infographic template**

```text
Based on the uploaded [logo/brand visual], generate a 4:5 vertical comic infographic: "What This Brand Feels Like."
Goal: turn the brand into a perceivable personality character, and explain how it talks, acts, sells, responds to competitors, and handles criticism.
Core rule: all colors, clothing, poses, tone, and graphic elements must come from the logo and brand keywords.
Main visual: a personified brand character whose clothing, expression, and pose embody [brand temperament].
Surrounding structure: 6-8 small comic panels, each with a short title, action, speech bubble, or inner monologue.
Supporting modules: Voice tone, Energy level, Social behavior, Communication style, DO / DON'T.
Style: comic + editorial infographic, expressive but still premium, text short and punchy, richly layered composition.
Constraints: no generic marketing jargon, no empty areas, don't turn the brand personality into a random unrelated character.
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "Brand Identity Design",
  "brand": {
    "name": "Nova Dynamics",
    "industry": "AI Technology",
    "keywords": ["Innovative", "Minimalist", "Trustworthy"]
  },
  "deliverables": [
    "Logo mark (geometric fusion of a neural network node and a star)",
    "Color palette (Electric Blue and Pure White)",
    "Business card mockup"
  ],
  "style": "Modern corporate, flat vector, high contrast",
  "constraints": "No gradients, scalable vector style, clean white background for logo"
}
```

**Pitfall guide**

- **Subtract, don't add**: define the brand keywords first, then request the visual — results are far more coherent. Don't ask for "a fire-breathing dragon wrapped around a Great Wall pillar with lightning" — that's an illustration, not a logo.
- **Force a plain background**: always emphasize "pure white background" to make later cutout/editing easier.
- **Do brand strategy before the logo**: without a target audience, competitors, and an emotional goal, the logo easily ends up as just a pretty shape with no rationale for why it fits the brand.
- **The logo must be checked in context**: require showing it on a business card, app icon, website, and billboard simultaneously — this quickly reveals problems like illegibility when scaled down or a bad aspect-ratio fit.
- **Write the brand book's "don'ts" too**: besides colors and fonts, also write down "how not to use it," or later extensions will easily break the brand's consistency.

<a name="tpl-architecture"></a>

### Architecture & Spaces

**Standard template**

```text
Generate a design render of a [space type], functioning as [use case].
Style: [modern minimalist/industrial/new Chinese], materials: [wood/stone/metal/glass].
Spatial structure: [open plan/zoned], circulation: [main pathway description].
Lighting: [natural light/artificial lighting plan], time: [day/night scene].
Output: realistic architectural-space render.
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "Architectural Visualization",
  "space": {
    "type": "Modern Cabin Interior",
    "function": "Living room",
    "materials": "Exposed concrete, large floor-to-ceiling glass, warm timber accents"
  },
  "environment": "Nestled in a dense, snowy pine forest visible through the glass",
  "camera": {
    "angle": "Eye-level perspective, wide-angle lens",
    "lighting": "Golden hour, warm interior lights glowing, cool blue ambient light outside"
  },
  "render_quality": "Unreal Engine 5 style, hyper-realistic, 8k resolution, ray tracing"
}
```

**Pitfall guide**

- **Control the camera angle**: perspective distortion is the easiest way for an architectural render to go wrong. Using "eye-level perspective" keeps it in check.
- **Warm/cool contrast**: pairing cool exterior light (blue/gray) with warm interior light (yellow/orange) is a cheat code for making a space feel more premium.

<a name="tpl-photo"></a>

### Photography & Realism

**Standard template**

```text
Subject: [a person/object/street scene], location: [place].
Camera-parameter style: [35mm/85mm], [shallow/deep depth of field], [documentary/cinematic feel].
Lighting: [natural light/night neon/backlit], mood: [mood word].
Detail requirements: [skin texture/material/film grain].
Output: highly realistic photographic-style image.
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "Hyper-realistic Photography",
  "subject": {
    "description": "A weary 30-year-old barista wiping a coffee cup",
    "details": "Subtle sweat on forehead, detailed skin pores, wearing a denim apron"
  },
  "setting": "Dimly lit vintage cafe, rain visible through the window behind",
  "camera_specs": {
    "gear": "Shot on Sony A7R IV, 50mm lens",
    "aperture": "f/1.4 (shallow depth of field, background completely blurred)",
    "lighting": "Cinematic lighting, neon sign reflecting on wet window, soft rim light on subject's hair"
  },
  "film_aesthetic": "Kodak Portra 400 emulation, subtle film grain"
}
```

**Realistic street-candid-moment photography template**

```text
Generate a vertical phone-camera documentary-style photo. Subject: [an unexpected event/everyday moment] happening at a [street/outdoor location].
Subject: [object/person's action/evidence at the scene], must show a realistic material state, e.g. [spreading liquid/scattered ice cubes/creased paper/dust particles].
Environment: [ground material/wall/street elements], keep natural clutter and signs of everyday life.
Lighting: [harsh midday sun/overcast diffuse light/night streetlamp], shadows must match the real light direction; may include [a person's shadow/a street-sign shadow/tree shadow].
Camera: handheld phone-camera POV, slightly overhead or low angle, natural framing, like a candid snapshot.
Image quality: raw unedited photo look, natural colors, realistic texture, high detail.
Negative constraints: no illustration, anime, CGI, studio lighting, overly clean look, overly composed framing, fake liquid, floating objects, brand text, watermark, or poster-design feel.
Output: a believable everyday documentary-style photograph.
```

**Pitfall guide**

- **Add a bit of imperfection**: AI-rendered people that are too perfect end up looking fake. Adding "skin pores," "freckles," "slight film grain" instantly boosts realism.
- **Speak in camera parameters**: use `f/1.4` instead of "shallow depth of field," use `50mm` instead of "half-body shot" — large models respond well to this.
- **Spell out the "imperfections" concretely**: writing "rough brick, scattered ice cubes, natural shadows, slight handheld feel" is more reliable than just writing "realistic."

<a name="tpl-illustration"></a>

### Illustration & Art

**Standard template**

```text
Create an illustration of [subject matter], with [character/main subject] as the protagonist.
Art style: [Japanese anime/watercolor/flat/digital painting], linework: [delicate/bold].
Color scheme: [palette], background: [simple/complex scene].
Composition: [close-up/medium shot/wide shot], emphasize [detail].
Output: high-quality illustration suitable for a cover or social-media post.
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "Artistic Illustration",
  "art_style": "Studio Ghibli inspired anime style",
  "scene": {
    "description": "A giant flying whale carrying a small cozy village on its back",
    "details": "Windmills turning, tiny people looking over the edge, fluffy white clouds"
  },
  "palette": "Vibrant sky blue, lush greens, soft pastel accents",
  "technique": "Cel shading, detailed background art, soft glowing magical aura",
  "mood": "Whimsical, adventurous, nostalgic"
}
```

**Pitfall guide**

- **Lock the brushwork**: if you don't constrain the brushwork (e.g. "thick paint," "watercolor bleed"), illustrations tend to come out in a soulless generic-AI plastic style.
- **Use master-artist names sparingly**: naming a famous artist is tempting, but the model easily copies the composition of their signature work verbatim. Better to extract the artist's stylistic traits (e.g. "Van Gogh's swirling starry-sky brushstrokes") rather than naming the artist directly.

<a name="tpl-character"></a>

### Characters & People

**Standard template**

```text
Design a character-sheet image for [character identity].
Appearance: [age/hairstyle/clothing/accessories], personality: [keywords].
Pose: [standing/dynamic action], expression: [emotion].
World setting: [era/faction/occupation], signature elements: [elements].
Output: a character front view + a style-consistent character-design sheet.
```

**Action-breakdown reference sheet template**

```text
Generate an action-breakdown reference sheet for [a character/person].
Style: [black-and-white line art/3D grayscale/comic storyboard/instructional diagram], clean background, technical-reference feel.
Layout: 4×4 grid, 16 equal-size panels total, thin dividing lines, each panel numbered 1-16 in the top-left corner.
Character consistency: all panels use the same character, keeping face shape, clothing, proportions, and hairstyle consistent.
Each panel's structure:
- Top: action title
- Center: full-body action pose
- Bottom: 3-4 lines of action description
- Overlay: directional arrows, rotation arrows, or motion-trail lines
Action sequence: [the complete steps from a base standing pose to the final action]
Constraints: no complex background, no additional characters, no distracting color, do not change the character's identity.
Output: a clear, readable character action sheet usable as reference for animation/dance/game moves.
```

**Reference photo → 3D collectible-toy template**

```text
Convert the input photo into a high-end 3D collectible-toy figure.
Identity preservation: preserve the original person/character's facial identity, main hairstyle, expression temperament, and recognizable clothing details.
Proportions/styling: chibi-style oversized head, slightly exaggerated features, toy-like body proportions, while keeping an overall premium design feel.
Material: matte vinyl / resin / collectible-figure finish, with detailed skin and clothing material.
Lighting & background: soft studio lighting, clean background [black/white/brand color], subject centered, sharp silhouette.
Texture: ultra-sharp detail, realistic material reflections, 8K render, premium designer-toy aesthetic.
Constraints: do not change the identity, no cheap-plastic look, no multiple characters, no complex background, no text or watermark.
Output: one complete, high-end collectible-toy render.
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "Character Concept Art",
  "character": {
    "identity": "Cybernetic Bounty Hunter",
    "appearance": "Short silver hair, glowing red synthetic left eye, athletic build",
    "attire": "Tactical trench coat with neon piping, holding a plasma rifle"
  },
  "pose": "Dynamic action stance, looking over shoulder with a smirk",
  "environment": "Rainy neon-lit alleyway background (blurred)",
  "style": "Concept art, sharp linework, vibrant cyberpunk palette"
}
```

**Pitfall guide**

- **Break down the facial features**: don't just write "a beautiful girl" — the model doesn't know your beauty standard. Break it down into specifics like "almond-shaped eyes, a high nose bridge, natural full eyebrows."
- **Clothing material matters**: specify the fabric clearly (e.g. "silk," "technical windbreaker fabric") — it instantly makes the character feel more three-dimensional.
- **Lock the grid for action sheets**: an action-breakdown sheet must specify the number of panels, numbering, and each panel's structure explicitly, or the model will cram the steps into one messy diagram.
- **Preserve identity anchors when toy-ifying**: lock the face shape, hairstyle, and recognizable clothing details first, then specify the oversized-head proportions and material — this reduces the chance of it "turning into a different person."
- **Front-load character consistency**: the longer an action sequence, the easier it is for the face or outfit to drift — state "same character, same outfit, same proportions" before the list of actions.

<a name="tpl-scene"></a>

### Scenes & Storytelling

**Standard template**

```text
Generate a scene image for [story theme], taking place at [time + location].
Main event: [event description], protagonist: [character], conflict point: [conflict].
Camera language: [wide establishing shot/medium narrative shot/close-up].
Atmosphere: [tense/warm/suspenseful], tone: [cool/warm/high-contrast].
Output: a concept image with narrative tension.
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "Narrative Scene",
  "story_context": "The exact moment an ancient seal breaks",
  "environment": "Crumbling stone temple overgrown with glowing blue vines",
  "action": "A young explorer dropping their torch as a massive beam of light shoots into the sky",
  "atmosphere": {
    "mood": "Awe-inspiring, terrifying",
    "lighting": "Blinding central light casting long dramatic shadows"
  },
  "camera": "Low angle shot, emphasizing the scale of the light beam"
}
```

**Pitfall guide**

- **There must be a "verb"**: a narrative scene's worst fate is looking like a scenic postcard. Always write in an "event" (e.g. "is collapsing," "just lit the torch") to make the image feel like it's happening.
- **Camera language**: use "low angle shot" or "Dutch angle" to add dramatic tension.

<a name="tpl-history"></a>

### History & Classical Chinese Themes

**Standard template**

```text
Generate an image in a [dynasty/classical-style setting], on the theme of [theme].
Characters: [identity/clothing/props], setting: [imperial court/marketplace/landscape].
Art style: [gongbi fine-line/xieyi freehand/cinematic realism], tone: [color tone].
Cultural detail: [patterns/etiquette/architectural elements].
Output: a classical-themed image with historically accurate atmosphere.
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "Historical/Oriental Scene",
  "setting": "Tang Dynasty Capital City at Night",
  "subject": {
    "identity": "Noblewoman",
    "clothing": "Traditional Ruqun (襦裙) with elaborate floral embroidery",
    "action": "Holding a glowing silk lantern, looking at fireworks"
  },
  "style": "Cinematic realism combined with subtle traditional ink wash (水墨) textures",
  "details": "Accurate Tang architecture, bustling crowd in background",
  "constraints": "No modern elements, historically accurate clothing structure"
}
```

**Pitfall guide**

- **Reject mash-ups**: specify the dynasty explicitly (Tang/Song/Ming), or the model will happily paint someone wearing a Japanese kimono and holding a Qing-dynasty folding fan inside a Tang-dynasty palace.
- **Force out anachronisms**: always add "no modern elements," to stop a classical beauty from suddenly holding a Starbucks cup.

<a name="tpl-document"></a>

### Documents & Publishing

**Standard template**

```text
Produce a [document type, e.g. menu/magazine spread/newspaper layout].
Layout structure: [column count/page margins/heading hierarchy].
Content modules: [cover area/body area/chart area/footnotes].
Typography style: [serif/sans-serif], color scheme: [palette].
Output: a highly readable, properly laid-out publication visual.
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "Editorial Layout",
  "document": "Fashion Magazine Double-page Spread",
  "grid": "3-column grid, wide margins",
  "content": {
    "left_page": "Full-bleed high-fashion photograph of a model in a red dress",
    "right_page": {
      "headline": "THE RED RENAISSANCE",
      "body_text": "(Simulated text blocks)",
      "pull_quote": "\"Color is power.\""
    }
  },
  "typography": "Elegant serif for headlines, clean sans-serif for body",
  "palette": "Monochrome with stark red accents"
}
```

**Corporate brochure system template**

> Source reference: [@MrLarus](https://x.com/MrLarus/status/2056974720893939950)

```text
Please generate a full enterprise-grade commercial brochure visual system for a promotional brochure about [Brand Name]'s [industry / product / solution].

Overall style: high-end, professional, with strong visual impact; avoid a look that feels like an ordinary Word document or generic PowerPoint slide. Use a [dark tech aesthetic / white minimalist business / high-end industrial / artistic brand brochure] style.

The brochure content should include:
1. Front and back cover
2. Company introduction and brand philosophy
3. Core products and technical advantages
4. Application scenarios and solutions
5. Client case studies and partnership models
6. A full-set system preview image

Requirements:
The layout must feel designed, with clear relationships between images, headlines, data, icons, whitespace, and hierarchy; maintain a consistent brand visual system across the whole set; emphasize the polish of real commercial materials, avoiding plain text layout.
```

**Pitfall guide**

- **Structure first**: specifying "column count" and "margins" matters more than piling on style words.
- **Give up on full body text**: don't expect the model to lay out an entire error-free page of body text — let it fill the body with "simulated text blocks," and only hard-write the main headline.
- **System preview**: for corporate-brochure tasks, it's best to also request a full-set preview image, to verify consistency across the cover, inner pages, case-study pages, and contact page.

<a name="tpl-other"></a>

### Other Use Cases

**Standard template**

```text
Task goal: [the type of content you want to generate].
Input constraints: subject [subject], scene [scene], style [style], color [palette].
Quality constraints: resolution [HD/4K], ratio [aspect ratio], composition [composition method].
Output constraints: for use in [use case], must highlight [core information].
Please output one main option + one alternative option.
```

**Concept product-development breakdown board template**

```text
Generate a complete concept product-R&D breakdown board for [product/furniture/installation] — not a single finished render.

Core concept:
Translate [source of inspiration, e.g. crumpled paper/a seashell/origami/a mechanical structure] into [product type].
Design philosophy: [one sentence explaining function and emotion, e.g. "turning controlled chaos into a highly comfortable chair"].

Layout structure:
Center: a high-quality hero render showing the final product's main form, material, and proportions.
Left side: observation and form analysis, including inspiration images, silhouette extraction, structural lines, and fold/texture/load-direction annotations.
Middle: the form-iteration process, showing 3-5 evolution steps from the raw form to the product shell.
Bottom: ergonomics or use-case validation, including dimensions, angles, usage posture, and key functional notes.
Right side: structural integration and material plan, showing a layered breakdown of the internal frame, shell, padding/fabric/connectors.
Very bottom: final materials, surface texture, color scheme, and a key spec table.

Visual style:
Industrial-design proposal board, clean white or light-gray background, a mix of technical-drawing and product-photography style, thin-line annotations, clear titles, realistic shadows, visible material detail.

Constraints:
Don't just render one pretty product — you must show analysis, iteration, ergonomics, structure, materials, and specs.
Don't let text crowd the image — keep only a short title and key labels at each stage.
The product's form should retain recognizable traits from [the source of inspiration], but must still look manufacturable and usable.
```

**JSON advanced template (recommended for agent calls)**

```json
{
  "type": "Custom Generation",
  "objective": "Generate [Specific content]",
  "inputs": {
    "subject": "[Main subject details]",
    "scene": "[Background and context]",
    "style": "[Artistic/Visual style]",
    "palette": "[Color scheme]"
  },
  "quality_constraints": {
    "resolution": "8k, hyper-detailed",
    "aspect_ratio": "[e.g., 16:9]",
    "composition": "[e.g., Rule of thirds]"
  },
  "output_requirements": {
    "usage": "[Intended use case]",
    "focus": "[Key element to highlight]"
  }
}
```

**Pitfall guide**

- **State the purpose first**: start by writing the "task goal and use case" so the model builds the right overall context, then write the visual details.
- **A/B test it**: for general-purpose scenes, it's a good idea to ask the prompt to "generate one main option + one alternative option in a single pass," so you can just pick the better one.

***
