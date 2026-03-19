# Implementation Plan: Visual Refresh

## Overview

Implement CSS customizations in `quartz/styles/custom.scss` to expand content width, refine typography, improve spacing, and add explorer sidebar truncation. All changes layer on top of Quartz's existing styling system without modifying core files.

## Tasks

- [x] 1. Expand content area width with responsive breakpoints
  - [x] 1.1 Update desktop content width to 750px minimum
    - Modify `.center > article` max-width from 680px to 750px
    - Add explicit desktop media query for viewport ≥1200px
    - _Requirements: 1.1_
  - [x] 1.2 Add tablet responsive styles
    - Add media query for 800px-1200px viewport range
    - Set content area to fill available space (max-width: 100%)
    - _Requirements: 1.2_
  - [x] 1.3 Refine mobile responsive styles
    - Ensure mobile breakpoint (<800px) uses 100% width
    - Add appropriate horizontal padding (1rem)
    - _Requirements: 1.3_

- [x] 2. Refine typography settings
  - [x] 2.1 Adjust body text line-height
    - Update line-height from 1.75 to 1.7 (within 1.6-1.8 range)
    - Apply to p, li, td, tbody elements within article
    - _Requirements: 3.1_
  - [x] 2.2 Enhance paragraph spacing
    - Increase paragraph margin-bottom from 1.2em to 1.4em
    - Ensure clear visual separation between paragraphs
    - _Requirements: 3.2_
  - [x] 2.3 Add heading hierarchy styles
    - Define font-size and margin-top for h1, h2, h3, h4
    - Ensure monotonically decreasing sizes (h1 > h2 > h3 > h4)
    - _Requirements: 3.3_

- [x] 3. Improve spacing and whitespace
  - [x] 3.1 Enhance code block spacing
    - Add padding (1rem) to pre elements
    - Add vertical margins (1.5rem 0) for visual separation
    - _Requirements: 4.2_
  - [x] 3.2 Improve blockquote styling
    - Add vertical margins (1.5rem 0)
    - Add padding (0.75rem 1rem) for internal spacing
    - Ensure border-left provides visual distinction
    - _Requirements: 4.3_
  - [x] 3.3 Add image spacing
    - Add vertical margins (1.5rem 0) to article images
    - Maintain existing border-radius and box-shadow
    - _Requirements: 4.4_

- [x] 4. Checkpoint - Verify core styling
  - Ensure all tests pass, ask the user if questions arise.
  - Build site with `npx quartz build` and visually verify at desktop, tablet, and mobile breakpoints

- [x] 5. Implement explorer sidebar truncation
  - [x] 5.1 Add truncation styles for page links
    - Target `.explorer-content li > a` selector
    - Apply white-space: nowrap, overflow: hidden, text-overflow: ellipsis
    - Set display: block and max-width: 100%
    - _Requirements: 5.1, 5.3_
  - [x] 5.2 Add truncation styles for folder names
    - Target `.folder-container div > a` and `.folder-container div > button span`
    - Apply same truncation properties
    - Ensure folder icons remain properly aligned
    - _Requirements: 5.2_

- [x] 6. Final checkpoint - Complete visual verification
  - Ensure all tests pass, ask the user if questions arise.
  - Build and serve site locally to verify all changes
  - Test explorer truncation with long page titles
  - Verify responsive behavior at all breakpoints

## Notes

- All changes are made exclusively in `quartz/styles/custom.scss`
- No Quartz core files are modified
- Existing CSS variables (`--secondary`, `--light`, etc.) are reused for consistency
- Quartz breakpoints: mobile (<800px), tablet (800-1200px), desktop (≥1200px)
