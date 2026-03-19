# Requirements Document

## Introduction

A visual refresh for The Data Pipeline Doctrine blog to create a more professional, modern appearance befitting a principal engineer's technical blog. The refresh focuses on expanding the content area width, refining the color palette, improving typography, fixing explorer sidebar layout issues, and ensuring excellent readability. All changes must be achievable through `quartz/styles/custom.scss` without modifying Quartz core files.

## Glossary

- **Content_Area**: The main article section where blog post content is displayed (`.center > article`)
- **Custom_Stylesheet**: The `quartz/styles/custom.scss` file where all visual customizations are applied
- **Explorer_Sidebar**: The navigation sidebar showing page and folder hierarchy
- **Page_Layout**: The overall grid structure including sidebars, content area, and footer
- **CSS_Variable**: Theme color values defined in `quartz.config.ts` and accessed via `var(--name)` syntax

## Requirements

### Requirement 1: Expanded Content Area Width

**User Story:** As a reader, I want the article content area to be wider, so that I can read longer lines of text comfortably and code blocks display without excessive horizontal scrolling.

#### Acceptance Criteria

1. WHEN a page is viewed on desktop (viewport width ≥ 1200px), THE Content_Area SHALL have a maximum width of at least 750px
2. WHEN a page is viewed on tablet (viewport width 800px-1200px), THE Content_Area SHALL expand to fill available space minus sidebar
3. WHEN a page is viewed on mobile (viewport width < 800px), THE Content_Area SHALL use 100% of available width with appropriate padding
4. THE Content_Area SHALL maintain comfortable reading line lengths (65-85 characters for body text)

### Requirement 2: Professional Color Palette

**User Story:** As a blog owner, I want a refined color palette, so that the site conveys professionalism and credibility appropriate for a principal engineer's blog.

#### Acceptance Criteria

1. THE Custom_Stylesheet SHALL define colors that provide sufficient contrast ratios (WCAG AA minimum 4.5:1 for body text)
2. THE Page_Layout SHALL use a clean, professional color scheme with subtle warmth
3. THE Custom_Stylesheet SHALL ensure link colors are distinguishable from body text
4. THE Custom_Stylesheet SHALL ensure code block backgrounds provide clear visual separation from surrounding content

### Requirement 3: Typography Refinements

**User Story:** As a reader, I want refined typography, so that long-form technical content is easy to read and scan.

#### Acceptance Criteria

1. THE Content_Area SHALL use line-height between 1.6 and 1.8 for body text
2. THE Content_Area SHALL use paragraph spacing that creates clear visual separation between paragraphs
3. THE Custom_Stylesheet SHALL style headings with appropriate visual hierarchy (size, weight, spacing)
4. THE Custom_Stylesheet SHALL ensure code blocks use a monospace font with comfortable line-height for readability

### Requirement 4: Improved Spacing and Whitespace

**User Story:** As a reader, I want generous whitespace, so that the content feels uncluttered and professional.

#### Acceptance Criteria

1. THE Content_Area SHALL have consistent vertical rhythm with appropriate margins between content elements
2. THE Custom_Stylesheet SHALL provide adequate padding around code blocks
3. THE Custom_Stylesheet SHALL style blockquotes with clear visual distinction and appropriate spacing
4. THE Custom_Stylesheet SHALL ensure images have appropriate margins and subtle visual treatment

### Requirement 5: Explorer Sidebar Title Truncation

**User Story:** As a reader, I want the explorer sidebar to display clean, consistent rows, so that I can easily scan and navigate the site structure.

#### Acceptance Criteria

1. WHEN a page title in the Explorer_Sidebar exceeds the available width, THE Custom_Stylesheet SHALL truncate the text with an ellipsis (`...`) and display the full title on hover via the `title` attribute
2. WHEN a folder name in the Explorer_Sidebar exceeds the available width, THE Custom_Stylesheet SHALL truncate the text with an ellipsis (`...`) while keeping the folder icon properly aligned
3. WHEN a page title fits within the available width, THE Explorer_Sidebar SHALL display the full title without truncation
4. WHEN a user clicks on a truncated title, THE Explorer_Sidebar SHALL navigate to the correct page
