**Project Goal:** Develop "Fashion Muse Studio," a sophisticated web application using **Vite + React + TypeScript**. It will generate high-end, magazine-quality fashion photography, initially using **fal.ai** as the AI image backend. The application will leverage **Supabase** for user authentication (Email/Password, Google, Apple, Facebook OAuth, Magic Links), database (PostgreSQL for user profiles, saved prompts, gallery metadata, projects, collections, user assets, user settings), file storage (user uploads, generated images), and an Edge Function to securely proxy all API calls to `fal.ai`.

**Core Application Architecture & Features (Full V1 Scope):**

Implement all features detailed in the PRD (provided as supplementary context) and utilize the "Cleaned Marked Descriptions List" (also provided as supplementary context) for UI option text.

1.  **User System (Supabase Auth & DB):**
    * Full authentication flows (Email/Password, Google, Apple, Facebook OAuth, Magic Links).
    * `user_profiles` table (schema provided in supplementary context).
    * User Dashboard: Personalized entry point.
    * Application Settings: Store user preferences in a `user_settings` table. Fal.ai API key is a Supabase Secret for the Edge Function.

2.  **Image Generation Core (Fashion Muse Studio Tabs - UI options and descriptive text from "Cleaned Marked Descriptions List"):**
    * **Tab 1: Scene Setup:** All controls for Overall Theme, Emotional Tone, Color Palette, Time/Era, Fashion Trend, Background/Setting, Weather, Time of Day, Props, Gear, Advanced Lighting Tool.
    * **Tab 2: Model Customization:** All controls for Hair, Makeup, Wardrobe, Accessories, Shoes, Body Type, Skin Tone.
    * **Tab 3: Pose & Composition:** Controls for Model Pose (descriptive dropdown), Composition Options.
    * **Tab 4: Magazine Layout Effects:** Controls for Filters & Effects, Magazine Template styles (aesthetic influence).

3.  **Advanced Features:**
    * **Advanced Prompting System:** UI for positive/negative prompts, "Prompt Assistance." "My Prompts" section (CRUD for `saved_prompts` Supabase table - schema provided). Folder/tagging for prompts. Prompt History. Random Prompt Generator.
    * **Image Evolution:** "Evolve/Remix" UI. Select Start/Base Image (upload to Supabase Storage or gallery URL). UI controls for Noise Level, Prompt Weight, Image Weight.
    * **Batch Generation & Variations:** UI to select number of images. "Generate Variations" button.
    * **Integrated AI Upscaling:** "Upscale Image" button. Calls `fal.ai` upscaler via Supabase Edge Function. Result to Supabase Storage & gallery.

4.  **Data & Asset Management (Supabase):**
    * **Image Gallery:** `gallery_items` table (schema provided). CRUD UI. Public/private toggle.
    * **Project-Based Organization:** `projects` table, `project_items` join table (schemas provided). Project management UI.
    * **User-Managed Asset Libraries:** `user_color_palettes`, `user_style_snippets`, `user_negative_prompt_sets` tables (schemas provided). UI to manage & apply.
    * **Collections / Mood Boards:** `collections` table, `collection_items` join table (schemas provided). UI for managing collections.

5.  **Community & Sharing (Supabase RLS for public/private):**
    * Public User Profiles (from `user_profiles` and public items).
    * Community Feed/Explore Page (public `gallery_items`). Sort/filter.
    * Likes: `likes` table (schema provided). UI to like/unlike. Atomic counts.
    * Remixing of public items.

6.  **Professional Utilities:**
    * Optional Watermarking (client-side or Edge Function). Settings in `user_profiles`.
    * Advanced Export Options (PNG/JPEG, quality - client-side).
    * "Simple Mode" with intelligent pre-filling of options based on Theme.

**Core Technical Implementation Modules (TypeScript):**

1.  **`styleDescriptionLibrary.ts`:** Object mapping UI selection keys to detailed descriptive text. **Populate this ENTIRELY from the "Cleaned Marked Descriptions List" (provided as supplementary context).**
2.  **`PromptConstructor.ts`:** Function `buildPrompt(options: GenerationOptions, library: StyleDescriptionLibrary)`: Takes `generationOptions` state and `styleDescriptionLibrary`. Constructs fluid, comma-separated positive/negative text prompts for `fal.ai`. Prepares other `fal.ai` parameters. Avoid explicit headings in the final image prompt string.
3.  **`SupabaseService.ts`:** Wrapper for `@supabase/supabase-js`. Handles all Supabase interactions (Auth, DB CRUD for all tables, Storage). Enforce RLS.
4.  **`FalApiProxyCaller.ts` (Frontend Service):** Calls the `fal-image-proxy` Supabase Edge Function.
5.  **Supabase Edge Function (`fal-image-proxy/index.ts`):** Receives request. Retrieves `FAL_AI_API_KEY` from Supabase secrets. Calls `fal.ai` models (generation/upscaling). Downloads image from `fal.ai` result. Uploads image to Supabase Storage. Returns persistent Supabase Storage URL.
6.  **State Management:** React Context API, Zustand, or Redux Toolkit for `generationOptions`, user session, UI state (TypeScript interfaces provided in supplementary context).
7.  **UI Components:** Modular React components (TypeScript) for all UI and features. Tab navigation.

**Instructions:**
Generate the initial Vite + React + TypeScript project. Implement Supabase integration (Auth, DB schema based on provided details, Storage). Create core service modules and the `fal-image-proxy` Edge Function. Begin with UI for Tab 1 and connect to the generation pipeline. Ensure a modular, well-typed, scalable codebase with good UX (loading states, notifications).