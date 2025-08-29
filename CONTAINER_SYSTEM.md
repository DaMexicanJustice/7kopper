# Container System for Consistent Padding

This document explains the new container system implemented to replace hardcoded `20vw` padding with a more flexible and consistent approach.

## Overview

The new container system provides:
- **Consistent padding** across all screen sizes
- **Responsive breakpoints** that scale appropriately
- **Multiple container widths** for different content types
- **Easy maintenance** through CSS custom properties

## Available Container Classes

### `.container` (Standard)
- **Max-width**: 1200px
- **Use case**: General content sections
- **Example**: Main content areas, hero sections

### `.container-wide`
- **Max-width**: 1400px
- **Use case**: Content that needs more horizontal space
- **Example**: Image galleries, wide layouts

### `.container-narrow`
- **Max-width**: 800px
- **Use case**: Focused content like forms, articles
- **Example**: Contact forms, blog posts

## Responsive Padding

The system automatically adjusts padding based on screen size:

| Screen Width | Padding |
|--------------|---------|
| Mobile (< 640px) | 1rem (16px) |
| Small (640px+) | 1.5rem (24px) |
| Medium (768px+) | 2rem (32px) |
| Large (1024px+) | 3rem (48px) |
| XL (1280px+) | 4rem (64px) |
| 2XL (1536px+) | 5rem (80px) |

## Usage Examples

### Basic Usage
```vue
<template>
  <div class="container">
    <h1>Your Content</h1>
    <p>This content will be centered with consistent padding.</p>
  </div>
</template>
```

### Full-width Background with Contained Content
```vue
<template>
  <section class="full-width-background">
    <div class="container">
      <h2>Content with Background</h2>
      <p>Background spans full width, content is contained.</p>
    </div>
  </section>
</template>
```

### Different Container Types
```vue
<template>
  <!-- Standard content -->
  <div class="container">
    <h2>Standard Layout</h2>
  </div>

  <!-- Wide content -->
  <div class="container-wide">
    <h2>Wide Layout</h2>
  </div>

  <!-- Narrow content -->
  <div class="container-narrow">
    <h2>Narrow Layout</h2>
  </div>
</template>
```

## Migration from 20vw Padding

### Before (Old Approach)
```css
@media (min-width: 1024px) {
  .content {
    padding: 0 20vw;
  }
}
```

### After (New Approach)
```vue
<template>
  <div class="container">
    <div class="content">
      <!-- Your content here -->
    </div>
  </div>
</template>
```

## Benefits

1. **Better Performance**: No viewport calculations on every resize
2. **Consistent Spacing**: Predictable padding across all components
3. **Easier Maintenance**: Centralized padding values in CSS custom properties
4. **Better Accessibility**: More predictable layout for screen readers
5. **Responsive Design**: Graceful scaling across all device sizes

## CSS Custom Properties

The system uses these CSS custom properties (defined in `src/assets/base.css`):

```css
:root {
  --container-padding: 1rem;
  --container-max-width: 1200px;
  --container-max-width-wide: 1400px;
  --container-max-width-narrow: 800px;
}
```

You can override these values in your components if needed:

```css
.my-custom-container {
  max-width: var(--container-max-width);
  margin: 0 auto;
  padding: 0 var(--container-padding);
}
```
