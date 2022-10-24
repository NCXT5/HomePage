<script lang="ts">
    let isDark = false;
    let isHome = false;

    if (typeof window !== "undefined") {
        isDark = window.matchMedia("(prefers-color-scheme: dark)").matches;
        isHome = window.location.pathname === "/";
    }

    interface Link {
        href: string;
        text: string;
    }

    const links: Link[] = [
        {
            href: "/",
            text: "Home",
        },
        {
            href: "/about",
            text: "About",
        },
        {
            href: "/blog",
            text: "Blog",
        }
    ];
</script>

<svelte:head>
    <link rel="icon" href="/logo/NCXTLogoLight.svg" type="image/svg+xml" media="(prefers-color-scheme: light)">
    <link rel="icon" href="/logo/NCXTLogoDark.svg" type="image/svg+xml" media="(prefers-color-scheme: dark)">
    <link rel="icon" href="/logo/NCXTLogoDark.svg" type="image/svg+xml">

    {#if isDark}
        <style>
            body {
                background: #181818;
                color: #fff;
                margin: 0;
            }

            * {
                box-sizing: border-box;
            }

            :root {
                --surface1: #181818;
                --surface2: #202020;

                --dynamic1: rgba(255, 255, 255, 0.03);
                --dynamic2: rgba(255, 255, 255, 0.08);

                --text1: #ffffff;
                --text2: #b3b3b3;

                --animeIn: 50ms;
                --animeOut: 150ms;

                --font: monospace;
                --border: #333;
            }
        </style>
    {:else}
        <style>
            body {
                background: #fff;
                color: #000;
                margin: 0;
            }

            * {
                box-sizing: border-box;
            }

            :root {
                --surface1: #fff;
                --surface2: #f5f5f5;

                --dynamic1: rgba(0, 0, 0, 0.03);
                --dynamic2: rgba(0, 0, 0, 0.08);

                --text1: #000;
                --text2: #333;

                --animeIn: 50ms;
                --animeOut: 150ms;

                --font: monospace;
                --border: #ccc;
            }
        </style>
    {/if}
</svelte:head>

<header>
    <div class="inner">
        <div class="logo">
            {#if isDark}
                <img src="/logo/NCXTLogoTextDark.svg" alt="NCXT Logo">
            {:else}
                <img src="/logo/NCXTLogoTextLight.svg" alt="NCXT Logo">
            {/if}
        </div>

        <div class="links">
            {#each links as link}
                <a href={link.href}>{link.text}</a>
            {/each}
        </div>

        <div class="buttons">
            <button>Button 1</button>
            <button>Button 2</button>
        </div>
    </div>
</header>

{#if isHome}
    <div class="banner">
        <div class="image">
            <img src="https://skylix.net/tempb/xeFx0.gif" alt="banner" />
        </div>

        <div class="inner">
            {#if isDark}
                <img src="/logo/NCXTTextDark.svg" alt="NCXT" />
            {:else}
                <img src="/logo/NCXTTextLight.svg" alt="NCXT" />
            {/if}
        </div>
    </div>
{/if}

<br />
<div class="content">
    <slot />
</div>

<footer>Bottom of HomePage</footer>

<style lang="scss">
    @import "../config.scss";

    body {
        background: $surface1;
    }

    header {
        display: flex;
        justify-content: center;
        align-items: center;
        border-bottom: 1px solid $border;

        .inner {
            display: flex;
            justify-content: space-between;
            height: 70px;
            background: $surface1;
            align-items: center;
            padding: 0 40px;
            width: 100%;
            max-width: 1500px;

            .logo {
                img {
                    height: 45px;
                    transition: $animeOut;
                    cursor: pointer;

                    &:hover {
                        transform: scale(1.1);
                        transition: $animeIn;
                    }
                }
            }

            .links {
                display: flex;
                font-family: $font;

                a {
                    transition: $animeOut;
                    color: $text2;
                    font-size: 16px;
                    height: 70px;
                    text-decoration: none;
                    display: flex;
                    align-items: center;
                    padding: 0 15px;

                    &:hover {
                        color: $text1;
                        transition: $animeIn;
                        background: $dynamic1;
                    }
                }
            }

            .buttons {
                display: flex;
                align-items: center;

                button {
                    height: 70px;
                    background: transparent;
                    border: none;
                    color: $text2;
                    transition: $animeOut;
                    font-family: $font;
                    padding: 0 15px;

                    &:hover {
                        color: $text1;
                        transition: $animeIn;
                        background: $dynamic1;
                    }
                }
            }
        }
    }

    .banner {
        height: 0;
        overflow: hidden;
        position: relative;
        display: flex;
        align-items: center;
        justify-content: center;
        animation: bannerSlideIn 1s ease-in-out forwards;

        .image {
            position: absolute;
            filter: blur(50px);
            min-width: calc(100% + 50px);
            animation: bannerImageAmbientSlideIn 10s ease-in-out infinite;

            img {
                min-width: 100%;
                animation: bannerImageSlideIn 1s ease-in-out forwards
            }
        }

        .inner {
            position: absolute;

            img {
                height: 200px;
            }
        }
    }

    @keyframes bannerSlideIn {
        from {
            height: 0;
        }

        to {
            height: 400px;
        }
    }

    @keyframes bannerImageSlideIn {
        from {
            transform: scale(1.9);
        }

        to {
            transform: scale(1);
        }
    }

    @keyframes bannerImageAmbientSlideIn {
        0% {
            transform: rotate(-4deg);
        }

        50% {
            transform: rotate(4deg);
        }

        100% {
            transform: rotate(-4deg);
        }
    }
</style>
