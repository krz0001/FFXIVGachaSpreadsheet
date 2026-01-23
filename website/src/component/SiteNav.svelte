<script lang="ts">
    import { page } from '$app/state';
    import { Github } from '@lucide/svelte';

    interface MenuItem {
        label: string;
        href: string;
    }

    interface MenuCategory {
        label: string;
        id: string;
        items: MenuItem[];
    }

    const menuCategories: MenuCategory[] = [
        {
            label: 'Containers',
            id: 'containers',
            items: [
                { label: 'Coffers', href: '/coffer/' },
                { label: 'Lockboxes', href: '/lockbox/' },
                { label: 'Card Packs', href: '/card/' },
                { label: 'Logograms and Fragments', href: '/logofrag/' }
            ]
        },
        {
            label: 'Instance Drops',
            id: 'instances',
            items: [
                { label: 'Deep Dungeons', href: '/deep/' },
                { label: 'Loot', href: '/loot/' }
            ]
        },
        {
            label: 'Others',
            id: 'others',
            items: [
                { label: 'Eureka Bunnies', href: '/bunny/' },
                { label: 'Occult', href: '/occult/' },
                { label: 'Desynthesis', href: '/desynth/' },
                { label: 'Ventures', href: '/venture/' }
            ]
        },
        {
            label: 'Submarines',
            id: 'submarine',
            items: [
                { label: 'Submarines', href: '/submarine/' }
            ]
        },
    ];

    // Normalize path for comparison (remove trailing slashes)
    function normalizePath(path: string): string {
        return path.replace(/\/$/, '') || '/';
    }

    // Check if a path matches the current page
    function isActivePath(href: string): boolean {
        const currentPath = normalizePath(page.url.pathname);
        const itemPath = normalizePath(href);
        return currentPath === itemPath;
    }

    // Track mobile menu state
    let isMobileMenuOpen = $state(false);

    // Toggle mobile menu
    function toggleMenu() {
        console.log('toggleMenu', isMobileMenuOpen);
        isMobileMenuOpen = !isMobileMenuOpen;
    }

    // Track which dropdown is currently open
    let openDropdown = $state<string | null>(null);

    // Toggle dropdown for a specific category
    function toggleDropdown(categoryId: string) {
        if (openDropdown === categoryId) {
            openDropdown = null;
        } else {
            openDropdown = categoryId;
        }
    }

    // Check if a dropdown is open
    function isDropdownOpen(categoryId: string): boolean {
        return openDropdown === categoryId;
    }
</script>

<nav class="navbar is-dark" aria-label="main navigation">
    <div class="navbar-brand">
        <a class="navbar-item" href="/">
            <strong>FFXIV Gacha</strong>
        </a>

        <button 
            type="button" 
            class="navbar-burger" 
            class:is-active={isMobileMenuOpen}
            aria-label="menu" 
            aria-expanded={isMobileMenuOpen}
            data-target="mainNavbar" 
            onclick={toggleMenu}
        >
            <!-- Keep 4 spans for the burger icon -->
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
        </button>
    </div>

    <div id="mainNavbar" class="navbar-menu" class:is-active={isMobileMenuOpen}>
        <div class="navbar-start">
            {#each menuCategories as category}
                <div class="navbar-item has-dropdown" class:is-active={isDropdownOpen(category.id)}>
                    <button 
                        type="button" 
                        class="navbar-link" 
                        onclick={() => toggleDropdown(category.id)}
                        aria-expanded={isDropdownOpen(category.id)}
                        aria-haspopup="true"
                    >
                        {category.label}
                    </button>

                    <div class="navbar-dropdown">
                        {#each category.items as item}
                            <a class="navbar-item" href={item.href} class:is-active={isActivePath(item.href)}>
                                {item.label}
                            </a>
                        {/each}
                    </div>
                </div>
            {/each}
        </div>

        <div class="navbar-end">
            <a class="navbar-item" href="/about">
                About
            </a>
            <a class="navbar-item" href="https://github.com/Infiziert90/FFXIVGachaSpreadsheet" target="_blank" rel="noopener noreferrer" aria-label="GitHub">
                <Github />
                <span class="is-sr-only">GitHub</span>
            </a>
        </div>
    </div>
</nav>