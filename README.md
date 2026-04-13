# Synthetic Image Detection using Gradient Fields

Can math tell real photos from AI-generated fakes? This project is an interactive educational guide that explains a lightweight, math-based technique for detecting synthetic images — **no AI classifier and no metadata required**. It is written for a general audience, not just engineers.

The entire guide is rendered from a single self-contained HTML page ([index.html](index.html)) with a sidebar-driven single-page layout, light/dark themes, and a reading progress bar.

## The Core Idea

Real cameras capture light that obeys the laws of physics (Lambert's law, sensor noise, lens optics). AI diffusion models generate pixels by guessing "what looks right." These two processes leave **mathematically different fingerprints** in how pixel brightness changes across an image. Gradient-field PCA exposes that difference.

Compared to alternatives:

| Method | How it works | Problem |
|---|---|---|
| Metadata inspection | Check embedded camera info | Easy to fake or strip |
| AI classifiers | Train another AI to spot fakes | Fooled by adversarial tricks |
| Visual inspection | Human experts look at it | Slow, expensive, subjective |
| **Gradient Field PCA** | Math-based pixel analysis | Lightweight, interpretable, robust |

## The Pipeline (5 Steps)

1. **Luminance** — Convert RGB to a single brightness channel using `L = 0.2126·R + 0.7152·G + 0.0722·B`.
2. **Gradients** — For every pixel compute horizontal change `Gx` and vertical change `Gy`.
3. **Matrix M** — Stack all N pixel gradient pairs into an `N × 2` matrix.
4. **Covariance C** — Compute the `2 × 2` covariance matrix of `Gx` and `Gy`.
5. **PCA** — Find the dominant axis of variation. Real vs. fake images produce distinctly shaped gradient clouds.

## Guide Structure

The [index.html](index.html) page is organized into four navigation groups:

- **Overview** — Introduction, The Problem, How It Works
- **Deep Dive Steps** — Luminance, Gradients, Matrix, Covariance, PCA
- **Insights** — Real vs Fake, Why It Works, Applications, Limitations
- **Advanced Topics** — Worked Example, Natural Image Statistics, AI Fingerprints, Detection Arms Race, Frequency Domain, Ethics & Society, Build It Yourself

## Viewing the Guide

Open [index.html](index.html) directly in any modern browser — no build step, no dependencies.

```bash
open index.html
```

Use the sidebar to navigate sections and the footer toggle to switch between light and dark themes.

## Applications & Limitations

**Use cases:** news verification, identity/document fraud detection, social-media integrity, legal evidence authentication.

**Known limitations:** heavy JPEG compression, post-processing transforms, evolving AI architectures, unusual real images (e.g. long-exposure, astrophotography), and non-diffusion generators may all reduce accuracy. This is a signal, not a verdict.
