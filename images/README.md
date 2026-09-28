# Product images

Drop your generated photos in this folder. **Nothing else needs changing** — the page
probes for each basename below in `.jpg`, `.jpeg`, `.png`, `.webp`, `.avif` order and
uses the first one it finds. Until a file appears, the matching `.svg` placeholder shows.

Keep the `.svg` files. They are the fallback.

## Filenames and shapes

Images are cropped with `object-fit: cover`, so exact pixel sizes don't matter — only the
rough shape does. Aim for the aspect ratio given; anything larger is fine and gets scaled down.

| Filename (any image extension) | Aspect | Used for |
|---|---|---|
| `hero` | 5:4 landscape | Hero panel, top right |
| `about` | 5:4 landscape | "Our Story" panel |
| `anarkali-rose-gold` | 3:4 portrait | Product card |
| `anarkali-midnight-blue` | 3:4 portrait | Product card |
| `anarkali-ivory-festive` | 3:4 portrait | Product card |
| `palazzo-printed-cotton` | 3:4 portrait | Product card |
| `palazzo-silk-dupatta` | 3:4 portrait | Product card |
| `palazzo-block-print` | 3:4 portrait | Product card |
| `straight-chanderi` | 3:4 portrait | Product card |
| `straight-embroidered` | 3:4 portrait | Product card |
| `straight-festive-silk` | 3:4 portrait | Product card |

So `anarkali-rose-gold.jpg` or `anarkali-rose-gold.png` both work. Product shots want
**1200x1600** or larger; the two landscape panels want **1600x1280** or larger.

## Prompts

A shared style suffix keeps the set looking like one shoot. Append it to every prompt:

> *...professional ecommerce product photography, garment on an invisible mannequin, plain
> warm off-white studio background, soft even diffused lighting, sharp fabric detail,
> full garment in frame, vertical 3:4 composition, no text, no watermark*

| File | Prompt |
|---|---|
| `anarkali-rose-gold` | A rose gold Anarkali suit, floor-length chiffon with a full flare skirt, gold zari border at the hem, matching sheer net dupatta draped beside it |
| `anarkali-midnight-blue` | A midnight blue Anarkali suit in flowing georgette, floor length, hand-sequinned bodice catching the light, deep navy dupatta |
| `anarkali-ivory-festive` | An ivory festive Anarkali suit, hand-embroidered neckline in gold thread, soft silk lining, subtle cream-on-cream tonal embroidery |
| `palazzo-printed-cotton` | A three-piece printed cotton palazzo set in warm ochre and rust, wide-leg palazzo trousers, short printed kurta, light cotton dupatta, small floral block print |
| `palazzo-silk-dupatta` | A dusty rose art silk palazzo set, wide-leg trousers with contrast maroon piping, matching kurta, draped silk dupatta with a soft sheen |
| `palazzo-block-print` | A sage green hand block-printed palazzo set, Sanganer-style geometric indigo print, vegetable-dyed cotton, wide-leg trousers with kurta and dupatta |
| `straight-chanderi` | A pale sage chanderi cotton-silk straight-cut suit, clean straight kurta with deep side slits, sheer chanderi dupatta with a fine gold border |
| `straight-embroidered` | A terracotta embroidered cotton straight-cut suit, tonal thread work across the yoke and cuffs, fully lined, straight narrow silhouette |
| `straight-festive-silk` | A plum raw silk straight-cut suit with a woven gold Banarasi border at the hem and cuffs, structured festive silhouette |
| `hero` | Bolts of colourful printed Indian cotton and silk fabric stacked on wooden shelves in a small Jaipur textile shop, warm natural light — *landscape 5:4, ignore the mannequin part of the style suffix* |
| `about` | A small tailoring workroom, sewing machine on a wooden table, folded fabric and measuring tape, warm afternoon light through a window, no people — *landscape 5:4, ignore the mannequin part of the style suffix* |

## Before going live

These are illustrations, not photographs of stock you hold. Selling from AI-generated
images of garments a customer will actually receive is misleading and, in several
markets, a consumer-protection problem. Treat them as design placeholders and swap in
real photography of real inventory before taking orders.
