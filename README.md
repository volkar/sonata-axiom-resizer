# SonataMedia Axiom resizer

## Settings
 
- **type**: 'resize' or 'crop' (default: resize)
- **width**: resize width (if set)
- **height**: resize height (if set)
- **minside**: shortest side (height for landscape, width for portrait)
- **maxside**: longest side (width for landscape, height for portrait)

'Crop' resizes image first to width/height, then crops to match exact size.

## Install

In services.yaml (example with imagick adapter):
```yaml
services:
    sonata.media.resizer.axiom:
        class: App\Admin\Resizer\AxiomResizer
        arguments: [ '@sonata.media.adapter.image.imagick', 0x00010002, '@sonata.media.metadata.proxy' ]
```

In sonata_media.yaml:

```yaml
sonata_media:
    providers:
        image:
            resizer: sonata.media.resizer.axiom
```

## Examples

All settings must be set inside 'resizer_options' to avoid Sonata's width/height limitations for standart width/height params.

```yaml
sonata_media:
    contexts:
        default:
            formats:
                small: { resizer_options: { type: 'resize', minside: 300 }, quality: 70 }
                large: { resizer_options: { type: 'resize', maxside: 1500 }, quality: 80 }
                exactwidth: { resizer_options: { type: 'resize', width: 1000 }, quality: 80 }
                exactheight: { resizer_options: { type: 'resize', height: 1000 }, quality: 80 }
                avatar: { resizer_options: { type: 'crop', width: 150, height: 200 }, quality: 60 }

    admin_format: { resizer_options: { type: 'crop', width: 400, height: 200 }, quality: 60 }
```

# Contact me

You always welcome to mail me at sergey@volkar.ru