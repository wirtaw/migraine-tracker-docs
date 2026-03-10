# 🎨 Theming & UI (Dark Mode)

When building an application for users who experience chronic migraines, **accessibility and visual comfort are not optional features—they are core requirements.** A bright white screen can be incredibly painful during an active migraine attack (Photophobia). Here is how we manage our styling to ensure the app is a safe space.

## 🌬️ Tailwind CSS

We use **Tailwind CSS** for all our styling (`tailwind.config.js`). It allows us to rapidly build responsive, consistent widgets without bloated CSS files. We adhere to a calm, muted color palette designed to reduce eye strain.

## 🌗 ThemeContext (Dark Mode First)

**Files:** `src/context/ThemeContext.tsx` & `src/context/ThemeContextMain.tsx`

We built a custom Theme Provider to give users absolute control over their visual experience.

* **System Default:** By default, the app respects the user's operating system preferences via the `prefers-color-scheme` media query.
* **Manual Override:** Users can toggle between Light and Dark mode manually via the `ThemeToggle` component found in the application header.
* **Persistence:** The user's theme preference is saved to `localStorage`, so their screen is never jarringly bright when they return to the app on a high-pain day.

When building new UI widgets, please ensure you use Tailwind's `dark:` modifier to define how your component should look in dark mode!