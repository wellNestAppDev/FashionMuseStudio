This file is vital. It's where you will consolidate all the granular technical details we discussed to "pre-build" the specifications further. This includes:
A. Detailed Supabase Table Schemas:
user_profiles
user_settings
saved_prompts
gallery_items
projects
project_items
inspiration_images (for mood boards/projects)
user_color_palettes
user_style_snippets
user_negative_prompt_sets
collections
collection_items
likes
(For each, list columns, data types (e.g., UUID, TEXT, BOOLEAN, TIMESTAMPTZ, JSONB, TEXT[]), Primary Keys, Foreign Keys and relationships, important constraints, and default values.)
B. Core TypeScript Interfaces:
GenerationOptions (and all its nested interfaces: SceneSetupOptions, ModelCustomizationOptions, LightingSource, etc.)
GalleryItem
SavedPrompt
UserProfile
UserAppSettings
Project, ProjectItem
InspirationImage
UserColorPalette, UserStyleSnippet, UserNegativePromptSet
Collection, CollectionItem
Like
StyleDescription (for the library structure)
(Provide the full TypeScript interface definitions for all of these.)
C. High-Level Logic Flow/Pseudo-code for PromptConstructor.ts:
A step-by-step textual description or pseudo-code detailing how this module processes generationOptions and the styleDescriptionLibrary to create the fluid, comma-separated positive and negative prompts for fal.ai.
D. Input/Output Definition for Supabase Edge Function (fal-image-proxy):
The example JSON structures for what the frontend sends to this Edge Function and what the Edge Function sends back (including success/error states and the Supabase Storage URL for the image).
E. Textual Component Hierarchy Idea for React:
The indented list outlining the main React components and their nesting.
Purpose: This file gives the AI build tool the specific blueprints for your database, your data shapes in TypeScript, and critical logic flows. The MASTER_PROMPT.MD will tell the AI to refer to this file for these details.