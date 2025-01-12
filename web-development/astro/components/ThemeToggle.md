## ThemeToggle.astro

```html
<button
    class="theme-toggle p-2 rounded-lg hover:bg-[#e6e9ef] dark:hover:bg-[#181825]"
    aria-label="Toggle Theme"
>
    <!-- SUN ICON (FOR LIGHT MODE) -->
    <svg
        class="w-6 h-6 hidden dark:block"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
    >
        <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"
        ></path>
    </svg>
    <!-- MOON ICON (FOR DARK MODE) -->
    <svg
        class="w-6 h-6 block dark:hidden"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
    >
        <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"
        ></path>
    </svg>
</button>

<!-- THEME TOGGLE FUNCTIONALITY -->
<script>
    const theme = (() => {
        if (typeof localStorage !== "undefined") {
            const storedTheme = localStorage.getItem("theme") ?? "light";
            return storedTheme;
        }
        if (window.matchMedia("(prefers-color-scheme: dark)").matches) {
            return "dark";
        }
        return "light";
    })();

    if (theme === "light") {
        document.documentElement.classList.remove("dark");
    } else {
        document.documentElement.classList.add("dark");
    }

    window.localStorage.setItem("theme", theme);

    const handleToggleClick = () => {
        const element = document.documentElement;
        element.classList.toggle("dark");

        const isDark = element.classList.contains("dark");
        localStorage.setItem("theme", isDark ? "dark" : "light");
    };

    // QUERY SELECTOR ALL TO GET ALL THEME TOGGLE BUTTONS
    const themeToggles = document.querySelectorAll(".theme-toggle");
    themeToggles.forEach((toggle) => {
        toggle.addEventListener("click", handleToggleClick);
    });
</script>
```

<br>

## tailwind.config.mjs

```js
/** @type {import('tailwindcss').Config} */
export default {
	content: ['./src/**/*.{astro,html,js,jsx,md,mdx,svelte,ts,tsx,vue}'],
    darkMode: 'class',
	theme: {
		extend: {},
	},
	plugins: [],
}
```

- `darkMode: 'class'` is what defines the dark theme to be used.