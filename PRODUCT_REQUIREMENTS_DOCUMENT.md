Product Requirements Document: Fashion Muse Studio (Comprehensive V1)
1. Introduction & Vision

Product Name: Fashion Muse Studio
Vision: To be a premier web application that empowers fashion designers, stylists, marketers, and enthusiasts to create high-end, magazine-quality fashion photography and concept art through an intuitive, highly customizable AI-powered interface.
Purpose: Fashion Muse Studio will provide users with granular control over every aspect of image generation, from scene setup and model customization to advanced lighting, posing, and stylistic effects. It leverages powerful AI image generation APIs (initially fal.ai) and a robust backend (Supabase) for user management, data persistence, and secure API operations, fostering a creative community.
Date: May 18, 2025 (Note: Current actual date is May 18, 2025)
2. Goals & Objectives

Provide a user-friendly platform for generating photorealistic and artistic fashion imagery comparable to leading fashion publications.
Offer extensive customization options across scene, model, lighting, composition, and style.
Implement an advanced prompting system allowing users to save, manage, share, and get assistance with prompts.
Enable iterative design through image evolution, batch generation, and variation capabilities.
Support secure user authentication (Email/Password, Google, Apple, Facebook OAuth, Magic Links via Supabase Auth) and personalized dashboards.
Ensure persistent storage for user profiles, saved prompts, image gallery metadata, projects, collections, user-managed assets, and user preferences using Supabase Database and Storage.
Implement community features for sharing, discovering, and interacting with creations.
Securely proxy calls to fal.ai (for generation and upscaling) via Supabase Edge Functions.
Build a modular Vite + React + TypeScript application for scalability and maintainability.
(Business Goal): Establish a foundation for potential future freemium models with premium tiers for advanced features or higher usage limits.
3. Target Audience

Professional Fashion Designers & Stylists: For mood board creation, concept visualization, collection previews, and campaign ideation.
Fashion Marketers & Advertisers: For creating unique ad creatives, social media content, and product showcases.
Fashion Students & Educators: As a tool for learning fashion aesthetics, styling, and visual presentation.
Hobbyists & Fashion Enthusiasts: For exploring creative fashion ideas and generating unique visuals.
Independent Creators & Influencers: For generating distinct visual content for their platforms.
4. Success Metrics

User Adoption & Engagement: Daily/Monthly Active Users (DAU/MAU), user registration rate, session duration, number of images generated per user, frequency of feature use (e.g., evolution, batch, collections).
Feature Adoption: Usage rates for Advanced Prompting, Image Evolution, Projects, Collections, Asset Libraries, and Community features.
Community Growth & Interaction: Number of public creations, likes, (future) comments, remixes, growth in active community members.
User Retention & Satisfaction: Churn rate (especially for future premium tiers), Net Promoter Score (NPS) or CSAT scores from user feedback.
Technical Performance: Successful image generation rates, average generation time, application uptime, API proxy performance.
(If Applicable Later) Conversion rate from free to potential premium tiers, revenue per user.
5. Product Features & Requirements

5.1. Core Application Features
* 5.1.1. User Authentication (via Supabase Auth):
* Secure user registration: Email/Password.
* Login: Email/Password, Google, Apple, Facebook (OAuth via Supabase).
* Passwordless Login: Magic Links (via Supabase).
* Secure session management using @supabase/supabase-js.
* Password recovery mechanism ("Forgot Password").
* RLS policies in Supabase to ensure users can only access/modify their own data unless explicitly public.
* 5.1.2. User Dashboard:
* Personalized landing page after login.
* Display user-specific data fetched from Supabase: quick access to start a new project, overview/links to recent gallery_items or projects, access to saved_prompts.
* (Future) Summarized community activity or notifications.
* Clear navigation to main app sections.
* 5.1.3. User Profile Management (Supabase user_profiles table):
* Users can view and edit their display name, unique public username, avatar (upload to Supabase Storage), bio, and website URL.
* Manage profile visibility (profile_is_public flag).
* (Future) Manage subscription status.
* 5.1.4. Application Settings (User Preferences in Supabase user_settings table):
* User-configurable default AI model (fal.ai), quality, aspect ratio for new projects.
* UI theme preference (dark/light mode).
* Auto-save to gallery toggle.
* Watermark settings: define text watermark, upload logo (to Supabase Storage), enable/disable default watermarking.
* (Note: fal.ai API key is an admin-managed Supabase Secret for the Edge Function, not a user setting).
* 5.1.5. Project-Based Organization ("Projects" - Supabase projects & project_items tables):
* Users can create, name, describe, and manage "Projects."
* Projects act as containers for related gallery_items, saved_prompts, uploaded inspiration_images (from Supabase Storage), user_color_palettes, and notes.
* UI to view project contents, add/remove items, and navigate projects.
* 5.1.6. User-Managed Asset Libraries (Supabase):
* My Color Palettes (user_color_palettes table): Create, name, save custom color palettes (arrays of hex codes). UI to apply to Scene Setup.
* My Style Snippets (user_style_snippets table): Save/manage reusable text snippets for prompts (styles, materials, artist influences, complex prompt components). UI to insert into Advanced Prompting.
* My Negative Prompt Sets (user_negative_prompt_sets table): Create, name, save collections of negative prompts. UI to append to current negative prompt.
* 5.1.7. Collections / Mood Boards (Supabase collections & collection_items tables):
* Users can create, name, and describe "Collections" or "Mood Boards."
* Add items: gallery_items, saved_prompts, inspiration_images (uploaded by user to Supabase Storage), user_color_palettes.
* UI to view, arrange (order), and manage items within a collection.
* Option to make collections public/shareable (controlled by is_public flag).

5.2. Image Generation Core - "Fashion Muse Studio" Tabs(This section details the four main tabs: Scene Setup, Model Customization, Pose & Composition, and Magazine Layout Effects. The UI controls for each option within these tabs will be populated and their descriptive power will come from the "Cleaned Marked Descriptions List" which will be used to build the styleDescriptionLibrary.ts. The AI build tool must implement all listed UI controls and connect them to the generationOptions state object.)
* 5.2.1. Tab 1: Scene Setup: UI controls for Overall Theme, Emotional Tone, Color Palette (including custom colors and Musky Haze toggle), Time/Era, Fashion Trend, Background/Setting (Type and Specifics), Weather, Time of Day, Props (multi-select), Gear (Camera, Lens), and the full Advanced Lighting Tool (multiple configurable light sources with Type, Position, Intensity, Color Temperature; global Natural Light, Flash Fill, Gold Reflectors toggles).
* 5.2.2. Tab 2: Model Customization: UI controls for Hair (Style, Color, Specifics, Voluminous/Extensions toggle), Makeup (Style, Specifics, Flawless Skin toggle, Waterproof toggle), Wardrobe (Style, Items input, Specifics, Body Paint as Wardrobe toggle), Accessories (multi-select), Shoes (Style, Specifics), Body Type (Type options, Specifics), Skin Tone (Tone options, Spray Tan toggle).
* 5.2.3. Tab 3: Pose & Composition: UI controls for Model Pose (initially a comprehensive descriptive dropdown), Composition Options (Shot Type, Framing Style, Rule of Thirds concept, Leading Lines concept, Depth of Field slider/options).
* 5.2.4. Tab 4: Magazine Layout Effects: UI controls for Filters & Effects (multi-select to influence prompt, e.g., Vintage, High-Contrast), Magazine Template styles (dropdown to influence overall aesthetic for single image generation, e.g., "Vogue High Fashion Spread Style").

5.3. Advanced Features (Integrated)
* 5.3.1. Advanced Prompting System:
* Dedicated UI text areas for main (positive) and negative prompts.
* "Prompt Assistance" feature (optional toggle/button) to refine user prompts.
* "My Prompts" section: CRUD operations for saved_prompts table in Supabase (store prompt text, name, tags, generation_options_snapshot (JSONB of settings used), optional thumbnail URL). Folder/tagging organization (metadata in Supabase). Prompt History (client-side localStorage or synced to Supabase).
* Random Prompt Generator ("Muse Spark") with thematic controls.
* 5.3.2. Image Evolution Capabilities:
* "Evolve/Remix" button available on generated images (preview & gallery).
* Option to "Use Start Image" / "Upload Base Image" (uploads to Supabase Storage, URL passed to generation flow).
* If start image has associated prompt/settings (from gallery item), populate UI fields.
* UI Controls (sliders/numerical inputs) for Noise Level/Denoising Strength, Overall Prompt Weight/Strength, and Start Image Influence/Image Weight. These parameters are passed to the fal.ai proxy.
* 5.3.3. Batch Generation & Variations:
* UI to select number of images to generate per prompt execution (e.g., 1-4, subject to fal.ai model capability).
* "Generate Variations" button on existing images (re-runs prompt, ideally with different seeds if controllable via fal.ai).
* 5.3.4. Integrated AI Upscaling:
* "Upscale Image" button on generated images.
* Sends image URL (from Supabase Storage or fal.ai) to a dedicated fal.ai upscaling model via the Supabase Edge Function proxy.
* Option for upscale factor (e.g., 2x, 4x).
* Upscaled image saved to Supabase Storage and linked in gallery_items.

5.4. Image Gallery (Supabase gallery_items table)
* Stores metadata: persistent Supabase Storage URL for image (critical), fal.ai original URL (optional), full prompt used (positive, negative), model ID, aspect ratio, quality, seed (if returned by fal.ai), timestamp, is_public flag, allow_prompt_sharing flag, allow_remixing flag, likes_count, view_count, user-assigned title, user-assigned tags, associated project_id (nullable FK).
* CRUD UI (View, Delete, Add/Edit Title/Tags, Toggle Public/Private). Filter and sort.
* Download image (from Supabase Storage URL).

5.5. Community & Sharing Features (Supabase)
* 5.5.1. Public User Profiles: Viewable via fashionmusestudio.app/u/[username]. Displays public user_profiles info and gallery of public gallery_items.
* 5.5.2. Privacy Control: Clear UI toggles for users to set their gallery_items and saved_prompts to public or private.
* 5.5.3. Community Feed / Explore Page: Displays public gallery_items. Sortable (Newest, Most Popular by likes_count). Filterable (by tags, themes).
* 5.5.4. Interaction - Likes: Authenticated users can like/unlike public gallery_items and saved_prompts. likes table in Supabase (id, user_id, target_type, target_id, created_at). Update likes_count atomically (Supabase Function or careful client logic).
* 5.5.5. Remixing / Evolving Public Creations: "Remix" button on public gallery_items (if allow_remixing = TRUE) loads image and prompt (if allow_prompt_sharing = TRUE) into user's Image Evolution UI.

5.6. Professional Utilities & Output
* 5.6.1. Watermarking (Optional): User configures text/logo (from user_profiles / Supabase Storage). Applied client-side (Canvas API) or via Edge Function before download.
* 5.6.2. Advanced Export Options: Choose format (PNG/JPEG), JPEG quality. Client-side (Canvas API) implementation.

5.7. Other Key Features
* Simple Mode vs. Advanced Mode: UI toggle. Simple mode auto-suggests/pre-fills a coherent set of options in Scene Setup based on selected Overall Theme. Advanced mode gives full manual control. Logic in PromptConstructor and UI managers.

6. Design and UX Considerations
* Aesthetic: Sleek, modern, sophisticated, fashion-forward, inspiring.
* Intuitive Navigation: Clear tab system, accessible controls.
* Progressive Disclosure: Hide advanced settings by default.
* Visual Feedback: Clear loading states, progress for generation, success/error notifications.
* Responsiveness: Primarily desktop/tablet optimized; graceful degradation on smaller screens.
* Performance: Smooth UI, reasonable generation times.

7. Technical Considerations
* Frontend Stack: Vite + React + TypeScript.
* BaaS: Supabase (Auth, PostgreSQL DB, Storage, Edge Functions).
* Use @supabase/supabase-js for all client-Supabase interactions.
* Implement comprehensive Row Level Security (RLS) on ALL Supabase tables.
* AI Image Gen API: fal.ai (for generation and upscaling).
* Secure API Proxy: All calls to fal.ai MUST go through a Supabase Edge Function (fal-image-proxy). This function will use the FAL_AI_API_KEY stored as a Supabase environment secret.
* The Edge Function will also handle downloading the image from fal.ai and uploading it to Supabase Storage, returning the persistent Supabase Storage URL to the client.
* Client-Side Modules (TypeScript):
* styleDescriptionLibrary.ts: Populated from the "Cleaned Marked Descriptions List."
* PromptConstructor.ts: Takes generationOptions and styleDescriptionLibrary to build fluid, comma-separated prompts for fal.ai.
* SupabaseService.ts: Wraps @supabase/supabase-js for Auth, DB, Storage operations.
* FalApiProxyCaller.ts: Calls the fal-image-proxy Supabase Edge Function.
* Services for Projects, Collections, Assets (e.g., ProjectService.ts).
* Client-side image processing for watermark/export.
* State Management: React Context API, Zustand, or Redux Toolkit for managing generationOptions, user session, UI state.
* Modularity & Organization: Code organized into logical components, services, types.

8. Future Considerations / Potential Roadmap
* Integration of additional AI models/APIs.
* True interactive Model Poser Tool (e.g., using 3D libraries).
* Full client-side Magazine Layout tools with text generators and multi-page spreads (post-processing on generated images).
* Advanced community features: comments on creations, following users, user-run challenges.
* Collaboration features (shared projects/mood boards).
* Premium features (e.g., access to more advanced/costly AI models, higher generation quotas, exclusive templates, team features).
* AI-driven trend analysis or style suggestions within the app.

9. Open Questions & Assumptions
* Initial focus is on a comprehensive V1 with the features listed above.
* fal.ai model capabilities (batch size, seed control, specific parameters for evolution/upscaling) will need to be confirmed during implementation of the Edge Function.
* The user will provide the "Cleaned Marked Descriptions List" to populate styleDescriptionLibrary.ts.
* The user will manage their fal.ai API key as a secret within their Supabase project for the Edge Function.