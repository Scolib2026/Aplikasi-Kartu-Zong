<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🃏 Sistem Pembagian Meja Turnamen Kartu Remi</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Roboto', Tahoma, Geneva, Verdana, sans-serif;
        }

        :root {
            --bg-dark: #0F0F1A;
            --bg-card: #1A1A2E;
            --bg-card-alt: #16213E;
            --bg-gold: linear-gradient(135deg, #B8860B, #DAA520, #FFD700, #DAA520, #B8860B);
            --gold-dark: #996515;
            --gold-mid: #D4AF37;
            --gold-light: #F5E7B2;
            --red-main: #9E0000;
            --red-dark: #660000;
            --red-soft: #C92A2A;
            --spade-club: #1A1A2E;
            --heart-diamond: #9E0000;
            --text-white: #FFFFFF;
            --text-soft: #E2E2E2;
            --text-muted: #9CA3AF;
            --shadow-gold: 0 0 30px rgba(212, 175, 55, 0.18);
            --shadow-card: 0 10px 30px rgba(0, 0, 0, 0.45);
            --radius-lg: 16px;
            --radius-md: 10px;
            --radius-sm: 6px;
        }

        html, body {
            background: linear-gradient(135deg, #0F0F1A 0%, #1A1A2E 40%, #16213E 70%, #0F0F1A 100%);
            color: var(--text-white);
            min-height: 100vh;
            padding: 20px;
            position: relative;
            overflow-x: hidden;
        }

        /* ===== BACKGROUND MOTIF KARTU REMI ===== */
        .bg-pattern {
            position: fixed;
            inset: 0;
            pointer-events: none;
            z-index: 0;
            opacity: 0.04;
            background-image: 
                radial-gradient(circle at 15% 15%, var(--spade-club) 2px, transparent 2px),
                radial-gradient(circle at 85% 15%, var(--heart-diamond) 2px, transparent 2px),
                radial-gradient(circle at 15% 85%, var(--heart-diamond) 2px, transparent 2px),
                radial-gradient(circle at 85% 85%, var(--spade-club) 2px, transparent 2px);
            background-size: 120px 120px;
        }

        .bg-symbols {
            position: fixed;
            inset: 0;
            pointer-events: none;
            z-index: 0;
            opacity: 0.025;
            background-image: 
                url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Cpath fill='%23D4AF37' d='M50 15c-3 8-12 15-22 25-9 9-15 18-15 27 0 9 7 16 16 16s16-7 16-16c0-9-6-18-15-27-10-10-19-17-22-25z' transform='scale(0.6)'/%3E%3C/svg%3E"),
                url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Cpath fill='%239E0000' d='M50 88c-5-8-40-32-40-58C10 14 26 6 50 25c24-19 40-11 40 5 0 26-35 50-40 58z' transform='scale(0.6)'/%3E%3C/svg%3E"),
                url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Cpath fill='%239E0000' d='M50 10c-5 0-10 5-10 12 0 11 10 22 10 22s10-11 10-22c0-7-5-12-10-12zM50 58c-8 0-14 6-14 14 0 12 14 20 14 20s14-8 14-20c0-8-6-14-14-14z' transform='scale(0.6)'/%3E%3C/svg%3E"),
                url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Cpath fill='%231A1A2E' d='M50 12c-7 0-13 5-13 13 0 11 13 21 13 21s13-10 13-21c0-8-6-13-13-13zM50 62c-9 0-16 7-16 16 0 13 16 22 16 22s16-9 16-22c0-9-7-16-16-16z' transform='scale(0.6)'/%3E%3C/svg%3E");
            background-size: 180px 180px;
            background-position: 0 0, 45px 90px, 135px 45px, 90px 135px;
            background-repeat: repeat;
        }

        /* ===== LAYAR LOGIN ===== */
        .login-screen {
            position: fixed;
            inset: 0;
            background: radial-gradient(ellipse at center, #1A1A2E 0%, #0F0F1A 60%, #000000 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 9999;
            padding: 20px;
        }
        .login-box {
            background: linear-gradient(145deg, #252540, #1A1A30);
            padding: 45px 40px;
            border-radius: var(--radius-lg);
            box-shadow: 
                0 0 0 2px var(--gold-mid),
                0 0 60px rgba(212, 175, 55, 0.12),
                0 20px 60px rgba(0, 0, 0, 0.5);
            width: 100%;
            max-width: 440px;
            text-align: center;
            animation: loginFadeIn 0.6s ease-out;
        }
        @keyframes loginFadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .login-box h2 {
            color: var(--gold-light);
            margin-bottom: 8px;
            font-size: 28px;
            font-weight: 700;
            letter-spacing: 1px;
        }
        .login-box .subtitle {
            color: var(--text-muted);
            font-size: 14px;
            margin-bottom: 30px;
        }
        .login-box input {
            width: 100%;
            padding: 15px 20px;
            margin-bottom: 16px;
            border: 2px solid #333355;
            border-radius: var(--radius-md);
            font-size: 15px;
            background: rgba(255, 255, 255, 0.03);
            color: var(--text-white);
            transition: all 0.3s ease;
        }
        .login-box input:focus {
            outline: none;
            border-color: var(--gold-mid);
            background: rgba(255, 255, 255, 0.05);
            box-shadow: 0 0 0 3px rgba(212, 175, 55, 0.1);
        }
        .login-box button {
            width: 100%;
            padding: 15px;
            background: var(--bg-gold);
            color: #2C1810;
            border: none;
            border-radius: var(--radius-md);
            font-size: 17px;
            font-weight: 700;
            cursor: pointer;
            box-shadow: 0 4px 20px rgba(184, 134, 11, 0.35);
            transition: all 0.3s ease;
        }
        .login-box button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 25px rgba(184, 134, 11, 0.45);
        }
        .login-error {
            color: #FF6B6B;
            margin-top: 15px;
            font-size: 14px;
            display: none;
        }
        .card-icon {
            font-size: 72px;
            margin-bottom: 10px;
            filter: drop-shadow(0 0 15px rgba(212, 175, 55, 0.3));
        }

        /* ===== TOMBOL MODE ===== */
        .btn-toggle-presentation, .btn-back-edit {
            position: fixed;
            top: 24px;
            right: 24px;
            z-index: 50;
            font-weight: 600;
            border: none;
            padding: 12px 24px;
            border-radius: var(--radius-md);
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 14px;
        }
        .btn-toggle-presentation {
            background: var(--bg-gold);
            color: #2C1810;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
        }
        .btn-toggle-presentation:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(212, 175, 55, 0.25);
        }
        .btn-back-edit {
            background: var(--red-main);
            color: white;
            display: none;
            box-shadow: 0 4px 15px rgba(158, 0, 0, 0.3);
        }
        .btn-back-edit:hover {
            background: var(--red-dark);
        }
        body.presentation-mode .btn-back-edit { display: block; }
        body.presentation-mode .btn-toggle-presentation,
        body.presentation-mode .admin-controls,
        body.presentation-mode .tournament-selector { display: none; }

        /* ===== KONTEN UTAMA ===== */
        .container {
            position: relative;
            z-index: 1;
            max-width: 1480px;
            margin: 0 auto;
            display: none;
            animation: fadeIn 0.5s ease-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* ======================================
           HEADER — TATA LETAK LOGO RAPI & MODERN
           ====================================== */
        .main-header {
            background: linear-gradient(180deg, rgba(37, 30, 18, 0.95) 0%, rgba(26, 22, 14, 0.9) 100%);
            border-radius: var(--radius-lg);
            padding: 30px;
            margin-bottom: 28px;
            border: 2px solid rgba(212, 175, 55, 0.25);
            box-shadow: var(--shadow-gold);
            position: relative;
            overflow: hidden;
        }
        .main-header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: var(--bg-gold);
        }

        .header-row-1 {
            display: grid;
            grid-template-columns: 1fr auto 1fr;
            gap: 30px;
            align-items: flex-start;
            margin-bottom: 24px;
        }

        .logo-block {
            display: flex;
            flex-direction: column;
        }
        .logo-block.left { align-items: flex-start; }
        .logo-block.center { align-items: center; text-align: center; }
        .logo-block.right { align-items: flex-end; }

        .logo-block h4 {
            font-size: 13px;
            color: var(--gold-light);
            text-transform: uppercase;
            letter-spacing: 1.5px;
            margin-bottom: 12px;
            padding-bottom: 6px;
            border-bottom: 1px solid rgba(212, 175, 55, 0.15);
            display: inline-block;
        }

        /* ===== GRID LOGO ===== */
        .logo-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            align-items: center;
        }
        .logo-grid.left { justify-content: flex-start; }
        .logo-grid.center { justify-content: center; }
        .logo-grid.right { justify-content: flex-end; }

        .logo-item {
            position: relative;
            width: 95px;
            height: 95px;
            background: #FFFFFF;
            border-radius: var(--radius-md);
            border: 2px solid var(--gold-mid);
            padding: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15), inset 0 0 0 1px rgba(255, 255, 255, 0.8);
            transition: all 0.3s ease;
        }
        .logo-item:hover {
            transform: translateY(-4px);
            box-shadow: 0 8px 20px rgba(212, 175, 55, 0.15), 0 4px 12px rgba(0, 0, 0, 0.2);
        }
        .logo-item.main-logo {
            width: 160px;
            height: 160px;
            border-width: 3px;
            box-shadow: 0 6px 20px rgba(212, 175, 55, 0.2);
        }
        .logo-item.main-logo:hover {
            transform: scale(1.02);
        }
        .logo-item img {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
        }

        .logo-delete-btn {
            position: absolute;
            top: -8px;
            right: -8px;
            width: 26px;
            height: 26px;
            background: var(--red-main);
            color: white;
            border: 2px solid white;
            border-radius: 50%;
            font-size: 15px;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 3px 8px rgba(0, 0, 0, 0.3);
            opacity: 0;
            transition: all 0.25s ease;
            z-index: 10;
        }
        .logo-item:hover .logo-delete-btn { opacity: 1; }
        .logo-delete-btn:hover {
            background: var(--red-dark);
            transform: scale(1.15);
        }

        .logo-add-btn {
            width: 95px;
            height: 95px;
            border: 2px dashed rgba(212, 175, 55, 0.5);
            background: rgba(255, 255, 255, 0.02);
            border-radius: var(--radius-md);
            color: var(--gold-mid);
            font-size: 28px;
            cursor: pointer;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }
        .logo-add-btn.main-logo {
            width: 160px;
            height: 160px;
            font-size: 36px;
        }
        .logo-add-btn:hover {
            background: rgba(212, 175, 55, 0.08);
            border-color: var(--gold-mid);
        }
        .logo-add-btn span {
            font-size: 11px;
            margin-top: 4px;
            color: var(--text-muted);
        }

        /* ===== SPONSOR SECTION ===== */
        .sponsor-section {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid rgba(212, 175, 55, 0.12);
            text-align: center;
        }
        .sponsor-section h4 {
            font-size: 13px;
            color: var(--gold-light);
            text-transform: uppercase;
            letter-spacing: 1.5px;
            margin-bottom: 12px;
        }

        /* ===== JUDUL & INFO TURNAMEN ===== */
        .header-info {
            text-align: center;
            margin: 28px 0 20px;
        }
        .header-info h1 {
            font-size: clamp(24px, 5vw, 38px);
            color: var(--gold-light);
            text-shadow: 0 0 30px rgba(212, 175, 55, 0.25);
            letter-spacing: 3px;
            margin-bottom: 14px;
            font-weight: 800;
        }
        .main-meta {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 12px 20px;
            font-size: 14px;
            color: var(--text-soft);
        }
        .main-meta span {
            background: rgba(212, 175, 55, 0.06);
            border: 1px solid rgba(212, 175, 55, 0.15);
            padding: 10px 20px;
            border-radius: 30px;
            backdrop-filter: blur(4px);
        }
        .round-display {
            text-align: center;
            margin-top: 20px;
            padding: 14px 30px;
            background: linear-gradient(90deg, transparent, rgba(184, 134, 11, 0.08), transparent);
            border-radius: var(--radius-md);
            font-size: clamp(20px, 4vw, 28px);
            font-weight: 700;
            color: var(--gold-light);
            letter-spacing: 4px;
        }
        .round-display span {
            display: inline-block;
            padding: 0 15px;
        }

        /* ======================================
           NAVIGASI SLIDER — LUAR AREA KONTEN
           ====================================== */
        .slider-nav-outer {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            align-items: center;
            gap: 16px;
            background: rgba(10, 10, 20, 0.85);
            padding: 16px 32px;
            border-radius: 50px;
            border: 2px solid rgba(212, 175, 55, 0.3);
            z-index: 60;
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.4);
            backdrop-filter: blur(10px);
        }
        body:not(.presentation-mode) .slider-nav-outer {
            position: relative;
            bottom: auto;
            margin: 30px auto;
            background: rgba(26, 26, 46, 0.6);
            max-width: 540px;
        }
        .slider-btn {
            background: var(--bg-gold);
            color: #2C1810;
            border: none;
            padding: 11px 22px;
            border-radius: var(--radius-md);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 14px;
        }
        .slider-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(212, 175, 55, 0.25);
        }
        .slider-btn.auto {
            background: linear-gradient(135deg, #1E7E32, #27AE60);
            color: white;
        }
        .slider-btn.auto.active {
            background: var(--red-main);
        }
        .slider-indicator {
            font-size: 14px;
            color: var(--text-soft);
            min-width: 110px;
            text-align: center;
            font-weight: 500;
        }

        /* ===== SLIDER PENAYANGAN ===== */
        .presentation-slider {
            position: relative;
            min-height: 400px;
        }
        .slide-page {
            display: none;
            width: 100%;
            animation: slideFadeIn 0.6s ease-out;
        }
        .slide-page.active { display: block; }
        @keyframes slideFadeIn {
            from { opacity: 0; transform: translateX(15px); }
            to { opacity: 1; transform: translateX(0); }
        }

        /* ===== PILIHAN TURNAMEN ===== */
        .tournament-selector {
            background: var(--bg-card);
            border-radius: var(--radius-lg);
            padding: 24px;
            margin-bottom: 28px;
            border: 1px solid rgba(212, 175, 55, 0.15);
        }
        .tournament-selector h4 {
            color: var(--gold-light);
            margin-bottom: 16px;
            font-size: 17px;
        }
        .tournament-item {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            padding: 14px 18px;
            background: rgba(255, 255, 255, 0.02);
            border-radius: var(--radius-md);
            margin-bottom: 10px;
            border-left: 3px solid transparent;
            transition: all 0.25s ease;
        }
        .tournament-item:hover {
            background: rgba(212, 175, 55, 0.04);
        }
        .tournament-item.active {
            border-left-color: var(--gold-mid);
            background: rgba(212, 175, 55, 0.06);
        }
        .tournament-item strong {
            color: var(--text-white);
            font-size: 15px;
        }
        .tournament-item span small {
            color: var(--text-muted);
            font-size: 13px;
        }

        /* ===== PANEL ADMIN ===== */
        .admin-controls {
            background: var(--bg-card);
            border-radius: var(--radius-lg);
            padding: 28px;
            margin-bottom: 28px;
            border: 1px solid rgba(212, 175, 55, 0.15);
        }
        .admin-section {
            margin-bottom: 26px;
            padding-bottom: 26px;
            border-bottom: 1px dashed rgba(212, 175, 55, 0.1);
        }
        .admin-section:last-child {
            border-bottom: none;
            margin-bottom: 0;
            padding-bottom: 0;
        }
        .admin-section h4 {
            color: var(--gold-light);
            margin-bottom: 16px;
            font-size: 17px;
        }

        input, select {
            padding: 12px 16px;
            border-radius: var(--radius-md);
            border: 1px solid #333355;
            background: rgba(255, 255, 255, 0.03);
            color: var(--text-white);
            font-size: 14px;
            margin: 6px;
            transition: all 0.25s ease;
        }
        input:focus, select:focus {
            outline: none;
            border-color: var(--gold-mid);
            background: rgba(255, 255, 255, 0.05);
        }
        input[type="file"] {
            border: none;
            padding: 8px 0;
            background: transparent;
            margin: 0;
        }

        .upload-limit-note {
            font-size: 12px;
            color: var(--text-muted);
            margin-top: 6px;
        }

        .btn-group {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 14px;
        }
        button {
            padding: 12px 20px;
            border-radius: var(--radius-md);
            border: none;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.25s ease;
            font-size: 14px;
        }
        button:hover {
            transform: translateY(-2px);
        }
        .btn-red {
            background: var(--red-main);
            color: white;
        }
        .btn-red:hover {
            background: var(--red-dark);
        }
        .btn-gold {
            background: var(--bg-gold);
            color: #2C1810;
            font-weight: 700;
        }
        .btn-gold:hover {
            box-shadow: 0 4px 15px rgba(184, 134, 11, 0.3);
        }
        .btn-dark {
            background: #2A2A40;
            color: white;
            border: 1px solid #444466;
        }
        .btn-dark:hover {
            background: #333355;
        }
        .btn-sm {
            padding: 9px 16px;
            font-size: 13px;
        }
        .status-saved {
            color: #68BB6A;
            font-size: 13px;
            margin-left: 12px;
            display: inline-flex;
            align-items: center;
        }

        /* ===== PILIHAN PUTARAN ===== */
        .round-selector {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        .round-option {
            padding: 10px 18px;
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid #333355;
            border-radius: var(--radius-sm);
            cursor: pointer;
            font-size: 14px;
            transition: all 0.25s ease;
        }
        .round-option:hover {
            border-color: var(--gold-mid);
            background: rgba(212, 175, 55, 0.04);
        }
        .round-option.active {
            background: var(--bg-gold);
            color: #2C1810;
            border-color: var(--gold-mid);
            font-weight: 600;
        }

        /* ======================================
           KARTU MEJA — DESAIN KARTU REMI
           ====================================== */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(360px, 1fr));
            gap: 24px;
        }
        .table-card {
            background: linear-gradient(145deg, #FFFFFF, #F8F6F0);
            color: #1A1A1A;
            border-radius: var(--radius-lg);
            box-shadow: var(--shadow-card);
            overflow: hidden;
            border: 5px solid #2C1810;
            position: relative;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .table-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.4);
        }
        .table-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 6px;
            background: var(--bg-gold);
        }
        .table-card::after {
            content: '♠ ♥ ♦ ♣';
            position: absolute;
            top: 12px;
            right: 18px;
            font-size: 14px;
            color: rgba(44, 24, 16, 0.15);
            letter-spacing: 6px;
        }
        .card-header {
            background: linear-gradient(180deg, #2C1810, #1A0F08);
            color: var(--gold-light);
            padding: 18px 22px;
            font-weight: 800;
            font-size: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 3px solid var(--gold-mid);
        }
        .card-header .suit {
            font-size: 22px;
            color: var(--gold-mid);
        }
        .card-round-info {
            font-size: 12px;
            opacity: 0.6;
            font-weight: 400;
        }

        .participant-row {
            padding: 15px 22px;
            border-bottom: 1px solid #E8E4DA;
            display: flex;
            align-items: center;
            font-size: 15px;
            gap: 14px;
            transition: background 0.2s ease;
        }
        .participant-row:hover {
            background: #F5F2E8;
        }
        .participant-num {
            background: var(--bg-gold);
            color: #2C1810;
            font-weight: 700;
            width: 32px;
            height: 32px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            flex-shrink: 0;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .participant-info {
            flex: 1;
        }
        .participant-name {
            font-weight: 600;
            color: #1A1A1A;
        }
        .participant-id {
            font-size: 12px;
            color: #777;
            margin-top: 3px;
        }
        .card-footer {
            padding: 14px 22px;
            background: #F0EBD8;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 13px;
            color: #666;
            border-top: 1px solid #D4C9A8;
        }

        /* ===== MODAL ===== */
        .modal-overlay {
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.8);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 100;
            padding: 20px;
            backdrop-filter: blur(6px);
        }
        .modal {
            background: linear-gradient(145deg, #FFFFFF, #F8F6F0);
            color: #1A1A1A;
            border-radius: var(--radius-lg);
            padding: 30px;
            max-width: 500px;
            width: 100%;
            border: 3px solid var(--gold-mid);
            box-shadow: 0 15px 50px rgba(0, 0, 0, 0.4);
            animation: modalPop 0.3s ease-out;
        }
        @keyframes modalPop {
            from { opacity: 0; transform: scale(0.9); }
            to { opacity: 1; transform: scale(1); }
        }
        .modal h3 {
            color: var(--red-main);
            margin-bottom: 22px;
            font-size: 20px;
        }
        .modal input, .modal select {
            width: 100%;
            margin-bottom: 16px;
            background: #FFFFFF;
            color: #1A1A1A;
            border: 1px solid #CCC;
        }
        .modal input:focus, .modal select:focus {
            border-color: var(--gold-mid);
        }
        .modal-buttons {
            display: flex;
            gap: 12px;
            justify-content: flex-end;
            margin-top: 10px;
        }

        /* ===== FOOTER ===== */
        .admin-footer {
            margin-top: 50px;
            text-align: center;
            padding: 30px;
            color: var(--text-muted);
            font-size: 13px;
            border-top: 1px solid rgba(212, 175, 55, 0.1);
        }
        .admin-name {
            color: var(--gold-mid);
            font-weight: 600;
        }
        .footer-symbols {
            font-size: 18px;
            margin-top: 8px;
            letter-spacing: 8px;
            color: var(--gold-mid);
            opacity: 0.6;
        }

        /* ======================================
           CETAK — SEMUA LOGO TAMPIL SEMPURNA
           ====================================== */
        @media print {
            * { -webkit-print-color-adjust: exact; print-color-adjust: exact; }
            body {
                background: white;
                color: black;
                padding: 15px;
            }
            .bg-pattern, .bg-symbols { display: none; }
            .admin-controls, .btn-toggle-presentation, .btn-back-edit,
            .tournament-selector, .slider-nav-outer, .admin-footer { display: none !important; }
            .main-header {
                background: white;
                border: 1px solid #333;
                box-shadow: none;
                padding: 20px;
            }
            .logo-item {
                border: 1px solid #CCC;
                box-shadow: none;
            }
            .logo-delete-btn { display: none !important; }
            .table-card {
                border: 2px solid #333;
                box-shadow: none;
            }
            .slide-page {
                display: block !important;
                page-break-after: always;
            }
            .slide-page:last-child { page-break-after: auto; }
            .grid { gap: 18px; }
        }

        /* ===== RESPONSIVE ===== */
        @media (max-width: 900px) {
            .header-row-1 {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            .logo-block.left, .logo-block.right { align-items: center; }
            .logo-grid.left, .logo-grid.right { justify-content: center; }
        }
    </style>
</head>
<body>

<div class="bg-pattern"></div>
<div class="bg-symbols"></div>

<!-- === LAYAR LOGIN === -->
<div class="login-screen" id="loginScreen">
    <div class="login-box">
        <div class="card-icon">♠♥♦♣</div>
        <h2>🃏 Login Admin</h2>
        <p class="subtitle">Sistem Pembagian Meja Turnamen Kartu Remi</p>
        <input type="text" id="username" placeholder="Username">
        <input type="password" id="password" placeholder="Password">
        <button onclick="doLogin()">MASUK KE APLIKASI</button>
        <div class="login-error" id="loginError">❌ Username atau Password salah!</div>
    </div>
</div>

<button class="btn-toggle-presentation" id="btnToggleMode" onclick="togglePresentationMode()">📺 Mode Penayangan</button>
<button class="btn-back-edit" id="btnBackEdit" onclick="togglePresentationMode()">⚙️ Kembali Edit</button>

<div class="container" id="displayArea">

    <!-- === PILIHAN TURNAMEN === -->
    <div class="tournament-selector" id="tournamentListSection">
        <h4>📂 Daftar Turnamen Tersimpan</h4>
        <div id="tournamentList"></div>
        <div class="btn-group" style="margin-top:12px;">
            <button class="btn-gold btn-sm" onclick="newTournament()">➕ Turnamen Baru</button>
            <span class="status-saved" id="saveStatus">✓ Tersimpan</span>
        </div>
    </div>

    <!-- ======================================
           HEADER — TATA LETAK LOGO LENGKAP
           ====================================== -->
    <div class="main-header">
        <div class="header-row-1">
            <!-- KIRI: Penyelenggara -->
            <div class="logo-block left">
                <h4>🏛️ Penyelenggara</h4>
                <div class="logo-grid left" id="logoOrgGrid"></div>
            </div>

            <!-- TENGAH: Logo Kegiatan (Utama) -->
            <div class="logo-block center">
                <h4>🏆 Logo Kegiatan</h4>
                <div class="logo-grid center" id="logoTournamentGrid"></div>
            </div>

            <!-- KANAN: Media Partner -->
            <div class="logo-block right">
                <h4>📢 Media Partner</h4>
                <div class="logo-grid right" id="logoMediaGrid"></div>
            </div>
        </div>

        <!-- SPONSOR — TENGAH BAWAH -->
        <div class="sponsor-section">
            <h4>💰 Sponsor</h4>
            <div class="logo-grid center" id="logoSponsorGrid"></div>
        </div>

        <!-- INFO & JUDUL -->
        <div class="header-info">
            <h1>🃏 <span id="dispTournamentName">TURNAMEN KARTU REMI</span> 🃏</h1>
            <div class="main-meta">
                <span>📍 <span id="dispLocation">-</span></span>
                <span>🏛️ <span id="dispOrganizer">-</span></span>
                <span>📅 <span id="dispDate">-</span></span>
            </div>
        </div>

        <div class="round-display">♠ <span id="dispCurrentRound">Round 1</span> ♥</div>
    </div>

    <!-- ======================================
           PANEL ADMIN — UPLOAD LOGO
           ====================================== -->
    <div class="admin-controls">
        <div class="admin-section">
            <h4>📋 Informasi Turnamen</h4>
            <input type="text" id="inpTournamentName" placeholder="Nama Turnamen / Kegiatan" style="width:100%;max-width:480px;">
            <input type="text" id="inpLocation" placeholder="Lokasi Kegiatan">
            <input type="text" id="inpOrganizerName" placeholder="Nama Penyelenggara">
            <input type="text" id="inpDate" placeholder="Tanggal Pelaksanaan">

            <h4 style="margin-top:24px;">🖼️ Upload Logo</h4>
            
            <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:18px;margin-top:10px;">
                <div>
                    <label style="color:var(--gold-light);font-size:14px;font-weight:500;">🏆 Logo Kegiatan (Utama)</label>
                    <input type="file" accept="image/*" onchange="handleUpload(event,'tournament')">
                    <p class="upload-limit-note">Maksimal 1 logo</p>
                </div>
                <div>
                    <label style="color:var(--gold-light);font-size:14px;font-weight:500;">🏛️ Logo Penyelenggara</label>
                    <input type="file" accept="image/*" onchange="handleUpload(event,'organizer')">
                    <p class="upload-limit-note">Bisa upload hingga 100 logo</p>
                </div>
                <div>
                    <label style="color:var(--gold-light);font-size:14px;font-weight:500;">💰 Logo Sponsor</label>
                    <input type="file" accept="image/*" onchange="handleUpload(event,'sponsor')">
                    <p class="upload-limit-note">Bisa upload hingga 100 logo</p>
                </div>
                <div>
                    <label style="color:var(--gold-light);font-size:14px;font-weight:500;">📢 Logo Media Partner</label>
                    <input type="file" accept="image/*" onchange="handleUpload(event,'media')">
                    <p class="upload-limit-note">Bisa upload hingga 100 logo</p>
                </div>
            </div>

            <div class="btn-group" style="margin-top:20px;">
                <button class="btn-dark btn-sm" onclick="updateTournamentDisplay()">🔄 Perbarui Info</button>
                <button class="btn-gold btn-sm" onclick="saveCurrentTournament()">💾 Simpan Turnamen</button>
            </div>
        </div>

        <div class="admin-section">
            <h4>🔄 Pilih Putaran</h4>
            <div class="round-selector" id="roundSelector"></div>
        </div>

        <div class="admin-section">
            <h4>⚙️ Pengelolaan Data</h4>
            <div class="btn-group">
                <button class="btn-red" onclick="openAddTableModal()">➕ Tambah Meja</button>
                <button class="btn-gold" onclick="openAddParticipantModal()">👤 Tambah Peserta</button>
                <button class="btn-dark btn-sm" onclick="window.print()">🖨️ Cetak Dokumen</button>
                <button class="btn-red btn-sm" onclick="logout()">🚪 Keluar</button>
            </div>
        </div>
    </div>

    <!-- NAVIGASI -->
    <div class="slider-nav-outer">
        <button class="slider-btn" onclick="prevPage()">◀ Sebelumnya</button>
        <span class="slider-indicator" id="pageIndicator">Halaman 1 / 1</span>
        <button class="slider-btn" onclick="nextPage()">Berikutnya ▶</button>
        <button class="slider-btn auto" id="autoPlayBtn" onclick="toggleAutoPlay()">▶ Auto</button>
    </div>

    <!-- SLIDER -->
    <div class="presentation-slider" id="presentationSlider">
        <div id="slidesContainer"></div>
    </div>

    <div class="admin-footer">
        🃏 Sistem Pembagian Meja Turnamen Kartu Remi • Dikelola oleh <span class="admin-name">Dennys Sefta Saemani</span>
        <div class="footer-symbols">♠ ♥ ♦ ♣</div>
    </div>
</div>

<!-- MODAL: TAMBAH MEJA -->
<div class="modal-overlay" id="addTableModal">
    <div class="modal">
        <h3>➕ Tambah Meja Baru</h3>
        <input type="text" id="newTableName" placeholder="Contoh: Meja 7">
        <div class="modal-buttons">
            <button class="btn-dark btn-sm" onclick="closeModal('addTableModal')">Batal</button>
            <button class="btn-gold btn-sm" onclick="addNewTable()">Buat Meja</button>
        </div>
    </div>
</div>

<!-- MODAL: TAMBAH PESERTA -->
<div class="modal-overlay" id="addParticipantModal">
    <div class="modal">
        <h3>👤 Tambah Peserta Baru</h3>
        <input type="text" id="partName" placeholder="Nama Lengkap Peserta">
        <input type="text" id="partId" placeholder="Nomor ID / Kontak">
        <select id="partTable"></select>
        <div class="modal-buttons">
            <button class="btn-dark btn-sm" onclick="closeModal('addParticipantModal')">Batal</button>
            <button class="btn-gold btn-sm" onclick="addParticipant()">Tambahkan</button>
        </div>
    </div>
</div>

<script>
// ======================================
// KONFIGURASI
// ======================================
const LOGIN_USERNAME = 'Denis7475';
const LOGIN_PASSWORD = '121912';
const RO
