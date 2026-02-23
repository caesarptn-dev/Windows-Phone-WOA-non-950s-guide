<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Windows ARM Guide</title>
    <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Crect x='18' y='4' width='28' height='56' rx='3' fill='%23FFC107' stroke='%23333' stroke-width='1.5'/%3E%3Crect x='20' y='10' width='24' height='40' fill='%230078D4'/%3E%3Cpath d='M24 14h4v4h-4zm6 0h4v4h-4zm6 0h4v4h-4zm-12 6h4v4h-4zm6 0h4v4h-4zm6 0h4v4h-4zm-12 6h4v4h-4zm6 0h4v4h-4zm6 0h4v4h-4zm-12 6h4v4h-4zm6 0h4v4h-4zm6 0h4v4h-4z' fill='%23fff' opacity='0.3'/%3E%3Crect x='28' y='52' width='8' height='4' rx='2' fill='%23555'/%3E%3Ccircle cx='25' cy='7' r='1' fill='%23555'/%3E%3C/svg%3E">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Helvetica Neue', Arial, sans-serif;
            background: url('data:image/svg+xml,%3Csvg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1920 1080"%3E%3Cdefs%3E%3CradialGradient id="grad1" cx="50%25" cy="50%25"%3E%3Cstop offset="0%25" style="stop-color:%230078d4;stop-opacity:1" /%3E%3Cstop offset="50%25" style="stop-color:%230067c0;stop-opacity:1" /%3E%3Cstop offset="100%25" style="stop-color:%23004f8c;stop-opacity:1" /%3E%3C/radialGradient%3E%3ClinearGradient id="grad2" x1="0%25" y1="0%25" x2="100%25" y2="100%25"%3E%3Cstop offset="0%25" style="stop-color:%230078d4;stop-opacity:0.8" /%3E%3Cstop offset="100%25" style="stop-color:%23667eea;stop-opacity:0.8" /%3E%3C/linearGradient%3E%3C/defs%3E%3Crect width="1920" height="1080" fill="url(%23grad1)"/%3E%3Cpath d="M960 200 L1400 540 L960 880 L520 540 Z" fill="url(%23grad2)" opacity="0.6" filter="blur(40px)"/%3E%3Cpath d="M960 300 L1300 540 L960 780 L620 540 Z" fill="%230078d4" opacity="0.4" filter="blur(60px)"/%3E%3C/svg%3E') center/cover no-repeat fixed;
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(0px);
            -webkit-backdrop-filter: blur(0px);
            pointer-events: none;
            z-index: 0;
        }

        body::after {
            content: '';
            position: fixed;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.05) 1px, transparent 1px);
            background-size: 50px 50px;
            animation: backgroundMove 20s linear infinite;
            pointer-events: none;
            z-index: 0;
        }

        @keyframes backgroundMove {
            0% {
                transform: translate(0, 0);
            }
            100% {
                transform: translate(50px, 50px);
            }
        }

        .liquid-blob {
            position: fixed;
            border-radius: 50%;
            filter: blur(60px);
            opacity: 0.3;
            animation: float 15s ease-in-out infinite;
            pointer-events: none;
            z-index: 1;
        }

        .blob1 {
            width: 300px;
            height: 300px;
            background: rgba(255, 255, 255, 0.3);
            top: 10%;
            left: 10%;
            animation-delay: 0s;
        }

        .blob2 {
            width: 400px;
            height: 400px;
            background: rgba(102, 126, 234, 0.4);
            top: 50%;
            right: 10%;
            animation-delay: 5s;
        }

        .blob3 {
            width: 250px;
            height: 250px;
            background: rgba(118, 75, 162, 0.4);
            bottom: 10%;
            left: 30%;
            animation-delay: 10s;
        }

        @keyframes float {
            0%, 100% {
                transform: translate(0, 0) scale(1);
            }
            33% {
                transform: translate(50px, -50px) scale(1.1);
            }
            66% {
                transform: translate(-50px, 50px) scale(0.9);
            }
        }

        .liquid-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 5;
        }

        .ripple {
            position: absolute;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(255, 255, 255, 0.5) 0%, rgba(255, 255, 255, 0) 70%);
            animation: rippleEffect 1.5s ease-out;
            pointer-events: none;
        }

        @keyframes rippleEffect {
            0% {
                width: 0;
                height: 0;
                opacity: 1;
            }
            100% {
                width: 500px;
                height: 500px;
                opacity: 0;
            }
        }

        nav {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(50px) saturate(200%);
            -webkit-backdrop-filter: blur(50px) saturate(200%);
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
            padding: 20px 0;
            box-shadow: 
                0 4px 30px rgba(0, 0, 0, 0.1),
                inset 0 1px 0 rgba(255, 255, 255, 0.15);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        nav ul {
            list-style: none;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 16px;
            flex-wrap: wrap;
            padding: 0 20px;
        }

        nav li {
            flex: 0;
        }

        nav button {
            width: 50px;
            height: 50px;
            padding: 0;
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(20px) saturate(180%);
            -webkit-backdrop-filter: blur(20px) saturate(180%);
            border: 1px solid rgba(255, 255, 255, 0.25);
            cursor: pointer;
            font-size: 13px;
            font-weight: 600;
            color: rgba(255, 255, 255, 0.8);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            line-height: 1.2;
            box-shadow: 
                0 4px 15px rgba(0, 0, 0, 0.12),
                inset 0 1px 0 rgba(255, 255, 255, 0.2);
        }

        nav button:hover {
            background: rgba(255, 255, 255, 0.15);
            color: #fff;
            transform: scale(1.1);
            box-shadow: 
                0 6px 20px rgba(0, 0, 0, 0.18),
                inset 0 1px 0 rgba(255, 255, 255, 0.3);
            backdrop-filter: blur(25px) saturate(200%);
            -webkit-backdrop-filter: blur(25px) saturate(200%);
        }

        nav button.active {
            color: #fff;
            background: rgba(255, 255, 255, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.4);
            transform: scale(1.15);
            box-shadow: 
                0 8px 25px rgba(0, 0, 0, 0.25),
                inset 0 1px 0 rgba(255, 255, 255, 0.4);
        }

        nav button:active {
            transform: scale(0.95);
        }

        .content {
            display: none;
            padding: 60px 20px;
            max-width: 800px;
            margin: 0 auto;
            animation: fadeIn 0.5s ease;
        }

        .content.active {
            display: block;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(60px) saturate(200%);
            -webkit-backdrop-filter: blur(60px) saturate(200%);
            border: 1.5px solid rgba(255, 255, 255, 0.3);
            border-radius: 35px;
            padding: 50px;
            box-shadow: 
                0 8px 32px rgba(0, 0, 0, 0.25),
                0 20px 60px rgba(0, 0, 0, 0.15),
                inset 0 1px 0 rgba(255, 255, 255, 0.3),
                inset 0 -1px 0 rgba(255, 255, 255, 0.1);
            text-align: center;
            position: relative;
            z-index: 10;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            cursor: pointer;
            overflow: hidden;
        }

        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            border-radius: 35px;
            padding: 2px;
            background: linear-gradient(135deg, 
                rgba(255,255,255,0.6) 0%, 
                rgba(255,255,255,0.1) 50%,
                rgba(255,255,255,0.3) 100%);
            -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
            pointer-events: none;
        }

        .card::after {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: linear-gradient(135deg, 
                rgba(255,255,255,0.4) 0%, 
                transparent 50%, 
                rgba(255,255,255,0.2) 100%);
            border-radius: 36px;
            opacity: 0.5;
            pointer-events: none;
            z-index: -1;
            filter: blur(10px);
        }

        .card:hover {
            backdrop-filter: blur(70px) saturate(220%);
            -webkit-backdrop-filter: blur(70px) saturate(220%);
            background: rgba(255, 255, 255, 0.08);
            transform: translateY(-8px) scale(1.02);
            box-shadow: 
                0 12px 48px rgba(0, 0, 0, 0.3), 
                0 30px 80px rgba(0, 0, 0, 0.2),
                inset 0 1px 0 rgba(255, 255, 255, 0.4),
                inset 0 -1px 0 rgba(255, 255, 255, 0.15);
            border: 1.5px solid rgba(255, 255, 255, 0.4);
        }

        .card:active {
            transform: translateY(-2px) scale(0.98);
            transition: all 0.1s ease;
        }

        .card:active {
            transform: translateY(-2px) scale(0.98);
        }

        .card-ripple {
            position: absolute;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(255, 255, 255, 0.6) 0%, rgba(255, 255, 255, 0) 70%);
            transform: translate(-50%, -50%);
            animation: cardRipple 0.8s ease-out;
            pointer-events: none;
        }

        @keyframes cardRipple {
            0% {
                width: 0;
                height: 0;
                opacity: 1;
            }
            100% {
                width: 350px;
                height: 350px;
                opacity: 0;
            }
        }

        .logo {
            width: 200px;
            height: 200px;
            margin: 0 auto 30px;
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
        }

        .win10-logo {
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 88 88"><path fill="%230078D4" d="M0 12.402l35.687-4.86.016 34.423-35.67.203zm35.67 33.529l.028 34.453L.028 75.48.026 45.7zm4.326-39.025L87.314 0v41.527l-47.318.376zm47.329 39.349l-.011 41.34-47.318-6.678-.066-34.739z"/></svg>');
        }

        .win81-logo {
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 88 88"><path fill="%2300BCF2" d="M0 12.402l35.687-4.86.016 34.423-35.67.203zm35.67 33.529l.028 34.453L.028 75.48.026 45.7zm4.326-39.025L87.314 0v41.527l-47.318.376zm47.329 39.349l-.011 41.34-47.318-6.678-.066-34.739z"/></svg>');
        }

        .winpe-logo {
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 88 88"><path fill="%2300A4EF" d="M0 12.402l35.687-4.86.016 34.423-35.67.203zm35.67 33.529l.028 34.453L.028 75.48.026 45.7zm4.326-39.025L87.314 0v41.527l-47.318.376zm47.329 39.349l-.011 41.34-47.318-6.678-.066-34.739z"/><circle cx="44" cy="44" r="18" fill="white" opacity="0.3"/><path d="M44 30v28M30 44h28" stroke="white" stroke-width="4" stroke-linecap="round"/></svg>');
        }

        h1 {
            color: #fff;
            margin-bottom: 20px;
            font-size: 32px;
            text-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
            font-weight: 600;
            letter-spacing: -0.5px;
        }

        .guide-link {
            display: inline-block;
            margin-top: 30px;
            padding: 16px 42px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(40px) saturate(180%);
            -webkit-backdrop-filter: blur(40px) saturate(180%);
            border: 1px solid rgba(255, 255, 255, 0.3);
            color: white;
            text-decoration: none;
            border-radius: 100px;
            font-weight: 600;
            font-size: 17px;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 
                0 6px 25px rgba(0, 0, 0, 0.2),
                inset 0 1px 0 rgba(255, 255, 255, 0.25);
            text-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
        }

        .guide-link:hover {
            transform: translateY(-3px) scale(1.05);
            background: rgba(255, 255, 255, 0.18);
            box-shadow: 
                0 12px 40px rgba(0, 0, 0, 0.3),
                inset 0 1px 0 rgba(255, 255, 255, 0.35);
            backdrop-filter: blur(50px) saturate(200%);
            -webkit-backdrop-filter: blur(50px) saturate(200%);
        }

        .guide-link:active {
            transform: translateY(-1px) scale(0.98);
            transition: all 0.1s ease;
        }

        .home-hero {
            text-align: center;
            margin-bottom: 30px;
        }

        .home-title {
            font-size: 42px;
            color: #fff;
            text-shadow: 0 2px 16px rgba(0, 0, 0, 0.2);
            margin-bottom: 15px;
            font-weight: 700;
            letter-spacing: -1px;
        }

        .home-subtitle {
            font-size: 20px;
            color: rgba(255, 255, 255, 0.95);
            margin-bottom: 40px;
            text-shadow: 0 1px 4px rgba(0, 0, 0, 0.15);
            font-weight: 500;
            letter-spacing: -0.3px;
        }

        .lumia-showcase {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(40px) saturate(180%);
            -webkit-backdrop-filter: blur(40px) saturate(180%);
            border: 1px solid rgba(255, 255, 255, 0.25);
            border-radius: 28px;
            padding: 35px;
            margin: 30px 0;
            box-shadow: 
                0 8px 32px rgba(0, 0, 0, 0.15),
                inset 0 1px 0 rgba(255, 255, 255, 0.2);
        }

        .lumia-image {
            max-width: 100%;
            height: auto;
            border-radius: 20px;
            box-shadow: 0 12px 40px rgba(0, 0, 0, 0.25);
        }

        .os-badges {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
            flex-wrap: wrap;
        }

        .os-badge {
            display: flex;
            align-items: center;
            gap: 10px;
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(30px) saturate(170%);
            -webkit-backdrop-filter: blur(30px) saturate(170%);
            border: 1px solid rgba(255, 255, 255, 0.3);
            padding: 14px 24px;
            border-radius: 100px;
            box-shadow: 
                0 4px 20px rgba(0, 0, 0, 0.15),
                inset 0 1px 0 rgba(255, 255, 255, 0.2);
            color: white;
            font-weight: 600;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .os-badge:hover {
            transform: translateY(-2px) scale(1.05);
            box-shadow: 
                0 8px 28px rgba(0, 0, 0, 0.2),
                inset 0 1px 0 rgba(255, 255, 255, 0.3);
            background: rgba(255, 255, 255, 0.12);
        }

        .os-badge-icon {
            width: 30px;
            height: 30px;
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
        }

        .issue-link {
            display: inline-block;
            margin-top: 15px;
            padding: 12px 28px;
            background: rgba(255, 255, 255, 0.12);
            backdrop-filter: blur(15px) saturate(150%);
            -webkit-backdrop-filter: blur(15px) saturate(150%);
            border: 0.5px solid rgba(255, 255, 255, 0.25);
            color: white;
            text-decoration: none;
            border-radius: 100px;
            font-size: 15px;
            font-weight: 500;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .issue-link:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-2px) scale(1.05);
            backdrop-filter: blur(20px) saturate(180%);
            -webkit-backdrop-filter: blur(20px) saturate(180%);
        }

        .issue-link:active {
            transform: translateY(0) scale(0.98);
            transition: all 0.1s ease;
        }

        .credits-list {
            text-align: left;
            margin-top: 30px;
        }

        .credit-item {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(20px) saturate(150%);
            -webkit-backdrop-filter: blur(20px) saturate(150%);
            border: 0.5px solid rgba(255, 255, 255, 0.2);
            padding: 24px;
            margin-bottom: 16px;
            border-radius: 24px;
            border-left: 4px solid rgba(255, 255, 255, 0.5);
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.08);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .credit-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
            background: rgba(255, 255, 255, 0.12);
        }

        .credit-item strong {
            color: #fff;
            font-size: 18px;
        }

        .credit-item p {
            margin-top: 5px;
            color: rgba(255, 255, 255, 0.85);
        }

        .experiment-badge {
            display: inline-block;
            background: rgba(255, 193, 7, 0.25);
            backdrop-filter: blur(15px) saturate(150%);
            -webkit-backdrop-filter: blur(15px) saturate(150%);
            border: 0.5px solid rgba(255, 193, 7, 0.4);
            color: #FFC107;
            padding: 10px 24px;
            border-radius: 100px;
            font-size: 15px;
            font-weight: 600;
            margin-top: 15px;
            text-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
            box-shadow: 0 4px 16px rgba(255, 193, 7, 0.15);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .experiment-badge:hover {
            transform: translateY(-2px) scale(1.05);
            box-shadow: 0 8px 24px rgba(255, 193, 7, 0.25);
        }
    </style>
</head>
<body>
    <div class="liquid-blob blob1"></div>
    <div class="liquid-blob blob2"></div>
    <div class="liquid-blob blob3"></div>
    <div class="liquid-container" id="liquidContainer"></div>
    
    <nav>
        <ul>
            <li><button onclick="showSection('home')" class="nav-btn active" id="btn-home" title="Home">🏠</button></li>
            <li><button onclick="showSection('win10')" class="nav-btn" id="btn-win10" title="Windows 10 ARM32">10</button></li>
            <li><button onclick="showSection('winpe')" class="nav-btn" id="btn-winpe" title="Windows PE ARM32">PE</button></li>
            <li><button onclick="showSection('winrt')" class="nav-btn" id="btn-winrt" title="Windows RT">RT</button></li>
            <li><button onclick="showSection('credits')" class="nav-btn" id="btn-credits" title="Credits">©</button></li>
        </ul>
    </nav>

    <div id="home" class="content active">
        <div class="card" onclick="createCardRipple(event, this)">
            <div class="home-hero">
                <h1 class="home-title">Introducing Windows on ARM</h1>
                <p class="home-subtitle">Experience Windows on your Lumia devices</p>
            </div>
            
            <div class="lumia-showcase">
                <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 800 500'%3E%3Cdefs%3E%3ClinearGradient id='grad1' x1='0%25' y1='0%25' x2='100%25' y2='100%25'%3E%3Cstop offset='0%25' style='stop-color:%23667eea;stop-opacity:1' /%3E%3Cstop offset='100%25' style='stop-color:%23764ba2;stop-opacity:1' /%3E%3C/linearGradient%3E%3C/defs%3E%3Crect width='800' height='500' fill='%23f0f0f0'/%3E%3Crect x='250' y='50' width='300' height='400' rx='20' fill='%23000' opacity='0.9'/%3E%3Crect x='260' y='80' width='280' height='340' fill='%23333'/%3E%3Crect x='270' y='90' width='260' height='150' fill='url(%23grad1)'/%3E%3Ctext x='400' y='180' font-family='Segoe UI, Arial' font-size='36' fill='white' text-anchor='middle' font-weight='bold'%3EWindows 10%3C/text%3E%3Crect x='270' y='250' width='260' height='150' fill='%2300BCF2'/%3E%3Ctext x='400' y='340' font-family='Segoe UI, Arial' font-size='36' fill='white' text-anchor='middle' font-weight='bold'%3EWindows RT%3C/text%3E%3Crect x='360' y='430' width='80' height='6' rx='3' fill='%23555'/%3E%3Ctext x='400' y='480' font-family='Segoe UI, Arial' font-size='20' fill='%23666' text-anchor='middle'%3ELumia Device%3C/text%3E%3C/svg%3E" alt="Lumia device with Windows 10 and Windows RT" class="lumia-image">
                
                <div class="os-badges">
                    <div class="os-badge">
                        <div class="os-badge-icon win10-logo"></div>
                        <span>Windows 10 ARM32</span>
                    </div>
                    <div class="os-badge">
                        <div class="os-badge-icon win81-logo"></div>
                        <span>Windows RT</span>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div id="win10" class="content">
        <div class="card" onclick="createCardRipple(event, this)">
            <div class="logo win10-logo"></div>
            <h1>Windows 10 ARM32</h1>
            <a href="https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://github.com/RedGreenBlue09/WFAv7_Installer&ved=2ahUKEwjhveGr8beSAxWsjK8BHWxQCYEQFnoECA8QAQ&usg=AOvVaw2B6mwHgs9rjImN4bOdb5R-" class="guide-link" target="_blank">View Installation Guide</a>
        </div>
    </div>

    <div id="winpe" class="content">
        <div class="card" onclick="createCardRipple(event, this)">
            <div class="logo winpe-logo"></div>
            <h1>Windows PE ARM32</h1>
            <span class="experiment-badge">⚗️ In Experiment</span>
        </div>
    </div>

    <div id="winrt" class="content">
        <div class="card" onclick="createCardRipple(event, this)">
            <div class="logo win81-logo"></div>
            <h1>Windows RT</h1>
            <a href="https://github.com/caesarptn-dev/Windows-RT-installer-for-Lumia-devices" class="guide-link" target="_blank">View Installation Guide</a>
            <br>
            <a href="https://github.com/caesarptn-dev/Windows-RT-installer-for-Lumia-devices/issues" class="issue-link" target="_blank">Report Issues</a>
        </div>
    </div>

    <div id="credits" class="content">
        <div class="card" onclick="createCardRipple(event, this)">
            <h1>Credits</h1>
            <div class="credits-list">
                <div class="credit-item">
                    <strong>@zazabutanimator</strong>
                    <p>For website (me)</p>
                </div>
                <div class="credit-item">
                    <strong>@Redgreenblue09</strong>
                    <p>For Windows 10 ARM32</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Navigation section switching
        function showSection(section) {
            document.querySelectorAll('.content').forEach(content => {
                content.classList.remove('active');
            });

            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });

            document.getElementById(section).classList.add('active');
            document.getElementById('btn-' + section).classList.add('active');
        }

        // Liquid ripple effect on body click
        document.addEventListener('click', function(e) {
            createRipple(e.pageX, e.pageY);
        });

        function createRipple(x, y) {
            const ripple = document.createElement('div');
            ripple.classList.add('ripple');
            ripple.style.left = x + 'px';
            ripple.style.top = y + 'px';
            
            document.getElementById('liquidContainer').appendChild(ripple);
            
            setTimeout(() => {
                ripple.remove();
            }, 1500);
        }

        // Card ripple effect on card click
        function createCardRipple(event, card) {
            const rect = card.getBoundingClientRect();
            const x = event.clientX - rect.left;
            const y = event.clientY - rect.top;
            
            const ripple = document.createElement('div');
            ripple.classList.add('card-ripple');
            ripple.style.left = x + 'px';
            ripple.style.top = y + 'px';
            
            card.appendChild(ripple);
            
            setTimeout(() => {
                ripple.remove();
            }, 800);
        }
    </script>
</body>
</html>
