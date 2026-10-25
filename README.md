<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Premium Savings Jars</title>
    <style>
        :root {
            --bg-color: #f0f4f8;
            --card-bg: #ffffff;
            --text-main: #2d3748;
            --text-muted: #718096;
            --border-color: #e2e8f0;
            --accent-default: #3182ce;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            padding: 40px 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }

        header {
            text-align: center;
            margin-bottom: 35px;
            max-width: 600px;
        }

        header h1 {
            font-size: 2.5rem;
            color: #1a202c;
            margin-bottom: 8px;
            font-weight: 800;
        }

        header p {
            color: var(--text-muted);
            font-size: 1.05rem;
        }

        .controls {
            margin-bottom: 35px;
        }

        .btn-add {
            background-color: #2b6cb0;
            color: white;
            border: none;
            padding: 12px 26px;
            font-size: 1rem;
            font-weight: 600;
            border-radius: 30px;
            cursor: pointer;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.08);
            transition: all 0.2s ease;
        }

        .btn-add:hover {
            background-color: #1a4975;
            transform: translateY(-1px);
        }

        .jars-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 30px;
            width: 100%;
            max-width: 1200px;
        }

        .jar-card {
            background: var(--card-bg);
            border-radius: 24px;
            padding: 24px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.04);
            border: 1px solid var(--border-color);
            display: flex;
            flex-direction: column;
            align-items: center;
            position: relative;
            transition: transform 0.2s;
        }

        .jar-card:hover {
            transform: translateY(-4px);
        }

        .delete-btn {
            position: absolute;
            top: 15px;
            right: 18px;
            background: none;
            border: none;
            color: #cbd5e0;
            cursor: pointer;
            font-size: 1.4rem;
            transition: color 0.2s;
            z-index: 10;
        }

        .delete-btn:hover {
            color: #e53e3e;
        }

        .settings-btn {
            position: absolute;
            top: 15px;
            left: 18px;
            background: none;
            border: none;
            color: #cbd5e0;
            cursor: pointer;
            font-size: 1.2rem;
            transition: color 0.2s;
            z-index: 10;
        }

        .settings-btn:hover {
            color: #4a5568;
        }
        
        /* Premium Smooth Mason Jar Aesthetics */
        .jar-container {
            position: relative;
            margin: 20px 0 10px 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            filter: drop-shadow(0 8px 12px rgba(0,0,0,0.06));
        }

        .jar-cap {
            width: 96px;
            height: 22px;
            background: linear-gradient(135deg, #fde047 0%, #eab308 100%);
            border: 2px solid #ca8a04;
            border-radius: 8px 8px 4px 4px;
            z-index: 5;
            position: relative;
            box-shadow: inset 0 2px 4px rgba(255,255,255,0.4), 0 2px 4px rgba(0,0,0,0.1);
        }

        /* Ridge lines on screw cap */
        .jar-cap::before {
            content: '';
            position: absolute;
            top: 3px;
            left: 10%;
            width: 80%;
            height: 12px;
            background: repeating-linear-gradient(90deg, transparent, transparent 6px, #ca8a04 6px, #ca8a04 8px);
            opacity: 0.3;
        }

        .jar-neck {
            width: 76px;
            height: 12px;
            background: linear-gradient(90deg, rgba(255,255,255,0.9) 0%, rgba(241,245,249,0.7) 50%, rgba(203,213,225,0.8) 100%);
            border-left: 2px solid #e2e8f0;
            border-right: 2px solid #cbd5e0;
            margin-top: -2px;
            z-index: 3;
        }

        .jar-visual {
            width: 144px;
            height: 190px;
            border: 4px solid rgba(226, 232, 240, 0.8);
            border-radius: 16px 16px 48px 48px;
            position: relative;
            overflow: hidden;
            background: linear-gradient(135deg, rgba(255,255,255,0.6) 0%, rgba(248,250,252,0.3) 100%);
            margin-top: -2px;
            z-index: 2;
            backdrop-filter: blur(1px);
        }

        /* Glass highlight shine reflection overlay */
        .jar-visual::before {
            content: '';
            position: absolute;
            top: 5%;
            left: 8px;
            width: 14px;
            height: 85%;
            background: linear-gradient(to bottom, rgba(255,255,255,0.6) 0%, rgba(255,255,255,0.1) 100%);
            border-radius: 20px;
            z-index: 4;
            pointer-events: none;
        }

        .jar-liquid {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 0%; 
            transition: height 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
            opacity: 0.85;
        }

        /* Moving water wave effect */
        .jar-liquid::after {
            content: '';
            position: absolute;
            top: -8px;
            left: 0;
            width: 200%;
            height: 16px;
            background: radial-gradient(circle at 50% 100%, transparent 35%, rgba(255,255,255,0.35) 40%, transparent 60%);
            background-size: 48px 16px;
            animation: wave 3s infinite linear;
        }

        @keyframes wave {
            0% { transform: translateX(0); }
            100% { transform: translateX(-48px); }
        }

        .jar-label-input {
            width: 90%;
            text-align: center;
            font-size: 1.3rem;
            font-weight: 700;
            color: var(--text-main);
            border: 1px solid transparent;
            background: transparent;
            padding: 4px;
            border-radius: 8px;
            margin-bottom: 2px;
            transition: background 0.2s;
        }

        .jar-label-input:hover {
            background: #f1f5f9;
        }

        .jar-label-input:focus {
            border-color: #cbd5e0;
            background: #ffffff;
            outline: none;
        }

        .input-group {
            width: 100%;
            margin-top: 15px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            font-size: 0.95rem;
        }

        .input-group label {
            color: var(--text-muted);
            font-weight: 700;
            font-size: 0.85rem;
            letter-spacing: 0.5px;
        }

        .number-input-wrapper {
            position: relative;
            display: flex;
            align-items: center;
            width: 65%;
        }

        .currency-symbol {
            position: absolute;
            left: 12px;
            color: var(--text-muted);
            font-weight: 600;
            pointer-events: none;
        }

        .number-input {
            width: 100%;
            padding: 10px 10px 10px 26px;
            border: 1px solid var(--border-color);
            border-radius: 12px;
            font-size: 1rem;
            font-weight: 600;
            color: var(--text-main);
            background: #f8fafc;
            transition: all 0.2s;
        }

        .number-input:focus {
            outline: none;
            border-color: #3182ce;
            background: #fff;
            box-shadow: 0 0 0 3px rgba(49, 130, 206, 0.1);
        }

        .theme-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
            width: 100%;
            margin-top: 18px;
            padding-top: 12px;
            border-top: 1px dashed var(--border-color);
        }

        .theme-row span {
            color: var(--text-muted);
            font-size: 0.8rem;
            font-weight: 700;
            letter-spacing: 0.5px;
        }

        .color-dots {
            display: flex;
            gap: 6px;
        }

        .color-dot {
            width: 20px;
            height: 20px;
            border-radius: 6px;
            cursor: pointer;
            border: 2px solid transparent;
            transition: transform 0.1s;
        }

        .color-dot:hover { transform: scale(1.15); }
        .color-dot.active { border-color: #4a5568; transform: scale(1.05); }

        .percentage-badge {
            font-size: 1rem;
            font-weight: 800;
            padding: 4px 14px;
            border-radius: 20px;
            letter-spacing: 0.3px;
        }

        .target-display {
            font-size: 0.8rem;
            color: var(--text-muted);
            font-weight: 600;
            margin-top: 4px;
        }

        @media(max-width: 640px) {
            body { padding: 20px 10px; }
            .jars-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <header>
        <h1>Custom Savings Jars</h1>
        <p>Click directly on titles to customize jar labels. Access target settings privately via the gear icon.</p>
    </header>

    <div class="controls">
