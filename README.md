# Camcorder for OBS

> [!WARNING]
> This project was developed with AI-assisted tooling. Please validate the shader and browser overlay in OBS before relying on them in live production, and be aware that this effect is intentionally stylized and may look different depending on your source, hardware, and scene settings.

Give your webcam or handcam footage the worn, nostalgic look of a 2005 consumer camcorder: soft detail, warm color, tape noise, visible scanlines, digital tracking glitches, and a blinking REC indicator.

This project includes both:

- a GLSL shader filter for OBS
- an HTML-based on-screen display (OSD) for the camcorder label, tape counter, battery, date, and time

It is designed to emulate the feel of a MiniDV or Handycam recording without needing a physical camcorder.

## Features

- Soft, slightly blurry image with analog-like edge treatment
- Warm white balance and saturated color
- Interlaced scanline / combing effect
- Tape wobble and rolling tracking glitch bands
- Video noise and line noise for aged tape texture
- Optional REC indicator and OSD overlay
- Easy setup as an OBS shader filter + browser source

## Files

- `camcorder.shader` — the main visual effect, loaded through OBS's "User-defined shader" filter
- `camcorder_osd.html` — the live camcorder overlay for REC, tape counter, battery, date, and time

## Requirements

- OBS Studio on Windows, macOS, or Linux
- The `obs-shaderfilter` plugin, which adds the "User-defined shader" effect to OBS
- Optional: the free VCR OSD Mono font for the more authentic OSD styling

## Setup

### 1. Add the shader effect

1. In OBS, right-click your source (for example, a webcam or capture source).
2. Open Filters.
3. Click the "+" button under Effect Filters.
4. Choose User-defined shader.
5. Enable Load shader from file.
6. Select `camcorder.shader`.
7. Rename the filter to "Camcorder" if you want it easier to identify.
8. Tweak the controls until the image matches the look you want.

### 2. Add the OSD overlay

1. Add a Browser source above the video source.
2. Set the browser source to Local file.
3. Select `camcorder_osd.html`.
4. Resize the browser source to match your source dimensions.
5. If desired, enable Refresh browser when scene becomes active so the tape counter resets when the scene is re-entered.

### 3. Optional low-frame-rate feel

A shader alone cannot make footage genuinely choppy. If you want the effect to feel more like a cheap camcorder, set your camera or source to around 15 fps in the source properties.

## Shader controls

| Control | Purpose |
| --- | --- |
| Vertical Resolution | Simulates the line count of the picture; 480 is a classic camcorder look. |
| Color Smear | Blurs chroma information sideways, like tape color bleed. |
| Softness | Adds a gentle lens softness. |
| Edge Sharpening | Creates bright and dark halos around edges. |
| Interlace Combing | Adds motion jitter between scanlines. |
| Scanlines | Darkens alternate lines to mimic interlacing. |
| Saturation | Controls color intensity. |
| Contrast | Adjusts contrast and punch. |
| Brightness | Raises or lowers exposure. |
| Highlight Blowout | Adds bloom-like clipping in bright regions. |
| Warm Cast | Shifts the white balance cooler or warmer. |
| Tape Wobble | Adds a slow sideways sway. |
| Tracking Glitch Bands | Creates rolling distortion bands. |
| Video Noise | Adds grain and texture. |
| Tape Line Noise | Adds per-line brightness flicker. |
| Vignette | Darkens the corners for a framed, worn look. |
| REC Dot / REC Dot Size | Controls the blinking red REC indicator. |

## Starting looks

- Clean MiniDV: Video Noise 0.2, Tape Line Noise 0.15, Tracking Glitch Bands 0.1, Tape Wobble 0.3
- Worn tape (default): leave the settings at default
- Heavy damage: Vertical Resolution 360, Color Smear 6, Video Noise 0.8, Tape Line Noise 0.8, Tracking Glitch Bands 0.8, Tape Wobble 2

## Troubleshooting

- The shader shows an error or does nothing: confirm that `obs-shaderfilter` is installed and that the file path in OBS is correct.
- The OSD does not line up with the REC dot: make the browser source the same size as the source it is layered over, then fine-tune the position percentages near the top of `camcorder_osd.html`.
- The video looks too clean or too noisy: raise or lower Video Noise, Tape Line Noise, and Color Smear.

## Notes

This effect is intentionally stylized. It is not meant to be a realistic restoration filter; it is built to evoke the visual identity of older consumer camcorders and analog tape recordings.

## Credits

Created by Dani.
