# Prompts completos — Laboratorio 4 ComfyUI

## Configuración base del KSampler

```
model: juggernautXL_v9.safetensors
scheduler: dpm++_2m_karras
vae: sdxl_vae.safetensors
resolution: 1024x1024
```

## Prompt negativo base (todos los experimentos)

```
deformed, blurry, bad anatomy, disfigured, poorly drawn face, extra limb, ugly,
tiling, out of frame, duplicate, watermark, signature, text, low quality,
jpeg artifacts, grainy, overexposed, underexposed, wrong proportions,
multiple faces, mutated hands, extra fingers, cloned face, weird colors
```

---

## NIVEL LEVE — Cambios de contexto e iluminación

### Retrato de estudio
```
positive: professional studio portrait, soft box lighting, neutral grey background,
photorealistic, 85mm lens, shallow depth of field, high detail skin texture,
natural expression, Latino South American man, professional headshot

cfg: 7.0 | steps: 30 | denoise: 0.65 | ip_weight: 0.85
```

### Golden hour
```
positive: golden hour portrait, warm sunset ambient lighting, outdoors,
natural skin tones, DSLR quality, photorealistic, bokeh background,
trees or park setting, warm color grading, Latino South American man

cfg: 7.0 | steps: 30 | denoise: 0.65 | ip_weight: 0.82
```

### Oficina profesional
```
positive: professional corporate office portrait, business attire, modern open
office background, glass walls, warm white lighting, corporate headshot quality,
photorealistic, slight bokeh on background, confident expression

cfg: 7.5 | steps: 30 | denoise: 0.68 | ip_weight: 0.80
```

### Cine noir sobrio
```
positive: film noir style portrait, dramatic chiaroscuro side lighting,
black and white photography, classic 1940s cinema aesthetic, moody shadows,
high contrast, sharp focus on face, cinematic quality, elegant

cfg: 7.5 | steps: 32 | denoise: 0.68 | ip_weight: 0.80
```

---

## NIVEL MODERADO — Cambios de estilo y ambiente

### Investigador en laboratorio futurista
```
positive: futuristic AI research laboratory, holographic screens with data
visualizations, white lab coat, neon blue and white ambient lighting,
cinematic composition, photorealistic, high detail, neural network displays,
clean futuristic interior, Latino South American scientist

cfg: 7.5 | steps: 35 | denoise: 0.75 | ip_weight: 0.70
```

### Editorial de revista
```
positive: high-end magazine editorial portrait, architectural concrete backdrop,
dramatic directional studio lighting, fashion forward styling, GQ or Vogue
aesthetic, sharp and cinematic, moody color grading, professional photography

cfg: 8.0 | steps: 35 | denoise: 0.75 | ip_weight: 0.68
```

### Estética cyberpunk
```
positive: cyberpunk street scene, neon signs in Japanese and Spanish,
rain-wet reflective streets, techwear outfit, augmented reality implants subtle,
night city background, cinematic atmospheric haze, hyper-detailed,
blade runner aesthetic, neon pink and blue color palette

cfg: 8.0 | steps: 38 | denoise: 0.78 | ip_weight: 0.65
```

### Escena urbana nocturna
```
positive: urban night photography, Tokyo-inspired street scene, colorful neon
store signs, rain reflections on pavement, street photography style, cinematic,
50mm lens look, natural night light, dynamic urban environment

cfg: 7.5 | steps: 35 | denoise: 0.75 | ip_weight: 0.68
```

---

## NIVEL FUERTE — Transformaciones semánticas agresivas

### Científico de 1920
```
positive: 1920s scientist portrait, vintage sepia photograph, period-accurate
three-piece suit and tie, old chemistry or physics laboratory, Bunsen burners,
glass apparatus, film grain texture, black and white with sepia toning,
formal stiff pose, vintage portrait photography style

cfg: 8.5 | steps: 40 | denoise: 0.85 | ip_weight: 0.52
```

### Visitando el Tahuantinsuyo
```
positive: Inca noble or warrior in Tahuantinsuyo, Machu Picchu stone citadel
background, Andean mountain peaks, traditional Quechua woven garments in red
and gold, quipu in hand, golden ornaments, epic cinematic photography,
warm golden hour lighting, photorealistic, historically accurate Inca culture,
Peruvian Andean man

cfg: 8.5 | steps: 40 | denoise: 0.85 | ip_weight: 0.50
```

### Explorador polar
```
positive: polar expedition member, Antarctica ice shelf, heavy expedition parka
in orange or red, mountaineering gear, blizzard wind, dramatic cold grey sky,
ice formations in background, National Geographic photography style,
photorealistic, epic environmental portrait

cfg: 8.5 | steps: 40 | denoise: 0.85 | ip_weight: 0.52
```

### Astronauta en la luna
```
positive: astronaut on the lunar surface, NASA Apollo-style spacesuit,
moon dust and craters visible, Earth rising above lunar horizon, dramatic
space photography, deep black starfield, sun lighting from the side,
hyper-detailed spacesuit texture, photorealistic, epic space exploration

cfg: 9.0 | steps: 42 | denoise: 0.88 | ip_weight: 0.45
```

---

## ESCENAS GRUPALES

### Equipo de investigación en IA (3 integrantes)
```
positive: AI research team in a futuristic control room, three scientists
standing together, holographic neural network displays, mixed professional
attire, cinematic wide shot composition, coherent studio lighting from above,
photorealistic, high detail faces, diverse team, collaborative atmosphere

cfg: 8.0 | steps: 40 | denoise: 0.80
ip_weight per person: 0.60 | method: dual IP-Adapter + masked attention
```

### Panel de conferencistas (2 integrantes)
```
positive: international conference panel discussion, two speakers at a modern
podium, professional business suits, large auditorium background, dramatic
stage lighting from above, audience silhouettes visible, prestigious academic
conference atmosphere, photorealistic, cinematic

cfg: 8.0 | steps: 40 | denoise: 0.78
ip_weight per person: 0.62 | method: sequential inpainting with region masks
```

### Tripulación explorando Marte (3 integrantes)
```
positive: Mars exploration crew, three astronauts in advanced spacesuits,
red rocky Martian terrain and dust, distant Olympus Mons in background,
dust storm atmosphere, NASA mission aesthetic, epic wide establishing shot,
photorealistic, dramatic orange-red Martian lighting, heroic composition

cfg: 8.5 | steps: 42 | denoise: 0.82
ip_weight per person: 0.52 | method: ControlNet OpenPose + sequential inpainting
```

### Exploradores en el Tahuantinsuyo (2 integrantes)
```
positive: two Inca explorers or nobles at Machu Picchu citadel, traditional
Andean woven garments in red gold and black, stone temple architecture,
Andean mountain panorama, golden hour warm lighting, epic cinematic photography,
photorealistic, historically inspired, Peruvian Andean men

cfg: 8.5 | steps: 40 | denoise: 0.82
ip_weight per person: 0.58 | method: background-first then sequential subject inpainting
```

---

## Notas de uso del pipeline

### Orden recomendado para escenas grupales
1. Generar el fondo/escena vacía con el prompt completo (sin personas)
2. Definir máscaras por región para cada sujeto (izq, centro, der)
3. Inpainting del sujeto más alejado primero (respeto de planos)
4. Inpainting de sujetos más cercanos
5. Refinamiento global con denoise bajo (0.30–0.40) para unificar iluminación

### Parámetro ip_weight — guía rápida
- 0.80–0.90: Máxima preservación, mínima libertad creativa
- 0.65–0.79: Balance entre identidad y transformación
- 0.50–0.64: Transformación predomina, identidad como guía estructural
- <0.50: Identidad como referencia débil, resultado mayormente semántico

### Prompt tips específicos
- Añadir `Latino, Peruvian, South American` reduce el sesgo de occidentalización de rasgos
- Especificar `photorealistic, high detail skin texture` mejora la calidad de piel
- Para escenas históricas, incluir `historically accurate` reduce la mezcla de culturas
- En cambios fuertes, incluir detalles específicos del contexto (`Machu Picchu stone citadel`, `NASA Apollo-style`) ayuda a la coherencia semántica
