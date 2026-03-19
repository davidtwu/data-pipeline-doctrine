# Requirements Document

## Introduction

This feature adds LLM-powered tag clustering and suggestion capabilities to the Quartz-based blog. The system analyzes existing blog content to identify thematic clusters and suggests appropriate tags for posts, helping maintain consistent taxonomy across the blog while reducing the cognitive load of manual tagging.

Given the blog's "zero maintenance" and "no external APIs" philosophy, this feature operates as an on-demand CLI tool that runs locally using a local LLM, producing suggestions that the author can review and apply manually.

## Glossary

- **Tag_Suggester**: The CLI tool that analyzes blog content and suggests tags
- **Content_Analyzer**: The component that reads and parses markdown files from the content directory
- **Cluster_Detector**: The component that identifies thematic groupings across multiple posts
- **Local_LLM**: A locally-running language model (e.g., Ollama with llama3, mistral) that performs text analysis without external API calls
- **Frontmatter**: The YAML metadata block at the top of each markdown file containing title, date, tags, and description
- **Tag_Vocabulary**: The set of existing tags already used across the blog
- **Suggestion_Report**: The output file containing tag recommendations for review

## Requirements

### Requirement 1: Content Analysis

**User Story:** As a blog author, I want the tool to read and parse all my blog posts, so that it can understand the content for tag analysis.

#### Acceptance Criteria

1. WHEN the Tag_Suggester is invoked, THE Content_Analyzer SHALL scan all markdown files in the `content/` directory
2. WHEN a markdown file contains YAML frontmatter, THE Content_Analyzer SHALL extract the title, existing tags, description, and body content
3. WHEN a markdown file has `draft: true` in frontmatter, THE Content_Analyzer SHALL include it in analysis (drafts need tags too)
4. WHEN a markdown file cannot be parsed, THE Content_Analyzer SHALL log a warning and continue processing other files
5. THE Content_Analyzer SHALL build a Tag_Vocabulary from all existing tags found across posts

### Requirement 2: Local LLM Integration

**User Story:** As a blog author who values zero maintenance and no external dependencies, I want the tool to use a local LLM, so that I don't need API keys or internet connectivity.

#### Acceptance Criteria

1. THE Tag_Suggester SHALL use Ollama as the Local_LLM runtime
2. WHEN Ollama is not running, THE Tag_Suggester SHALL display an error message with instructions to start Ollama
3. THE Tag_Suggester SHALL default to the `llama3` model but allow configuration via command-line flag
4. WHEN the configured model is not available in Ollama, THE Tag_Suggester SHALL display an error listing available models
5. THE Tag_Suggester SHALL send content to the Local_LLM without transmitting data to external services

### Requirement 3: Tag Suggestion for Individual Posts

**User Story:** As a blog author, I want to get tag suggestions for a specific post, so that I can quickly tag new content consistently.

#### Acceptance Criteria

1. WHEN invoked with a file path argument, THE Tag_Suggester SHALL analyze only that specific post
2. WHEN analyzing a post, THE Tag_Suggester SHALL provide the Local_LLM with the post content and the existing Tag_Vocabulary
3. THE Tag_Suggester SHALL prioritize suggesting tags from the existing Tag_Vocabulary over inventing new tags
4. WHEN a new tag is suggested that doesn't exist in Tag_Vocabulary, THE Tag_Suggester SHALL mark it as "new" in the output
5. THE Tag_Suggester SHALL suggest between 2 and 5 tags per post
6. THE Tag_Suggester SHALL output suggestions to stdout in a human-readable format

### Requirement 4: Cluster Detection Across All Posts

**User Story:** As a blog author, I want to discover thematic clusters in my content, so that I can identify patterns and potentially reorganize my taxonomy.

#### Acceptance Criteria

1. WHEN invoked with the `--cluster` flag, THE Cluster_Detector SHALL analyze all posts to identify thematic groupings
2. THE Cluster_Detector SHALL group posts by semantic similarity using the Local_LLM
3. THE Cluster_Detector SHALL suggest a descriptive label for each identified cluster
4. THE Cluster_Detector SHALL list which posts belong to each cluster
5. WHEN a post fits multiple clusters, THE Cluster_Detector SHALL list it under each relevant cluster
6. THE Cluster_Detector SHALL identify posts that don't fit well into any cluster as "uncategorized"

### Requirement 5: Suggestion Report Generation

**User Story:** As a blog author, I want suggestions saved to a file, so that I can review them at my leisure and track changes over time.

#### Acceptance Criteria

1. WHEN invoked with the `--output` flag, THE Tag_Suggester SHALL write the Suggestion_Report to the specified file path
2. THE Suggestion_Report SHALL be formatted as markdown for easy reading in Obsidian
3. THE Suggestion_Report SHALL include a timestamp of when the analysis was run
4. THE Suggestion_Report SHALL group suggestions by post, showing current tags and suggested tags
5. WHEN cluster analysis is included, THE Suggestion_Report SHALL contain a separate section for cluster findings
6. THE Tag_Suggester SHALL default to outputting to stdout when no `--output` flag is provided

### Requirement 6: CLI Interface

**User Story:** As a blog author, I want a simple CLI interface, so that I can run tag analysis with minimal friction.

#### Acceptance Criteria

1. THE Tag_Suggester SHALL be invokable via `npx ts-node scripts/suggest-tags.ts` or a package.json script
2. WHEN invoked with `--help`, THE Tag_Suggester SHALL display usage instructions and available flags
3. THE Tag_Suggester SHALL support the following flags: `--cluster`, `--output <path>`, `--model <name>`, `--verbose`
4. WHEN invoked with `--verbose`, THE Tag_Suggester SHALL display progress information during analysis
5. WHEN invoked with no arguments, THE Tag_Suggester SHALL analyze all posts and suggest tags for each
6. THE Tag_Suggester SHALL exit with code 0 on success and non-zero on error

### Requirement 7: Performance and Constraints

**User Story:** As a blog author, I want the tool to complete in reasonable time, so that it doesn't interrupt my writing flow.

#### Acceptance Criteria

1. WHEN analyzing a single post, THE Tag_Suggester SHALL complete within 30 seconds on typical hardware
2. WHEN analyzing all posts, THE Tag_Suggester SHALL process posts sequentially to avoid overwhelming the Local_LLM
3. THE Tag_Suggester SHALL display a progress indicator when analyzing multiple posts
4. THE Tag_Suggester SHALL work offline without any network connectivity after initial Ollama model download
5. THE Tag_Suggester SHALL not modify any source files in the `content/` directory (read-only operation)
