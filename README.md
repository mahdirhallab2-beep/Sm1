<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بوت تداول Deriv - 7 أسواق متوازية</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4A90E2;
            --primary-dark: #357ABD;
            --secondary: #A85AEC;
            --success: #3DDC84;
            --danger: #FF6B6B;
            --warning: #FFD93D;
            --info: #64B5F6;
            --text-color: #EAEAEA;
            --gradient-start: #1D2D44;
            --gradient-end: #121E2F;
            --card-bg: rgba(45, 62, 80, 0.5);
            --card-shadow: 0 15px 30px rgba(0, 0, 0, 0.7);
            --card-border: 1px solid rgba(255, 255, 255, 0.15);
            --input-bg: rgba(255, 255, 255, 0.08);
            --log-bg: rgba(30, 45, 60, 0.9);
            --chart-bg: #2C3E50;
            --grid-color: rgba(255, 255, 255, 0.1);
            --log-border-bottom: rgba(255, 255, 255, 0.1);
            --table-row-even: rgba(255, 255, 255, 0.05);
            --table-row-hover: rgba(255, 255, 255, 0.1);
            --placeholder-color: rgba(255, 255, 255, 0.5);
        }

        .light-mode {
            --primary: #0077b6;
            --primary-dark: #005f96;
            --secondary: #6A1B9A;
            --success: #28A745;
            --danger: #DC3545;
            --warning: #FFC107;
            --info: #17A2B8;
            --text-color: #343A40;
            --gradient-start: #F0F4F8;
            --gradient-end: #E3EAF0;
            --card-bg: #FFFFFF;
            --card-shadow: 0 6px 16px rgba(0, 0, 0, 0.1);
            --card-border: 1px solid #DCE3EB;
            --input-bg: #F8F9FA;
            --log-bg: #FFFFFF;
            --chart-bg: #FFFFFF;
            --grid-color: rgba(0, 0, 0, 0.1);
            --log-border-bottom: rgba(0, 0, 0, 0.05);
            --table-row-even: rgba(0, 0, 0, 0.03);
            --table-row-hover: rgba(0, 0, 0, 0.07);
            --placeholder-color: rgba(52, 58, 64, 0.5);
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Tajawal', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            transition: background-color 0.3s, color 0.3s, border-color 0.3s, box-shadow 0.3s;
        }
        
        body {
            background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
            color: var(--text-color);
            line-height: 1.6;
            min-height: 100vh;
            padding: 30px 20px;
            background-attachment: fixed;
        }

        .container {
            max-width: 1800px;
            margin: 0 auto;
        }
        
        header {
            background: var(--card-bg);
            color: var(--primary);
            padding: 30px;
            text-align: center;
            border-radius: 20px;
            margin-bottom: 30px;
            box-shadow: var(--card-shadow);
            backdrop-filter: blur(10px);
            border: var(--card-border);
            position: relative;
            overflow: hidden;
            border-right: 5px solid var(--primary);
        }
        
        header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 5px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
        }
        
        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
            color: var(--text-color);
            font-weight: 500;
        }
        
        .card {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 25px;
            box-shadow: var(--card-shadow);
            backdrop-filter: blur(10px);
            transition: transform 0.4s ease;
            border: var(--card-border);
            position: relative;
            overflow: hidden;
            margin-bottom: 30px;
        }
        
        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            transform: scaleX(0);
            transition: transform 0.4s ease;
        }
        
        .card:hover::before {
            transform: scaleX(1);
        }
        
        .card:hover {
            transform: translateY(-5px);
        }
        
        .card-title {
            font-size: 1.6rem;
            margin-bottom: 20px;
            color: var(--primary);
            border-bottom: 2px solid rgba(0, 119, 182, 0.2);
            padding-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 700;
        }
        
        .card-title i {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .form-group {
            margin-bottom: 20px;
            position: relative;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--text-color);
            font-size: 1rem;
            opacity: 0.9;
        }
        
        input, select {
            width: 100%;
            padding: 15px 18px;
            border: var(--card-border);
            border-radius: 10px;
            font-size: 1rem;
            transition: all 0.3s ease;
            background: var(--input-bg);
            color: var(--text-color);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        input[type="number"]::-webkit-inner-spin-button, 
        input[type="number"]::-webkit-outer-spin-button { 
            -webkit-appearance: none;
            margin: 0;
        }

        input::placeholder {
            color: var(--placeholder-color);
        }
        
        input:focus, select:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 5px rgba(74, 144, 226, 0.3);
            transform: translateY(-2px);
            background: var(--input-bg);
        }
        
        small {
            color: var(--info);
            display: block;
            margin-top: 5px;
            opacity: 0.8;
            font-size: 0.85rem;
        }

        button {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 16px 22px;
            border-radius: 12px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 700;
            transition: all 0.3s ease;
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            box-shadow: 0 8px 20px rgba(0, 119, 182, 0.3);
            position: relative;
            overflow: hidden;
            margin-top: 12px;
        }
        
        .btn-success {
            background: linear-gradient(135deg, var(--success), #2ECC71);
            box-shadow: 0 8px 20px rgba(61, 220, 132, 0.4);
        }
        
        .btn-danger {
            background: linear-gradient(135deg, var(--danger), #E74C3C);
            box-shadow: 0 8px 20px rgba(255, 107, 107, 0.4);
        }

        .btn-warning {
            background: linear-gradient(135deg, var(--warning), #F39C12);
            color: var(--text-color);
            box-shadow: 0 8px 20px rgba(255, 217, 61, 0.4);
        }
        
        .status-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .status-box {
            background: var(--card-bg);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            box-shadow: var(--card-shadow);
            backdrop-filter: blur(10px);
            transition: all 0.4s ease;
            border: var(--card-border);
            position: relative;
            overflow: hidden;
            border-left: 5px solid var(--primary); 
        }

        .status-box:nth-child(1) { border-left-color: var(--success); }
        .status-box:nth-child(2) { border-left-color: var(--info); }
        .status-box:nth-child(3) { border-left-color: var(--warning); }
        .status-box:nth-child(4) { border-left-color: var(--primary); }
        .status-box:nth-child(5) { border-left-color: var(--secondary); }
        .status-box:nth-child(6) { border-left-color: var(--danger); }
        .status-box:nth-child(7) { border-left-color: var(--info); }
        .status-box:nth-child(8) { border-left-color: var(--success); }
        .status-box:nth-child(9) { border-left-color: var(--warning); }
        .status-box:nth-child(10) { border-left-color: var(--secondary); }
        .status-box:nth-child(11) { border-left-color: var(--primary); }
        .status-box:nth-child(12) { border-left-color: var(--danger); }
        
        .status-label {
            font-size: 1rem;
            color: var(--text-color);
            opacity: 0.7;
            margin-bottom: 12px;
            font-weight: 600;
        }
        
        .status-value {
            font-size: 2rem;
            font-weight: bold;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); 
        }
        
        .profit {
            -webkit-text-fill-color: var(--success) !important;
        }
        
        .loss {
            -webkit-text-fill-color: var(--danger) !important;
        }
        
        .log-container {
            height: 350px;
            overflow-y: auto;
            border: var(--card-border);
            border-radius: 15px;
            padding: 15px;
            background-color: var(--log-bg);
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
            box-shadow: inset 0 5px 15px rgba(0, 0, 0, 0.1);
            color: var(--text-color);
        }
        
        .log-entry {
            padding: 10px 0;
            border-bottom: 1px solid var(--log-border-bottom);
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.3s ease;
            color: var(--text-color);
            font-size: 0.9rem;
        }
        
        .log-entry:hover {
            background-color: var(--table-row-hover);
            border-radius: 8px;
            padding-left: 8px;
            padding-right: 8px;
        }
        
        .log-time {
            color: var(--text-color);
            opacity: 0.5;
            font-size: 0.8rem;
            min-width: 80px;
            font-weight: 600;
        }
        
        .log-success { color: var(--success); }
        .log-error { color: var(--danger); }
        .log-info { color: var(--info); }
        .log-warning { color: var(--warning); }
        
        #theme-toggle {
            position: fixed;
            top: 20px;
            left: 20px;
            z-index: 1000;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: var(--card-bg);
            color: var(--text-color);
            border: 2px solid var(--primary);
            box-shadow: var(--card-shadow);
            font-size: 1.5rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }
        
        #theme-toggle:hover {
            background: var(--primary);
            color: white;
        }
        
        .log-container::-webkit-scrollbar {
            width: 8px;
        }
        
        .log-container::-webkit-scrollbar-track {
            background: var(--chart-bg);
            border-radius: 4px;
        }
        
        .log-container::-webkit-scrollbar-thumb {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border-radius: 4px;
        }

        .log-container::-webkit-scrollbar-thumb:hover {
            background: linear-gradient(135deg, var(--primary-dark), var(--secondary));
        }

        .settings-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
        
        @media (max-width: 768px) {
            .settings-grid {
                grid-template-columns: 1fr;
            }
        }
        
        .checkbox-group {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 12px;
        }
        
        .checkbox-group input[type="checkbox"] {
            width: 18px;
            height: 18px;
            box-shadow: none;
        }
        
        .checkbox-group label {
            margin-bottom: 0;
            opacity: 1;
            font-weight: normal;
            font-size: 0.95rem;
        }
        
        .badge {
            padding: 4px 8px;
            border-radius: 6px;
            font-size: 0.8rem;
            font-weight: bold;
            color: white;
            display: inline-block;
            margin-left: 5px;
        }
        
        .badge-success { background-color: var(--success); }
        .badge-danger { background-color: var(--danger); }
        .badge-info { background-color: var(--info); }
        .badge-warning { background-color: var(--warning); }
        .badge-primary { background-color: var(--primary); }
        
        .monitoring-panel {
            background: var(--card-bg);
            border-radius: 15px;
            padding: 20px;
            margin-top: 20px;
            border: 2px solid var(--info);
            box-shadow: var(--card-shadow);
            margin-bottom: 25px;
        }
        
        .monitoring-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 12px;
            margin-top: 12px;
        }
        
        .monitoring-item {
            background: rgba(0, 0, 0, 0.1);
            border-radius: 8px;
            padding: 12px;
            text-align: center;
        }
        
        .light-mode .monitoring-item {
            background: rgba(0, 0, 0, 0.03);
        }
        
        .monitoring-value {
            font-size: 1.3rem;
            font-weight: bold;
            color: var(--primary);
            margin-top: 5px;
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 1.8rem;
            }
            
            .status-value {
                font-size: 1.5rem;
            }
            
            .card {
                padding: 15px;
            }
            
            .monitoring-grid {
                grid-template-columns: 1fr;
            }
        }
        
        .markets-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }
        
        .market-card {
            background: var(--card-bg);
            border-radius: 15px;
            padding: 20px;
            border: 2px solid rgba(74, 144, 226, 0.3);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .market-card:hover {
            border-color: var(--primary);
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
        }
        
        .market-card.using-martingale {
            border-color: var(--warning);
            background: rgba(255, 217, 61, 0.05);
        }
        
        .market-card.disabled {
            border-color: var(--danger);
            background: rgba(255, 107, 107, 0.05);
            opacity: 0.7;
        }
        
        .market-card.trading-active {
            border-color: var(--success);
            background: rgba(61, 220, 132, 0.05);
        }
        
        .market-card.token-missing {
            border-color: var(--info);
            background: rgba(100, 181, 246, 0.05);
        }
        
        .market-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid var(--card-border);
        }
        
        .market-name {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .market-status {
            font-size: 0.9rem;
            padding: 4px 10px;
            border-radius: 20px;
            font-weight: bold;
        }
        
        .status-active { background: rgba(61, 220, 132, 0.2); color: var(--success); }
        .status-martingale { background: rgba(255, 217, 61, 0.2); color: var(--warning); }
        .status-disabled { background: rgba(255, 107, 107, 0.2); color: var(--danger); }
        .status-waiting { background: rgba(100, 181, 246, 0.2); color: var(--info); }
        .status-no-token { background: rgba(255, 255, 255, 0.1); color: var(--text-color); opacity: 0.7; }
        .status-trading { background: rgba(61, 220, 132, 0.3); color: var(--success); animation: pulse 1s infinite; }
        
        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.6; }
            100% { opacity: 1; }
        }
        
        .market-info {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 15px;
        }
        
        .info-item {
            background: rgba(0, 0, 0, 0.1);
            border-radius: 8px;
            padding: 10px;
            text-align: center;
        }
        
        .info-label {
            font-size: 0.85rem;
            color: var(--text-color);
            opacity: 0.7;
            margin-bottom: 5px;
        }
        
        .info-value {
            font-size: 1.1rem;
            font-weight: bold;
            color: var(--text-color);
        }
        
        .info-value.profit { color: var(--success); }
        .info-value.loss { color: var(--danger); }
        
        .ticks-preview {
            background: rgba(0, 0, 0, 0.1);
            border-radius: 8px;
            padding: 10px;
            margin-top: 15px;
            min-height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 5px;
        }
        
        .tick-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            transition: all 0.3s ease;
        }
        
        .tick-up { background-color: var(--success); }
        .tick-down { background-color: var(--danger); }
        .tick-neutral { background-color: var(--info); opacity: 0.5; }
        
        .layout-grid {
            display: grid;
            grid-template-columns: 1fr 1.5fr;
            gap: 25px;
            margin-bottom: 25px;
        }
        
        @media (max-width: 1200px) {
            .layout-grid {
                grid-template-columns: 1fr;
            }
        }
        
        .markets-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            background: var(--card-bg);
            border-radius: 12px;
            overflow: hidden;
            box-shadow: var(--card-shadow);
        }
        
        .markets-table th, .markets-table td {
            padding: 12px 15px;
            text-align: center;
            border-bottom: 1px solid var(--card-border);
        }
        
        .markets-table th {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            font-weight: 700;
            font-size: 0.95rem;
            text-align: center;
        }
        
        .markets-table tr:nth-child(even) {
            background-color: var(--table-row-even);
        }
        
        .markets-table tr:hover {
            background-color: var(--table-row-hover);
        }
        
        .timer-container {
            background: var(--card-bg);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            margin-bottom: 25px;
            box-shadow: var(--card-shadow);
            backdrop-filter: blur(10px);
            border: var(--card-border);
            position: relative;
            overflow: hidden;
            border-right: 5px solid var(--secondary);
        }
        
        .timer-container h3 {
            font-size: 1.3rem;
            color: var(--text-color);
            margin-bottom: 15px;
        }
        
        .timer-display {
            font-size: 3rem;
            font-weight: bold;
            background: linear-gradient(135deg, var(--success), var(--info));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
        }
        
        .martingale-status {
            background: rgba(255, 217, 61, 0.1);
            border-radius: 12px;
            padding: 20px;
            margin-top: 20px;
            border: 2px solid var(--warning);
        }
        
        .martingale-info {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }
        
        .martingale-item {
            text-align: center;
            padding: 10px;
            background: rgba(255, 217, 61, 0.05);
            border-radius: 8px;
        }
        
        .martingale-label {
            font-size: 0.9rem;
            color: var(--warning);
            margin-bottom: 5px;
        }
        
        .martingale-value {
            font-size: 1.3rem;
            font-weight: bold;
            color: var(--warning);
        }
        
        .alert {
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
            animation: fadeIn 0.5s ease;
        }
        
        .alert-info {
            background: rgba(100, 181, 246, 0.2);
            border: 1px solid var(--info);
            color: var(--info);
        }
        
        .alert-warning {
            background: rgba(255, 217, 61, 0.2);
            border: 1px solid var(--warning);
            color: var(--warning);
        }
        
        .alert-danger {
            background: rgba(255, 107, 107, 0.2);
            border: 1px solid var(--danger);
            color: var(--danger);
        }
        
        .alert-success {
            background: rgba(61, 220, 132, 0.2);
            border: 1px solid var(--success);
            color: var(--success);
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .market-settings {
            background: rgba(0, 0, 0, 0.1);
            border-radius: 10px;
            padding: 15px;
            margin-top: 10px;
        }
        
        .market-settings h5 {
            color: var(--primary);
            margin-bottom: 10px;
            font-size: 1rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .market-settings-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
        }
        
        .market-settings-item {
            margin-bottom: 10px;
        }
        
        .market-settings-item label {
            font-size: 0.85rem;
            margin-bottom: 5px;
        }
        
        .market-settings-item input {
            padding: 10px 12px;
            font-size: 0.9rem;
        }
        
        .required-token {
            border: 2px solid var(--warning) !important;
            background: rgba(255, 217, 61, 0.05) !important;
            padding: 15px;
            border-radius: 10px;
        }
        
        .required-token .form-group:first-child {
            position: relative;
        }
        
        .required-token .form-group:first-child::after {
            content: 'ضروري';
            position: absolute;
            top: -10px;
            left: -10px;
            background: var(--warning);
            color: white;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 0.75rem;
            font-weight: bold;
        }
        
        .primary-stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .primary-stat-card {
            background: rgba(255, 217, 61, 0.1);
            border-radius: 12px;
            padding: 15px;
            text-align: center;
            border: 1px solid var(--warning);
        }
        
        .primary-stat-label {
            font-size: 0.9rem;
            color: var(--warning);
            margin-bottom: 8px;
        }
        
        .primary-stat-value {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--warning);
        }
        
        .capital-input-group {
            display: flex;
            gap: 10px;
            align-items: center;
        }
        
        .capital-input-group input {
            flex: 1;
        }
        
        .capital-input-group button {
            width: auto;
            padding: 15px 20px;
            margin-top: 0;
        }
        
        .max-martingale-reached {
            background: rgba(255, 107, 107, 0.2);
            border-color: var(--danger);
        }
    </style>
</head>
<body class="dark-mode"> 
    <button id="theme-toggle" title="تبديل الوضع الليلي/النهاري">
        <i class="fas fa-sun"></i> 
    </button>

    <div class="container">
        <header>
            <h1><i class="fas fa-robot"></i> نظام تداول Deriv - 7 أسواق متوازية</h1>
            <p class="subtitle">كل سوق مستقل - توكن مارتينجال مركزي - إعادة تعيين تلقائي للخسائر</p>
        </header>
        
        <div class="timer-container">
            <h3><i class="fas fa-clock"></i> وقت تشغيل النظام</h3>
            <div class="timer-display" id="trading-timer">00:00:00</div>
            <div id="timer-status" style="font-size: 1rem; color: var(--info);">النظام متوقف</div>
            <div style="margin-top: 10px; font-size: 0.9rem; color: var(--text-color); opacity: 0.8;">
                <span id="daily-stats">اليوم: 0 صفقات | 0.00 USD</span>
            </div>
        </div>
        
        <div class="status-container">
            <div class="status-box">
                <div class="status-label">حالة النظام</div>
                <div class="status-value" id="bot-status">متوقف</div>
            </div>
            <div class="status-box">
                <div class="status-label">إجمالي الأرباح</div>
                <div class="status-value" id="total-profit">0.00</div>
            </div>
            <div class="status-box">
                <div class="status-label">الصفقات النشطة</div>
                <div class="status-value" id="total-active-trades">0</div>
            </div>
            <div class="status-box">
                <div class="status-label">إجمالي الصفقات</div>
                <div class="status-value" id="total-trades">0</div>
            </div>
            <div class="status-box">
                <div class="status-label">السوق باستخدام مارتينجال</div>
                <div class="status-value" id="martingale-market">لا أحد</div>
            </div>
            <div class="status-box">
                <div class="status-label">مرحلة المارتينجال</div>
                <div class="status-value" id="martingale-stage">1</div>
            </div>
            <div class="status-box">
                <div class="status-label">أسواق مفعلة</div>
                <div class="status-value" id="active-markets-count">0/7</div>
            </div>
            <div class="status-box">
                <div class="status-label">نسبة النجاح</div>
                <div class="status-value" id="success-rate">0%</div>
            </div>
            <div class="status-box">
                <div class="status-label">أرباح/خسارة الرئيسي</div>
                <div class="status-value" id="primary-pnl">0.00</div>
            </div>
            <div class="status-box">
                <div class="status-label">رأس مال الرئيسي</div>
                <div class="status-value" id="primary-capital">0.00</div>
            </div>
            <div class="status-box">
                <div class="status-label">الحد الأقصى للمارتينجال</div>
                <div class="status-value" id="global-max-martingale">10</div>
            </div>
            <div class="status-box">
                <div class="status-label">أعلى مرحلة وصل لها</div>
                <div class="status-value" id="max-martingale-reached">0</div>
            </div>
        </div>
        
        <div class="layout-grid">
            <div class="card">
                <h2 class="card-title"><i class="fas fa-cogs"></i> إعدادات النظام</h2>
                
                <div class="form-group">
                    <label for="ticks-required"><i class="fas fa-sort-numeric-up"></i> عدد التيكات المطلوبة للإشارة</label>
                    <input type="number" id="ticks-required" value="2" min="2" max="10">
                    <small>عدد التيكات اللازمة لتحديد اتجاه السوق (الأخير أعلى من الأول = CALL)</small>
                </div>
                
                <div class="form-group">
                    <label for="trade-duration"><i class="fas fa-hourglass-half"></i> مدة الصفقة (تيكات)</label>
                    <input type="number" id="trade-duration" value="2" min="1" max="10">
                    <small>عدد التيكات التي تستمر بها كل صفقة</small>
                </div>
                
                <div class="settings-grid">
                    <div class="form-group">
                        <label for="multiplier"><i class="fas fa-arrows-alt-v"></i> مضاعف مارتينجال (عام)</label>
                        <input type="number" id="multiplier" value="2.2" step="0.1" min="1.1" max="10">
                        <small>يستخدم لجميع الأسواق</small>
                    </div>
                    <div class="form-group">
                        <label for="max-martingale"><i class="fas fa-shield-alt"></i> الحد الأقصى لمراحل المارتينجال</label>
                        <input type="number" id="max-martingale" value="10" min="1" max="20">
                        <small>الحد الأقصى للمراحل (يمكن تعديله حتى 20)</small>
                    </div>
                </div>
                
                <div class="checkbox-group">
                    <input type="checkbox" id="enable-ping" checked>
                    <label for="enable-ping"><i class="fas fa-signal"></i> تفعيل نظام Ping التلقائي</label>
                </div>
                
                <div class="form-group" id="ping-settings-group">
                    <label for="ping-interval">فترة Ping (ثانية)</label>
                    <input type="number" id="ping-interval" value="30" min="10" max="120">
                    <small>فترة إرسال Ping للتوكنات غير المتداولة</small>
                </div>

                <button id="start-bot" class="btn-success">
                    <i class="fas fa-play"></i> بدء النظام (اتصال حقيقي)
                </button>
                <button id="test-mode-btn" class="btn-warning">
                    <i class="fas fa-vial"></i> وضع الاختبار
                </button>
                <button id="stop-bot" class="btn-danger" disabled>
                    <i class="fas fa-stop"></i> إيقاف النظام
                </button>
            </div>
            
            <div class="card">
                <h2 class="card-title"><i class="fas fa-chart-line"></i> الأسواق السبعة</h2>
                
                <div id="markets-alerts"></div>
                
                <div class="markets-grid" id="markets-grid">
                    <!-- سيتم ملء الأسواق ديناميكياً -->
                </div>
                
                <table class="markets-table">
                    <thead>
                        <tr>
                            <th>السوق</th>
                            <th>الحالة</th>
                            <th>الخسائر</th>
                            <th>حجم الصفقة الثابت</th>
                            <th>حجم مارتينجال</th>
                            <th>رأس المال</th>
                            <th>الأرباح</th>
                            <th>الإشارة</th>
                            <th>التداول</th>
                        </tr>
                    </thead>
                    <tbody id="markets-table-body">
                        <!-- سيتم ملء الجدول ديناميكياً -->
                    </tbody>
                </table>
            </div>
        </div>
        
        <div class="card">
            <h2 class="card-title"><i class="fas fa-key"></i> التوكنات الرئيسية والإعدادات</h2>
            
            <div class="settings-grid">
                <div class="form-group">
                    <div class="required-token">
                        <label for="primary-token"><i class="fas fa-crown"></i> التوكن الرئيسي (مارتينجال) <span style="color: var(--warning);">* ضروري</span></label>
                        <input type="password" id="primary-token" placeholder="أدخل رمز API للتوكن الرئيسي" required>
                        <small>يستخدم عندما يصل أي سوق للحد الأقصى للخسائر</small>
                    </div>
                </div>
            </div>
            
            <div class="primary-stats-grid">
                <div class="primary-stat-card">
                    <div class="primary-stat-label">أرباح/خسارة التوكن الرئيسي</div>
                    <div class="primary-stat-value" id="primary-pnl-detail">0.00 USD</div>
                </div>
                <div class="primary-stat-card">
                    <div class="primary-stat-label">رأس مال التوكن الرئيسي</div>
                    <div class="primary-stat-value" id="primary-capital-detail">0.00 USD</div>
                </div>
                <div class="primary-stat-card">
                    <div class="primary-stat-label">حجم الصفقة الحالي</div>
                    <div class="primary-stat-value" id="primary-current-stake">0.77 USD</div>
                </div>
                <div class="primary-stat-card">
                    <div class="primary-stat-label">المرحلة الحالية</div>
                    <div class="primary-stat-value" id="primary-current-stage">1</div>
                </div>
                <div class="primary-stat-card" style="background: rgba(255, 107, 107, 0.2); border-color: var(--danger);">
                    <div class="primary-stat-label">أعلى مرحلة مارتينجال وصل لها</div>
                    <div class="primary-stat-value" id="primary-max-stage-reached" style="color: var(--danger);">0</div>
                </div>
            </div>
            
            <div class="martingale-status">
                <h4 style="color: var(--warning); margin-bottom: 15px;">
                    <i class="fas fa-chart-line"></i> حالة المارتينجال
                </h4>
                <div class="martingale-info">
                    <div class="martingale-item">
                        <div class="martingale-label">المرحلة الحالية</div>
                        <div class="martingale-value" id="current-martingale-stage">1</div>
                    </div>
                    <div class="martingale-item">
                        <div class="martingale-label">حجم الصفقة الحالي</div>
                        <div class="martingale-value" id="current-martingale-stake">0.77 USD</div>
                    </div>
                    <div class="martingale-item">
                        <div class="martingale-label">الحد الأقصى للمراحل</div>
                        <div class="martingale-value" id="max-martingale-display">10 مراحل</div>
                    </div>
                    <div class="martingale-item">
                        <div class="martingale-label">السوق المستخدم</div>
                        <div class="martingale-value" id="martingale-for-market">لا أحد</div>
                    </div>
                </div>
            </div>
            
            <div class="markets-grid" id="markets-tokens-grid">
                <!-- سيتم ملء توكنات الأسواق ديناميكياً -->
            </div>
        </div>
        
        <div class="layout-grid">
            <div class="card">
                <h2 class="card-title"><i class="fas fa-list-ul"></i> سجل النظام</h2>
                <div class="log-container" id="trade-log">
                    <div class="log-entry log-info">
                        <span class="log-time">[00:00:00]</span> 
                        <i class="fas fa-info-circle"></i>
                        النظام جاهز للتشغيل.
                    </div>
                </div>
            </div>
            
            <div class="card">
                <h2 class="card-title"><i class="fas fa-history"></i> سجل الصفقات</h2>
                <div class="log-container" id="trades-log">
                    <div class="log-entry log-info">
                        <span class="log-time">[00:00:00]</span> 
                        <i class="fas fa-info-circle"></i>
                        لا توجد صفقات حتى الآن.
                    </div>
                </div>
            </div>
        </div>
        
        <div class="monitoring-panel">
            <h3><i class="fas fa-heartbeat"></i> مراقبة النظام</h3>
            <div class="monitoring-grid">
                <div class="monitoring-item">
                    <div>استخدام الذاكرة</div>
                    <div class="monitoring-value" id="memory-usage">--</div>
                </div>
                <div class="monitoring-item">
                    <div>عدد السجلات</div>
                    <div class="monitoring-value" id="log-count">0</div>
                </div>
                <div class="monitoring-item">
                    <div>معدل الأخطاء</div>
                    <div class="monitoring-value" id="error-rate">0%</div>
                </div>
                <div class="monitoring-item">
                    <div>أسواق مفعلة</div>
                    <div class="monitoring-value" id="enabled-markets">0/7</div>
                </div>
            </div>
        </div>
    </div>

    <script>
        'use strict';
        
        // **********************************************
        // * نظام إدارة الثيمات *
        // **********************************************
        const themeToggleBtn = document.getElementById('theme-toggle');
        const body = document.body;

        function applyTheme(theme) {
            if (theme === 'dark') {
                body.classList.add('dark-mode');
                body.classList.remove('light-mode');
                themeToggleBtn.innerHTML = '<i class="fas fa-sun"></i>';
                localStorage.setItem('theme', 'dark');
            } else {
                body.classList.add('light-mode');
                body.classList.remove('dark-mode');
                themeToggleBtn.innerHTML = '<i class="fas fa-moon"></i>';
                localStorage.setItem('theme', 'light');
            }
        }

        document.addEventListener('DOMContentLoaded', () => {
            applyTheme(localStorage.getItem('theme') || 'dark');
            initializeSystem();
            startSystemMonitoring();
        });

        themeToggleBtn.addEventListener('click', () => {
            applyTheme(body.classList.contains('dark-mode') ? 'light' : 'dark');
        });

        // **********************************************
        // * تعريف الأسواق السبعة *
        // **********************************************
        const MARKETS = [
            { id: 1, name: 'EUR/USD', symbol: 'R_100', token: '', maxConsecutiveLosses: 3, consecutiveLosses: 0, fixedStake: 0.35, martingaleStake: 0.77, usingMartingale: false, enabled: false, isTrading: false, totalPnl: 0, balance: 0, capital: 0, lastSignal: 'WAIT', tickData: [], activeTrades: [], wsConnection: null, connected: false, lastPingTime: 0, lastTradeTime: 0, tradeCooldown: 3000, maxMartingaleStageReached: 0 },
            { id: 2, name: 'GBP/USD', symbol: 'R_50', token: '', maxConsecutiveLosses: 3, consecutiveLosses: 0, fixedStake: 0.35, martingaleStake: 0.77, usingMartingale: false, enabled: false, isTrading: false, totalPnl: 0, balance: 0, capital: 0, lastSignal: 'WAIT', tickData: [], activeTrades: [], wsConnection: null, connected: false, lastPingTime: 0, lastTradeTime: 0, tradeCooldown: 3000, maxMartingaleStageReached: 0 },
            { id: 3, name: 'EUR/USD Forex', symbol: 'frxEURUSD', token: '', maxConsecutiveLosses: 3, consecutiveLosses: 0, fixedStake: 0.35, martingaleStake: 0.77, usingMartingale: false, enabled: false, isTrading: false, totalPnl: 0, balance: 0, capital: 0, lastSignal: 'WAIT', tickData: [], activeTrades: [], wsConnection: null, connected: false, lastPingTime: 0, lastTradeTime: 0, tradeCooldown: 3000, maxMartingaleStageReached: 0 },
            { id: 4, name: 'GBP/USD Forex', symbol: 'frxGBPUSD', token: '', maxConsecutiveLosses: 3, consecutiveLosses: 0, fixedStake: 0.35, martingaleStake: 0.77, usingMartingale: false, enabled: false, isTrading: false, totalPnl: 0, balance: 0, capital: 0, lastSignal: 'WAIT', tickData: [], activeTrades: [], wsConnection: null, connected: false, lastPingTime: 0, lastTradeTime: 0, tradeCooldown: 3000, maxMartingaleStageReached: 0 },
            { id: 5, name: 'Volatility 50 (1s) Index', symbol: '1HZ100V', token: '', maxConsecutiveLosses: 3, consecutiveLosses: 0, fixedStake: 0.35, martingaleStake: 0.77, usingMartingale: false, enabled: false, isTrading: false, totalPnl: 0, balance: 0, capital: 0, lastSignal: 'WAIT', tickData: [], activeTrades: [], wsConnection: null, connected: false, lastPingTime: 0, lastTradeTime: 0, tradeCooldown: 3000, maxMartingaleStageReached: 0 },
            { id: 6, name: 'Volatility 10 Index', symbol: 'R_10', token: '', maxConsecutiveLosses: 3, consecutiveLosses: 0, fixedStake: 0.35, martingaleStake: 0.77, usingMartingale: false, enabled: false, isTrading: false, totalPnl: 0, balance: 0, capital: 0, lastSignal: 'WAIT', tickData: [], activeTrades: [], wsConnection: null, connected: false, lastPingTime: 0, lastTradeTime: 0, tradeCooldown: 3000, maxMartingaleStageReached: 0 },
            { id: 7, name: 'Volatility 25 Index', symbol: 'R_25', token: '', maxConsecutiveLosses: 3, consecutiveLosses: 0, fixedStake: 0.35, martingaleStake: 0.77, usingMartingale: false, enabled: false, isTrading: false, totalPnl: 0, balance: 0, capital: 0, lastSignal: 'WAIT', tickData: [], activeTrades: [], wsConnection: null, connected: false, lastPingTime: 0, lastTradeTime: 0, tradeCooldown: 3000, maxMartingaleStageReached: 0 }
        ];

        // **********************************************
        // * التوكن الرئيسي (مارتينجال) *
        // **********************************************
        const PRIMARY_TOKEN = {
            token: '', wsConnection: null, connected: false, isTrading: false,
            martingaleStage: 1, martingaleStake: 0.77,
            martingaleMultiplier: 2.2, maxMartingale: 10, consecutiveLosses: 0,
            totalPnl: 0, balance: 0, capital: 0, lastPingTime: 0, activeTrades: [],
            currentMarketUsing: null, lastTradeTime: 0, tradeCooldown: 3000,
            highestStageReached: 0
        };

        // **********************************************
        // * متغيرات النظام *
        // **********************************************
        let botActive = false, testMode = false, tradingTimer = 0;
        let timerInterval = null, pingInterval = null, cleanupInterval = null, simulationInterval = null;
        let errorCount = 0, totalOperations = 0, totalTrades = 0, totalProfit = 0, successfulTrades = 0;
        let dailyTradesCount = 0, dailyPnl = 0, ticksRequired = 2, tradeDuration = 2;
        let enablePingSystem = true, pingIntervalValue = 30;

        // **********************************************
        // * عناصر واجهة المستخدم *
        // **********************************************
        const uiElements = {
            tradingTimer: document.getElementById('trading-timer'), timerStatus: document.getElementById('timer-status'),
            dailyStats: document.getElementById('daily-stats'), botStatus: document.getElementById('bot-status'),
            totalProfit: document.getElementById('total-profit'), totalActiveTrades: document.getElementById('total-active-trades'),
            totalTrades: document.getElementById('total-trades'), martingaleMarket: document.getElementById('martingale-market'),
            martingaleStage: document.getElementById('martingale-stage'), activeMarketsCount: document.getElementById('active-markets-count'),
            successRate: document.getElementById('success-rate'), currentMartingaleStage: document.getElementById('current-martingale-stage'),
            currentMartingaleStake: document.getElementById('current-martingale-stake'), maxMartingaleDisplay: document.getElementById('max-martingale-display'),
            martingaleForMarket: document.getElementById('martingale-for-market'), ticksRequired: document.getElementById('ticks-required'),
            tradeDuration: document.getElementById('trade-duration'), multiplier: document.getElementById('multiplier'),
            maxMartingale: document.getElementById('max-martingale'), enablePingCheckbox: document.getElementById('enable-ping'),
            pingIntervalInput: document.getElementById('ping-interval'), primaryToken: document.getElementById('primary-token'),
            primaryPnl: document.getElementById('primary-pnl'), primaryCapital: document.getElementById('primary-capital'),
            primaryPnlDetail: document.getElementById('primary-pnl-detail'), primaryCapitalDetail: document.getElementById('primary-capital-detail'),
            primaryCurrentStake: document.getElementById('primary-current-stake'), primaryCurrentStage: document.getElementById('primary-current-stage'),
            primaryMaxStageReached: document.getElementById('primary-max-stage-reached'),
            globalMaxMartingale: document.getElementById('global-max-martingale'), maxMartingaleReached: document.getElementById('max-martingale-reached'),
            startBotBtn: document.getElementById('start-bot'), stopBotBtn: document.getElementById('stop-bot'),
            testModeBtn: document.getElementById('test-mode-btn'), marketsGrid: document.getElementById('markets-grid'),
            marketsTableBody: document.getElementById('markets-table-body'), marketsTokensGrid: document.getElementById('markets-tokens-grid'),
            marketsAlerts: document.getElementById('markets-alerts'), tradeLog: document.getElementById('trade-log'),
            tradesLog: document.getElementById('trades-log'), memoryUsage: document.getElementById('memory-usage'),
            logCount: document.getElementById('log-count'), errorRate: document.getElementById('error-rate'),
            enabledMarkets: document.getElementById('enabled-markets')
        };

        // **********************************************
        // * نظام السجلات *
        // **********************************************
        class Logger {
            static add(message, type = 'info', marketId = null) {
                totalOperations++;
                if (type === 'error') errorCount++;
                const now = new Date();
                const timeString = `[${now.getHours().toString().padStart(2, '0')}:${now.getMinutes().toString().padStart(2, '0')}:${now.getSeconds().toString().padStart(2, '0')}]`;
                const icons = { 'info': 'info-circle', 'success': 'check-circle', 'error': 'exclamation-circle', 'warning': 'exclamation-triangle' };
                const marketPrefix = marketId ? `[${MARKETS[marketId-1]?.name || 'نظام'}] ` : '';
                const logEntry = document.createElement('div');
                logEntry.className = `log-entry log-${type}`;
                logEntry.innerHTML = `<span class="log-time">${timeString}</span> <i class="fas fa-${icons[type]}"></i> ${marketPrefix}${message}`;
                uiElements.tradeLog.appendChild(logEntry);
                uiElements.tradeLog.scrollTop = uiElements.tradeLog.scrollHeight;
                Logger.cleanup();
            }
            static addTrade(message, type = 'info') {
                const now = new Date();
                const timeString = `[${now.getHours().toString().padStart(2, '0')}:${now.getMinutes().toString().padStart(2, '0')}:${now.getSeconds().toString().padStart(2, '0')}]`;
                const icons = { 'info': 'info-circle', 'success': 'check-circle', 'error': 'exclamation-circle', 'warning': 'exclamation-triangle' };
                const logEntry = document.createElement('div');
                logEntry.className = `log-entry log-${type}`;
                logEntry.innerHTML = `<span class="log-time">${timeString}</span> <i class="fas fa-${icons[type]}"></i> ${message}`;
                uiElements.tradesLog.appendChild(logEntry);
                uiElements.tradesLog.scrollTop = uiElements.tradesLog.scrollHeight;
                const tradeEntries = uiElements.tradesLog.querySelectorAll('.log-entry');
                if (tradeEntries.length > 50) tradeEntries[0].remove();
            }
            static cleanup() {
                const maxLogEntries = 100;
                const logEntries = uiElements.tradeLog.querySelectorAll('.log-entry');
                if (logEntries.length > maxLogEntries) {
                    for(let i = 0; i < logEntries.length - maxLogEntries; i++) logEntries[i].remove();
                }
            }
        }

        // **********************************************
        // * تهيئة النظام *
        // **********************************************
        function initializeSystem() {
            createMarketsCards();
            createMarketsTokensInputs();
            updateMarketsTable();
            updateUI();
            uiElements.startBotBtn.addEventListener('click', startSystem);
            uiElements.testModeBtn.addEventListener('click', startTestMode);
            uiElements.stopBotBtn.addEventListener('click', stopSystem);
            uiElements.enablePingCheckbox.addEventListener('change', function() {
                enablePingSystem = this.checked;
                if (enablePingSystem && botActive) PingSystem.start();
                else if (!enablePingSystem && pingInterval) { clearInterval(pingInterval); pingInterval = null; }
            });
            uiElements.pingIntervalInput.addEventListener('change', function() {
                pingIntervalValue = parseInt(this.value);
                if (enablePingSystem && botActive) PingSystem.start();
            });
            uiElements.multiplier.addEventListener('change', updateMartingaleSettings);
            uiElements.maxMartingale.addEventListener('change', updateMartingaleSettings);
        }

        function createMarketsCards() {
            let html = '';
            MARKETS.forEach(market => {
                html += `<div class="market-card" id="market-card-${market.id}">
                    <div class="market-header"><div class="market-name"><i class="fas fa-chart-line"></i> ${market.name}</div>
                    <div class="market-status status-no-token" id="market-status-${market.id}">بدون توكن</div></div>
                    <div class="market-info">
                        <div class="info-item"><div class="info-label">الخسائر</div><div class="info-value" id="market-losses-${market.id}">${market.consecutiveLosses}/${market.maxConsecutiveLosses}</div></div>
                        <div class="info-item"><div class="info-label">حجم ثابت</div><div class="info-value" id="market-stake-${market.id}">${market.fixedStake.toFixed(2)} USD</div></div>
                        <div class="info-item"><div class="info-label">حجم مارتينجال</div><div class="info-value" id="market-martingale-stake-${market.id}">${market.martingaleStake.toFixed(2)} USD</div></div>
                        <div class="info-item"><div class="info-label">الأرباح</div><div class="info-value" id="market-profit-${market.id}">${market.totalPnl.toFixed(2)} USD</div></div>
                    </div>
                    <div class="ticks-preview" id="market-ticks-${market.id}"><div class="tick-dot tick-neutral"></div><div class="tick-dot tick-neutral"></div><div class="tick-dot tick-neutral"></div><div class="tick-dot tick-neutral"></div><div class="tick-dot tick-neutral"></div></div>
                </div>`;
            });
            uiElements.marketsGrid.innerHTML = html;
        }

        function createMarketsTokensInputs() {
            let html = '';
            MARKETS.forEach(market => {
                html += `<div class="market-card">
                    <div class="market-header"><div class="market-name"><i class="fas fa-key"></i> ${market.name}</div>
                    <span class="badge badge-info" id="market-token-status-${market.id}">غير مفعل</span></div>
                    <div class="form-group"><label for="market-token-${market.id}">رمز API (اختياري)</label>
                    <input type="password" id="market-token-${market.id}" placeholder="أدخل رمز API لـ ${market.name} (اختياري)" class="market-token-input">
                    <small>اتركه فارغاً لإيقاف هذا السوق</small></div>
                    <div class="market-settings"><h5><i class="fas fa-cog"></i> إعدادات السوق</h5>
                    <div class="market-settings-grid">
                        <div class="market-settings-item"><label for="market-max-losses-${market.id}">حد الخسائر المتتالية</label>
                        <input type="number" id="market-max-losses-${market.id}" value="${market.maxConsecutiveLosses}" min="1" max="10" class="market-max-losses"></div>
                        <div class="market-settings-item"><label for="market-fixed-stake-${market.id}">حجم الصفقة الثابت (USD)</label>
                        <input type="number" id="market-fixed-stake-${market.id}" value="${market.fixedStake.toFixed(2)}" step="0.01" min="0.01" max="1000" class="market-fixed-stake"></div>
                        <div class="market-settings-item"><label for="market-martingale-stake-${market.id}">حجم صفقة المارتينجال الابتدائي (USD)</label>
                        <input type="number" id="market-martingale-stake-${market.id}" value="${market.martingaleStake.toFixed(2)}" step="0.01" min="0.01" max="1000" class="market-martingale-stake"></div>
                        <div class="market-settings-item"><label for="market-capital-${market.id}">رأس المال (USD)</label>
                        <input type="number" id="market-capital-${market.id}" value="${market.capital.toFixed(2)}" step="10" min="0" class="market-capital"></div>
                    </div></div>
                </div>`;
            });
            uiElements.marketsTokensGrid.innerHTML = html;
            MARKETS.forEach(market => {
                const tokenInput = document.getElementById(`market-token-${market.id}`);
                const stakeInput = document.getElementById(`market-fixed-stake-${market.id}`);
                const martingaleStakeInput = document.getElementById(`market-martingale-stake-${market.id}`);
                const lossesInput = document.getElementById(`market-max-losses-${market.id}`);
                const capitalInput = document.getElementById(`market-capital-${market.id}`);
                if (tokenInput) tokenInput.addEventListener('input', () => updateMarketEnabledStatus(market.id));
                if (stakeInput) stakeInput.addEventListener('change', () => { MARKETS[market.id-1].fixedStake = parseFloat(stakeInput.value) || 0.35; updateUI(); });
                if (martingaleStakeInput) martingaleStakeInput.addEventListener('change', () => { MARKETS[market.id-1].martingaleStake = parseFloat(martingaleStakeInput.value) || 0.77; updateUI(); });
                if (lossesInput) lossesInput.addEventListener('change', () => { MARKETS[market.id-1].maxConsecutiveLosses = parseInt(lossesInput.value) || 3; updateUI(); });
                if (capitalInput) capitalInput.addEventListener('change', () => { MARKETS[market.id-1].capital = parseFloat(capitalInput.value) || 0; updateUI(); });
            });
        }

        function updateMarketEnabledStatus(marketId) {
            const market = MARKETS[marketId-1];
            const tokenInput = document.getElementById(`market-token-${marketId}`);
            const tokenStatus = document.getElementById(`market-token-status-${marketId}`);
            const marketCard = document.getElementById(`market-card-${marketId}`);
            if (tokenInput && tokenStatus && marketCard) {
                const hasToken = tokenInput.value.trim() !== '';
                if (hasToken) {
                    market.enabled = true; market.token = tokenInput.value.trim();
                    tokenStatus.textContent = 'مفعل'; tokenStatus.className = 'badge badge-success';
                    marketCard.classList.remove('token-missing');
                } else {
                    market.enabled = false; market.token = ''; market.connected = false; market.isTrading = false; market.usingMartingale = false;
                    tokenStatus.textContent = 'غير مفعل'; tokenStatus.className = 'badge badge-info';
                    marketCard.classList.add('token-missing');
                }
                updateUI();
            }
        }

        function updateMarketsTable() {
            let html = '';
            MARKETS.forEach(market => {
                const statusText = market.usingMartingale ? 'مارتينجال' : market.isTrading ? 'يتداول' : market.enabled ? 'نشط' : 'بدون توكن';
                const statusClass = market.usingMartingale ? 'status-martingale' : market.isTrading ? 'status-trading' : market.enabled ? 'status-active' : 'status-no-token';
                html += `<tr>
                    <td><strong>${market.name}</strong></td>
                    <td><span class="market-status ${statusClass}">${statusText}</span></td>
                    <td>${market.consecutiveLosses}/${market.maxConsecutiveLosses}</td>
                    <td>${market.fixedStake.toFixed(2)} USD</td>
                    <td>${market.martingaleStake.toFixed(2)} USD</td>
                    <td class="${market.capital >= 0 ? 'profit' : 'loss'}">${market.capital.toFixed(2)} USD</td>
                    <td class="${market.totalPnl >= 0 ? 'profit' : 'loss'}">${market.totalPnl.toFixed(2)} USD</td>
                    <td id="table-signal-${market.id}">${market.lastSignal}</td>
                    <td id="table-trading-${market.id}">${market.isTrading ? 'نشط' : 'متوقف'}</td>
                </tr>`;
            });
            uiElements.marketsTableBody.innerHTML = html;
        }

        function updateUI() {
            const hours = Math.floor(tradingTimer / 3600), minutes = Math.floor((tradingTimer % 3600) / 60), seconds = tradingTimer % 60;
            uiElements.tradingTimer.textContent = `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            uiElements.botStatus.textContent = botActive ? 'نشط' : 'متوقف';
            uiElements.botStatus.style.color = botActive ? getComputedStyle(body).getPropertyValue('--success').trim() : getComputedStyle(body).getPropertyValue('--danger').trim();
            const activeTradesCount = getActiveTradesCount();
            uiElements.timerStatus.textContent = botActive ? `النظام يعمل - ${activeTradesCount} صفقات نشطة` : 'النظام متوقف';
            uiElements.totalProfit.textContent = `${totalProfit.toFixed(2)} USD`;
            uiElements.totalProfit.className = `status-value ${totalProfit >= 0 ? 'profit' : 'loss'}`;
            uiElements.totalTrades.textContent = totalTrades;
            uiElements.totalActiveTrades.textContent = activeTradesCount;
            const successRate = totalTrades > 0 ? ((successfulTrades / totalTrades) * 100).toFixed(1) : 0;
            uiElements.successRate.textContent = `${successRate}%`;
            uiElements.successRate.className = `status-value ${successRate >= 50 ? 'profit' : 'loss'}`;
            
            // إحصائيات التوكن الرئيسي
            uiElements.primaryPnl.textContent = `${PRIMARY_TOKEN.totalPnl.toFixed(2)} USD`;
            uiElements.primaryPnl.className = `status-value ${PRIMARY_TOKEN.totalPnl >= 0 ? 'profit' : 'loss'}`;
            uiElements.primaryCapital.textContent = `${PRIMARY_TOKEN.capital.toFixed(2)} USD`;
            uiElements.primaryPnlDetail.textContent = `${PRIMARY_TOKEN.totalPnl.toFixed(2)} USD`;
            uiElements.primaryPnlDetail.style.color = PRIMARY_TOKEN.totalPnl >= 0 ? 'var(--success)' : 'var(--danger)';
            uiElements.primaryCapitalDetail.textContent = `${PRIMARY_TOKEN.capital.toFixed(2)} USD`;
            uiElements.primaryCurrentStake.textContent = `${PRIMARY_TOKEN.martingaleStake.toFixed(2)} USD`;
            uiElements.primaryCurrentStage.textContent = PRIMARY_TOKEN.martingaleStage;
            uiElements.primaryMaxStageReached.textContent = PRIMARY_TOKEN.highestStageReached;
            uiElements.globalMaxMartingale.textContent = PRIMARY_TOKEN.maxMartingale;
            uiElements.maxMartingaleReached.textContent = PRIMARY_TOKEN.highestStageReached;
            
            const martingaleMarket = PRIMARY_TOKEN.currentMarketUsing;
            uiElements.martingaleMarket.textContent = martingaleMarket ? MARKETS[martingaleMarket-1]?.name || 'لا أحد' : 'لا أحد';
            uiElements.martingaleStage.textContent = PRIMARY_TOKEN.martingaleStage;
            uiElements.currentMartingaleStage.textContent = PRIMARY_TOKEN.martingaleStage;
            uiElements.currentMartingaleStake.textContent = `${PRIMARY_TOKEN.martingaleStake.toFixed(2)} USD`;
            uiElements.maxMartingaleDisplay.textContent = `${PRIMARY_TOKEN.maxMartingale} مراحل`;
            uiElements.martingaleForMarket.textContent = martingaleMarket ? MARKETS[martingaleMarket-1]?.name || 'لا أحد' : 'لا أحد';
            
            const enabledMarketsCount = MARKETS.filter(m => m.enabled).length;
            uiElements.activeMarketsCount.textContent = `${enabledMarketsCount}/7`;
            uiElements.enabledMarkets.textContent = `${enabledMarketsCount}/7`;
            
            MARKETS.forEach(market => {
                const card = document.getElementById(`market-card-${market.id}`);
                const statusElement = document.getElementById(`market-status-${market.id}`);
                const lossesElement = document.getElementById(`market-losses-${market.id}`);
                const stakeElement = document.getElementById(`market-stake-${market.id}`);
                const martingaleStakeElement = document.getElementById(`market-martingale-stake-${market.id}`);
                const profitElement = document.getElementById(`market-profit-${market.id}`);
                const tableSignalElement = document.getElementById(`table-signal-${market.id}`);
                const tableTradingElement = document.getElementById(`table-trading-${market.id}`);
                const stakeInput = document.getElementById(`market-fixed-stake-${market.id}`);
                const martingaleStakeInput = document.getElementById(`market-martingale-stake-${market.id}`);
                const capitalInput = document.getElementById(`market-capital-${market.id}`);
                
                if (stakeInput && parseFloat(stakeInput.value) !== market.fixedStake) stakeInput.value = market.fixedStake.toFixed(2);
                if (martingaleStakeInput && parseFloat(martingaleStakeInput.value) !== market.martingaleStake) martingaleStakeInput.value = market.martingaleStake.toFixed(2);
                if (capitalInput && parseFloat(capitalInput.value) !== market.capital) capitalInput.value = market.capital.toFixed(2);
                
                if (card) {
                    card.classList.remove('using-martingale', 'disabled', 'token-missing', 'trading-active', 'max-martingale-reached');
                    if (market.usingMartingale) card.classList.add('using-martingale');
                    else if (market.isTrading) card.classList.add('trading-active');
                    else if (!market.enabled) card.classList.add('token-missing');
                    else if (!market.connected) card.classList.add('disabled');
                    
                    if (market.maxMartingaleStageReached >= PRIMARY_TOKEN.maxMartingale) {
                        card.classList.add('max-martingale-reached');
                    }
                }
                if (statusElement) {
                    if (market.usingMartingale) { statusElement.textContent = 'مارتينجال'; statusElement.className = 'market-status status-martingale'; }
                    else if (market.isTrading) { statusElement.textContent = 'يتداول'; statusElement.className = 'market-status status-trading'; }
                    else if (market.enabled) { statusElement.textContent = market.connected ? 'نشط' : 'غير متصل'; statusElement.className = market.connected ? 'market-status status-active' : 'market-status status-disabled'; }
                    else { statusElement.textContent = 'بدون توكن'; statusElement.className = 'market-status status-no-token'; }
                }
                if (lossesElement) { lossesElement.textContent = `${market.consecutiveLosses}/${market.maxConsecutiveLosses}`; lossesElement.className = `info-value ${market.consecutiveLosses >= market.maxConsecutiveLosses ? 'loss' : ''}`; }
                if (stakeElement) stakeElement.textContent = `${market.fixedStake.toFixed(2)} USD`;
                if (martingaleStakeElement) martingaleStakeElement.textContent = `${market.martingaleStake.toFixed(2)} USD`;
                if (profitElement) { profitElement.textContent = `${market.totalPnl.toFixed(2)} USD`; profitElement.className = `info-value ${market.totalPnl >= 0 ? 'profit' : 'loss'}`; }
                if (tableSignalElement) {
                    tableSignalElement.textContent = market.lastSignal;
                    tableSignalElement.style.color = market.lastSignal === 'CALL' ? getComputedStyle(body).getPropertyValue('--success').trim() : market.lastSignal === 'PUT' ? getComputedStyle(body).getPropertyValue('--danger').trim() : getComputedStyle(body).getPropertyValue('--info').trim();
                }
                if (tableTradingElement) tableTradingElement.textContent = market.isTrading ? 'نشط' : 'متوقف';
                updateTicksDisplay(market.id);
            });
            updateMarketsTable();
        }

        function updateMartingaleSettings() {
            PRIMARY_TOKEN.martingaleMultiplier = parseFloat(uiElements.multiplier.value) || 2.2;
            PRIMARY_TOKEN.maxMartingale = parseInt(uiElements.maxMartingale.value) || 10;
            updateUI();
        }

        function updateTicksDisplay(marketId) {
            const market = MARKETS[marketId - 1];
            const ticksElement = document.getElementById(`market-ticks-${marketId}`);
            if (!ticksElement || !market || market.tickData.length < 5) return;
            const recentTicks = market.tickData.slice(-5);
            let ticksHTML = '';
            recentTicks.forEach((tick, index) => {
                let tickClass = 'tick-neutral';
                if (index > 0 && recentTicks[index - 1]) {
                    if (tick.quote > recentTicks[index - 1].quote) tickClass = 'tick-up';
                    else if (tick.quote < recentTicks[index - 1].quote) tickClass = 'tick-down';
                }
                ticksHTML += `<div class="tick-dot ${tickClass}"></div>`;
            });
            ticksElement.innerHTML = ticksHTML;
        }

        function getActiveTradesCount() {
            let count = 0;
            MARKETS.forEach(market => count += market.activeTrades.length);
            count += PRIMARY_TOKEN.activeTrades.length;
            return count;
        }

        // **********************************************
        // * نظام الاتصال *
        // **********************************************
        class ConnectionManager {
            static async connectAllMarkets() {
                try {
                    PRIMARY_TOKEN.token = uiElements.primaryToken.value.trim();
                    PRIMARY_TOKEN.maxMartingale = parseInt(uiElements.maxMartingale.value) || 10;
                    PRIMARY_TOKEN.martingaleMultiplier = parseFloat(uiElements.multiplier.value) || 2.2;
                    if (!PRIMARY_TOKEN.token) throw new Error('التوكن الرئيسي مطلوب لبدء النظام');
                    
                    MARKETS.forEach(market => {
                        const tokenInput = document.getElementById(`market-token-${market.id}`);
                        const maxLossesInput = document.getElementById(`market-max-losses-${market.id}`);
                        const fixedStakeInput = document.getElementById(`market-fixed-stake-${market.id}`);
                        const martingaleStakeInput = document.getElementById(`market-martingale-stake-${market.id}`);
                        const capitalInput = document.getElementById(`market-capital-${market.id}`);
                        if (tokenInput) { market.token = tokenInput.value.trim(); market.enabled = market.token !== ''; }
                        if (maxLossesInput && market.enabled) market.maxConsecutiveLosses = parseInt(maxLossesInput.value) || 3;
                        if (fixedStakeInput && market.enabled) market.fixedStake = parseFloat(fixedStakeInput.value) || 0.35;
                        if (martingaleStakeInput && market.enabled) market.martingaleStake = parseFloat(martingaleStakeInput.value) || 0.77;
                        if (capitalInput && market.enabled) market.capital = parseFloat(capitalInput.value) || 0;
                    });
                    
                    ticksRequired = parseInt(uiElements.ticksRequired.value) || 2;
                    tradeDuration = parseInt(uiElements.tradeDuration.value) || 2;
                    
                    await ConnectionManager.connectPrimaryToken();
                    const connectionPromises = MARKETS.filter(m => m.enabled).map(m => ConnectionManager.connectMarket(m));
                    await Promise.all(connectionPromises);
                    Logger.add('تم الاتصال بجميع التوكنات بنجاح', 'success');
                    return true;
                } catch (error) { Logger.add(`خطأ في الاتصال: ${error.message}`, 'error'); return false; }
            }
            static async connectMarket(market) {
                return new Promise((resolve, reject) => {
                    if (!market.enabled || !market.token) { resolve(null); return; }
                    if (market.wsConnection) market.wsConnection.close();
                    const ws = new WebSocket('wss://ws.binaryws.com/websockets/v3?app_id=1089');
                    ws.onopen = () => { Logger.add(`${market.name}: تم إنشاء اتصال WebSocket`, 'info', market.id); ws.send(JSON.stringify({ "authorize": market.token })); };
                    ws.onmessage = (event) => {
                        try {
                            const data = JSON.parse(event.data);
                            ConnectionManager.handleMarketMessage(data, market);
                            if (data.msg_type === 'authorize') {
                                market.connected = true; market.balance = data.authorize?.balance || 0; market.lastPingTime = Date.now();
                                ws.send(JSON.stringify({ "ticks": market.symbol, "subscribe": 1 }));
                                Logger.add(`${market.name}: متصل - الرصيد: ${market.balance.toFixed(2)} USD`, 'success', market.id);
                                updateUI(); resolve(ws);
                            }
                        } catch (e) { Logger.add(`${market.name}: خطأ في معالجة الرسالة`, 'error', market.id); }
                    };
                    ws.onerror = (error) => { Logger.add(`${market.name}: خطأ في الاتصال`, 'error', market.id); reject(error); };
                    ws.onclose = () => {
                        Logger.add(`${market.name}: تم إغلاق الاتصال`, 'warning', market.id);
                        market.connected = false; market.isTrading = false; updateUI();
                        if (botActive && market.enabled) setTimeout(() => { if (botActive && market.enabled && market.token) ConnectionManager.connectMarket(market); }, 5000);
                    };
                    market.wsConnection = ws;
                });
            }
            static async connectPrimaryToken() {
                return new Promise((resolve, reject) => {
                    if (PRIMARY_TOKEN.wsConnection) PRIMARY_TOKEN.wsConnection.close();
                    const ws = new WebSocket('wss://ws.binaryws.com/websockets/v3?app_id=1089');
                    ws.onopen = () => { Logger.add('التوكن الرئيسي: تم إنشاء اتصال WebSocket', 'info'); ws.send(JSON.stringify({ "authorize": PRIMARY_TOKEN.token })); };
                    ws.onmessage = (event) => {
                        try {
                            const data = JSON.parse(event.data);
                            ConnectionManager.handlePrimaryTokenMessage(data);
                            if (data.msg_type === 'authorize') {
                                PRIMARY_TOKEN.connected = true; PRIMARY_TOKEN.balance = data.authorize?.balance || 0; PRIMARY_TOKEN.lastPingTime = Date.now();
                                Logger.add(`التوكن الرئيسي: متصل - الرصيد: ${PRIMARY_TOKEN.balance.toFixed(2)} USD`, 'success');
                                updateUI(); resolve(ws);
                            }
                        } catch (e) { Logger.add('التوكن الرئيسي: خطأ في معالجة الرسالة', 'error'); }
                    };
                    ws.onerror = (error) => { Logger.add('التوكن الرئيسي: خطأ في الاتصال', 'error'); reject(error); };
                    ws.onclose = () => {
                        Logger.add('التوكن الرئيسي: تم إغلاق الاتصال', 'warning');
                        PRIMARY_TOKEN.connected = false; PRIMARY_TOKEN.isTrading = false; updateUI();
                        if (botActive) setTimeout(() => { if (botActive && PRIMARY_TOKEN.token) ConnectionManager.connectPrimaryToken(); }, 5000);
                    };
                    PRIMARY_TOKEN.wsConnection = ws;
                });
            }
            static handleMarketMessage(data, market) {
                if (data.error) { Logger.add(`${market.name}: ${data.error.message}`, 'error', market.id); return; }
                switch(data.msg_type) {
                    case 'tick': TradingSystem.processTick(market.id, data.tick); break;
                    case 'ping': market.lastPingTime = Date.now(); break;
                    case 'balance': if (data.balance) { market.balance = parseFloat(data.balance.balance); updateUI(); } break;
                }
            }
            static handlePrimaryTokenMessage(data) {
                if (data.error) { Logger.add(`التوكن الرئيسي: ${data.error.message}`, 'error'); return; }
                switch(data.msg_type) {
                    case 'ping': PRIMARY_TOKEN.lastPingTime = Date.now(); break;
                    case 'balance': if (data.balance) { PRIMARY_TOKEN.balance = parseFloat(data.balance.balance); updateUI(); } break;
                }
            }
            static disconnectAll() {
                MARKETS.forEach(market => { if (market.wsConnection) { try { market.wsConnection.close(); } catch(e) {} market.wsConnection = null; market.connected = false; market.isTrading = false; } });
                if (PRIMARY_TOKEN.wsConnection) { try { PRIMARY_TOKEN.wsConnection.close(); } catch(e) {} PRIMARY_TOKEN.wsConnection = null; PRIMARY_TOKEN.connected = false; PRIMARY_TOKEN.isTrading = false; }
                updateUI();
            }
        }

        // **********************************************
        // * نظام التداول *
        // **********************************************
        class TradingSystem {
            static processTick(marketId, tickData) {
                const market = MARKETS[marketId - 1];
                if (!market || !market.enabled || !market.connected) return;
                market.tickData.push({ quote: parseFloat(tickData.quote), epoch: tickData.epoch || Date.now(), timestamp: Date.now() });
                if (market.tickData.length > 100) market.tickData.shift();
                const signal = TradingSystem.analyzeSignal(market);
                market.lastSignal = signal;
                const now = Date.now();
                if (market.usingMartingale) {
                    if (signal === 'CALL' && !PRIMARY_TOKEN.isTrading && !market.isTrading && now - PRIMARY_TOKEN.lastTradeTime > PRIMARY_TOKEN.tradeCooldown) {
                        TradingSystem.openMartingaleTrade(market);
                    }
                } else if (market.enabled && market.connected && signal === 'CALL' && !market.isTrading && market.consecutiveLosses < market.maxConsecutiveLosses && now - market.lastTradeTime > market.tradeCooldown) {
                    TradingSystem.openNormalTrade(market);
                }
                updateUI();
            }
            static analyzeSignal(market) {
                if (market.tickData.length < ticksRequired) return 'WAIT';
                const recentTicks = market.tickData.slice(-ticksRequired);
                const firstTick = recentTicks[0]?.quote, lastTick = recentTicks[recentTicks.length - 1]?.quote;
                if (firstTick === undefined || lastTick === undefined) return 'WAIT';
                return lastTick > firstTick ? 'CALL' : (lastTick < firstTick ? 'PUT' : 'WAIT');
            }
            static openNormalTrade(market) {
                market.isTrading = true; market.lastTradeTime = Date.now();
                const tradeId = 'TRADE_' + Date.now() + '_' + market.id;
                const stake = market.fixedStake;
                market.activeTrades.push({ id: tradeId, marketId: market.id, isMartingale: false, contract_type: 'CALL', stake: stake, open_time: new Date(), status: 'open' });
                totalTrades++; dailyTradesCount++;
                Logger.add(`${market.name}: فتح صفقة CALL بمبلغ ${stake.toFixed(2)} USD`, 'info', market.id);
                Logger.addTrade(`${market.name}: فتح CALL - ${stake.toFixed(2)} USD`);
                setTimeout(() => { TradingSystem.closeTrade(tradeId, market.id, false); }, tradeDuration * 1000);
                updateUI();
            }
            static openMartingaleTrade(market) {
                if (!PRIMARY_TOKEN.connected) { Logger.add(`${market.name}: التوكن الرئيسي غير متصل`, 'error', market.id); market.isTrading = false; return; }
                PRIMARY_TOKEN.isTrading = true; PRIMARY_TOKEN.lastTradeTime = Date.now();
                const tradeId = 'MART_' + Date.now() + '_' + market.id;
                const stake = market.martingaleStake;
                PRIMARY_TOKEN.activeTrades.push({ id: tradeId, marketId: market.id, isMartingale: true, contract_type: 'CALL', stake: stake, open_time: new Date(), status: 'open', stage: PRIMARY_TOKEN.martingaleStage });
                totalTrades++; dailyTradesCount++;
                Logger.add(`${market.name}: فتح صفقة مارتينجال CALL بمبلغ ${stake.toFixed(2)} USD (المرحلة ${PRIMARY_TOKEN.martingaleStage})`, 'warning', market.id);
                Logger.addTrade(`${market.name}: مارتينجال - فتح CALL - ${stake.toFixed(2)} USD (المرحلة ${PRIMARY_TOKEN.martingaleStage})`);
                setTimeout(() => { TradingSystem.closeTrade(tradeId, market.id, true); }, tradeDuration * 1000);
                updateUI();
            }
            static closeTrade(tradeId, marketId, isMartingale) {
                const market = MARKETS[marketId - 1];
                let tradeArray, token;
                if (isMartingale) { tradeArray = PRIMARY_TOKEN.activeTrades; token = PRIMARY_TOKEN; }
                else { tradeArray = market.activeTrades; token = market; }
                const tradeIndex = tradeArray.findIndex(t => t.id === tradeId);
                if (tradeIndex === -1) return;
                const trade = tradeArray[tradeIndex];
                const isWin = Math.random() < 0.55;
                const profit = isWin ? trade.stake * 0.95 : -trade.stake;
                tradeArray.splice(tradeIndex, 1);
                token.totalPnl += profit;
                if (isMartingale) PRIMARY_TOKEN.isTrading = false;
                else market.isTrading = false;
                totalProfit += profit; dailyPnl += profit;
                if (isWin) successfulTrades++;
                const typeText = isMartingale ? 'مارتينجال' : 'عادي';
                const resultText = isWin ? 'ربح' : 'خسارة';
                Logger.add(`${market.name}: إغلاق صفقة ${typeText} - ${resultText} ${Math.abs(profit).toFixed(2)} USD`, isWin ? 'success' : 'error', market.id);
                Logger.addTrade(`${market.name}: ${typeText} - ${resultText} - ${Math.abs(profit).toFixed(2)} USD`);
                if (isMartingale) TradingSystem.updateMartingaleSystem(market, isWin);
                else TradingSystem.updateNormalSystem(market, isWin);
                updateUI();
            }
            static updateNormalSystem(market, isWin) {
                if (isWin) {
                    market.consecutiveLosses = 0;
                    Logger.add(`${market.name}: فوز - إعادة تعيين الخسائر المتتالية`, 'success', market.id);
                } else {
                    market.consecutiveLosses++;
                    Logger.add(`${market.name}: خسارة - الخسائر المتتالية: ${market.consecutiveLosses}/${market.maxConsecutiveLosses}`, 'warning', market.id);
                    if (market.consecutiveLosses >= market.maxConsecutiveLosses && !market.usingMartingale) {
                        TradingSystem.activateMartingaleForMarket(market);
                    }
                }
            }
            static updateMartingaleSystem(market, isWin) {
                if (isWin) {
                    if (PRIMARY_TOKEN.martingaleStage > PRIMARY_TOKEN.highestStageReached) {
                        PRIMARY_TOKEN.highestStageReached = PRIMARY_TOKEN.martingaleStage;
                        Logger.add(`🎯 إنجاز جديد: التوكن الرئيسي وصل للمرحلة ${PRIMARY_TOKEN.highestStageReached} من المارتينجال`, 'success');
                    }
                    
                    PRIMARY_TOKEN.consecutiveLosses = 0;
                    PRIMARY_TOKEN.martingaleStage = 1;
                    PRIMARY_TOKEN.martingaleStake = market.martingaleStake;
                    market.usingMartingale = false;
                    market.consecutiveLosses = 0;
                    PRIMARY_TOKEN.currentMarketUsing = null;
                    
                    let resetCount = 0;
                    MARKETS.forEach(m => {
                        if (m.consecutiveLosses >= m.maxConsecutiveLosses) {
                            m.consecutiveLosses = 0;
                            m.usingMartingale = false;
                            resetCount++;
                            Logger.add(`${m.name}: إعادة تعيين الخسائر المتتالية بعد فوز المارتينجال لسوق ${market.name}`, 'info', m.id);
                        }
                    });
                    
                    Logger.add(`${market.name}: فوز في المارتينجال - إعادة السوق للتداول العادي وتم إعادة تعيين ${resetCount} سوق آخر`, 'success', market.id);
                    showAlert(`${market.name}: تم استعادة السوق بعد فوز المارتينجال وتم إعادة تعيين ${resetCount} سوق آخر`, 'success');
                    
                } else {
                    PRIMARY_TOKEN.consecutiveLosses++;
                    PRIMARY_TOKEN.martingaleStage++;
                    
                    if (PRIMARY_TOKEN.martingaleStage > PRIMARY_TOKEN.highestStageReached) {
                        PRIMARY_TOKEN.highestStageReached = PRIMARY_TOKEN.martingaleStage;
                        Logger.add(`⚠️ التوكن الرئيسي وصل للمرحلة ${PRIMARY_TOKEN.highestStageReached} من المارتينجال`, 'warning');
                    }
                    
                    if (PRIMARY_TOKEN.martingaleStage > PRIMARY_TOKEN.maxMartingale) {
                        PRIMARY_TOKEN.consecutiveLosses = 0;
                        PRIMARY_TOKEN.martingaleStage = 1;
                        PRIMARY_TOKEN.martingaleStake = market.martingaleStake;
                        market.usingMartingale = false;
                        PRIMARY_TOKEN.currentMarketUsing = null;
                        Logger.add(`${market.name}: تجاوز الحد الأقصى للمارتينجال (${PRIMARY_TOKEN.maxMartingale}) - تم إيقاف المارتينجال`, 'error', market.id);
                        showAlert(`${market.name}: تم إيقاف المارتينجال بعد تجاوز الحد الأقصى ${PRIMARY_TOKEN.maxMartingale}`, 'danger');
                    } else {
                        PRIMARY_TOKEN.martingaleStake = market.martingaleStake * Math.pow(PRIMARY_TOKEN.martingaleMultiplier, PRIMARY_TOKEN.martingaleStage - 1);
                        Logger.add(`${market.name}: خسارة مارتينجال - المرحلة ${PRIMARY_TOKEN.martingaleStage}/${PRIMARY_TOKEN.maxMartingale} - الحجم: ${PRIMARY_TOKEN.martingaleStake.toFixed(2)} USD`, 'warning', market.id);
                    }
                }
                updateUI();
            }
            static activateMartingaleForMarket(market) {
                if (!PRIMARY_TOKEN.connected) { Logger.add(`${market.name}: لا يمكن تفعيل المارتينجال - التوكن الرئيسي غير متصل`, 'error', market.id); return; }
                if (PRIMARY_TOKEN.currentMarketUsing !== null) { Logger.add(`${market.name}: لا يمكن تفعيل المارتينجال - سوق آخر يستخدمه حالياً`, 'warning', market.id); return; }
                market.usingMartingale = true;
                PRIMARY_TOKEN.currentMarketUsing = market.id;
                PRIMARY_TOKEN.consecutiveLosses = 0;
                PRIMARY_TOKEN.martingaleStage = 1;
                PRIMARY_TOKEN.martingaleStake = market.martingaleStake;
                
                if (PRIMARY_TOKEN.martingaleStage > market.maxMartingaleStageReached) {
                    market.maxMartingaleStageReached = PRIMARY_TOKEN.martingaleStage;
                }
                
                Logger.add(`${market.name}: وصل للحد الأقصى للخسائر - تفعيل المارتينجال بحجم ابتدائي ${market.martingaleStake.toFixed(2)} USD`, 'warning', market.id);
                showAlert(`${market.name}: تم تفعيل المارتينجال بعد ${market.maxConsecutiveLosses} خسارات متتالية بحجم ${market.martingaleStake.toFixed(2)} USD`, 'warning');
                updateUI();
            }
        }

        // **********************************************
        // * نظام Ping *
        // **********************************************
        class PingSystem {
            static start() {
                if (pingInterval) clearInterval(pingInterval);
                pingInterval = setInterval(() => {
                    if (!botActive || !enablePingSystem) return;
                    MARKETS.forEach(market => { if (market.enabled && !market.isTrading && market.wsConnection && market.wsConnection.readyState === WebSocket.OPEN) { try { market.wsConnection.send(JSON.stringify({ "ping": 1 })); market.lastPingTime = Date.now(); } catch(e) {} } });
                    if (!PRIMARY_TOKEN.isTrading && PRIMARY_TOKEN.wsConnection && PRIMARY_TOKEN.wsConnection.readyState === WebSocket.OPEN) { try { PRIMARY_TOKEN.wsConnection.send(JSON.stringify({ "ping": 1 })); PRIMARY_TOKEN.lastPingTime = Date.now(); } catch(e) {} }
                }, pingIntervalValue * 1000);
                Logger.add(`نظام Ping مفعّل - فترة: ${pingIntervalValue} ثانية`, 'info');
            }
            static stop() { if (pingInterval) { clearInterval(pingInterval); pingInterval = null; } }
        }

        function showAlert(message, type = 'info') {
            const alertDiv = document.createElement('div');
            alertDiv.className = `alert alert-${type}`;
            alertDiv.innerHTML = `<i class="fas fa-${type === 'info' ? 'info-circle' : type === 'warning' ? 'exclamation-triangle' : type === 'danger' ? 'exclamation-circle' : 'check-circle'}"></i> ${message}`;
            uiElements.marketsAlerts.appendChild(alertDiv);
            setTimeout(() => { if (alertDiv.parentNode) alertDiv.remove(); }, 5000);
            const alerts = uiElements.marketsAlerts.querySelectorAll('.alert');
            if (alerts.length > 3) alerts[0].remove();
        }

        class SystemMonitor {
            static interval = null;
            static start() {
                if (SystemMonitor.interval) clearInterval(SystemMonitor.interval);
                SystemMonitor.interval = setInterval(() => { SystemMonitor.updateMetrics(); SystemMonitor.cleanupMemory(); }, 5000);
            }
            static updateMetrics() {
                if (performance.memory) {
                    const usedMB = performance.memory.usedJSHeapSize / 1024 / 1024;
                    const totalMB = performance.memory.jsHeapSizeLimit / 1024 / 1024;
                    const usagePercent = (usedMB / totalMB) * 100;
                    uiElements.memoryUsage.textContent = `${usedMB.toFixed(1)}MB`;
                    uiElements.memoryUsage.style.color = usagePercent > 70 ? 'var(--danger)' : usagePercent > 50 ? 'var(--warning)' : 'var(--success)';
                }
                const logCount = uiElements.tradeLog.querySelectorAll('.log-entry').length;
                uiElements.logCount.textContent = logCount;
                const errorRate = totalOperations > 0 ? (errorCount / totalOperations * 100).toFixed(1) : 0;
                uiElements.errorRate.textContent = `${errorRate}%`;
                uiElements.errorRate.style.color = errorRate > 5 ? 'var(--danger)' : errorRate > 2 ? 'var(--warning)' : 'var(--success)';
                uiElements.dailyStats.textContent = `اليوم: ${dailyTradesCount} صفقات | ${dailyPnl.toFixed(2)} USD`;
            }
            static cleanupMemory() {
                if (!botActive) return;
                MARKETS.forEach(market => { if (market.tickData.length > 200) market.tickData.splice(0, market.tickData.length - 100); });
                const now = Date.now();
                MARKETS.forEach(market => { market.activeTrades = market.activeTrades.filter(trade => now - trade.open_time.getTime() < 5 * 60 * 1000); });
                PRIMARY_TOKEN.activeTrades = PRIMARY_TOKEN.activeTrades.filter(trade => now - trade.open_time.getTime() < 5 * 60 * 1000);
            }
        }

        // **********************************************
        // * إدارة النظام *
        // **********************************************
        function startSystem() {
            if (!uiElements.primaryToken.value.trim()) { alert('التوكن الرئيسي مطلوب لبدء النظام'); return; }
            uiElements.startBotBtn.disabled = true; uiElements.stopBotBtn.disabled = false; uiElements.testModeBtn.disabled = true; testMode = false;
            resetStatistics();
            ConnectionManager.connectAllMarkets().then(success => {
                if (success) {
                    botActive = true; tradingTimer = 0;
                    if (timerInterval) clearInterval(timerInterval);
                    timerInterval = setInterval(() => { tradingTimer++; updateUI(); }, 1000);
                    if (enablePingSystem) PingSystem.start();
                    SystemMonitor.start();
                    const enabledMarkets = MARKETS.filter(m => m.enabled).length;
                    Logger.add(`تم بدء النظام بنجاح - ${enabledMarkets} أسواق مفعلة`, 'success');
                    showAlert(`النظام يعمل - ${enabledMarkets} أسواق مفعلة`, 'success');
                } else { uiElements.stopBotBtn.click(); }
            });
            updateUI();
        }
        
        function startTestMode() {
            uiElements.startBotBtn.disabled = true; uiElements.stopBotBtn.disabled = false; uiElements.testModeBtn.disabled = true; testMode = true;
            resetStatistics();
            MARKETS.forEach(market => {
                const tokenInput = document.getElementById(`market-token-${market.id}`);
                const capitalInput = document.getElementById(`market-capital-${market.id}`);
                const martingaleStakeInput = document.getElementById(`market-martingale-stake-${market.id}`);
                const hasToken = tokenInput && tokenInput.value.trim() !== '';
                market.enabled = hasToken; market.connected = hasToken; 
                market.balance = hasToken ? (capitalInput ? parseFloat(capitalInput.value) || 1000 : 1000) : 0;
                market.capital = hasToken ? (capitalInput ? parseFloat(capitalInput.value) || 1000 : 1000) : 0;
                market.martingaleStake = hasToken ? (martingaleStakeInput ? parseFloat(martingaleStakeInput.value) || 0.77 : 0.77) : 0.77;
                market.lastPingTime = hasToken ? Date.now() : 0;
                market.usingMartingale = false; market.consecutiveLosses = 0; market.totalPnl = 0; market.tickData = []; market.activeTrades = []; market.isTrading = false; market.lastTradeTime = 0;
                market.maxMartingaleStageReached = 0;
            });
            PRIMARY_TOKEN.connected = true; 
            PRIMARY_TOKEN.capital = 1000;
            PRIMARY_TOKEN.balance = 1000; 
            PRIMARY_TOKEN.lastPingTime = Date.now(); 
            PRIMARY_TOKEN.consecutiveLosses = 0;
            PRIMARY_TOKEN.martingaleStage = 1; 
            PRIMARY_TOKEN.martingaleStake = MARKETS[0].martingaleStake;
            PRIMARY_TOKEN.maxMartingale = parseInt(uiElements.maxMartingale.value) || 10;
            PRIMARY_TOKEN.martingaleMultiplier = parseFloat(uiElements.multiplier.value) || 2.2;
            PRIMARY_TOKEN.totalPnl = 0; 
            PRIMARY_TOKEN.activeTrades = [];
            PRIMARY_TOKEN.currentMarketUsing = null; 
            PRIMARY_TOKEN.isTrading = false; 
            PRIMARY_TOKEN.lastTradeTime = 0;
            PRIMARY_TOKEN.highestStageReached = 0;
            botActive = true; tradingTimer = 0;
            if (timerInterval) clearInterval(timerInterval);
            timerInterval = setInterval(() => { tradingTimer++; updateUI(); if (testMode) simulateTestTicks(); }, 1000);
            if (enablePingSystem) PingSystem.start();
            SystemMonitor.start();
            const enabledMarkets = MARKETS.filter(m => m.enabled).length;
            Logger.add(`تم بدء وضع الاختبار - ${enabledMarkets} أسواق مفعلة`, 'success');
            showAlert(`وضع الاختبار يعمل - ${enabledMarkets} أسواق مفعلة`, 'info');
            updateUI();
        }
        
        function stopSystem() {
            botActive = false;
            uiElements.startBotBtn.disabled = false; uiElements.stopBotBtn.disabled = true; uiElements.testModeBtn.disabled = false;
            if (timerInterval) clearInterval(timerInterval);
            if (pingInterval) clearInterval(pingInterval);
            if (SystemMonitor.interval) clearInterval(SystemMonitor.interval);
            if (simulationInterval) clearInterval(simulationInterval);
            timerInterval = null; pingInterval = null; SystemMonitor.interval = null; simulationInterval = null;
            if (!testMode) ConnectionManager.disconnectAll();
            PingSystem.stop();
            Logger.add('تم إيقاف النظام', 'warning');
            showAlert('تم إيقاف النظام', 'info');
            updateUI();
        }
        
        function resetStatistics() {
            totalProfit = 0; totalTrades = 0; successfulTrades = 0; dailyTradesCount = 0; dailyPnl = 0; errorCount = 0; totalOperations = 0;
            MARKETS.forEach(market => {
                market.consecutiveLosses = 0; market.totalPnl = 0; market.balance = 0; market.tickData = []; market.activeTrades = []; market.isTrading = false; market.usingMartingale = false; market.lastTradeTime = 0;
            });
            PRIMARY_TOKEN.consecutiveLosses = 0; PRIMARY_TOKEN.martingaleStage = 1; PRIMARY_TOKEN.totalPnl = 0; PRIMARY_TOKEN.balance = 0; PRIMARY_TOKEN.activeTrades = [];
            PRIMARY_TOKEN.isTrading = false; PRIMARY_TOKEN.currentMarketUsing = null; 
            PRIMARY_TOKEN.lastTradeTime = 0;
            PRIMARY_TOKEN.highestStageReached = 0;
            uiElements.tradeLog.innerHTML = `<div class="log-entry log-info"><span class="log-time">[00:00:00]</span> <i class="fas fa-info-circle"></i> تم إعادة تعيين النظام.</div>`;
            uiElements.tradesLog.innerHTML = `<div class="log-entry log-info"><span class="log-time">[00:00:00]</span> <i class="fas fa-info-circle"></i> لا توجد صفقات حتى الآن.</div>`;
        }
        
        function simulateTestTicks() {
            MARKETS.forEach(market => {
                if (!market.enabled) return;
                const basePrice = market.tickData.length > 0 ? market.tickData[market.tickData.length - 1]?.quote || 1.0 : (market.symbol.includes('R_') ? 1.0 : 5000);
                const volatility = market.symbol.includes('Volatility') ? 0.05 : 0.0001;
                const change = (Math.random() - 0.5) * volatility;
                const newPrice = Math.max(0.01, basePrice + change);
                TradingSystem.processTick(market.id, { quote: parseFloat(newPrice.toFixed(4)), epoch: Date.now(), timestamp: Date.now() });
            });
        }

        function startSystemMonitoring() { SystemMonitor.start(); }
        updateUI();
    </script>
</body>
</html>
