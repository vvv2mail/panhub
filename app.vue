<!DOCTYPE html>
<html lang="zh-CN">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no, viewport-fit=cover">
        <title>PanHub - 全网最全的网盘搜索 · PanHub</title>
        <style>
            @import"https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;700;800&family=Noto+Sans+SC:wght@400;500;700;900&family=Syne:wght@600;700;800&display=swap";:root {
                --primary: #0f766e;
                --primary-dark: #115e59;
                --secondary: #f59e0b;
                --success: #10b981;
                --warning: #d97706;
                --error: #ef4444;
                --bg-primary: #fffdf8;
                --bg-secondary: #f7f3ea;
                --bg-glass: rgba(255,253,248,.86);
                --text-primary: #1f2937;
                --text-secondary: #4b5563;
                --text-tertiary: #9ca3af;
                --border-light: #e5dfd0;
                --border-medium: #d4c7ab;
                --shadow-sm: 0 1px 2px 0 rgba(0,0,0,.05);
                --shadow-md: 0 4px 6px -1px rgba(0,0,0,.1);
                --shadow-lg: 0 10px 15px -3px rgba(0,0,0,.1);
                --shadow-xl: 0 20px 25px -5px rgba(0,0,0,.1);
                --radius-sm: 8px;
                --radius-md: 12px;
                --radius-lg: 16px;
                --radius-xl: 24px;
                --transition-fast: .15s ease;
                --transition-normal: .25s ease;
                --transition-slow: .35s ease
            }

            * {
                box-sizing: border-box
            }

            body,html {
                background: radial-gradient(circle at 12% -10%,#fff3d9 0,transparent 42%),radial-gradient(circle at 90% 8%,#d9f7f3 0,transparent 35%),#fffdf8;
                color: var(--text-primary);
                font-family: Manrope,Noto Sans SC,PingFang SC,Hiragino Sans GB,Microsoft YaHei,sans-serif;
                margin: 0;
                padding: 0;
                -webkit-text-size-adjust: 100%;
                -webkit-tap-highlight-color: transparent;
                -webkit-overflow-scrolling: touch
            }

            ::-webkit-scrollbar {
                height: 8px;
                width: 8px
            }

            ::-webkit-scrollbar-track {
                background: transparent
            }

            ::-webkit-scrollbar-thumb {
                background: var(--border-medium);
                border-radius: 4px
            }

            ::-webkit-scrollbar-thumb:hover {
                background: var(--text-tertiary)
            }

            input[type=email],input[type=number],input[type=password],input[type=search],input[type=text],select,textarea {
                -webkit-appearance: none;
                border-radius: 0;
                -webkit-text-size-adjust: 100%;
                font-family: inherit
            }

            button {
                -webkit-appearance: none;
                -webkit-tap-highlight-color: transparent;
                cursor: pointer;
                font-family: inherit
            }

            @media(max-width: 640px) {
                button,input,select,textarea {
                    min-height:44px;
                    min-width: 44px
                }
            }

            @keyframes fadeIn {
                0% {
                    opacity: 0;
                    transform: translateY(10px)
                }

                to {
                    opacity: 1;
                    transform: translateY(0)
                }
            }

            @keyframes slideInRight {
                0% {
                    transform: translate(100%)
                }

                to {
                    transform: translate(0)
                }
            }

            @keyframes blobFloat {
                0%,to {
                    transform: translate(0) scale(1)
                }

                33% {
                    transform: translate(30px,-50px) scale(1.1)
                }

                66% {
                    transform: translate(-20px,20px) scale(.9)
                }
            }

            @keyframes pulse {
                0%,to {
                    opacity: 1
                }

                50% {
                    opacity: .5
                }
            }
        </style>
        <style>
            .layout[data-v-5c746fb8] {
                display: flex;
                flex-direction: column;
                min-height: 100vh;
                overflow-x: hidden;
                position: relative
            }

            .bg-decoration[data-v-5c746fb8] {
                height: 100%;
                left: 0;
                overflow: hidden;
                pointer-events: none;
                position: fixed;
                top: 0;
                width: 100%;
                z-index: -1
            }

            .blob[data-v-5c746fb8] {
                animation: blobFloat 8s ease-in-out infinite;
                border-radius: 50%;
                filter: blur(48px);
                opacity: .28;
                position: absolute
            }

            .blob-1[data-v-5c746fb8] {
                animation-delay: 0s;
                background: linear-gradient(135deg,#0f766e,#14b8a6);
                height: 400px;
                left: -100px;
                top: -100px;
                width: 400px
            }

            .blob-2[data-v-5c746fb8] {
                animation-delay: 2s;
                background: linear-gradient(135deg,#f59e0b,#fb7185);
                bottom: -50px;
                height: 300px;
                right: -50px;
                width: 300px
            }

            .blob-3[data-v-5c746fb8] {
                animation-delay: 4s;
                background: linear-gradient(135deg,#0ea5e9,#14b8a6);
                height: 250px;
                left: 70%;
                top: 50%;
                width: 250px
            }

            .header[data-v-5c746fb8] {
                backdrop-filter: blur(20px);
                -webkit-backdrop-filter: blur(20px);
                background: var(--bg-glass);
                border-bottom: 1px solid hsla(0,0%,100%,.3);
                box-shadow: var(--shadow-sm);
                position: sticky;
                top: 0;
                z-index: 100
            }

            .nav[data-v-5c746fb8] {
                gap: 16px;
                justify-content: space-between;
                margin: 0 auto;
                max-width: 1100px;
                padding: 16px 24px
            }

            .brand[data-v-5c746fb8],.nav[data-v-5c746fb8] {
                align-items: center;
                display: flex
            }

            .brand[data-v-5c746fb8] {
                color: var(--text-primary);
                font-size: 20px;
                font-weight: 700;
                gap: 8px;
                text-decoration: none;
                transition: transform var(--transition-fast)
            }

            .brand[data-v-5c746fb8]:hover {
                transform: scale(1.05)
            }

            .brand-icon[data-v-5c746fb8] {
                filter: drop-shadow(0 2px 4px rgba(15,118,110,.3));
                font-size: 24px
            }

            .brand-text[data-v-5c746fb8] {
                background: linear-gradient(135deg,var(--primary),var(--secondary));
                -webkit-background-clip: text;
                -webkit-text-fill-color: transparent;
                background-clip: text
            }

            .nav-actions[data-v-5c746fb8] {
                gap: 8px
            }

            .btn-icon[data-v-5c746fb8],.nav-actions[data-v-5c746fb8] {
                align-items: center;
                display: flex
            }

            .btn-icon[data-v-5c746fb8] {
                -webkit-backdrop-filter: blur(10px);
                backdrop-filter: blur(10px);
                background: #ffffff80;
                border: none;
                border: 1px solid hsla(0,0%,100%,.3);
                border-radius: var(--radius-md);
                color: var(--text-primary);
                height: 40px;
                justify-content: center;
                transition: background-color var(--transition-fast),color var(--transition-fast),transform var(--transition-fast),box-shadow var(--transition-fast);
                width: 40px
            }

            .btn-icon[data-v-5c746fb8]:hover {
                background: #fffc;
                box-shadow: var(--shadow-md);
                transform: translateY(-2px)
            }

            .btn-icon[data-v-5c746fb8]:active {
                transform: translateY(0)
            }

            .btn-icon svg[data-v-5c746fb8] {
                stroke: currentColor
            }

            .github-btn[data-v-5c746fb8] {
                color: var(--text-secondary)
            }

            .github-btn[data-v-5c746fb8]:hover {
                background: #fffc;
                color: var(--primary)
            }

            .github-btn svg[data-v-5c746fb8] {
                fill: currentColor;
                stroke: none
            }

            .main[data-v-5c746fb8] {
                animation: fadeIn .5s ease;
                flex: 1;
                margin: 0 auto;
                max-width: 1100px;
                padding: 24px;
                width: 100%
            }

            .toast[data-v-5c746fb8] {
                align-items: center;
                animation: slideInRight .3s ease;
                background: var(--bg-primary);
                border: 1px solid var(--border-light);
                border-radius: var(--radius-md);
                box-shadow: var(--shadow-xl);
                display: flex;
                font-weight: 500;
                gap: 8px;
                padding: 12px 20px;
                position: fixed;
                right: 24px;
                top: 80px;
                z-index: 1000
            }

            .toast[data-v-5c746fb8]:before {
                background: currentColor;
                border-radius: 50%;
                content: "";
                height: 8px;
                width: 8px
            }

            .toast.info[data-v-5c746fb8] {
                border-left: 4px solid var(--primary);
                color: var(--primary)
            }

            .toast.success[data-v-5c746fb8] {
                border-left: 4px solid var(--success);
                color: var(--success)
            }

            .toast.error[data-v-5c746fb8] {
                border-left: 4px solid var(--error);
                color: var(--error)
            }

            @media(max-width: 640px) {
                .nav[data-v-5c746fb8] {
                    padding:12px 16px
                }

                .main[data-v-5c746fb8] {
                    padding: 16px
                }

                .brand[data-v-5c746fb8] {
                    font-size: 18px
                }

                .btn-icon[data-v-5c746fb8] {
                    height: 36px;
                    width: 36px
                }

                .toast[data-v-5c746fb8] {
                    left: 16px;
                    right: 16px;
                    top: 70px
                }

                .blob[data-v-5c746fb8] {
                    filter: blur(40px)
                }
            }

            @media(prefers-color-scheme: dark) {
                [data-v-5c746fb8]:root {
                    --bg-primary:#0d1117;
                    --bg-secondary: #161b22;
                    --bg-glass: rgba(13,17,23,.82);
                    --text-primary: #e6edf3;
                    --text-secondary: #a1aab5;
                    --text-tertiary: #7d8794;
                    --border-light: #21262d;
                    --border-medium: #30363d;
                    --primary: #2dd4bf;
                    --primary-dark: #14b8a6;
                    --secondary: #fbbf24;
                    --shadow-sm: 0 1px 2px 0 rgba(0,0,0,.3);
                    --shadow-md: 0 4px 6px -1px rgba(0,0,0,.4);
                    --shadow-lg: 0 10px 15px -3px rgba(0,0,0,.4);
                    --shadow-xl: 0 20px 25px -5px rgba(0,0,0,.5)
                }

                body[data-v-5c746fb8] {
                    background: radial-gradient(ellipse at 10% 0,rgba(13,148,136,.12) 0,transparent 50%),radial-gradient(ellipse at 85% 5%,rgba(217,119,6,.08) 0,transparent 40%),#0a0e14
                }

                .blob[data-v-5c746fb8] {
                    opacity: .12
                }

                .blob-1[data-v-5c746fb8] {
                    background: linear-gradient(135deg,#0d9488,#2dd4bf)
                }

                .blob-2[data-v-5c746fb8] {
                    background: linear-gradient(135deg,#d97706,#fbbf24)
                }

                .blob-3[data-v-5c746fb8] {
                    background: linear-gradient(135deg,#0891b2,#2dd4bf)
                }

                .header[data-v-5c746fb8] {
                    background: #0d1117c7;
                    border-bottom: 1px solid var(--border-light);
                    box-shadow: 0 1px #0000004d
                }

                .brand-text[data-v-5c746fb8] {
                    background: linear-gradient(135deg,#2dd4bf,#fbbf24);
                    -webkit-background-clip: text;
                    background-clip: text
                }

                .btn-icon[data-v-5c746fb8] {
                    background: #ffffff0f;
                    border: 1px solid var(--border-light);
                    color: var(--text-secondary)
                }

                .btn-icon[data-v-5c746fb8]:hover {
                    background: #ffffff1a;
                    border-color: var(--border-medium);
                    box-shadow: 0 2px 8px #0000004d;
                    color: var(--text-primary)
                }

                .github-btn[data-v-5c746fb8] {
                    color: var(--text-tertiary)
                }

                .github-btn[data-v-5c746fb8]:hover {
                    color: var(--text-primary)
                }

                .toast[data-v-5c746fb8] {
                    background: var(--bg-secondary);
                    border-color: var(--border-light);
                    box-shadow: 0 8px 24px #00000080
                }

                .toast.info[data-v-5c746fb8] {
                    border-left-color: var(--primary);
                    color: var(--primary)
                }

                .toast.success[data-v-5c746fb8] {
                    border-left-color: #34d399;
                    color: #34d399
                }

                .toast.error[data-v-5c746fb8] {
                    border-left-color: #f87171;
                    color: #f87171
                }

                [data-v-5c746fb8]::-webkit-scrollbar-thumb {
                    background: var(--border-medium)
                }

                [data-v-5c746fb8]::-webkit-scrollbar-thumb:hover {
                    background: var(--text-tertiary)
                }
            }

            @media(prefers-contrast:high) {
                .btn-icon[data-v-5c746fb8] {
                    border-width: 2px
                }

                .brand-text[data-v-5c746fb8] {
                    -webkit-text-fill-color: var(--text-primary);
                    color: var(--text-primary)
                }
            }

            @media(prefers-reduced-motion:reduce) {
                [data-v-5c746fb8] {
                    animation-duration: .01ms!important;
                    animation-iteration-count: 1!important;
                    transition-duration: .01ms!important
                }

                .blob[data-v-5c746fb8] {
                    animation: none
                }
            }
        </style>
        <style>
            .home[data-v-7a6a3b93] {
                display: flex;
                flex-direction: column;
                gap: 24px;
                width: 100%
            }

            .hero-row[data-v-7a6a3b93] {
                align-items: stretch;
                background: linear-gradient(145deg,#0f766e1f,#0f766e0a 35%,#f59e0b0f 70%,#0f766e14);
                border-radius: 20px;
                box-shadow: 0 4px 20px -4px #0f766e26;
                display: flex;
                gap: 0;
                overflow: hidden;
                position: relative
            }

            .hero-noise[data-v-7a6a3b93] {
                background-image: url("data:image/svg+xml;charset=utf-8,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 256 256'%3E%3Cfilter id='a'%3E%3CfeTurbulence baseFrequency='.9' numOctaves='4' stitchTiles='stitch' type='fractalNoise'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23a)'/%3E%3C/svg%3E");
                inset: 0;
                mix-blend-mode: overlay;
                opacity: .04;
                pointer-events: none;
                position: absolute;
                z-index: 0
            }

            .hero[data-v-7a6a3b93] {
                flex: 1;
                min-width: 0;
                padding: 24px 28px;
                position: relative;
                text-align: left;
                z-index: 1
            }

            .hero-accent[data-v-7a6a3b93] {
                background: linear-gradient(180deg,var(--primary) 0,var(--secondary) 50%,var(--primary) 100%);
                height: 100%;
                left: 0;
                opacity: 1;
                position: absolute;
                top: 0;
                width: 6px
            }

            .hero-content[data-v-7a6a3b93] {
                padding-left: 12px;
                position: relative;
                z-index: 2
            }

            .hero-badge[data-v-7a6a3b93] {
                animation: heroReveal-7a6a3b93 .6s ease-out both;
                animation-delay: .05s;
                background: #0f766e1f;
                border: 1px solid rgba(15,118,110,.25);
                border-radius: 8px;
                color: var(--primary);
                display: inline-block;
                font-family: Manrope,sans-serif;
                font-size: 11px;
                font-weight: 800;
                letter-spacing: .16em;
                margin-bottom: 10px;
                padding: 6px 12px;
                text-transform: uppercase
            }

            .hero-title[data-v-7a6a3b93] {
                animation: heroReveal-7a6a3b93 .6s ease-out both;
                animation-delay: .12s;
                color: var(--text-primary);
                font-family: Syne,Manrope,sans-serif;
                font-size: 36px;
                font-weight: 800;
                letter-spacing: -.04em;
                line-height: 1.1;
                margin: 0 0 10px;
                max-width: 560px
            }

            .hero-title-line[data-v-7a6a3b93] {
                display: block
            }

            .hero-title-line--accent[data-v-7a6a3b93] {
                background: linear-gradient(120deg,var(--primary) 0,#0d9488 40%,var(--secondary) 100%);
                -webkit-background-clip: text;
                -webkit-text-fill-color: transparent;
                background-clip: text
            }

            .hero-description[data-v-7a6a3b93] {
                animation: heroReveal-7a6a3b93 .6s ease-out both;
                animation-delay: .2s;
                color: var(--text-secondary);
                font-size: 14px;
                line-height: 1.65;
                margin: 0 0 16px;
                max-width: 520px
            }

            .hero-features[data-v-7a6a3b93] {
                display: flex;
                flex-wrap: wrap;
                gap: 12px 20px;
                list-style: none;
                margin: 0;
                padding: 0
            }

            .hero-feature[data-v-7a6a3b93] {
                animation: heroReveal-7a6a3b93 .6s ease-out both;
                background: #fff9;
                border: 1px solid rgba(15,118,110,.2);
                border-radius: 10px;
                color: var(--primary-dark);
                font-size: 12px;
                font-weight: 700;
                letter-spacing: .02em;
                padding: 6px 12px;
                transition: transform .2s ease,box-shadow .2s ease,border-color .2s ease
            }

            .hero-feature[data-v-7a6a3b93]:first-child {
                animation-delay: .28s
            }

            .hero-feature[data-v-7a6a3b93]:nth-child(2) {
                animation-delay: .34s
            }

            .hero-feature[data-v-7a6a3b93]:nth-child(3) {
                animation-delay: .4s
            }

            .hero-feature[data-v-7a6a3b93]:hover {
                border-color: #0f766e59;
                box-shadow: 0 4px 12px #0f766e26;
                transform: translateY(-2px)
            }

            .hero-shape[data-v-7a6a3b93] {
                background: linear-gradient(135deg,#0f766e26,#f59e0b14);
                border-radius: 30% 70% 70% 30%/30% 30% 70% 70%;
                bottom: 10%;
                filter: blur(24px);
                height: 120px;
                pointer-events: none;
                position: absolute;
                right: 8%;
                width: 120px;
                z-index: 0
            }

            @keyframes heroReveal-7a6a3b93 {
                0% {
                    opacity: 0;
                    transform: translateY(12px)
                }

                to {
                    opacity: 1;
                    transform: translateY(0)
                }
            }

            .hero-aside[data-v-7a6a3b93] {
                flex-shrink: 0;
                width: 340px
            }

            .hero-aside[data-v-7a6a3b93] .loading-state,.hero-aside[data-v-7a6a3b93] .tag-cloud-placeholder,.hero-aside[data-v-7a6a3b93] .tag-cloud-wrap {
                background: transparent;
                border: none;
                border-radius: 0;
                box-shadow: none
            }

            .hero-aside[data-v-7a6a3b93] .tag-cloud-wrap {
                min-height: 260px;
                padding: 12px 16px
            }

            .hero-aside[data-v-7a6a3b93] .hot-tagcloud {
                height: 240px!important
            }

            .stats-bar[data-v-7a6a3b93] {
                animation: fadeIn .4s ease;
                -webkit-backdrop-filter: blur(10px);
                backdrop-filter: blur(10px);
                background: var(--bg-primary);
                border: 1px solid var(--border-light);
                border-radius: var(--radius-lg);
                box-shadow: var(--shadow-md);
                padding: 16px
            }

            .stats-content[data-v-7a6a3b93] {
                display: flex;
                flex-direction: column;
                gap: 16px
            }

            .stats-main[data-v-7a6a3b93] {
                flex-wrap: wrap;
                gap: 16px
            }

            .stat-item[data-v-7a6a3b93],.stats-main[data-v-7a6a3b93] {
                align-items: center;
                display: flex
            }

            .stat-item[data-v-7a6a3b93] {
                background: var(--bg-secondary);
                border: 1px solid var(--border-light);
                border-radius: var(--radius-md);
                gap: 8px;
                padding: 8px 12px
            }

            .stat-label[data-v-7a6a3b93] {
                color: var(--text-tertiary);
                font-size: 13px;
                font-weight: 500
            }

            .stat-value[data-v-7a6a3b93] {
                color: var(--primary);
                font-size: 18px;
                font-weight: 700
            }

            .loading-indicator[data-v-7a6a3b93] {
                align-items: center;
                background: #0f766e1a;
                border: 1px solid rgba(15,118,110,.2);
                border-radius: var(--radius-md);
                display: inline-flex;
                gap: 8px;
                padding: 8px 12px
            }

            .pulse-dot[data-v-7a6a3b93] {
                animation: pulse 1.5s ease-in-out infinite;
                background: var(--primary);
                border-radius: 50%;
                height: 8px;
                width: 8px
            }

            .loading-text[data-v-7a6a3b93] {
                color: var(--primary);
                font-size: 13px;
                font-weight: 500
            }

            .paused-indicator-bar[data-v-7a6a3b93] {
                align-items: center;
                background: #f59e0b1a;
                border: 1px solid rgba(245,158,11,.3);
                border-radius: var(--radius-md);
                color: #f59e0b;
                display: inline-flex;
                font-weight: 500;
                gap: 8px;
                padding: 8px 12px
            }

            .pause-icon[data-v-7a6a3b93] {
                font-size: 14px
            }

            .paused-text[data-v-7a6a3b93] {
                font-size: 13px
            }

            .platform-filters[data-v-7a6a3b93] {
                align-items: center;
                display: flex;
                flex-wrap: wrap;
                gap: 8px
            }

            .filter-pill[data-v-7a6a3b93] {
                background: var(--bg-secondary);
                border: 1px solid var(--border-light);
                border-radius: 999px;
                color: var(--text-secondary);
                cursor: pointer;
                font-size: 13px;
                font-weight: 500;
                padding: 6px 12px;
                transition: background-color var(--transition-fast),border-color var(--transition-fast),color var(--transition-fast),transform var(--transition-fast),box-shadow var(--transition-fast);
                white-space: nowrap
            }

            .filter-pill[data-v-7a6a3b93]:hover {
                background: var(--bg-primary);
                border-color: var(--border-medium);
                transform: translateY(-1px)
            }

            .filter-pill.active[data-v-7a6a3b93] {
                background: linear-gradient(135deg,var(--primary),var(--secondary));
                border-color: transparent;
                box-shadow: 0 4px 12px #0f766e47;
                color: #fff
            }

            .sorter[data-v-7a6a3b93] {
                align-items: center;
                display: flex;
                gap: 8px
            }

            .sort-select[data-v-7a6a3b93] {
                background: var(--bg-secondary);
                border: 1px solid var(--border-light);
                border-radius: var(--radius-md);
                color: var(--text-primary);
                cursor: pointer;
                font-size: 13px;
                font-weight: 500;
                min-width: 140px;
                padding: 8px 12px;
                transition: background-color var(--transition-fast),border-color var(--transition-fast),box-shadow var(--transition-fast)
            }

            .sort-select[data-v-7a6a3b93]:hover {
                background: var(--bg-primary);
                border-color: var(--border-medium)
            }

            .sort-select[data-v-7a6a3b93]:focus {
                border-color: var(--primary);
                box-shadow: 0 0 0 3px #0f766e1f;
                outline: none
            }

            .results-section[data-v-7a6a3b93] {
                animation: fadeIn .5s ease
            }

            .results-grid[data-v-7a6a3b93] {
                display: grid;
                gap: 16px;
                grid-template-columns: 1fr
            }

            .empty-state[data-v-7a6a3b93] {
                align-items: center;
                animation: fadeIn .4s ease;
                display: flex;
                justify-content: center;
                padding: 48px 24px
            }

            .empty-card[data-v-7a6a3b93] {
                -webkit-backdrop-filter: blur(20px);
                backdrop-filter: blur(20px);
                background: var(--bg-glass);
                border: 1px solid hsla(0,0%,100%,.3);
                border-radius: var(--radius-xl);
                box-shadow: var(--shadow-lg);
                max-width: 400px;
                padding: 32px;
                text-align: center
            }

            .empty-icon[data-v-7a6a3b93] {
                font-size: 48px;
                margin-bottom: 16px;
                opacity: .6
            }

            .empty-card h3[data-v-7a6a3b93] {
                color: var(--text-primary);
                font-size: 20px;
                margin: 0 0 8px
            }

            .empty-card p[data-v-7a6a3b93] {
                color: var(--text-secondary);
                font-size: 14px;
                line-height: 1.6;
                margin: 0
            }

            .error-alert[data-v-7a6a3b93] {
                align-items: center;
                animation: fadeIn .3s ease;
                background: #ef44441a;
                border: 1px solid rgba(239,68,68,.3);
                border-radius: var(--radius-md);
                color: var(--error);
                display: flex;
                font-weight: 500;
                gap: 12px;
                padding: 12px 16px
            }

            .error-icon[data-v-7a6a3b93] {
                font-size: 18px
            }

            .hot-search-section[data-v-7a6a3b93] {
                animation: fadeIn .6s ease
            }

            @media(max-width: 900px) {
                .hero-row[data-v-7a6a3b93] {
                    flex-direction:column
                }

                .hero-aside[data-v-7a6a3b93] {
                    width: 100%
                }
            }

            @media(max-width: 640px) {
                .hero-aside[data-v-7a6a3b93] {
                    display:none
                }

                .hero[data-v-7a6a3b93] {
                    padding: 24px 18px
                }

                .hero-content[data-v-7a6a3b93] {
                    padding-left: 4px
                }

                .hero-badge[data-v-7a6a3b93] {
                    font-size: 10px;
                    letter-spacing: .1em;
                    margin-bottom: 10px
                }

                .hero-title[data-v-7a6a3b93] {
                    font-size: 26px
                }

                .hero-description[data-v-7a6a3b93] {
                    font-size: 14px;
                    margin-bottom: 16px
                }

                .hero-feature[data-v-7a6a3b93] {
                    font-size: 12px;
                    padding: 6px 12px
                }

                .hero-shape[data-v-7a6a3b93] {
                    bottom: 5%;
                    height: 80px;
                    right: 5%;
                    width: 80px
                }

                .stats-bar[data-v-7a6a3b93] {
                    padding: 12px
                }

                .stats-main[data-v-7a6a3b93] {
                    gap: 8px
                }

                .stat-item[data-v-7a6a3b93] {
                    padding: 6px 10px
                }

                .stat-value[data-v-7a6a3b93] {
                    font-size: 16px
                }

                .platform-filters[data-v-7a6a3b93] {
                    gap: 6px
                }

                .filter-pill[data-v-7a6a3b93] {
                    font-size: 12px;
                    padding: 5px 10px
                }

                .sort-select[data-v-7a6a3b93] {
                    font-size: 12px;
                    min-width: 120px
                }

                .empty-card[data-v-7a6a3b93] {
                    padding: 24px
                }

                .empty-icon[data-v-7a6a3b93] {
                    font-size: 36px
                }

                .empty-card h3[data-v-7a6a3b93] {
                    font-size: 18px
                }

                .suggestions-card[data-v-7a6a3b93] {
                    padding: 16px
                }

                .tag[data-v-7a6a3b93] {
                    font-size: 12px;
                    padding: 6px 12px
                }
            }

            @media(prefers-color-scheme: dark) {
                .hero-row[data-v-7a6a3b93] {
                    background:linear-gradient(160deg,#0d948824,#0d94880a 40%,#d9770614 80%,#0d94880f);
                    border: 1px solid var(--border-light);
                    box-shadow: 0 4px 24px -4px #0006
                }

                .hero-accent[data-v-7a6a3b93] {
                    background: linear-gradient(180deg,var(--primary) 0,var(--secondary) 50%,var(--primary) 100%)
                }

                .hero-badge[data-v-7a6a3b93] {
                    background: #0d948833;
                    border-color: #2dd4bf33;
                    color: var(--primary)
                }

                .hero-title-line--accent[data-v-7a6a3b93] {
                    background: linear-gradient(120deg,#2dd4bf,#14b8a6 40%,#fbbf24);
                    -webkit-background-clip: text;
                    background-clip: text
                }

                .hero-description[data-v-7a6a3b93] {
                    color: var(--text-secondary)
                }

                .hero-feature[data-v-7a6a3b93] {
                    background: #0d94881a;
                    border-color: #2dd4bf26;
                    color: var(--primary)
                }

                .hero-feature[data-v-7a6a3b93]:hover {
                    background: #0d948829;
                    border-color: #2dd4bf4d;
                    box-shadow: 0 4px 12px #0d948826
                }

                .hero-shape[data-v-7a6a3b93] {
                    background: linear-gradient(135deg,#0d94881f,#d977060f)
                }

                .hero-noise[data-v-7a6a3b93] {
                    opacity: .03
                }

                .stats-bar[data-v-7a6a3b93] {
                    background: var(--bg-glass);
                    box-shadow: var(--shadow-md)
                }

                .stat-item[data-v-7a6a3b93],.stats-bar[data-v-7a6a3b93] {
                    border-color: var(--border-light)
                }

                .stat-item[data-v-7a6a3b93] {
                    background: var(--bg-secondary)
                }

                .stat-value[data-v-7a6a3b93] {
                    color: var(--primary)
                }

                .loading-indicator[data-v-7a6a3b93] {
                    background: #0d94881f;
                    border-color: #0d948833
                }

                .loading-text[data-v-7a6a3b93] {
                    color: var(--primary)
                }

                .paused-indicator-bar[data-v-7a6a3b93] {
                    background: #d977061a;
                    border-color: #d9770640;
                    color: #fbbf24
                }

                .filter-pill[data-v-7a6a3b93] {
                    background: var(--bg-secondary);
                    border-color: var(--border-light);
                    color: var(--text-secondary)
                }

                .filter-pill[data-v-7a6a3b93]:hover {
                    background: #ffffff0f;
                    border-color: var(--border-medium);
                    color: var(--text-primary)
                }

                .filter-pill.active[data-v-7a6a3b93] {
                    background: linear-gradient(135deg,#0d9488,#14b8a6);
                    box-shadow: 0 4px 12px #0d948859;
                    color: #042f2e
                }

                .sort-select[data-v-7a6a3b93] {
                    background: var(--bg-secondary);
                    border-color: var(--border-light);
                    color: var(--text-primary)
                }

                .sort-select[data-v-7a6a3b93]:hover {
                    background: #ffffff0f;
                    border-color: var(--border-medium)
                }

                .sort-select[data-v-7a6a3b93]:focus {
                    border-color: var(--primary);
                    box-shadow: 0 0 0 3px #0d948826
                }

                .empty-card[data-v-7a6a3b93] {
                    background: var(--bg-glass);
                    border-color: var(--border-light);
                    box-shadow: var(--shadow-lg)
                }

                .empty-card h3[data-v-7a6a3b93] {
                    color: var(--text-primary)
                }

                .empty-card p[data-v-7a6a3b93] {
                    color: var(--text-secondary)
                }

                .error-alert[data-v-7a6a3b93] {
                    background: #f872721a;
                    border-color: #f8727240;
                    color: #f87171
                }
            }

            @media(prefers-contrast:high) {
                .hero-title-line--accent[data-v-7a6a3b93] {
                    -webkit-text-fill-color: var(--primary);
                    background: none
                }

                .filter-pill.active[data-v-7a6a3b93],.hero-badge[data-v-7a6a3b93],.hero-feature[data-v-7a6a3b93],.sort-select[data-v-7a6a3b93],.tag[data-v-7a6a3b93] {
                    border-width: 2px
                }
            }

            @media(prefers-reduced-motion:reduce) {
                .hero-badge[data-v-7a6a3b93],.hero-description[data-v-7a6a3b93],.hero-feature[data-v-7a6a3b93],.hero-title[data-v-7a6a3b93] {
                    animation: none
                }

                .hero-feature[data-v-7a6a3b93]:hover {
                    transform: none
                }

                .empty-state[data-v-7a6a3b93],.error-alert[data-v-7a6a3b93],.hero[data-v-7a6a3b93],.hot-search-section[data-v-7a6a3b93],.results-section[data-v-7a6a3b93],.stats-bar[data-v-7a6a3b93] {
                    animation: none
                }

                .filter-pill[data-v-7a6a3b93]:hover,.sort-select[data-v-7a6a3b93]:hover {
                    transform: none
                }

                .pulse-dot[data-v-7a6a3b93] {
                    animation: none;
                    opacity: .7
                }
            }
        </style>
        <style>
            .cloud-container[data-v-4a8e0845],.hot-search-section[data-v-4a8e0845] {
                width: 100%
            }

            .tag-cloud-wrap[data-v-4a8e0845] {
                -webkit-backdrop-filter: blur(8px);
                backdrop-filter: blur(8px);
                cursor: pointer;
                padding: 20px
            }

            .tag-cloud-placeholder[data-v-4a8e0845],.tag-cloud-wrap[data-v-4a8e0845] {
                background: #ffffff8c;
                border: 1px solid var(--border-light);
                border-radius: 14px;
                min-height: 340px
            }

            .tag-cloud-wrap[data-v-4a8e0845] .hot-tagcloud {
                height: 300px;
                position: relative;
                transform: translateZ(0);
                width: 100%;
                will-change: transform
            }

            .tag-cloud-wrap[data-v-4a8e0845] .hot-tagcloud-item {
                color: var(--primary-dark,#0f766e)!important;
                cursor: pointer;
                font-family: inherit!important;
                font-weight: 600!important;
                transform: translateZ(0);
                transition: opacity .15s ease;
                will-change: transform,opacity
            }

            .tag-cloud-wrap[data-v-4a8e0845] .hot-tagcloud-item:hover {
                opacity: .9
            }

            .loading-state[data-v-4a8e0845] {
                align-items: center;
                -webkit-backdrop-filter: blur(8px);
                backdrop-filter: blur(8px);
                background: #ffffff8c;
                border: 1px solid var(--border-light);
                border-radius: 14px;
                color: var(--text-secondary);
                display: flex;
                flex-direction: column;
                gap: 12px;
                justify-content: center;
                padding: 40px 20px
            }

            .spinner[data-v-4a8e0845] {
                animation: spin-4a8e0845 1s linear infinite;
                border: 3px solid rgba(15,118,110,.2);
                border-radius: 50%;
                border-top: 3px solid var(--primary);
                height: 28px;
                width: 28px
            }

            @keyframes spin-4a8e0845 {
                to {
                    transform: rotate(1turn)
                }
            }

            @media(max-width: 640px) {
                .tag-cloud-wrap[data-v-4a8e0845] {
                    min-height:260px;
                    padding: 12px
                }

                .tag-cloud-wrap[data-v-4a8e0845] .hot-tagcloud {
                    height: 240px
                }

                .loading-state[data-v-4a8e0845] {
                    padding: 24px 12px
                }
            }

            @media(prefers-color-scheme: dark) {
                .tag-cloud-wrap[data-v-4a8e0845] {
                    background:#161b2280;
                    border-color: var(--border-light)
                }

                .tag-cloud-wrap[data-v-4a8e0845] .hot-tagcloud-item {
                    color: var(--primary)!important
                }

                .tag-cloud-wrap[data-v-4a8e0845] .hot-tagcloud-item:hover {
                    color: #fbbf24!important
                }

                .loading-state[data-v-4a8e0845],.tag-cloud-placeholder[data-v-4a8e0845] {
                    background: #161b2280;
                    border-color: var(--border-light)
                }

                .loading-state[data-v-4a8e0845] {
                    color: var(--text-secondary)
                }

                .spinner[data-v-4a8e0845] {
                    border-color: #0d948833;
                    border-top-color: var(--primary)
                }
            }

            .hidden[data-v-4a8e0845] {
                display: none
            }
        </style>
        <style>
            .search[data-v-32c52767],.search-container[data-v-32c52767] {
                width: 100%
            }

            .search-box[data-v-32c52767] {
                align-items: center;
                backdrop-filter: blur(10px);
                -webkit-backdrop-filter: blur(10px);
                background: var(--bg-glass);
                border: 1px solid var(--border-medium);
                border-radius: 18px;
                box-shadow: var(--shadow-lg);
                display: flex;
                gap: 12px;
                overflow: hidden;
                padding: 12px 16px;
                position: relative;
                transition: border-color var(--transition-normal),box-shadow var(--transition-normal),transform var(--transition-normal)
            }

            .search-box[data-v-32c52767]:before {
                background: linear-gradient(90deg,var(--primary),var(--secondary));
                content: "";
                height: 1px;
                left: 0;
                opacity: 0;
                position: absolute;
                right: 0;
                top: 0;
                transition: opacity var(--transition-normal)
            }

            .search-box.focused[data-v-32c52767] {
                border-color: var(--primary);
                box-shadow: 0 10px 26px #0f766e24;
                transform: translateY(-2px)
            }

            .search-box.focused[data-v-32c52767]:before {
                opacity: 1
            }

            .search-box.loading[data-v-32c52767] {
                animation: searchPulse-32c52767 2.2s ease-in-out infinite;
                border-color: var(--primary)
            }

            @keyframes searchPulse-32c52767 {
                0%,to {
                    box-shadow: 0 8px 32px #0f766e38
                }

                50% {
                    box-shadow: 0 8px 40px #0f766e57
                }
            }

            .search-icon[data-v-32c52767] {
                align-items: center;
                color: var(--text-tertiary);
                display: flex;
                flex-shrink: 0;
                justify-content: center;
                transition: color var(--transition-fast)
            }

            .search-box.focused .search-icon[data-v-32c52767] {
                color: var(--primary)
            }

            .search-icon svg[data-v-32c52767] {
                stroke: currentColor
            }

            .search-input[data-v-32c52767] {
                -webkit-appearance: none;
                background: transparent;
                border: none;
                border-radius: 0;
                color: var(--text-primary);
                flex: 1;
                font-size: 16px;
                font-weight: 500;
                min-width: 0;
                outline: none;
                -webkit-text-size-adjust: 100%;
                -webkit-tap-highlight-color: transparent
            }

            .search-input[data-v-32c52767]::-moz-placeholder {
                color: var(--text-tertiary);
                font-weight: 400
            }

            .search-input[data-v-32c52767]::placeholder {
                color: var(--text-tertiary);
                font-weight: 400
            }

            .search-actions[data-v-32c52767] {
                flex-shrink: 0;
                gap: 8px
            }

            .action-btn[data-v-32c52767],.search-actions[data-v-32c52767] {
                align-items: center;
                display: flex
            }

            .action-btn[data-v-32c52767] {
                -webkit-appearance: none;
                border: none;
                border-radius: var(--radius-md);
                cursor: pointer;
                font-size: 14px;
                font-weight: 600;
                gap: 6px;
                padding: 8px 12px;
                transition: background-color var(--transition-fast),color var(--transition-fast),border-color var(--transition-fast),transform var(--transition-fast),box-shadow var(--transition-fast);
                white-space: nowrap;
                -webkit-tap-highlight-color: transparent;
                -webkit-user-select: none;
                -moz-user-select: none;
                user-select: none
            }

            .action-btn[data-v-32c52767]:disabled {
                cursor: not-allowed;
                opacity: .5;
                pointer-events: none
            }

            .action-btn.primary[data-v-32c52767] {
                background: linear-gradient(135deg,var(--primary),#14b8a6);
                box-shadow: 0 4px 12px #0f766e4d;
                color: #fff
            }

            .action-btn.primary[data-v-32c52767]:hover:not(:disabled) {
                box-shadow: 0 8px 18px #0f766e5c;
                transform: translateY(-1px)
            }

            .action-btn.primary[data-v-32c52767]:active:not(:disabled) {
                transform: translateY(0)
            }

            .action-btn.ghost[data-v-32c52767] {
                background: #ffffff80;
                border: 1px solid var(--border-light);
                color: var(--text-secondary);
                padding: 8px
            }

            .action-btn.ghost[data-v-32c52767]:hover {
                background: var(--bg-primary);
                border-color: var(--border-medium);
                color: var(--text-primary)
            }

            .action-btn.ghost[data-v-32c52767]:active {
                background: var(--border-light)
            }

            .action-btn.pause[data-v-32c52767] {
                background: linear-gradient(135deg,#f59e0b,#fbbf24);
                box-shadow: 0 4px 12px #f59e0b4d;
                color: #fff
            }

            .action-btn.pause[data-v-32c52767]:hover:not(:disabled) {
                box-shadow: 0 6px 16px #f59e0b66;
                transform: translateY(-1px)
            }

            .action-btn.pause[data-v-32c52767]:active:not(:disabled) {
                transform: translateY(0)
            }

            .action-btn.resume[data-v-32c52767] {
                background: linear-gradient(135deg,#10b981,#34d399);
                box-shadow: 0 4px 12px #10b9814d;
                color: #fff
            }

            .action-btn.resume[data-v-32c52767]:hover:not(:disabled) {
                box-shadow: 0 6px 16px #10b98166;
                transform: translateY(-1px)
            }

            .action-btn.resume[data-v-32c52767]:active:not(:disabled) {
                transform: translateY(0)
            }

            .action-btn.reset[data-v-32c52767] {
                background: linear-gradient(135deg,#ef4444,#f87171);
                box-shadow: 0 4px 12px #ef44444d;
                color: #fff
            }

            .action-btn.reset[data-v-32c52767]:hover:not(:disabled) {
                box-shadow: 0 6px 16px #ef444466;
                transform: translateY(-1px)
            }

            .action-btn.reset[data-v-32c52767]:active:not(:disabled) {
                transform: translateY(0)
            }

            .paused-indicator[data-v-32c52767] {
                align-items: center;
                animation: pulse-32c52767 2s ease-in-out infinite;
                color: #f59e0b;
                display: flex;
                flex-shrink: 0;
                height: 32px;
                justify-content: center;
                width: 32px
            }

            @keyframes pulse-32c52767 {
                0%,to {
                    opacity: .6;
                    transform: scale(1)
                }

                50% {
                    opacity: 1;
                    transform: scale(1.1)
                }
            }

            .action-btn svg[data-v-32c52767] {
                flex-shrink: 0;
                stroke: currentColor
            }

            .btn-text[data-v-32c52767] {
                display: inline-block
            }

            .loading-spinner[data-v-32c52767] {
                animation: spin-32c52767 .8s linear infinite;
                border: 2px solid rgba(99,102,241,.2);
                border-radius: 50%;
                border-top: 2px solid var(--primary);
                flex-shrink: 0;
                height: 20px;
                width: 20px
            }

            @keyframes spin-32c52767 {
                to {
                    transform: rotate(1turn)
                }
            }

            @media(max-width: 640px) {
                .search-box[data-v-32c52767] {
                    gap:8px;
                    padding: 10px 12px
                }

                .search-icon[data-v-32c52767] {
                    display: none
                }

                .search-input[data-v-32c52767] {
                    font-size: 15px
                }

                .search-actions[data-v-32c52767] {
                    gap: 6px
                }

                .action-btn[data-v-32c52767] {
                    align-items: center;
                    display: flex;
                    font-size: 13px;
                    justify-content: center;
                    padding: 8px 10px
                }

                .action-btn.pause .btn-text[data-v-32c52767],.action-btn.primary .btn-text[data-v-32c52767],.action-btn.reset .btn-text[data-v-32c52767],.action-btn.resume .btn-text[data-v-32c52767] {
                    display: none
                }

                .action-btn.ghost[data-v-32c52767] {
                    padding: 6px
                }

                .action-btn.pause[data-v-32c52767],.action-btn.reset[data-v-32c52767],.action-btn.resume[data-v-32c52767] {
                    padding: 8px
                }

                .loading-spinner[data-v-32c52767] {
                    height: 18px;
                    width: 18px
                }

                .paused-indicator[data-v-32c52767] {
                    height: 28px;
                    width: 28px
                }
            }

            @media(max-width: 360px) {
                .search-box[data-v-32c52767] {
                    padding:8px 10px
                }

                .action-btn[data-v-32c52767] {
                    font-size: 12px;
                    padding: 6px 8px
                }
            }

            @media(prefers-color-scheme: dark) {
                .search-box[data-v-32c52767] {
                    background:var(--bg-glass);
                    border-color: var(--border-light);
                    box-shadow: 0 4px 16px #0000004d
                }

                .search-box[data-v-32c52767]:before {
                    background: linear-gradient(90deg,var(--primary),var(--secondary))
                }

                .search-box.focused[data-v-32c52767] {
                    box-shadow: 0 8px 32px #0d94882e
                }

                .search-box.focused[data-v-32c52767],.search-box.loading[data-v-32c52767] {
                    border-color: var(--primary)
                }

                @keyframes searchPulse-32c52767 {
                    0%,to {
                        box-shadow: 0 8px 32px #0d948829
                    }

                    50% {
                        box-shadow: 0 8px 40px #0d948847
                    }
                }

                .search-icon[data-v-32c52767] {
                    color: var(--text-tertiary)
                }

                .search-box.focused .search-icon[data-v-32c52767] {
                    color: var(--primary)
                }

                .search-input[data-v-32c52767] {
                    color: var(--text-primary)
                }

                .search-input[data-v-32c52767]::-moz-placeholder {
                    color: var(--text-tertiary)
                }

                .search-input[data-v-32c52767]::placeholder {
                    color: var(--text-tertiary)
                }

                .action-btn.primary[data-v-32c52767] {
                    background: linear-gradient(135deg,#0d9488,#14b8a6);
                    box-shadow: 0 4px 12px #0d948859;
                    color: #042f2e
                }

                .action-btn.primary[data-v-32c52767]:hover:not(:disabled) {
                    box-shadow: 0 8px 18px #0d948866
                }

                .action-btn.ghost[data-v-32c52767] {
                    background: #ffffff0f;
                    border-color: var(--border-light);
                    color: var(--text-secondary)
                }

                .action-btn.ghost[data-v-32c52767]:hover {
                    background: #ffffff1a;
                    border-color: var(--border-medium);
                    color: var(--text-primary)
                }

                .action-btn.ghost[data-v-32c52767]:active {
                    background: #ffffff0a
                }

                .action-btn.pause[data-v-32c52767] {
                    background: linear-gradient(135deg,#d97706,#fbbf24);
                    color: #451a03
                }

                .action-btn.resume[data-v-32c52767] {
                    background: linear-gradient(135deg,#059669,#34d399);
                    color: #022c22
                }

                .action-btn.reset[data-v-32c52767] {
                    background: linear-gradient(135deg,#dc2626,#f87171);
                    color: #450a0a
                }

                .paused-indicator[data-v-32c52767] {
                    color: #fbbf24
                }

                .loading-spinner[data-v-32c52767] {
                    border-color: #0d948833;
                    border-top-color: var(--primary)
                }
            }

            @media(prefers-contrast:high) {
                .search-box[data-v-32c52767] {
                    border-width: 3px
                }

                .action-btn.primary[data-v-32c52767] {
                    border: 2px solid #fff
                }

                .action-btn.ghost[data-v-32c52767] {
                    border-width: 2px
                }
            }

            @media(prefers-reduced-motion:reduce) {
                .action-btn[data-v-32c52767],.search-box[data-v-32c52767] {
                    transition: none
                }

                .search-box.loading[data-v-32c52767] {
                    animation: none
                }

                .loading-spinner[data-v-32c52767] {
                    animation: none;
                    opacity: .7
                }

                .action-btn.primary[data-v-32c52767]:active:not(:disabled),.action-btn.primary[data-v-32c52767]:hover:not(:disabled) {
                    transform: none
                }
            }

            @supports (-webkit-touch-callout:none) {
                .search-box[data-v-32c52767] {
                    -webkit-text-size-adjust: 100%;
                    -webkit-tap-highlight-color: transparent
                }

                .search-input[data-v-32c52767] {
                    -webkit-appearance: none;
                    border-radius: 0
                }

                .action-btn[data-v-32c52767] {
                    -webkit-appearance: none;
                    min-height: 44px;
                    min-width: 44px
                }
            }
        </style>
        <style>
            .douban-section[data-v-266df928] {
                width: 100%
            }

            .category-nav[data-v-266df928] {
                display: flex;
                flex-wrap: wrap;
                gap: 8px;
                margin-bottom: 20px;
                padding: 8px 0
            }

            .tab-button[data-v-266df928] {
                align-items: center;
                -webkit-backdrop-filter: blur(8px);
                backdrop-filter: blur(8px);
                background: #ffffffb3;
                border: 1px solid var(--border-light,#e5e7eb);
                border-radius: 10px;
                color: var(--text-secondary,#6b7280);
                cursor: pointer;
                display: flex;
                font-size: 13px;
                font-weight: 500;
                gap: 6px;
                overflow: hidden;
                padding: 8px 14px;
                position: relative;
                transition: all .2s ease
            }

            .tab-button[data-v-266df928]:before {
                background: linear-gradient(135deg,#0f766e1a,#f59e0b0d);
                content: "";
                inset: 0;
                opacity: 0;
                position: absolute;
                transition: opacity .2s ease
            }

            .tab-button[data-v-266df928]:hover:before {
                opacity: 1
            }

            .tab-button[data-v-266df928]:active {
                transform: scale(.98)
            }

            .tab-button.is-active[data-v-266df928] {
                background: #0f766e14;
                border-color: var(--primary,#0f766e);
                box-shadow: 0 2px 8px #0f766e26;
                color: var(--primary,#0f766e);
                font-weight: 600
            }

            .tab-label[data-v-266df928] {
                font-weight: 600
            }

            .tab-type[data-v-266df928] {
                font-size: 11px;
                opacity: .85
            }

            .content-area[data-v-266df928] {
                min-height: 300px;
                position: relative
            }

            .skeleton-grid[data-v-266df928] {
                display: grid;
                gap: 12px;
                grid-template-columns: repeat(5,1fr)
            }

            .skeleton-card[data-v-266df928] {
                animation: skeleton-pulse-266df928 2s ease-in-out infinite;
                -webkit-backdrop-filter: blur(10px);
                backdrop-filter: blur(10px);
                background: #ffffffbf;
                border: 1px solid var(--border-light,#e5e7eb);
                border-radius: 12px;
                display: flex;
                flex-direction: column;
                overflow: hidden
            }

            .skeleton-cover[data-v-266df928] {
                aspect-ratio: 2/3;
                background: linear-gradient(90deg,#f0f0f0 25%,#e0e0e0,#f0f0f0 75%);
                background-size: 200% 100%;
                overflow: hidden;
                position: relative
            }

            .skeleton-shimmer[data-v-266df928] {
                animation: shimmer-266df928 1.5s ease-in-out infinite;
                background: linear-gradient(90deg,transparent,hsla(0,0%,100%,.6) 50%,transparent);
                inset: 0;
                position: absolute;
                transform: translate(-100%)
            }

            .skeleton-info[data-v-266df928] {
                display: flex;
                flex-direction: column;
                gap: 4px;
                padding: 10px 12px
            }

            .skeleton-title[data-v-266df928] {
                animation: skeleton-shimmer-266df928 1.5s ease-in-out infinite;
                background: linear-gradient(90deg,#e5e7eb 25%,#d1d5db,#e5e7eb 75%);
                background-size: 200% 100%;
                border-radius: 4px;
                height: 32px
            }

            .skeleton-desc[data-v-266df928] {
                animation: skeleton-shimmer-266df928 1.5s ease-in-out .2s infinite;
                background: linear-gradient(90deg,#f3f4f6 25%,#e5e7eb,#f3f4f6 75%);
                background-size: 200% 100%;
                border-radius: 4px;
                height: 12px
            }

            @keyframes skeleton-pulse-266df928 {
                0%,to {
                    opacity: 1
                }

                50% {
                    opacity: .8
                }
            }

            @keyframes shimmer-266df928 {
                0% {
                    transform: translate(-100%)
                }

                to {
                    transform: translate(100%)
                }
            }

            @keyframes skeleton-shimmer-266df928 {
                0% {
                    background-position: 200% 0
                }

                to {
                    background-position: -200% 0
                }
            }

            .grid-container[data-v-266df928] {
                display: grid;
                gap: 12px;
                grid-template-columns: repeat(5,1fr)
            }

            .movie-card[data-v-266df928] {
                align-items: stretch;
                -webkit-backdrop-filter: blur(10px);
                backdrop-filter: blur(10px);
                background: #ffffffbf;
                border: 1px solid var(--border-light,#e5e7eb);
                border-radius: 12px;
                cursor: pointer;
                display: flex;
                flex-direction: column;
                overflow: hidden;
                padding: 0;
                text-align: left;
                transition: transform .2s ease,box-shadow .2s ease;
                will-change: transform
            }

            .movie-card[data-v-266df928]:hover {
                box-shadow: 0 8px 20px #0f766e1f;
                transform: translateY(-4px)
            }

            .card-cover[data-v-266df928] {
                aspect-ratio: 2/3;
                background: linear-gradient(135deg,#e5e7eb,#d1d5db);
                overflow: hidden;
                position: relative
            }

            .card-cover img[data-v-266df928] {
                display: block;
                height: 100%;
                -o-object-fit: cover;
                object-fit: cover;
                transition: transform .3s ease;
                width: 100%
            }

            .movie-card:hover .card-cover img[data-v-266df928] {
                transform: scale(1.05)
            }

            .cover-placeholder[data-v-266df928] {
                align-items: center;
                background: #0f766e0d;
                display: flex;
                font-size: 32px;
                height: 100%;
                justify-content: center;
                width: 100%
            }

            .card-info[data-v-266df928] {
                display: flex;
                flex-direction: column;
                gap: 4px;
                min-height: 0;
                padding: 10px 12px
            }

            .card-title[data-v-266df928] {
                color: var(--text-primary,#1f2937);
                display: -webkit-box;
                font-size: 13px;
                font-weight: 600;
                -webkit-line-clamp: 2;
                line-height: 1.3;
                -webkit-box-orient: vertical;
                overflow: hidden
            }

            .card-desc[data-v-266df928] {
                color: var(--text-tertiary,#9ca3af);
                font-size: 11px;
                line-height: 1.2;
                overflow: hidden;
                text-overflow: ellipsis;
                white-space: nowrap
            }

            .load-section[data-v-266df928] {
                margin-top: 8px
            }

            .load-trigger[data-v-266df928] {
                justify-content: center;
                min-height: 60px;
                padding: 24px 0
            }

            .load-trigger[data-v-266df928],.loading-more[data-v-266df928] {
                align-items: center;
                display: flex
            }

            .loading-more[data-v-266df928] {
                color: var(--text-secondary,#6b7280);
                font-size: 14px;
                gap: 10px
            }

            .spinner-dots[data-v-266df928] {
                display: flex;
                gap: 4px
            }

            .spinner-dots span[data-v-266df928] {
                animation: bounce-266df928 1.4s ease-in-out infinite both;
                background: var(--primary,#0f766e);
                border-radius: 50%;
                height: 8px;
                width: 8px
            }

            .spinner-dots span[data-v-266df928]:first-child {
                animation-delay: -.32s
            }

            .spinner-dots span[data-v-266df928]:nth-child(2) {
                animation-delay: -.16s
            }

            @keyframes bounce-266df928 {
                0%,80%,to {
                    opacity: .6;
                    transform: scale(.8)
                }

                40% {
                    opacity: 1;
                    transform: scale(1)
                }
            }

            .end-message[data-v-266df928] {
                color: var(--text-tertiary,#9ca3af);
                font-size: 13px;
                font-weight: 500;
                letter-spacing: .05em;
                padding: 20px 0;
                text-align: center
            }

            .grid-transition-enter-active[data-v-266df928],.grid-transition-leave-active[data-v-266df928] {
                transition: opacity .25s ease
            }

            .grid-transition-enter-from[data-v-266df928],.grid-transition-leave-to[data-v-266df928] {
                opacity: 0
            }

            .card-fade-enter-active[data-v-266df928],.card-fade-leave-active[data-v-266df928] {
                transition: all .3s ease
            }

            .card-fade-enter-from[data-v-266df928],.card-fade-leave-to[data-v-266df928] {
                opacity: 0;
                transform: scale(.95)
            }

            .card-fade-move[data-v-266df928] {
                transition: transform .3s ease
            }

            .hidden[data-v-266df928] {
                display: none
            }

            @media(max-width: 640px) {
                .category-nav[data-v-266df928] {
                    gap:6px
                }

                .tab-button[data-v-266df928] {
                    font-size: 12px;
                    padding: 6px 10px
                }

                .grid-container[data-v-266df928],.skeleton-grid[data-v-266df928] {
                    gap: 10px;
                    grid-template-columns: repeat(4,1fr)
                }

                .card-title[data-v-266df928] {
                    font-size: 12px
                }

                .card-desc[data-v-266df928] {
                    font-size: 10px
                }
            }

            @media(min-width: 640px) {
                .grid-container[data-v-266df928] {
                    gap:14px
                }

                .card-title[data-v-266df928] {
                    font-size: 13px
                }
            }

            @media(prefers-color-scheme: dark) {
                .tab-button[data-v-266df928] {
                    background:#161b2299;
                    border-color: var(--border-light);
                    color: var(--text-secondary)
                }

                .tab-button[data-v-266df928]:before {
                    background: linear-gradient(135deg,#0d948814,#fbbf240a)
                }

                .tab-button[data-v-266df928]:hover {
                    background: #ffffff0f;
                    border-color: var(--border-medium)
                }

                .tab-button.is-active[data-v-266df928] {
                    background: #0d94881f;
                    border-color: var(--primary);
                    box-shadow: 0 2px 8px #0d948833;
                    color: var(--primary)
                }

                .skeleton-card[data-v-266df928] {
                    background: #161b22b3;
                    border-color: var(--border-light)
                }

                .skeleton-cover[data-v-266df928] {
                    background: linear-gradient(90deg,#161b22 25%,#21262d,#161b22 75%);
                    background-size: 200% 100%
                }

                .skeleton-shimmer[data-v-266df928] {
                    background: linear-gradient(90deg,transparent,hsla(0,0%,100%,.04) 50%,transparent)
                }

                .skeleton-title[data-v-266df928] {
                    background: linear-gradient(90deg,#21262d 25%,#30363d,#21262d 75%);
                    background-size: 200% 100%
                }

                .skeleton-desc[data-v-266df928] {
                    background: linear-gradient(90deg,#1a1f26 25%,#262c34,#1a1f26 75%);
                    background-size: 200% 100%
                }

                .movie-card[data-v-266df928] {
                    background: #161b22b3;
                    border-color: var(--border-light)
                }

                .card-cover[data-v-266df928] {
                    background: linear-gradient(135deg,#161b22,#21262d)
                }

                .cover-placeholder[data-v-266df928] {
                    background: #0d948814
                }

                .movie-card[data-v-266df928]:hover {
                    box-shadow: 0 8px 20px #0d948826
                }

                .card-info[data-v-266df928] {
                    background: transparent
                }

                .card-title[data-v-266df928] {
                    color: var(--text-primary)
                }

                .card-desc[data-v-266df928] {
                    color: var(--text-tertiary)
                }

                .loading-more[data-v-266df928] {
                    color: var(--text-secondary)
                }

                .spinner-dots span[data-v-266df928] {
                    background: var(--primary)
                }

                .end-message[data-v-266df928] {
                    color: var(--text-tertiary)
                }
            }

            @media(prefers-reduced-motion:reduce) {
                .movie-card[data-v-266df928],.skeleton-card[data-v-266df928],.tab-button[data-v-266df928] {
                    animation: none;
                    transition: none
                }

                .movie-card[data-v-266df928]:hover {
                    transform: none
                }

                .card-fade-enter-active[data-v-266df928],.card-fade-leave-active[data-v-266df928],.card-fade-move[data-v-266df928],.grid-transition-enter-active[data-v-266df928],.grid-transition-leave-active[data-v-266df928] {
                    transition: none
                }

                .skeleton-shimmer[data-v-266df928] {
                    animation: none
                }

                .skeleton-cover[data-v-266df928] {
                    background: var(--bg-secondary)
                }

                .skeleton-desc[data-v-266df928],.skeleton-title[data-v-266df928] {
                    animation: none;
                    background: var(--border-light)
                }

                .spinner-dots span[data-v-266df928] {
                    animation: none
                }
            }
        </style>
        <link rel="stylesheet" href="/_nuxt/entry.BzSI-0kc.css" crossorigin>
        <link rel="preload" as="fetch" crossorigin="anonymous" href="/_payload.json?ceb3a145-6f54-4137-88cd-2929afe0ee1a">
        <link rel="modulepreload" as="script" crossorigin href="/_nuxt/CHbT_gfP.js">
        <link rel="modulepreload" as="script" crossorigin href="/_nuxt/BtBh0ot0.js">
        <link rel="modulepreload" as="script" crossorigin href="/_nuxt/BmQtR8ch.js">
        <script type="module" src="/_nuxt/CHbT_gfP.js" crossorigin></script>
        <meta name="description" content="聚合阿里云盘、夸克、百度网盘、115、迅雷等平台，实时检索各类分享链接与资源，免费、快速、无广告。">
        <meta name="keywords" content="网盘搜索, 阿里云盘搜索, 夸克网盘搜索, 百度网盘搜索, 115 网盘, 迅雷云盘, 资源搜索, 盘搜, PanHub">
        <meta name="theme-color" content="#111111">
        <meta property="og:type" content="website">
        <meta property="og:site_name" content="PanHub">
        <link rel="icon" type="image/x-icon" href="/favicon.ico">
        <meta property="og:title" content="PanHub - 全网最全的网盘搜索">
        <meta property="og:description" content="聚合阿里云盘、夸克、百度网盘、115、迅雷等平台，实时检索各类分享链接与资源，免费、快速、无广告。">
        <meta property="og:image" content="https://panhub.shenzjd.com/og.svg">
        <meta name="twitter:card" content="summary_large_image">
        <meta name="twitter:title" content="PanHub - 全网最全的网盘搜索">
        <meta name="twitter:description" content="聚合阿里云盘、夸克、百度网盘、115、迅雷等平台，实时检索各类分享链接与资源，免费、快速、无广告。">
        <meta name="twitter:image" content="https://panhub.shenzjd.com/og.svg">
        <link rel="canonical" href="https://panhub.shenzjd.com/">
        <script type="application/ld+json">
            {
                "@context": "https://schema.org",
                "@type": "WebSite",
                "name": "PanHub",
                "url": "https://panhub.shenzjd.com",
                "potentialAction": {
                    "@type": "SearchAction",
                    "target": "https://panhub.shenzjd.com/?q={search_term_string}",
                    "query-input": "required name=search_term_string"
                }
            }</script>
        <script id="unhead:payload" type="application/json">
            {
                "titleTemplate": "%s · PanHub"
            }</script>
    </head>
    <body>
        <div id="__nuxt">
            <div class="layout" data-v-5c746fb8>
                <div class="bg-decoration" data-v-5c746fb8>
                    <div class="blob blob-1" data-v-5c746fb8></div>
                    <div class="blob blob-2" data-v-5c746fb8></div>
                    <div class="blob blob-3" data-v-5c746fb8></div>
                </div>
                <header class="header" data-v-5c746fb8>
                    <nav class="nav" data-v-5c746fb8>
                        <a aria-current="page" href="/" class="router-link-active router-link-exact-active brand" data-v-5c746fb8>
                            <span class="brand-icon" data-v-5c746fb8>🔍</span>
                            <span class="brand-text" data-v-5c746fb8>PanHub</span>
                        </a>
                        <div class="nav-actions" data-v-5c746fb8>
                            <a href="https://github.com/wu529778790/panhub.shenzjd.com" target="_blank" rel="noopener noreferrer" class="btn-icon github-btn" aria-label="打开 GitHub 仓库" title="GitHub 仓库" data-v-5c746fb8>
                                <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor" data-v-5c746fb8>
                                    <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z" data-v-5c746fb8></path>
                                </svg>
                            </a>
                            <button class="btn-icon" type="button" aria-label="打开设置" title="设置" data-v-5c746fb8>
                                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" data-v-5c746fb8>
                                    <circle cx="12" cy="12" r="3" data-v-5c746fb8></circle>
                                    <path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 2.83 0l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z" data-v-5c746fb8></path>
                                </svg>
                            </button>
                        </div>
                    </nav>
                </header>
                <main class="main" data-v-5c746fb8>
                    <div class="home" data-v-7a6a3b93>
                        <div class="hero-row" data-v-7a6a3b93>
                            <div class="hero-noise" aria-hidden="true" data-v-7a6a3b93></div>
                            <header class="hero" data-v-7a6a3b93>
                                <div class="hero-accent" aria-hidden="true" data-v-7a6a3b93></div>
                                <div class="hero-content" data-v-7a6a3b93>
                                    <div class="hero-badge" data-v-7a6a3b93>PanHub 搜索聚合引擎</div>
                                    <h1 class="hero-title" data-v-7a6a3b93>
                                        <span class="hero-title-line" data-v-7a6a3b93>一键检索</span>
                                        <span class="hero-title-line hero-title-line--accent" data-v-7a6a3b93>全网网盘资源</span>
                                    </h1>
                                    <p class="hero-description" data-v-7a6a3b93>聚合阿里云盘、夸克、百度网盘、115、迅雷等平台 · 快速、直达、少打扰 </p>
                                    <ul class="hero-features" role="list" data-v-7a6a3b93>
                                        <li class="hero-feature" data-v-7a6a3b93>实时聚合</li>
                                        <li class="hero-feature" data-v-7a6a3b93>多平台覆盖</li>
                                        <li class="hero-feature" data-v-7a6a3b93>结果去重</li>
                                    </ul>
                                </div>
                                <div class="hero-shape" aria-hidden="true" data-v-7a6a3b93></div>
                            </header>
                            <aside class="hero-aside" data-v-7a6a3b93>
                                <div class="hidden" data-v-7a6a3b93 data-v-4a8e0845></div>
                            </aside>
                        </div>
                        <section class="search" data-v-7a6a3b93 data-v-32c52767>
                            <div class="search-container" data-v-32c52767>
                                <div class="search-box" data-v-32c52767>
                                    <div class="search-icon" data-v-32c52767>
                                        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" data-v-32c52767>
                                            <circle cx="11" cy="11" r="8" data-v-32c52767></circle>
                                            <path d="m21 21-4.35-4.35" data-v-32c52767></path>
                                        </svg>
                                    </div>
                                    <input value="" placeholder="搜索网盘资源，支持百度云、阿里云盘、夸克网盘、115网盘、迅雷云盘、天翼云盘、123网盘、移动云盘、UC网盘等" name="kw" aria-label="搜索关键词" autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false" class="search-input" data-v-32c52767>
                                    <div class="search-actions" data-v-32c52767>
                                        <!---->
                                        <!---->
                                        <!---->
                                        <button class="action-btn primary" type="button" disabled aria-label="开始搜索" data-v-32c52767>
                                            <span class="btn-text" data-v-32c52767>搜索</span>
                                            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" data-v-32c52767>
                                                <path d="M5 12h14M12 5l7 7-7 7" data-v-32c52767></path>
                                            </svg>
                                        </button>
                                        <!---->
                                    </div>
                                </div>
                            </div>
                        </section>
                        <!---->
                        <!---->
                        <!---->
                        <section class="douban-hot-section" data-v-7a6a3b93>
                            <div class="hidden" data-v-7a6a3b93 data-v-266df928></div>
                        </section>
                    </div>
                </main>
                <span data-v-5c746fb8></span>
                <!---->
                <span data-v-5c746fb8></span>
            </div>
        </div>
        <div id="teleports"></div>
        <script>
            window.__NUXT__ = {};
            window.__NUXT__.config = {
                public: {
                    apiBase: "/api",
                    siteUrl: "https://panhub.shenzjd.com",
                    tgDefaultChannels: ["tgsearchers3", "yunpanxunlei", "tianyifc", "BaiduCloudDisk", "txtyzy", "peccxinpd", "gotopan", "xingqiump4", "yunpanqk", "PanjClub", "kkxlzy", "baicaoZY", "MCPH01", "share_aliyun", "bdwpzhpd", "ysxb48", "jdjdn1111", "yggpan", "MCPH086", "zaihuayun", "Q66Share", "NewAliPan", "ypquark", "Oscar_4Kmovies", "ucwpzy", "alyp_TV", "alyp_4K_Movies", "shareAliyun", "alyp_1", "dianyingshare", "Quark_Movies", "XiangxiuNBB", "NewQuark", "ydypzyfx", "kuakeyun", "ucquark", "xx123pan", "yingshifenxiang123", "zyfb123", "tyypzhpd", "tianyirigeng", "cloudtianyi", "hdhhd21", "Lsp115", "oneonefivewpfx", "Maidanglaocom", "qixingzhenren", "taoxgzy", "tgsearchers115", "Channel_Shares_115", "tyysypzypd", "vip115hot", "wp123zy", "yunpan139", "yunpan189", "yunpanuc", "yydf_hzl", "alyp_Animation", "alyp_JLP", "leoziyuan", "AliyunDrive_Share_Channel", "aliyunys", "Aliyun_4K_Movies", "yunpanpan", "Quark_Share_Channel", "quarkshare", "baiduyun", "iAliyun", "quanziyuanshe"]
                },
                app: {
                    baseURL: "/",
                    buildId: "ceb3a145-6f54-4137-88cd-2929afe0ee1a",
                    buildAssetsDir: "/_nuxt/",
                    cdnURL: ""
                }
            }
        </script>
        <script type="application/json" data-nuxt-data="nuxt-app" data-ssr="true" id="__NUXT_DATA__" data-src="/_payload.json?ceb3a145-6f54-4137-88cd-2929afe0ee1a">
            [
                {
                    "state": 1,
                    "once": 6,
                    "_errors": 7,
                    "serverRendered": 4,
                    "path": 9,
                    "prerenderedAt": -1
                },
                [
                    "Reactive",
                    2
                ],
                {
                    "$sauth-locked": 3,
                    "$sauth-loading": 4,
                    "$sauth-error": 5
                },
                false,
                true,
                "",
                [
                    "Set"
                ],
                [
                    "ShallowReactive",
                    8
                ],
                {
                },
                "/"
            ]</script>
        <script>
            (function() {
                function c() {
                    var b = a.contentDocument || a.contentWindow.document;
                    if (b) {
                        var d = b.createElement('script');
                        d.innerHTML = "window.__CF$cv$params={r:'9fe7efe1ce198ea8',t:'MTc3OTI0NDQxMQ=='};var a=document.createElement('script');a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";
                        b.getElementsByTagName('head')[0].appendChild(d)
                    }
                }
                if (document.body) {
                    var a = document.createElement('iframe');
                    a.height = 1;
                    a.width = 1;
                    a.style.position = 'absolute';
                    a.style.top = 0;
                    a.style.left = 0;
                    a.style.border = 'none';
                    a.style.visibility = 'hidden';
                    document.body.appendChild(a);
                    if ('loading' !== document.readyState)
                        c();
                    else if (window.addEventListener)
                        document.addEventListener('DOMContentLoaded', c);
                    else {
                        var e = document.onreadystatechange || function() {}
                        ;
                        document.onreadystatechange = function(b) {
                            e(b);
                            'loading' !== document.readyState && (document.onreadystatechange = e,
                            c())
                        }
                    }
                }
            }
            )();
        </script>
    </body>
</html>
