لا ابغى نفس الكود <!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>اختبار قواعد الحفاظ على الحياة</title>
<link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800;900&display=swap" rel="stylesheet">
<style>
  :root {
    --primary: #1a5276;
    --primary-dark: #0e2f44;
    --accent: #e67e22;
    --accent-glow: #f39c12;
    --correct: #27ae60;
    --correct-bg: rgba(39, 174, 96, 0.15);
    --wrong: #e74c3c;
    --wrong-bg: rgba(231, 76, 60, 0.15);
    --text: #ecf0f1;
    --text-muted: #95a5a6;
    --card-bg: rgba(255,255,255,0.07);
    --card-border: rgba(255,255,255,0.1);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'Tajawal', sans-serif;
    min-height: 100vh;
    background: linear-gradient(145deg, #0a1628 0%, #112240 40%, #1a3a5c 100%);
    color: var(--text);
    overflow-x: hidden;
  }

  .bg-pattern {
    position: fixed; inset: 0; z-index: 0;
    overflow: hidden; pointer-events: none;
  }
  .bg-pattern::before {
    content: ''; position: absolute; top: -50%; right: -30%;
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(230, 126, 34, 0.08) 0%, transparent 70%);
    border-radius: 50%; animation: floatOrb 15s ease-in-out infinite;
  }
  .bg-pattern::after {
    content: ''; position: absolute; bottom: -30%; left: -20%;
    width: 500px; height: 500px;
    background: radial-gradient(circle, rgba(26, 82, 118, 0.15) 0%, transparent 70%);
    border-radius: 50%; animation: floatOrb 20s ease-in-out infinite reverse;
  }
  @keyframes floatOrb {
    0%, 100% { transform: translate(0, 0) scale(1); }
    33% { transform: translate(40px, -30px) scale(1.1); }
    66% { transform: translate(-20px, 20px) scale(0.95); }
  }

  .app-container {
    position: relative; z-index: 1;
    max-width: 640px; margin: 0 auto;
    padding: 20px 16px 40px;
  }

  /* ===== HOME SCREEN ===== */
  .home-screen { text-align: center; animation: fadeIn 0.6s ease-out; }
  .home-screen.hidden { display: none; }

  .home-title {
    font-size: 30px; font-weight: 900; margin-bottom: 6px;
    background: linear-gradient(90deg, #fff, #d4e6f1);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  }
  .home-subtitle {
    color: var(--text-muted); font-size: 15px; font-weight: 500;
    margin-bottom: 28px; line-height: 1.6;
  }
  .home-label {
    font-size: 14px; font-weight: 700; color: var(--accent);
    letter-spacing: 1px; margin-bottom: 18px;
  }

  .rule-cards {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 16px;
    justify-items: center;
    padding: 0 4px;
  }

  .rule-card {
    display: flex; flex-direction: column; align-items: center;
    cursor: pointer; transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    position: relative;
    gap: 8px;
  }
  .rule-card:hover { transform: translateY(-6px) scale(1.05); }
  .rule-card:active { transform: scale(0.93); }

  .rule-card .rc-num {
    width: 58px; height: 58px; border-radius: 16px;
    background: linear-gradient(145deg, var(--accent), #c0392b);
    display: flex; align-items: center; justify-content: center;
    font-size: 20px; font-weight: 900; color: #fff;
    box-shadow: 0 4px 14px rgba(230,126,34,0.3);
    transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    position: relative;
    overflow: hidden;
  }
  .rule-card .rc-num::after {
    content: '';
    position: absolute;
    top: -50%; left: -50%;
    width: 200%; height: 200%;
    background: linear-gradient(135deg, transparent 40%, rgba(255,255,255,0.15) 50%, transparent 60%);
    transition: transform 0.6s;
    transform: translateX(-100%);
  }
  .rule-card:hover .rc-num::after { transform: translateX(100%); }
  .rule-card:hover .rc-num {
    box-shadow: 0 8px 28px rgba(230,126,34,0.55);
    transform: rotate(-3deg);
  }
  .rule-card .rc-icon {
    font-size: 18px;
    opacity: 0.8;
    transition: all 0.3s;
    filter: grayscale(0.3);
  }
  .rule-card:hover .rc-icon {
    opacity: 1;
    filter: grayscale(0);
    transform: scale(1.15);
  }
  .rule-card .rc-label {
    font-size: 10px;
    font-weight: 700;
    color: var(--text-muted);
    max-width: 64px;
    text-align: center;
    line-height: 1.3;
    opacity: 0;
    transform: translateY(-4px);
    transition: all 0.3s ease;
  }
  .rule-card:hover .rc-label {
    opacity: 1;
    transform: translateY(0);
    color: var(--accent);
  }

  .bottom-row {
    margin-top: 24px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
  }
  .mini-box {
    border-radius: 16px;
    padding: 14px 10px;
    cursor: pointer;
    transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    position: relative;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    gap: 6px;
    border: none;
    font-family: 'Tajawal', sans-serif;
    color: #fff;
  }
  .mini-box::before {
    content: '';
    position: absolute;
    top: 0; left: -100%; width: 80%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
    animation: btnShimmer 3.5s ease-in-out infinite;
  }
  @keyframes btnShimmer {
    0% { left: -100%; }
    45% { left: 120%; }
    100% { left: 120%; }
  }
  .mini-box:hover {
    transform: translateY(-4px) scale(1.04);
  }
  .mini-box:active { transform: scale(0.96); }
  .mini-box .box-icon {
    font-size: 28px;
    filter: drop-shadow(0 2px 6px rgba(0,0,0,0.3));
    line-height: 1;
  }
  .mini-box .box-label {
    font-size: 11.5px;
    font-weight: 800;
    text-shadow: 0 1px 4px rgba(0,0,0,0.2);
    line-height: 1.3;
  }
  .mini-box .box-sub {
    font-size: 9.5px;
    font-weight: 600;
    opacity: 0.75;
    line-height: 1.2;
  }
  .play-box {
    background: linear-gradient(145deg, #1a5276, #2980b9);
    box-shadow: 0 4px 16px rgba(26,82,118,0.35);
  }
  .play-box:hover {
    box-shadow: 0 8px 28px rgba(26,82,118,0.5);
  }
  .play-box .box-icon {
    animation: playBounce 2.5s ease-in-out infinite;
  }
  @keyframes playBounce {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.15) rotate(-5deg); }
  }
  .stop-box {
    background: linear-gradient(145deg, #d35400, #c0392b);
    box-shadow: 0 4px 16px rgba(192,57,43,0.35);
  }
  .stop-box:hover {
    box-shadow: 0 8px 28px rgba(192,57,43,0.5);
  }
  .stop-box .box-icon {
    animation: stopPulse 2.5s ease-in-out infinite;
  }

  /* ===== REGISTER SCREEN ===== */
  .register-screen { display: none; text-align: center; animation: fadeIn 0.5s ease-out; }
  .register-screen.visible { display: block; }

  .reg-card {
    background: linear-gradient(160deg, rgba(255,255,255,0.06) 0%, rgba(255,255,255,0.02) 100%);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 24px;
    padding: 32px 24px;
    margin-top: 12px;
    position: relative;
    overflow: hidden;
  }
  .reg-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--accent), #3498db, var(--accent));
    background-size: 200% auto;
    animation: regBarMove 3s linear infinite;
  }
  @keyframes regBarMove {
    0% { background-position: 0% center; }
    100% { background-position: 200% center; }
  }

  .reg-avatar {
    width: 72px; height: 72px;
    margin: 0 auto 16px;
    border-radius: 50%;
    background: linear-gradient(145deg, rgba(230,126,34,0.15), rgba(52,152,219,0.15));
    border: 2px solid rgba(230,126,34,0.25);
    display: flex; align-items: center; justify-content: center;
    font-size: 32px;
    position: relative;
  }
  .reg-avatar::after {
    content: '';
    position: absolute;
    inset: -5px;
    border-radius: 50%;
    border: 1.5px dashed rgba(230,126,34,0.2);
    animation: regAvatarSpin 12s linear infinite;
  }
  @keyframes regAvatarSpin { to { transform: rotate(360deg); } }

  .reg-title {
    font-size: 20px;
    font-weight: 900;
    color: #fff;
    margin-bottom: 4px;
  }
  .reg-subtitle {
    font-size: 13px;
    color: var(--text-muted);
    margin-bottom: 24px;
  }

  .reg-field {
    margin-bottom: 16px;
    text-align: right;
  }
  .reg-field label {
    display: block;
    font-size: 13px;
    font-weight: 700;
    color: rgba(255,255,255,0.65);
    margin-bottom: 6px;
    padding-right: 4px;
  }
  .reg-field label .req {
    color: #e74c3c;
    margin-right: 2px;
  }
  .reg-input {
    width: 100%;
    padding: 14px 16px;
    background: rgba(255,255,255,0.05);
    border: 1.5px solid rgba(255,255,255,0.1);
    border-radius: 14px;
    color: #fff;
    font-family: 'Tajawal', sans-serif;
    font-size: 16px;
    font-weight: 600;
    transition: all 0.3s ease;
    outline: none;
  }
  .reg-input::placeholder {
    color: rgba(255,255,255,0.25);
    font-weight: 500;
  }
  .reg-input:focus {
    border-color: var(--accent);
    background: rgba(230,126,34,0.06);
    box-shadow: 0 0 0 3px rgba(230,126,34,0.1);
  }
  .reg-input.error {
    border-color: #e74c3c;
    background: rgba(231,76,60,0.06);
    box-shadow: 0 0 0 3px rgba(231,76,60,0.1);
    animation: regShake 0.4s ease;
  }
  @keyframes regShake {
    0%, 100% { transform: translateX(0); }
    20% { transform: translateX(-6px); }
    40% { transform: translateX(6px); }
    60% { transform: translateX(-4px); }
    80% { transform: translateX(4px); }
  }
  .reg-error-msg {
    font-size: 11.5px;
    color: #e74c3c;
    margin-top: 5px;
    padding-right: 4px;
    display: none;
  }
  .reg-error-msg.show { display: block; animation: fadeIn 0.3s ease; }

  .reg-start-btn {
    width: 100%;
    margin-top: 8px;
    padding: 15px 20px;
    background: linear-gradient(135deg, var(--accent), #d35400);
    border: none;
    border-radius: 16px;
    color: #fff;
    font-family: 'Tajawal', sans-serif;
    font-size: 17px;
    font-weight: 800;
    cursor: pointer;
    transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    position: relative;
    overflow: hidden;
    box-shadow: 0 4px 18px rgba(230,126,34,0.3);
  }
  .reg-start-btn::before {
    content: '';
    position: absolute;
    top: 0; left: -100%; width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
    animation: btnShimmer 3s ease-in-out infinite;
  }
  .reg-start-btn:hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 28px rgba(230,126,34,0.45);
  }
  .reg-start-btn:active { transform: scale(0.97); }

  .reg-quiz-tag {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    background: rgba(52,152,219,0.12);
    border: 1px solid rgba(52,152,219,0.2);
    border-radius: 10px;
    padding: 8px 14px;
    margin-bottom: 20px;
    font-size: 13px;
    font-weight: 700;
    color: #3498db;
  }

  /* ===== RESULTS - EMPLOYEE INFO ===== */
  .result-employee {
    background: linear-gradient(135deg, rgba(255,255,255,0.06), rgba(255,255,255,0.02));
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 16px;
    padding: 14px 18px;
    margin-bottom: 18px;
    display: flex;
    align-items: center;
    gap: 14px;
    text-align: right;
  }
  .result-emp-avatar {
    width: 44px; height: 44px;
    border-radius: 50%;
    background: linear-gradient(145deg, rgba(230,126,34,0.2), rgba(52,152,219,0.2));
    border: 1.5px solid rgba(230,126,34,0.3);
    display: flex; align-items: center; justify-content: center;
    font-size: 20px;
    flex-shrink: 0;
  }
  .result-emp-details { flex: 1; }
  .result-emp-name {
    font-size: 15px;
    font-weight: 800;
    color: #fff;
  }
  .result-emp-id {
    font-size: 12px;
    color: var(--text-muted);
    font-weight: 600;
    direction: ltr;
    text-align: right;
  }

  .export-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 12px 24px;
    background: linear-gradient(135deg, #1a5276, #2471a3);
    border: 1px solid rgba(52,152,219,0.3);
    border-radius: 14px;
    color: #fff;
    font-family: 'Tajawal', sans-serif;
    font-size: 14px;
    font-weight: 700;
    cursor: pointer;
    transition: all 0.3s ease;
    margin-top: 10px;
    text-decoration: none;
  }
  .export-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(26,82,118,0.4);
  }

  /* ===== RULE INFO MODAL ===== */
  .rinfo-overlay {
    position: fixed; inset: 0; z-index: 999;
    display: none; align-items: center; justify-content: center;
    padding: 16px;
  }
  .rinfo-overlay.visible { display: flex; }
  .rinfo-backdrop {
    position: absolute; inset: 0;
    background: rgba(0,0,0,0.7);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    animation: fadeInBackdrop 0.3s ease;
  }
  .rinfo-modal {
    position: relative; z-index: 1;
    max-width: 400px; width: 100%;
    border-radius: 24px;
    overflow: hidden;
    animation: stopModalIn 0.55s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    box-shadow: 0 20px 60px rgba(0,0,0,0.5), 0 0 60px rgba(230,126,34,0.08);
  }
  .rinfo-header {
    padding: 28px 22px 20px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .rinfo-header::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.25), transparent);
  }
  .rinfo-num {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 52px; height: 52px;
    border-radius: 16px;
    font-size: 22px; font-weight: 900;
    color: #fff;
    margin-bottom: 10px;
    position: relative;
    background: rgba(255,255,255,0.15);
    border: 2px solid rgba(255,255,255,0.2);
    box-shadow: 0 0 20px rgba(255,255,255,0.1);
    animation: stopHandReveal 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.15s both;
  }
  .rinfo-name {
    font-size: 21px; font-weight: 900; color: #fff;
    text-shadow: 0 2px 8px rgba(0,0,0,0.3);
    animation: stopFadeUp 0.4s ease-out 0.2s both;
  }
  .rinfo-body {
    background: linear-gradient(180deg, #111827, #0d1b2a);
    padding: 18px;
  }
  .rinfo-fact {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    padding: 12px 14px;
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.06);
    border-radius: 14px;
    margin-bottom: 10px;
    position: relative;
    overflow: hidden;
  }
  .rinfo-fact::before {
    content: '';
    position: absolute;
    right: 0; top: 0; bottom: 0; width: 3px;
    border-radius: 3px 0 0 3px;
  }
  .rinfo-fact:nth-child(1) { animation: stopSlideIn 0.4s ease-out 0.25s both; }
  .rinfo-fact:nth-child(1)::before { background: var(--accent); box-shadow: 0 0 10px rgba(230,126,34,0.4); }
  .rinfo-fact:nth-child(2) { animation: stopSlideIn 0.4s ease-out 0.35s both; }
  .rinfo-fact:nth-child(2)::before { background: #3498db; box-shadow: 0 0 10px rgba(52,152,219,0.4); }
  .rinfo-fact:nth-child(3) { animation: stopSlideIn 0.4s ease-out 0.45s both; }
  .rinfo-fact:nth-child(3)::before { background: #2ecc71; box-shadow: 0 0 10px rgba(46,204,113,0.4); }
  .rinfo-fact-icon {
    width: 34px; height: 34px;
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0; font-size: 16px;
    background: rgba(230,126,34,0.1);
    border: 1px solid rgba(230,126,34,0.2);
  }
  .rinfo-fact:nth-child(2) .rinfo-fact-icon {
    background: rgba(52,152,219,0.1);
    border-color: rgba(52,152,219,0.2);
  }
  .rinfo-fact:nth-child(3) .rinfo-fact-icon {
    background: rgba(46,204,113,0.1);
    border-color: rgba(46,204,113,0.2);
  }
  .rinfo-fact-text {
    font-size: 13px; font-weight: 600;
    color: rgba(255,255,255,0.85);
    line-height: 1.7;
  }
  .rinfo-actions {
    display: flex; gap: 10px;
    margin-top: 6px;
    padding: 0 18px 18px;
    background: linear-gradient(180deg, #0d1b2a, #0d1b2a);
  }
  .rinfo-start-btn {
    flex: 1;
    padding: 13px 16px;
    background: linear-gradient(135deg, var(--accent), #d35400);
    border: none; border-radius: 14px;
    color: #fff; font-family: 'Tajawal', sans-serif;
    font-size: 15px; font-weight: 800;
    cursor: pointer;
    transition: all 0.3s ease;
    position: relative; overflow: hidden;
    box-shadow: 0 4px 16px rgba(230,126,34,0.3);
  }
  .rinfo-start-btn::before {
    content: '';
    position: absolute;
    top: 0; left: -100%; width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
    animation: btnShimmer 3s ease-in-out infinite;
  }
  .rinfo-start-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 24px rgba(230,126,34,0.45);
  }
  .rinfo-close-link {
    padding: 13px 18px;
    background: rgba(255,255,255,0.06);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 14px;
    color: rgba(255,255,255,0.6);
    font-family: 'Tajawal', sans-serif;
    font-size: 14px; font-weight: 700;
    cursor: pointer;
    transition: all 0.3s ease;
  }
  .rinfo-close-link:hover {
    background: rgba(255,255,255,0.1);
    color: #fff;
  }

  /* ===== QUIZ SCREEN ===== */
  .quiz-screen { display: none; }
  .quiz-screen.visible { display: block; animation: fadeIn 0.5s ease-out; }

  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
  @keyframes slideDown { from { opacity: 0; transform: translateY(-30px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes cardEnter { from { opacity: 0; transform: translateY(20px) scale(0.97); } to { opacity: 1; transform: translateY(0) scale(1); } }
  @keyframes fadeSlideUp { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes correctPulse { 0% { transform: scale(1); } 30% { transform: scale(1.02); } 100% { transform: scale(1); } }
  @keyframes shake {
    0%, 100% { transform: translateX(0); } 20% { transform: translateX(8px); }
    40% { transform: translateX(-8px); } 60% { transform: translateX(6px); } 80% { transform: translateX(-4px); }
  }
  @keyframes pulseGlow {
    0%, 100% { box-shadow: 0 4px 20px rgba(230, 126, 34, 0.35); }
    50% { box-shadow: 0 4px 30px rgba(230, 126, 34, 0.55); }
  }

  .header { text-align: center; margin-bottom: 28px; animation: slideDown 0.7s ease-out; }

  .rule-badge {
    display: inline-flex; align-items: center; gap: 10px;
    background: linear-gradient(135deg, var(--accent), #d35400);
    padding: 8px 22px; border-radius: 50px;
    font-size: 18px; font-weight: 800; margin-bottom: 14px;
    box-shadow: 0 4px 20px rgba(230, 126, 34, 0.35);
    animation: pulseGlow 3s ease-in-out infinite;
  }
  .rule-badge .num {
    background: #fff; color: var(--accent);
    width: 32px; height: 32px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 16px; font-weight: 900;
  }

  .header h1 {
    font-size: 26px; font-weight: 900; margin-bottom: 6px;
    background: linear-gradient(90deg, #fff, #d4e6f1);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  }
  .header p { color: var(--text-muted); font-size: 14px; font-weight: 500; line-height: 1.6; }

  .back-btn {
    display: inline-flex; align-items: center; gap: 6px;
    background: none; border: none; color: var(--text-muted);
    font-family: 'Tajawal', sans-serif; font-size: 14px; font-weight: 600;
    cursor: pointer; margin-bottom: 16px; padding: 6px 0;
    transition: color 0.3s;
  }
  .back-btn:hover { color: var(--accent); }

  .progress-section { margin-bottom: 24px; }
  .progress-info {
    display: flex; justify-content: space-between; align-items: center;
    margin-bottom: 8px; font-size: 14px; font-weight: 500; color: var(--text-muted);
  }
  .progress-bar-track {
    width: 100%; height: 8px; background: rgba(255,255,255,0.08);
    border-radius: 10px; overflow: hidden;
  }
  .progress-bar-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--accent), var(--accent-glow));
    border-radius: 10px;
    transition: width 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
    box-shadow: 0 0 10px rgba(230, 126, 34, 0.4);
  }

  .score-display {
    display: flex; align-items: center; gap: 6px;
    font-weight: 700; color: var(--accent-glow);
  }
  .score-display svg { width: 18px; height: 18px; }

  .question-card {
    background: var(--card-bg); border: 1px solid var(--card-border);
    border-radius: 20px; padding: 28px 22px; margin-bottom: 20px;
    backdrop-filter: blur(10px); animation: cardEnter 0.5s ease-out;
    position: relative; overflow: hidden;
  }
  .question-card::before {
    content: ''; position: absolute; top: 0; right: 0; left: 0; height: 3px;
    background: linear-gradient(90deg, var(--accent), var(--accent-glow), var(--accent));
  }

  .rule-tag {
    display: inline-block; padding: 4px 12px; border-radius: 8px;
    font-size: 11px; font-weight: 700; margin-bottom: 10px;
    background: rgba(230,126,34,0.15); color: var(--accent); border: 1px solid rgba(230,126,34,0.25);
  }

  .question-number {
    font-size: 13px; font-weight: 700; color: var(--accent);
    letter-spacing: 1px; margin-bottom: 12px;
  }
  .question-text {
    font-size: 19px; font-weight: 700; line-height: 1.7;
    margin-bottom: 24px; color: #fff;
  }

  .options-list { display: flex; flex-direction: column; gap: 12px; }

  .option-btn {
    display: flex; align-items: center; gap: 14px;
    width: 100%; padding: 16px 18px;
    background: rgba(255,255,255,0.04); border: 2px solid rgba(255,255,255,0.1);
    border-radius: 14px; cursor: pointer; transition: all 0.3s ease;
    text-align: right; font-family: 'Tajawal', sans-serif;
    font-size: 16px; font-weight: 500; color: var(--text);
    position: relative; overflow: hidden;
  }
  .option-btn::before {
    content: ''; position: absolute; inset: 0;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.03));
    opacity: 0; transition: opacity 0.3s;
  }
  .option-btn:hover:not(.disabled) {
    border-color: var(--accent); background: rgba(230, 126, 34, 0.08);
    transform: translateX(-4px);
  }
  .option-btn:hover:not(.disabled)::before { opacity: 1; }

  .option-icon {
    width: 40px; height: 40px; border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px; font-weight: 800; flex-shrink: 0;
    background: rgba(255,255,255,0.06); border: 1px solid rgba(255,255,255,0.1);
    transition: all 0.3s ease;
  }

  .option-btn.correct { border-color: var(--correct); background: var(--correct-bg); animation: correctPulse 0.5s ease; }
  .option-btn.correct .option-icon { background: var(--correct); color: #fff; border-color: var(--correct); }
  .option-btn.wrong { border-color: var(--wrong); background: var(--wrong-bg); animation: shake 0.5s ease; }
  .option-btn.wrong .option-icon { background: var(--wrong); color: #fff; border-color: var(--wrong); }
  .option-btn.disabled { pointer-events: none; opacity: 0.5; }
  .option-btn.correct.disabled, .option-btn.wrong.disabled { opacity: 1; }

  .feedback-box {
    margin-top: 18px; padding: 16px 18px; border-radius: 14px;
    font-size: 15px; font-weight: 600; line-height: 1.7;
    animation: fadeSlideUp 0.4s ease-out; display: none;
  }
  .feedback-box.correct-feedback {
    background: var(--correct-bg); border: 1px solid rgba(39, 174, 96, 0.3);
    color: #2ecc71; display: block;
  }
  .feedback-box.wrong-feedback {
    background: var(--wrong-bg); border: 1px solid rgba(231, 76, 60, 0.3);
    color: #e74c3c; display: block;
  }

  .next-btn {
    display: none; width: 100%; padding: 16px; margin-top: 16px;
    background: linear-gradient(135deg, var(--accent), #d35400);
    color: #fff; border: none; border-radius: 14px;
    font-family: 'Tajawal', sans-serif; font-size: 17px; font-weight: 700;
    cursor: pointer; transition: all 0.3s ease;
    box-shadow: 0 4px 15px rgba(230, 126, 34, 0.3);
  }
  .next-btn:hover { transform: translateY(-2px); box-shadow: 0 6px 25px rgba(230, 126, 34, 0.45); }
  .next-btn.visible { display: block; animation: fadeSlideUp 0.4s ease-out; }

  /* ===== RESULTS ===== */
  .results-screen { display: none; text-align: center; animation: cardEnter 0.6s ease-out; }
  .results-screen.visible { display: block; }

  .result-circle {
    width: 160px; height: 160px; border-radius: 50%;
    margin: 0 auto 24px; display: flex; flex-direction: column;
    align-items: center; justify-content: center; position: relative;
  }
  .result-circle::before {
    content: ''; position: absolute; inset: -4px; border-radius: 50%; padding: 4px;
    background: conic-gradient(var(--accent) var(--pct), rgba(255,255,255,0.1) var(--pct));
    -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
    mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
    -webkit-mask-composite: xor; mask-composite: exclude;
  }
  .result-score { font-size: 44px; font-weight: 900; color: var(--accent-glow); }
  .result-total { font-size: 16px; color: var(--text-muted); font-weight: 600; }
  .result-title { font-size: 26px; font-weight: 800; margin-bottom: 8px; }
  .result-msg {
    font-size: 16px; color: var(--text-muted); line-height: 1.7;
    margin-bottom: 28px; max-width: 400px; margin-left: auto; margin-right: auto;
  }

  .summary-list {
    text-align: right; margin: 28px 0;
    display: flex; flex-direction: column; gap: 10px;
  }
  .summary-item {
    display: flex; align-items: center; gap: 12px;
    padding: 14px 16px; background: var(--card-bg);
    border-radius: 12px; border: 1px solid var(--card-border);
    font-size: 14px; font-weight: 500; line-height: 1.5;
  }
  .summary-icon {
    width: 32px; height: 32px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 16px; flex-shrink: 0;
  }
  .summary-icon.correct-icon { background: var(--correct-bg); color: var(--correct); }
  .summary-icon.wrong-icon { background: var(--wrong-bg); color: var(--wrong); }

  .result-buttons { display: flex; flex-direction: column; gap: 12px; align-items: center; }
  .restart-btn, .home-btn-result {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 14px 36px; color: #fff; border: none; border-radius: 14px;
    font-family: 'Tajawal', sans-serif; font-size: 17px; font-weight: 700;
    cursor: pointer; transition: all 0.3s ease;
  }
  .restart-btn {
    background: linear-gradient(135deg, var(--accent), #d35400);
    box-shadow: 0 4px 15px rgba(230, 126, 34, 0.3); width: 100%; justify-content: center;
  }
  .restart-btn:hover { transform: translateY(-2px); box-shadow: 0 6px 25px rgba(230, 126, 34, 0.45); }
  .home-btn-result {
    background: rgba(255,255,255,0.08); border: 1px solid var(--card-border);
    width: 100%; justify-content: center;
  }
  .home-btn-result:hover { background: rgba(255,255,255,0.12); }

  @keyframes stopPulse {
    0%, 100% { transform: scale(1) rotate(0deg); }
    25% { transform: scale(1.08) rotate(-5deg); }
    50% { transform: scale(1.12) rotate(0deg); }
    75% { transform: scale(1.08) rotate(5deg); }
  }

  /* ===== STOP MODAL ===== */
  .stop-overlay {
    position: fixed;
    inset: 0;
    z-index: 1000;
    display: none;
    align-items: center;
    justify-content: center;
    padding: 16px;
  }
  .stop-overlay.visible { display: flex; }
  .stop-backdrop {
    position: absolute;
    inset: 0;
    background: rgba(0,0,0,0.75);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    animation: fadeInBackdrop 0.3s ease;
  }
  @keyframes fadeInBackdrop { from { opacity: 0; } to { opacity: 1; } }
  .stop-modal {
    position: relative;
    z-index: 1;
    max-width: 400px;
    width: 100%;
    border-radius: 28px;
    overflow: hidden;
    animation: stopModalIn 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    box-shadow: 0 0 0 1px rgba(231,76,60,0.2), 0 25px 70px rgba(0,0,0,0.6), 0 0 80px rgba(231,76,60,0.1);
  }
  @keyframes stopModalIn {
    from { transform: scale(0.6) translateY(40px); opacity: 0; }
    to { transform: scale(1) translateY(0); opacity: 1; }
  }
  .stop-modal-header {
    background: linear-gradient(170deg, #c0392b 0%, #96281b 50%, #1a1a2e 100%);
    padding: 36px 24px 30px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .stop-modal-header::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at 50% 80%, rgba(231,76,60,0.25) 0%, transparent 70%);
    pointer-events: none;
  }
  .stop-modal-header::after {
    content: '';
    position: absolute;
    bottom: -1px; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, transparent, #e74c3c, #f39c12, #e74c3c, transparent);
    animation: stopBarGlow 2.5s ease-in-out infinite;
  }
  @keyframes stopBarGlow {
    0%, 100% { opacity: 0.5; }
    50% { opacity: 1; }
  }
  .stop-modal-icon {
    width: 72px;
    height: 72px;
    margin: 0 auto 14px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 36px;
    position: relative;
    z-index: 1;
    animation: stopHandReveal 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.2s both;
    background: radial-gradient(circle, rgba(255,255,255,0.12) 0%, transparent 70%);
  }
  .stop-modal-icon::before {
    content: '';
    position: absolute;
    inset: -4px;
    border-radius: 50%;
    border: 2px solid rgba(231,76,60,0.5);
    animation: stopRingPulse 2s ease-in-out infinite;
  }
  .stop-modal-icon::after {
    content: '';
    position: absolute;
    inset: -12px;
    border-radius: 50%;
    border: 1px solid rgba(231,76,60,0.2);
    animation: stopRingPulse 2s ease-in-out 0.5s infinite;
  }
  @keyframes stopHandReveal {
    from { transform: scale(0) rotate(-20deg); opacity: 0; }
    to { transform: scale(1) rotate(0deg); opacity: 1; }
  }
  @keyframes stopRingPulse {
    0%, 100% { transform: scale(1); opacity: 0.5; }
    50% { transform: scale(1.12); opacity: 1; }
  }
  .stop-modal-title {
    font-size: 23px;
    font-weight: 900;
    color: #fff;
    text-shadow: 0 0 20px rgba(231,76,60,0.4), 0 2px 8px rgba(0,0,0,0.3);
    position: relative;
    z-index: 1;
    animation: stopFadeUp 0.5s ease-out 0.3s both;
  }
  .stop-modal-body {
    background: linear-gradient(180deg, #111827, #0d1b2a);
    padding: 20px 18px;
    position: relative;
  }
  .stop-modal-body::before {
    content: '';
    position: absolute;
    top: 0; left: 50%; transform: translateX(-50%);
    width: 60%;
    height: 1px;
    background: linear-gradient(90deg, transparent, rgba(231,76,60,0.3), transparent);
  }
  .stop-authority {
    background: linear-gradient(135deg, rgba(231,76,60,0.08), rgba(243,156,18,0.06));
    border: 1px solid rgba(231,76,60,0.15);
    border-radius: 16px;
    padding: 14px 16px;
    margin-bottom: 14px;
    text-align: center;
    animation: stopFadeUp 0.5s ease-out 0.35s both;
    position: relative;
    overflow: hidden;
  }
  .stop-authority::before {
    content: '';
    position: absolute;
    top: 0; left: -100%; width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(231,76,60,0.06), transparent);
    animation: stopSweepAuth 4s ease-in-out infinite;
  }
  @keyframes stopSweepAuth {
    0% { left: -100%; } 50% { left: 100%; } 100% { left: 100%; }
  }
  .stop-authority-text {
    font-size: 14px;
    font-weight: 700;
    color: #f39c12;
    line-height: 1.7;
  }
  .stop-items {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  .stop-item {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 14px;
    background: rgba(255,255,255,0.03);
    border-radius: 14px;
    transition: all 0.4s ease;
    position: relative;
    overflow: hidden;
    border: 1px solid rgba(255,255,255,0.05);
  }
  .stop-item::before {
    content: '';
    position: absolute;
    right: 0; top: 0; bottom: 0;
    width: 3px;
    border-radius: 3px 0 0 3px;
    transition: all 0.4s ease;
  }
  .stop-item:nth-child(1)::before { background: #e74c3c; box-shadow: 0 0 12px rgba(231,76,60,0.4); }
  .stop-item:nth-child(2)::before { background: #f39c12; box-shadow: 0 0 12px rgba(243,156,18,0.4); }
  .stop-item:nth-child(3)::before { background: #e67e22; box-shadow: 0 0 12px rgba(230,126,34,0.4); }
  .stop-item:nth-child(1) { animation: stopSlideIn 0.5s ease-out 0.4s both; }
  .stop-item:nth-child(2) { animation: stopSlideIn 0.5s ease-out 0.55s both; }
  .stop-item:nth-child(3) { animation: stopSlideIn 0.5s ease-out 0.7s both; }
  @keyframes stopSlideIn {
    from { transform: translateX(30px); opacity: 0; }
    to { transform: translateX(0); opacity: 1; }
  }
  @keyframes stopFadeUp {
    from { transform: translateY(15px); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
  }
  .stop-item-icon {
    width: 38px;
    height: 38px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    font-size: 17px;
  }
  .stop-item:nth-child(1) .stop-item-icon {
    background: rgba(231,76,60,0.12);
    border: 1px solid rgba(231,76,60,0.25);
  }
  .stop-item:nth-child(2) .stop-item-icon {
    background: rgba(243,156,18,0.12);
    border: 1px solid rgba(243,156,18,0.25);
  }
  .stop-item:nth-child(3) .stop-item-icon {
    background: rgba(230,126,34,0.12);
    border: 1px solid rgba(230,126,34,0.25);
  }
  .stop-item-text {
    font-size: 13.5px;
    font-weight: 600;
    color: rgba(255,255,255,0.88);
    line-height: 1.65;
  }
  .stop-responsibility {
    margin-top: 14px;
    padding: 16px;
    border-radius: 16px;
    text-align: center;
    animation: stopFadeUp 0.5s ease-out 0.85s both;
    position: relative;
    background: linear-gradient(135deg, rgba(26,82,118,0.2), rgba(39,174,96,0.1));
    border: 1px solid rgba(39,174,96,0.15);
    overflow: hidden;
  }
  .stop-responsibility::before {
    content: '';
    position: absolute;
    inset: -1px;
    border-radius: 16px;
    background: conic-gradient(from 0deg, transparent, rgba(39,174,96,0.15), transparent, rgba(52,152,219,0.15), transparent);
    animation: stopRotateBorder 6s linear infinite;
    z-index: 0;
  }
  @keyframes stopRotateBorder {
    to { transform: rotate(360deg); }
  }
  .stop-responsibility-icon {
    font-size: 26px;
    margin-bottom: 6px;
    position: relative;
    z-index: 1;
    animation: stopShieldGlow 2s ease-in-out infinite;
  }
  @keyframes stopShieldGlow {
    0%, 100% { filter: drop-shadow(0 0 4px rgba(39,174,96,0.3)); }
    50% { filter: drop-shadow(0 0 12px rgba(39,174,96,0.6)); }
  }
  .stop-responsibility-text {
    font-size: 14px;
    font-weight: 700;
    color: #2ecc71;
    line-height: 1.7;
    position: relative;
    z-index: 1;
  }
  .stop-footer {
    background: linear-gradient(135deg, #111827, #0d1b2a);
    border-top: 1px solid rgba(255,255,255,0.05);
    padding: 12px 20px;
    text-align: center;
    font-size: 11px;
    font-weight: 700;
    color: rgba(243,156,18,0.7);
    letter-spacing: 0.3px;
    line-height: 1.6;
  }
  .stop-close-btn {
    position: absolute;
    top: 12px;
    left: 12px;
    width: 34px;
    height: 34px;
    border-radius: 50%;
    border: 1px solid rgba(255,255,255,0.15);
    background: rgba(0,0,0,0.35);
    color: rgba(255,255,255,0.7);
    font-size: 16px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s;
    z-index: 2;
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
  }
  .stop-close-btn:hover {
    background: rgba(231,76,60,0.4);
    border-color: rgba(231,76,60,0.5);
    color: #fff;
    transform: rotate(90deg);
  }

  @media (max-width: 400px) {
    .home-title { font-size: 26px; }
    .header h1 { font-size: 22px; }
    .question-text { font-size: 17px; }
    .option-btn { padding: 14px 14px; font-size: 15px; }
    .app-container { padding: 16px 12px 32px; }
    .rule-card .rc-num { width: 50px; height: 50px; font-size: 18px; border-radius: 14px; }
    .rule-card .rc-icon { font-size: 15px; }
    .rule-cards { gap: 12px; }
    .stop-modal-title { font-size: 20px; }
    .stop-modal-header { padding: 28px 18px 24px; }
    .stop-modal-body { padding: 16px 14px; }
    .stop-modal-icon { width: 60px; height: 60px; font-size: 30px; }
    .stop-item-icon { width: 32px; height: 32px; font-size: 14px; }
    .stop-item-text { font-size: 12.5px; }
    .stop-authority-text { font-size: 13px; }
    .bottom-row { gap: 10px; }
    .mini-box { padding: 12px 8px; }
    .mini-box .box-icon { font-size: 24px; }
    .mini-box .box-label { font-size: 10.5px; }
    .mini-box .box-sub { font-size: 9px; }
  }
</style>
</head>
<body>

<div class="bg-pattern"></div>

<div class="app-container">

  <!-- ===== HOME SCREEN ===== -->
  <div class="home-screen" id="homeScreen">
    <div style="margin-bottom: 20px; animation: slideDown 0.7s ease-out;">
      <div class="home-title">قواعد الحفاظ على الحياة</div>
      <div class="home-subtitle">اختر القاعدة لبدء الاختبار</div>
    </div>
    <div class="home-label">اختر القاعدة</div>
    <div class="rule-cards">
      <div class="rule-card" onclick="showRuleInfo('rule1')" style="animation: cardEnter 0.4s ease-out 0.1s both;">
        <div class="rc-icon">⚡</div><div class="rc-num">01</div><div class="rc-label">عزل الطاقة</div>
      </div>
      <div class="rule-card" onclick="showRuleInfo('rule2')" style="animation: cardEnter 0.4s ease-out 0.16s both;">
        <div class="rc-icon">📋</div><div class="rc-num">02</div><div class="rc-label">تصريح العمل</div>
      </div>
      <div class="rule-card" onclick="showRuleInfo('rule3')" style="animation: cardEnter 0.4s ease-out 0.22s both;">
        <div class="rc-icon">🦺</div><div class="rc-num">03</div><div class="rc-label">معدات الحماية</div>
      </div>
      <div class="rule-card" onclick="showRuleInfo('rule4')" style="animation: cardEnter 0.4s ease-out 0.28s both;">
        <div class="rc-icon">🪜</div><div class="rc-num">04</div><div class="rc-label">المرتفعات</div>
      </div>
      <div class="rule-card" onclick="showRuleInfo('rule5')" style="animation: cardEnter 0.4s ease-out 0.34s both;">
        <div class="rc-icon">🚫</div><div class="rc-num">05</div><div class="rc-label">تجاوز السلامة</div>
      </div>
      <div class="rule-card" onclick="showRuleInfo('rule6')" style="animation: cardEnter 0.4s ease-out 0.4s both;">
        <div class="rc-icon">🔥</div><div class="rc-num">06</div><div class="rc-label">العمل الساخن</div>
      </div>
      <div class="rule-card" onclick="showRuleInfo('rule7')" style="animation: cardEnter 0.4s ease-out 0.46s both;">
        <div class="rc-icon">🕳️</div><div class="rc-num">07</div><div class="rc-label">أماكن محصورة</div>
      </div>
      <div class="rule-card" onclick="showRuleInfo('rule8')" style="animation: cardEnter 0.4s ease-out 0.52s both;">
        <div class="rc-icon">⚠️</div><div class="rc-num">08</div><div class="rc-label">منطقة الخطر</div>
      </div>
      <div class="rule-card" onclick="showRuleInfo('rule9')" style="animation: cardEnter 0.4s ease-out 0.58s both;">
        <div class="rc-icon">🏗️</div><div class="rc-num">09</div><div class="rc-label">عمليات الرفع</div>
      </div>
      <div class="rule-card" onclick="showRuleInfo('rule10')" style="animation: cardEnter 0.4s ease-out 0.64s both;">
        <div class="rc-icon">🚗</div><div class="rc-num">10</div><div class="rc-label">قيادة المركبات</div>
      </div>
    </div>
    <div class="bottom-row" style="animation: cardEnter 0.5s ease-out 0.9s both;">
      <button class="mini-box play-box" onclick="showRegister('all')">
        <div class="box-icon">🎯</div>
        <div class="box-label">اختبار شامل</div>
        <div class="box-sub">٨٠ سؤال</div>
      </button>
      <div class="mini-box stop-box" onclick="openStopModal()">
        <div class="box-icon">✋</div>
        <div class="box-label">أوقف العمل</div>
        <div class="box-sub">الغير آمن</div>
      </div>
    </div>
  </div>

  <!-- ===== REGISTER SCREEN ===== -->
  <div class="register-screen" id="registerScreen">
    <button class="back-btn" onclick="goHomeFromReg()">→ العودة للقائمة</button>
    <div class="reg-card">
      <div class="reg-avatar">👷</div>
      <div class="reg-title">تسجيل بيانات الموظف</div>
      <div class="reg-subtitle">أدخل بياناتك قبل بدء الاختبار</div>

      <div class="reg-quiz-tag" id="regQuizTag">📝 اختبار عزل الطاقة</div>

      <div class="reg-field">
        <label><span class="req">*</span> الاسم الكامل</label>
        <input type="text" class="reg-input" id="regName" placeholder="مثال: أحمد محمد العتيبي" autocomplete="off">
        <div class="reg-error-msg" id="regNameErr">يرجى إدخال الاسم</div>
      </div>
      <div class="reg-field">
        <label><span class="req">*</span> الرقم الوظيفي</label>
        <input type="text" class="reg-input" id="regId" placeholder="مثال: 100234" autocomplete="off" inputmode="numeric">
        <div class="reg-error-msg" id="regIdErr">يرجى إدخال الرقم الوظيفي</div>
      </div>

      <button class="reg-start-btn" onclick="submitRegistration()">ابدأ الاختبار ←</button>
    </div>
  </div>

  <!-- ===== RULE INFO MODAL ===== -->
  <div class="rinfo-overlay" id="rinfoOverlay">
    <div class="rinfo-backdrop" onclick="closeRuleInfo()"></div>
    <div class="rinfo-modal">
      <div class="rinfo-header" id="rinfoHeader">
        <div class="rinfo-num" id="rinfoNum">01</div>
        <div class="rinfo-name" id="rinfoName">عزل الطاقة</div>
      </div>
      <div class="rinfo-body" id="rinfoBody"></div>
      <div class="rinfo-actions">
        <button class="rinfo-start-btn" id="rinfoStartBtn" onclick="proceedToRegister()">📝 ابدأ الاختبار</button>
        <button class="rinfo-close-link" onclick="closeRuleInfo()">رجوع</button>
      </div>
    </div>
  </div>

  <!-- ===== STOP WORK MODAL ===== -->
  <div class="stop-overlay" id="stopOverlay">
    <div class="stop-backdrop" onclick="closeStopModal()"></div>
    <div class="stop-modal">
      <button class="stop-close-btn" onclick="closeStopModal()">✕</button>
      <div class="stop-modal-header">
        <div class="stop-modal-icon">✋</div>
        <div class="stop-modal-title">أوقف العمل الغير آمن</div>
      </div>
      <div class="stop-modal-body">
        <div class="stop-authority">
          <div class="stop-authority-text">جميع الموظفون والمقاولون لديهم الصلاحية لإيقاف العمل الغير آمن</div>
        </div>
        <div class="stop-items">
          <div class="stop-item">
            <div class="stop-item-icon">⚡</div>
            <div class="stop-item-text">أوقف العمل إذا لم يتم عزل الطاقة والتأكد من خلال الاختبار</div>
          </div>
          <div class="stop-item">
            <div class="stop-item-icon">🦺</div>
            <div class="stop-item-text">أوقف العمل عند عدم ارتداء معدات الوقاية الشخصية المناسبة للعمل</div>
          </div>
          <div class="stop-item">
            <div class="stop-item-icon">⚠️</div>
            <div class="stop-item-text">أوقف العمل إذا لم يتم إتباع إجراءات السلامة بشكل صحيح</div>
          </div>
        </div>
        <div class="stop-responsibility">
          <div class="stop-responsibility-icon">🛡️</div>
          <div class="stop-responsibility-text">أنا مسؤول عن سلامتي وسلامة الأخرين</div>
        </div>
      </div>
      <div class="stop-footer">أحافظ على حياتي وحياة الأخرين باستخدام صلاحيتي بإيقاف العمل الغير آمن</div>
    </div>
  </div>

  <!-- ===== QUIZ SCREEN ===== -->
  <div class="quiz-screen" id="quizScreen">
    <button class="back-btn" onclick="goHome()">→ العودة للقائمة</button>

    <div class="header">
      <div class="rule-badge" id="ruleBadge">
        <span class="num" id="ruleNum">01</span>
        <span id="ruleName">عزل الطاقة</span>
      </div>
      <h1 id="quizTitle">اختبار قواعد إنقاذ الحياة</h1>
      <p id="quizDesc"></p>
    </div>

    <div class="progress-section">
      <div class="progress-info">
        <span id="questionCounter"></span>
        <div class="score-display">
          <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2L15.09 8.26L22 9.27L17 14.14L18.18 21.02L12 17.77L5.82 21.02L7 14.14L2 9.27L8.91 8.26L12 2Z"/></svg>
          <span id="scoreDisplay">٠</span>
        </div>
      </div>
      <div class="progress-bar-track">
        <div class="progress-bar-fill" id="progressFill" style="width: 0%"></div>
      </div>
    </div>

    <div class="question-card" id="questionCard">
      <div class="rule-tag" id="ruleTag"></div>
      <div class="question-number" id="questionLabel"></div>
      <div class="question-text" id="questionText"></div>
      <div class="options-list" id="optionsList"></div>
      <div class="feedback-box" id="feedbackBox"></div>
      <button class="next-btn" id="nextBtn" onclick="nextQuestion()">السؤال التالي ←</button>
    </div>
  </div>

  <!-- ===== RESULTS SCREEN ===== -->
  <div class="results-screen" id="resultsScreen">
    <div class="result-employee" id="resultEmployee">
      <div class="result-emp-avatar">👷</div>
      <div class="result-emp-details">
        <div class="result-emp-name" id="resultEmpName"></div>
        <div class="result-emp-id" id="resultEmpId"></div>
      </div>
    </div>
    <div class="result-circle" id="resultCircle">
      <div class="result-score" id="resultScore"></div>
      <div class="result-total" id="resultTotal"></div>
    </div>
    <div class="result-title" id="resultTitle"></div>
    <div class="result-msg" id="resultMsg"></div>
    <div class="summary-list" id="summaryList"></div>
    <div class="result-buttons">
      <button class="restart-btn" onclick="restartQuiz()">↺ إعادة الاختبار</button>
      <button class="home-btn-result" onclick="goHome()">→ العودة للقائمة</button>
    </div>
    <button class="export-btn" onclick="exportResults()">📄 تحميل النتيجة</button>
  </div>

</div>

<script>
  var arabicNums = ['٠','١','٢','٣','٤','٥','٦','٧','٨','٩'];
  function toArabic(n) {
    return String(n).split('').map(function(d) { return arabicNums[parseInt(d)] || d; }).join('');
  }
  var ordinals = ['الأول','الثاني','الثالث','الرابع','الخامس','السادس','السابع','الثامن',
    'التاسع','العاشر','الحادي عشر','الثاني عشر','الثالث عشر','الرابع عشر','الخامس عشر','السادس عشر',
    'السابع عشر','الثامن عشر','التاسع عشر','العشرون','الحادي والعشرون','الثاني والعشرون','الثالث والعشرون','الرابع والعشرون',
    'الخامس والعشرون','السادس والعشرون','السابع والعشرون','الثامن والعشرون','التاسع والعشرون','الثلاثون','الحادي والثلاثون','الثاني والثلاثون',
    'الثالث والثلاثون','الرابع والثلاثون','الخامس والثلاثون','السادس والثلاثون','السابع والثلاثون','الثامن والثلاثون','التاسع والثلاثون','الأربعون',
    'الحادي والأربعون','الثاني والأربعون','الثالث والأربعون','الرابع والأربعون','الخامس والأربعون','السادس والأربعون','السابع والأربعون','الثامن والأربعون',
    'التاسع والأربعون','الخمسون','الحادي والخمسون','الثاني والخمسون','الثالث والخمسون','الرابع والخمسون','الخامس والخمسون','السادس والخمسون',
    'السابع والخمسون','الثامن والخمسون','التاسع والخمسون','الستون','الحادي والستون','الثاني والستون','الثالث والستون','الرابع والستون',
    'الخامس والستون','السادس والستون','السابع والستون','الثامن والستون','التاسع والستون','السبعون','الحادي والسبعون','الثاني والسبعون',
    'الثالث والسبعون','الرابع والسبعون','الخامس والسبعون','السادس والسبعون','السابع والسبعون','الثامن والسبعون','التاسع والسبعون','الثمانون'];

  var rule1Questions = [
    {
      rule: "01 — عزل الطاقة",
      q: "قبل بدء العمل على معدات كهربائية، ما أول خطوة يجب اتخاذها؟",
      options: ["البدء بالعمل فوراً لتوفير الوقت","تحديد جميع مصادر الطاقة المتصلة بالمعدات","ارتداء القفازات فقط والبدء بالعمل","سؤال زميل إذا كانت الطاقة مفصولة"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب دائماً تحديد جميع مصادر الطاقة كخطوة أولى قبل أي عمل.",
      feedback_wrong: "✗ خطأ! الخطوة الأولى هي تحديد جميع مصادر الطاقة المتصلة بالمعدات."
    },
    {
      rule: "01 — عزل الطاقة",
      q: "بعد عزل مصادر الطاقة، ما الإجراء الصحيح؟",
      options: ["وضع الأقفال والبطاقات التحذيرية على نقاط العزل","ترك نقاط العزل مفتوحة ليراها الجميع","إبلاغ المشرف شفهياً فقط","كتابة ملاحظة على ورقة وتركها بجانب المعدة"],
      correct: 0,
      feedback_correct: "✓ صحيح! يجب وضع الأقفال وعلامات البطاقات التحذيرية على جميع نقاط العزل.",
      feedback_wrong: "✗ خطأ! يجب وضع الأقفال والبطاقات التحذيرية على نقاط العزل لضمان عدم إعادة تشغيل الطاقة."
    },
    {
      rule: "01 — عزل الطاقة",
      q: "ما المقصود بالطاقة المتبقية أو المخزنة؟",
      options: ["الطاقة التي تبقى في النظام حتى بعد فصل المصدر الرئيسي","الطاقة الكهربائية في الشبكة العامة","طاقة البطاريات الاحتياطية فقط","لا يوجد شيء اسمه طاقة متبقية"],
      correct: 0,
      feedback_correct: "✓ صحيح! الطاقة المتبقية هي الطاقة التي تبقى مخزنة في النظام مثل الضغط أو الحرارة أو الشحنة.",
      feedback_wrong: "✗ خطأ! الطاقة المتبقية هي الطاقة التي تبقى في النظام حتى بعد فصل المصدر الرئيسي."
    },
    {
      rule: "01 — عزل الطاقة",
      q: "أي من التالي يُعتبر تصرفاً خاطئاً عند عزل الطاقة؟",
      options: ["اختبار المعدات للتأكد من عدم وجود طاقة","وضع القفل الشخصي على نقطة العزل","الاعتماد على شخص آخر لعزل الطاقة دون التحقق بنفسك","تحديد جميع مصادر الطاقة قبل العمل"],
      correct: 2,
      feedback_correct: "✓ صحيح! يجب عليك دائماً التحقق بنفسك من العزل وعدم الاعتماد على الآخرين فقط.",
      feedback_wrong: "✗ خطأ! الاعتماد على شخص آخر دون التحقق بنفسك هو تصرف خاطئ وخطير."
    },
    {
      rule: "01 — عزل الطاقة",
      q: "متى يجب التحقق من عدم تسرب أو وجود أي طاقة متبقية؟",
      options: ["بعد الانتهاء من العمل فقط","فقط عند العمل على معدات كهربائية","قبل بدء العمل وبعد عزل جميع مصادر الطاقة","ليس ضرورياً إذا تم وضع الأقفال"],
      correct: 2,
      feedback_correct: "✓ صحيح! يجب التحقق من عدم وجود طاقة متبقية قبل بدء العمل وبعد إتمام العزل.",
      feedback_wrong: "✗ خطأ! يجب التحقق من عدم وجود طاقة متبقية قبل بدء العمل وبعد عزل جميع المصادر."
    },
    {
      rule: "01 — عزل الطاقة",
      q: "أي من هذه المصادر يجب تحديدها عند عزل الطاقة؟",
      options: ["الكهرباء فقط","جميع مصادر الطاقة: كهربائية، ميكانيكية، هيدروليكية، حرارية، وغيرها","الطاقة الكهربائية والميكانيكية فقط","المصادر التي يحددها المشرف فقط"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب تحديد جميع مصادر الطاقة بدون استثناء.",
      feedback_wrong: "✗ خطأ! يجب تحديد جميع مصادر الطاقة بما فيها الكهربائية والميكانيكية والهيدروليكية والحرارية."
    },
    {
      rule: "01 — عزل الطاقة",
      q: "ما الهدف من وضع البطاقات التحذيرية على نقاط العزل؟",
      options: ["لتزيين المعدات وجعلها مميزة","لتحذير الآخرين من إعادة تشغيل الطاقة أثناء العمل","لتسجيل وقت بدء العمل فقط","ليست ضرورية إذا كان القفل موجوداً"],
      correct: 1,
      feedback_correct: "✓ صحيح! البطاقات التحذيرية تحذر الآخرين من إعادة تشغيل الطاقة وتحمي العاملين.",
      feedback_wrong: "✗ خطأ! الهدف من البطاقات التحذيرية هو تحذير الآخرين من إعادة تشغيل الطاقة أثناء العمل."
    },
    {
      rule: "01 — عزل الطاقة",
      q: "أي من التالي يُعتبر من الممارسات الصحيحة لعزل الطاقة؟",
      options: ["فصل مفتاح الطاقة الرئيسي فقط والبدء بالعمل","عزل الطاقة ثم وضع الأقفال والبطاقات واختبار عدم وجود طاقة متبقية","طلب من شخص آخر أن يمسك المفتاح بيده","العمل بسرعة قبل أن يعيد أحد تشغيل الطاقة"],
      correct: 1,
      feedback_correct: "✓ صحيح! الممارسة الصحيحة تشمل العزل ثم القفل والبطاقة ثم اختبار عدم وجود طاقة.",
      feedback_wrong: "✗ خطأ! الممارسة الصحيحة هي: عزل الطاقة → وضع الأقفال والبطاقات → اختبار عدم وجود طاقة متبقية."
    }
  ];

  var rule2Questions = [
    {
      rule: "02 — تصريح العمل",
      q: "ما أول شيء يجب التأكد منه قبل البدء بأي عمل يتطلب تصريحاً؟",
      options: ["البدء بالعمل ثم استخراج التصريح لاحقاً","التأكد مما إذا كان التصريح مطلوباً لهذا العمل","سؤال الزملاء عن رأيهم","الاعتماد على خبرتك السابقة بدون تصريح"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب أولاً التأكد مما إذا كان التصريح مطلوباً قبل أي عمل.",
      feedback_wrong: "✗ خطأ! الخطوة الأولى هي التأكد مما إذا كان التصريح مطلوباً لهذا العمل."
    },
    {
      rule: "02 — تصريح العمل",
      q: "من يحق له تنفيذ العمل الذي يتطلب تصريحاً؟",
      options: ["أي شخص متواجد في الموقع","شخص مخول ومؤهل لأداء هذا العمل فقط","المشرف فقط حتى لو لم يكن مؤهلاً تقنياً","من لديه أقدمية في العمل"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب أن يكون العامل مخولاً ومؤهلاً لأداء العمل المطلوب.",
      feedback_wrong: "✗ خطأ! يجب أن يكون الشخص مخولاً ومؤهلاً لأداء العمل."
    },
    {
      rule: "02 — تصريح العمل",
      q: "ماذا يجب أن تفعل إذا لم تفهم محتوى تصريح العمل؟",
      options: ["تبدأ العمل وتسأل لاحقاً","تتوقف وتطلب شرح التصريح قبل البدء","تتجاهل الأجزاء غير المفهومة","توقّع التصريح وتبدأ العمل فوراً"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب أن تفهم التصريح بالكامل قبل البدء بأي عمل.",
      feedback_wrong: "✗ خطأ! يجب التوقف وطلب شرح التصريح — لا تبدأ العمل بدون فهم كامل."
    },
    {
      rule: "02 — تصريح العمل",
      q: "قبل البدء بالعمل، ماذا يجب التأكد منه بخصوص المخاطر؟",
      options: ["لا حاجة للتحقق إذا كان التصريح موجوداً","التأكد من أن المخاطر تم التحكم بها وأن العمل يمكن البدء به بشكل آمن","الاكتفاء بارتداء معدات الحماية فقط","الاعتماد على تقييم المخاطر السابق بدون مراجعة"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التأكد من السيطرة على المخاطر وأن العمل آمن قبل البدء.",
      feedback_wrong: "✗ خطأ! يجب التأكد من أن المخاطر تم التحكم بها وأن العمل يمكن البدء به بأمان."
    },
    {
      rule: "02 — تصريح العمل",
      q: "إذا تغيرت ظروف العمل أثناء التنفيذ، ما التصرف الصحيح؟",
      options: ["الاستمرار في العمل دون توقف","التوقف وإعادة تقييم الوضع","إبلاغ زميلك فقط ومتابعة العمل","الانتظار حتى نهاية الوردية لإبلاغ المشرف"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التوقف فوراً وإعادة تقييم الوضع عند تغير الظروف.",
      feedback_wrong: "✗ خطأ! يجب التوقف وإعادة التقييم فوراً إذا تغيرت ظروف العمل."
    },
    {
      rule: "02 — تصريح العمل",
      q: "ما المطلوب عند الانتهاء من العمل الذي يتطلب تصريحاً؟",
      options: ["ترك الموقع فوراً بعد إنهاء المهمة","تطبيق جميع متطلبات إنهاء تصريح العمل وإغلاقه رسمياً","إبلاغ زميل شفهياً بأنك انتهيت","لا حاجة لأي إجراء إضافي بعد الانتهاء"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب تطبيق جميع متطلبات إنهاء التصريح وإغلاقه رسمياً.",
      feedback_wrong: "✗ خطأ! يجب تطبيق جميع متطلبات تصريح العمل بما فيها إنهاء التصريح وإغلاقه."
    },
    {
      rule: "02 — تصريح العمل",
      q: "أي من التالي يُعتبر تصرفاً خاطئاً بخصوص تصريح العمل؟",
      options: ["مراجعة التصريح قبل بدء العمل","التأكد من صلاحية التصريح","العمل بتصريح منتهي الصلاحية لأن المهمة مستعجلة","إعادة التقييم عند تغير الظروف"],
      correct: 2,
      feedback_correct: "✓ صحيح! لا يجوز أبداً العمل بتصريح منتهي الصلاحية مهما كانت الظروف.",
      feedback_wrong: "✗ خطأ! العمل بتصريح منتهي الصلاحية خطأ جسيم حتى لو كانت المهمة مستعجلة."
    },
    {
      rule: "02 — تصريح العمل",
      q: "لماذا يجب أن يفهم العامل تصريح العمل بالكامل؟",
      options: ["لأنه مطلوب للتوقيع فقط","لمعرفة المخاطر وإجراءات السلامة والحدود المسموح بها للعمل","ليس ضرورياً إذا كان المشرف حاضراً","لأغراض التوثيق فقط"],
      correct: 1,
      feedback_correct: "✓ صحيح! فهم التصريح يضمن معرفة المخاطر وإجراءات السلامة وحدود العمل.",
      feedback_wrong: "✗ خطأ! فهم التصريح ضروري لمعرفة المخاطر وإجراءات السلامة والحدود المسموح بها."
    }
  ];

  var rule3Questions = [
    {
      rule: "03 — معدات الحماية الشخصية",
      q: "ما المبدأ الأساسي لاستخدام معدات الحماية الشخصية (PPE)؟",
      options: ["ارتداء أي معدات متاحة بغض النظر عن المهمة","ارتداء واستخدام معدات الحماية الشخصية المناسبة لهذه المهمة","ارتداء معدات الحماية فقط عند وجود المشرف","معدات الحماية اختيارية للعمال ذوي الخبرة"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب ارتداء واستخدام معدات الحماية المناسبة تحديداً للمهمة المطلوبة.",
      feedback_wrong: "✗ خطأ! المبدأ الأساسي هو ارتداء واستخدام معدات الحماية الشخصية المناسبة لهذه المهمة بالتحديد."
    },
    {
      rule: "03 — معدات الحماية الشخصية",
      q: "كيف تعرف ما هي معدات الحماية الإضافية المطلوبة للعمل؟",
      options: ["تسأل زملاءك فقط","تعتمد على خبرتك السابقة فقط","تراجع تصريح العمل أو تعليمات العمل لمعرفة المعدات المطلوبة","تختار المعدات التي تراها مناسبة بنفسك"],
      correct: 2,
      feedback_correct: "✓ صحيح! يجب معرفة واستخدام معدات الحماية الإضافية كما هو منصوص عليه في تصريح العمل أو تعليمات العمل.",
      feedback_wrong: "✗ خطأ! يجب مراجعة تصريح العمل أو تعليمات العمل لمعرفة معدات الحماية المطلوبة."
    },
    {
      rule: "03 — معدات الحماية الشخصية",
      q: "ما أهمية اللوحات الإرشادية والتعليمات في موقع العمل بخصوص معدات الحماية؟",
      options: ["هي للديكور فقط ولا تتعلق بالسلامة","تحدد معدات الوقاية الشخصية المطلوبة في تلك المنطقة","مخصصة للزوار فقط وليس للعمال","يمكن تجاهلها إذا كنت ترتدي معدات أخرى"],
      correct: 1,
      feedback_correct: "✓ صحيح! اللوحات الإرشادية تحدد معدات الوقاية الشخصية المطلوبة ويجب اتباعها.",
      feedback_wrong: "✗ خطأ! اللوحات الإرشادية تحدد معدات الوقاية المطلوبة في المنطقة ويجب الالتزام بها."
    },
    {
      rule: "03 — معدات الحماية الشخصية",
      q: "كم مرة يجب فحص حالة معدات الوقاية الشخصية الخاصة بك؟",
      options: ["مرة واحدة عند استلامها فقط","بانتظام وبشكل دوري","فقط عند وقوع حادث","مرة كل سنة"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التحقق بانتظام من حالة معدات الوقاية الشخصية لضمان سلامتها وفعاليتها.",
      feedback_wrong: "✗ خطأ! يجب فحص معدات الوقاية الشخصية بانتظام وليس فقط عند استلامها أو عند وقوع حادث."
    },
    {
      rule: "03 — معدات الحماية الشخصية",
      q: "ماذا يجب أن تفعل إذا رأيت زميلاً لا يرتدي معدات الوقاية المحددة له؟",
      options: ["تتجاهل الأمر لأنه مسؤوليته الشخصية","تحمّله المسؤولية وتنبّهه لارتداء المعدات المطلوبة","تبلغ عنه سراً بدون تنبيهه","تنتظر حتى يلاحظ المشرف"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب تحميل الآخرين المسؤولية وتنبيههم عند عدم ارتداء معدات الوقاية المحددة لهم.",
      feedback_wrong: "✗ خطأ! من مسؤوليتك تنبيه زملائك وتحميلهم المسؤولية عند عدم ارتداء معدات الوقاية."
    },
    {
      rule: "03 — معدات الحماية الشخصية",
      q: "أي من التالي يُعتبر تصرفاً خاطئاً بخصوص معدات الحماية الشخصية؟",
      options: ["فحص المعدات قبل كل استخدام","ارتداء المعدات المحددة في تصريح العمل","استخدام معدات حماية تالفة لأنه لا يوجد بديل متاح","اتباع اللوحات الإرشادية في الموقع"],
      correct: 2,
      feedback_correct: "✓ صحيح! لا يجوز أبداً استخدام معدات حماية تالفة مهما كانت الظروف.",
      feedback_wrong: "✗ خطأ! استخدام معدات حماية تالفة خطأ جسيم حتى لو لم يكن هناك بديل — يجب التوقف عن العمل."
    },
    {
      rule: "03 — معدات الحماية الشخصية",
      q: "متى يجب ارتداء معدات الحماية الشخصية الإضافية المنصوص عليها في تصريح العمل؟",
      options: ["فقط عند الشعور بالخطر","طوال فترة تنفيذ العمل كما هو محدد في التصريح","في بداية العمل فقط ثم يمكن خلعها","عند وجود المشرف فقط"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب ارتداء معدات الحماية الإضافية طوال فترة العمل كما هو منصوص عليه.",
      feedback_wrong: "✗ خطأ! يجب ارتداء معدات الحماية الإضافية طوال فترة تنفيذ العمل وليس في أوقات محددة فقط."
    },
    {
      rule: "03 — معدات الحماية الشخصية",
      q: "ما التصرف الصحيح إذا اكتشفت أن معدات الحماية الخاصة بك بها عيب أو تلف؟",
      options: ["الاستمرار في استخدامها حتى نهاية الوردية","التوقف عن العمل واستبدالها فوراً بمعدات سليمة","إصلاحها بنفسك ومتابعة العمل","تجاهل العيب إذا كان صغيراً"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التوقف فوراً واستبدال المعدات التالفة بمعدات سليمة قبل متابعة العمل.",
      feedback_wrong: "✗ خطأ! يجب التوقف عن العمل واستبدال المعدات التالفة فوراً — سلامتك أولاً."
    }
  ];

  var rule4Questions = [
    {
      rule: "04 — العمل على المرتفعات",
      q: "ما المبدأ الأساسي عند العمل على المرتفعات؟",
      options: ["العمل بسرعة لتقليل وقت التعرض للخطر","احمِ نفسك من السقوط عند العمل على المرتفعات","الاعتماد على التوازن الشخصي بدون معدات","العمل فقط في الأيام غير العاصفة"],
      correct: 1,
      feedback_correct: "✓ صحيح! المبدأ الأساسي هو حماية نفسك من السقوط عند العمل على المرتفعات.",
      feedback_wrong: "✗ خطأ! المبدأ الأساسي هو حماية نفسك من السقوط باستخدام معدات الحماية المناسبة."
    },
    {
      rule: "04 — العمل على المرتفعات",
      q: "متى يجب فحص معدات الحماية من السقوط؟",
      options: ["مرة واحدة في الشهر","قبل كل استخدام","فقط عند شراء معدات جديدة","بعد وقوع حادث سقوط فقط"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب فحص معدات الحماية من السقوط قبل كل استخدام للتأكد من سلامتها.",
      feedback_wrong: "✗ خطأ! يجب فحص معدات الحماية من السقوط قبل كل استخدام وليس بشكل دوري فقط."
    },
    {
      rule: "04 — العمل على المرتفعات",
      q: "ماذا يجب فعله بخصوص الأدوات ومواد العمل عند العمل على المرتفعات؟",
      options: ["وضعها على حافة منطقة العمل لسهولة الوصول","تأمينها ومنعها من السقوط","حملها باليد فقط أثناء الصعود","تركها على الأرض والنزول عند الحاجة إليها"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب تأمين الأدوات ومواد العمل لمنع سقوطها وحماية من هم أسفل منطقة العمل.",
      feedback_wrong: "✗ خطأ! يجب تأمين جميع الأدوات ومواد العمل لمنع سقوطها."
    },
    {
      rule: "04 — العمل على المرتفعات",
      q: "ما المقصود بالربط ١٠٠٪ عند العمل على المرتفعات؟",
      options: ["ربط الأدوات فقط بنسبة ١٠٠٪","أن تكون مربوطاً بنقاط ربط معتمدة في جميع الأوقات خارج المنطقة المحمية","ربط نفسك ١٠٠٪ من وقت الوردية","استخدام حبل واحد فقط طوال العمل"],
      correct: 1,
      feedback_correct: "✓ صحيح! الربط ١٠٠٪ يعني أن تكون مربوطاً بنقاط الربط المعتمدة في جميع الأوقات خارج المنطقة المحمية.",
      feedback_wrong: "✗ خطأ! الربط ١٠٠٪ يعني البقاء مربوطاً بنقاط الربط المعتمدة طوال فترة التواجد خارج المنطقة المحمية."
    },
    {
      rule: "04 — العمل على المرتفعات",
      q: "أي من التالي يُعتبر تصرفاً خاطئاً عند العمل على المرتفعات؟",
      options: ["فحص حزام الأمان قبل الاستخدام","الربط بنقطة ربط معتمدة","فك الربط أثناء الانتقال بين نقطتين بدون حماية بديلة","تأمين الأدوات بحبال لمنع سقوطها"],
      correct: 2,
      feedback_correct: "✓ صحيح! فك الربط أثناء الانتقال بدون حماية بديلة ينتهك قاعدة الربط ١٠٠٪ ويعرض حياتك للخطر.",
      feedback_wrong: "✗ خطأ! فك الربط أثناء الانتقال بدون حماية بديلة هو تصرف خاطئ وخطير جداً."
    },
    {
      rule: "04 — العمل على المرتفعات",
      q: "ما هي نقاط الربط المعتمدة؟",
      options: ["أي نقطة ثابتة يمكن الربط بها","نقاط محددة ومعتمدة رسمياً تتحمل قوة السقوط","السلالم والأنابيب القريبة","الحواجز والسياجات المحيطة بمنطقة العمل"],
      correct: 1,
      feedback_correct: "✓ صحيح! نقاط الربط المعتمدة هي نقاط محددة ومعتمدة رسمياً مصممة لتحمل قوة السقوط.",
      feedback_wrong: "✗ خطأ! يجب استخدام نقاط ربط معتمدة رسمياً فقط وليس أي نقطة ثابتة."
    },
    {
      rule: "04 — العمل على المرتفعات",
      q: "ماذا يجب أن تفعل إذا وجدت أن حزام الأمان به تلف أثناء الفحص؟",
      options: ["استخدامه مع الحذر الإضافي","إصلاحه بنفسك واستخدامه","عدم استخدامه والإبلاغ فوراً واستبداله","تجاهل التلف إذا كان بسيطاً"],
      correct: 2,
      feedback_correct: "✓ صحيح! يجب عدم استخدام أي معدات حماية من السقوط تالفة والإبلاغ عنها واستبدالها فوراً.",
      feedback_wrong: "✗ خطأ! أي تلف في معدات الحماية من السقوط يعني عدم استخدامها — يجب الإبلاغ والاستبدال فوراً."
    },
    {
      rule: "04 — العمل على المرتفعات",
      q: "لماذا يجب تأمين الأدوات عند العمل على المرتفعات؟",
      options: ["لمنع سرقتها فقط","لمنع سقوطها وإصابة الأشخاص أسفل منطقة العمل","لتسهيل الوصول إليها فقط","ليس ضرورياً إذا كانت المنطقة السفلية مغلقة"],
      correct: 1,
      feedback_correct: "✓ صحيح! تأمين الأدوات يمنع سقوطها ويحمي الأشخاص المتواجدين أسفل منطقة العمل.",
      feedback_wrong: "✗ خطأ! تأمين الأدوات ضروري لمنع سقوطها وحماية الأشخاص في الأسفل."
    }
  ];

  var rule5Questions = [
    {
      rule: "05 — تجاوز وسائل تحكم السلامة",
      q: "ما المبدأ الأساسي بخصوص تجاوز أو تعطيل وسائل تحكم السلامة؟",
      options: ["يمكن تجاوزها في حالات الطوارئ بدون إذن","يجب الحصول على إذن قبل تجاوز أو تعطيل وسائل تحكم السلامة","يمكن تعطيلها إذا كانت تعيق سرعة العمل","يحق للعمال ذوي الخبرة تجاوزها بدون إذن"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب دائماً الحصول على إذن قبل تجاوز أو تعطيل أي وسيلة تحكم بالسلامة.",
      feedback_wrong: "✗ خطأ! المبدأ الأساسي هو الحصول على إذن قبل أي تجاوز أو تعطيل لوسائل تحكم السلامة."
    },
    {
      rule: "05 — تجاوز وسائل تحكم السلامة",
      q: "ماذا يجب أن تفعل قبل البدء بمهمتك فيما يتعلق بمعدات وإجراءات السلامة؟",
      options: ["البدء مباشرة والتعلم أثناء العمل","فهم واستخدام معدات وإجراءات السلامة الضرورية التي تنطبق على مهمتك","الاكتفاء بما تعرفه من خبرتك السابقة","سؤال زميل عن الإجراءات بشكل سريع"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب فهم واستخدام جميع معدات وإجراءات السلامة التي تنطبق على مهمتك.",
      feedback_wrong: "✗ خطأ! يجب فهم واستخدام معدات وإجراءات السلامة الضرورية قبل البدء بالمهمة."
    },
    {
      rule: "05 — تجاوز وسائل تحكم السلامة",
      q: "أي من الحالات التالية تتطلب الحصول على إذن مسبق؟",
      options: ["ارتداء معدات الحماية الشخصية","تعطيل أو تجاوز معدات أو وسائل التحكم بالسلامة","فحص معدات السلامة","الإبلاغ عن خلل في معدات السلامة"],
      correct: 1,
      feedback_correct: "✓ صحيح! تعطيل أو تجاوز معدات أو وسائل التحكم بالسلامة يتطلب إذناً مسبقاً.",
      feedback_wrong: "✗ خطأ! تعطيل أو تجاوز أي وسيلة تحكم بالسلامة يتطلب الحصول على إذن مسبق."
    },
    {
      rule: "05 — تجاوز وسائل تحكم السلامة",
      q: "ماذا يجب أن تفعل إذا احتجت للانحراف عن الإجراءات المتبعة؟",
      options: ["الانحراف إذا كنت واثقاً من خبرتك","الحصول على إذن قبل الانحراف عن الإجراءات المتبعة","إبلاغ زميلك فقط والمتابعة","تسجيل الانحراف بعد الانتهاء من العمل"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب الحصول على إذن مسبق قبل أي انحراف عن الإجراءات المتبعة.",
      feedback_wrong: "✗ خطأ! أي انحراف عن الإجراءات المتبعة يتطلب الحصول على إذن مسبق."
    },
    {
      rule: "05 — تجاوز وسائل تحكم السلامة",
      q: "هل يجوز تجاوز الحواجز الأمنية بدون إذن؟",
      options: ["نعم، إذا كانت المنطقة تبدو آمنة","نعم، للعمال المعتمدين فقط","لا، يجب الحصول على إذن قبل تجاوز أي حاجز","نعم، في حالة الاستعجال لإنجاز العمل"],
      correct: 2,
      feedback_correct: "✓ صحيح! لا يجوز تجاوز أي حاجز أمني بدون الحصول على إذن مسبق.",
      feedback_wrong: "✗ خطأ! تجاوز الحواجز يتطلب الحصول على إذن — لا استثناءات."
    },
    {
      rule: "05 — تجاوز وسائل تحكم السلامة",
      q: "أي من التالي يُعتبر تصرفاً خاطئاً بخصوص وسائل تحكم السلامة؟",
      options: ["فهم إجراءات السلامة قبل بدء العمل","طلب إذن لتجاوز حاجز أمني","تعطيل جهاز إنذار لأنه يصدر ضوضاء مزعجة بدون إذن","الإبلاغ عن وسيلة سلامة معطلة"],
      correct: 2,
      feedback_correct: "✓ صحيح! تعطيل جهاز إنذار بدون إذن هو انتهاك خطير لقواعد السلامة.",
      feedback_wrong: "✗ خطأ! تعطيل أي وسيلة سلامة بدون إذن مسبق — حتى لو كانت مزعجة — هو تصرف خاطئ."
    },
    {
      rule: "05 — تجاوز وسائل تحكم السلامة",
      q: "ما الهدف من وجود وسائل تحكم السلامة في موقع العمل؟",
      options: ["لتعقيد العمل وإبطائه","لحماية العمال والمنشآت من المخاطر والحوادث","لأغراض التوثيق والتفتيش فقط","لتحديد مسؤولية العمال في حالة الحوادث"],
      correct: 1,
      feedback_correct: "✓ صحيح! وسائل تحكم السلامة موجودة لحماية العمال والمنشآت من المخاطر.",
      feedback_wrong: "✗ خطأ! الهدف الأساسي من وسائل تحكم السلامة هو حماية العمال والمنشآت من المخاطر والحوادث."
    },
    {
      rule: "05 — تجاوز وسائل تحكم السلامة",
      q: "إذا وجدت أن وسيلة تحكم بالسلامة معطلة، ماذا يجب أن تفعل؟",
      options: ["تتجاهل الأمر وتستمر بالعمل","تحاول إصلاحها بنفسك بدون تأهيل","تبلغ فوراً وتتوقف عن العمل حتى يتم إصلاحها","تستمر بالعمل مع أخذ احتياطات إضافية"],
      correct: 2,
      feedback_correct: "✓ صحيح! يجب الإبلاغ فوراً عن أي وسيلة سلامة معطلة والتوقف حتى يتم إصلاحها.",
      feedback_wrong: "✗ خطأ! يجب الإبلاغ فوراً والتوقف عن العمل حتى يتم إصلاح وسيلة السلامة المعطلة."
    }
  ];

  var rule6Questions = [
    {
      rule: "06 — العمل الساخن",
      q: "ما المبدأ الأساسي عند القيام بالعمل الساخن؟",
      options: ["إنجاز العمل بأسرع وقت ممكن","السيطرة على المواد القابلة للاشتعال ومصادر الاشتعال","ارتداء ملابس مقاومة للحرارة فقط","العمل في مناطق مفتوحة فقط"],
      correct: 1,
      feedback_correct: "✓ صحيح! المبدأ الأساسي هو السيطرة على المواد القابلة للاشتعال ومصادر الاشتعال.",
      feedback_wrong: "✗ خطأ! يجب السيطرة على المواد القابلة للاشتعال ومصادر الاشتعال قبل وأثناء العمل الساخن."
    },
    {
      rule: "06 — العمل الساخن",
      q: "ما أول إجراء يجب اتخاذه بخصوص مصادر الاشتعال؟",
      options: ["تجاهلها إذا كانت بعيدة","تحديد مصادر الاشتعال والتحكم بها","الاكتفاء بوجود طفاية حريق قريبة","إبلاغ المشرف فقط بدون اتخاذ إجراء"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب تحديد جميع مصادر الاشتعال والتحكم بها قبل بدء العمل.",
      feedback_wrong: "✗ خطأ! الخطوة الأولى هي تحديد مصادر الاشتعال والتحكم بها."
    },
    {
      rule: "06 — العمل الساخن",
      q: "قبل البدء بأي عمل ساخن، ماذا يجب التأكد منه بخصوص المواد القابلة للاشتعال؟",
      options: ["تغطيتها بقماش فقط","التأكد من إزالة المواد القابلة للاشتعال أو عزلها","ترك المواد في مكانها مع مراقبتها","نقلها لمسافة متر واحد فقط"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب إزالة المواد القابلة للاشتعال أو عزلها قبل البدء بالعمل الساخن.",
      feedback_wrong: "✗ خطأ! يجب التأكد من إزالة جميع المواد القابلة للاشتعال أو عزلها تماماً."
    },
    {
      rule: "06 — العمل الساخن",
      q: "هل يمكن البدء بالعمل الساخن بدون تفويض؟",
      options: ["نعم، إذا كنت مؤهلاً للعمل","نعم، في الحالات البسيطة فقط","لا، يجب الحصول على التفويض قبل البدء","نعم، إذا كان المشرف غير متاحاً"],
      correct: 2,
      feedback_correct: "✓ صحيح! يجب الحصول على التفويض المناسب قبل البدء بأي عمل ساخن.",
      feedback_wrong: "✗ خطأ! لا يجوز البدء بأي عمل ساخن بدون الحصول على التفويض."
    },
    {
      rule: "06 — العمل الساخن",
      q: "عند العمل الساخن في منطقة خطرة، ما الذي يجب التأكد من اكتماله؟",
      options: ["توفر طفاية حريق فقط","اكتمال اختبار الغازات","تواجد شخصين على الأقل","إغلاق جميع الأبواب"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التأكد من اكتمال اختبار الغازات قبل البدء بالعمل الساخن في منطقة خطرة.",
      feedback_wrong: "✗ خطأ! اكتمال اختبار الغازات شرط أساسي قبل العمل الساخن في المناطق الخطرة."
    },
    {
      rule: "06 — العمل الساخن",
      q: "ما المطلوب بخصوص مراقبة الغازات أثناء العمل الساخن في منطقة خطرة؟",
      options: ["اختبار الغازات مرة واحدة في بداية العمل فقط","مراقبة الغازات بشكل دوري ومستمر","الاختبار فقط إذا شعرت برائحة غريبة","ليس ضرورياً إذا تم الاختبار الأولي"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب مراقبة الغازات بشكل دوري ومستمر أثناء العمل الساخن في المناطق الخطرة.",
      feedback_wrong: "✗ خطأ! يجب مراقبة الغازات بشكل دوري وليس مرة واحدة فقط."
    },
    {
      rule: "06 — العمل الساخن",
      q: "أي من التالي يُعتبر تصرفاً خاطئاً عند العمل الساخن؟",
      options: ["إزالة المواد القابلة للاشتعال من المنطقة","الحصول على تفويض العمل الساخن","البدء باللحام بجانب مواد قابلة للاشتعال لأن العمل مستعجل","إجراء اختبار الغازات قبل البدء"],
      correct: 2,
      feedback_correct: "✓ صحيح! البدء باللحام بجانب مواد قابلة للاشتعال خطأ جسيم مهما كان الاستعجال.",
      feedback_wrong: "✗ خطأ! العمل بجانب مواد قابلة للاشتعال بدون إزالتها أو عزلها هو تصرف خاطئ وخطير."
    },
    {
      rule: "06 — العمل الساخن",
      q: "ماذا يجب فعله إذا أظهر اختبار الغازات وجود غازات قابلة للاشتعال في المنطقة؟",
      options: ["البدء بالعمل مع فتح التهوية","تقليل مدة العمل الساخن فقط","عدم البدء بالعمل الساخن حتى تصبح المنطقة آمنة","ارتداء قناع غاز والبدء بالعمل"],
      correct: 2,
      feedback_correct: "✓ صحيح! يجب عدم البدء بالعمل الساخن حتى تكون نتائج اختبار الغازات آمنة.",
      feedback_wrong: "✗ خطأ! يجب عدم البدء بالعمل الساخن إطلاقاً حتى تصبح المنطقة آمنة من الغازات القابلة للاشتعال."
    }
  ];

  var rule7Questions = [
    {
      rule: "07 — العمل في الأماكن المحصورة",
      q: "ما المبدأ الأساسي قبل دخول مكان محصور؟",
      options: ["الدخول بسرعة لإنجاز المهمة","الحصول على إذن قبل دخول أي مكان محصور","الدخول إذا كان المكان يبدو آمناً","الدخول فقط مع زميل بدون إذن رسمي"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب الحصول على إذن رسمي قبل دخول أي مكان محصور.",
      feedback_wrong: "✗ خطأ! لا يجوز دخول أي مكان محصور بدون الحصول على إذن مسبق."
    },
    {
      rule: "07 — العمل في الأماكن المحصورة",
      q: "ما الذي يجب التأكد منه بخصوص مصادر الطاقة قبل الدخول لمكان محصور؟",
      options: ["أنها مخفضة للحد الأدنى","أن مصادر الطاقة معزولة تماماً","أنها تعمل بشكل طبيعي","أنها متصلة بمصدر احتياطي"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التأكد من أن جميع مصادر الطاقة معزولة قبل دخول المكان المحصور.",
      feedback_wrong: "✗ خطأ! يجب أن تكون مصادر الطاقة معزولة تماماً وليس فقط مخفضة."
    },
    {
      rule: "07 — العمل في الأماكن المحصورة",
      q: "ماذا يجب التأكد منه بخصوص المحيط الجوي داخل المكان المحصور؟",
      options: ["أنه يبدو طبيعياً بالنظر","أن المحيط الجوي قد تم اختباره ومراقبته","أن التهوية الطبيعية كافية","أنه لا توجد روائح غريبة"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب اختبار ومراقبة المحيط الجوي — لا يمكن الاعتماد على الحواس فقط.",
      feedback_wrong: "✗ خطأ! يجب اختبار المحيط الجوي بأجهزة متخصصة ومراقبته — العديد من الغازات الخطرة لا رائحة لها."
    },
    {
      rule: "07 — العمل في الأماكن المحصورة",
      q: "ما الإجراء الصحيح بخصوص جهاز التنفس عند العمل في مكان محصور؟",
      options: ["ليس ضرورياً إذا كانت التهوية جيدة","التحقق من جهاز التنفس الخاص بي واستخدامه عند الحاجة","حمله فقط بدون فحص","استخدامه فقط في حالات الطوارئ"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التحقق من جهاز التنفس واستخدامه عند الحاجة لضمان سلامتك.",
      feedback_wrong: "✗ خطأ! يجب التحقق من جهاز التنفس الخاص بك واستخدامه عند الحاجة."
    },
    {
      rule: "07 — العمل في الأماكن المحصورة",
      q: "هل يجوز العمل في مكان محصور بدون مراقب للعمل بالموقع؟",
      options: ["نعم، إذا كانت المهمة قصيرة","نعم، إذا كان هناك جهاز اتصال","لا، يجب وجود مراقب للعمل بالموقع طوال فترة العمل","نعم، إذا كان العامل ذا خبرة"],
      correct: 2,
      feedback_correct: "✓ صحيح! يجب أن يكون هناك مراقب للعمل متواجد بالموقع طوال فترة العمل في المكان المحصور.",
      feedback_wrong: "✗ خطأ! وجود مراقب للعمل بالموقع طوال فترة العمل شرط أساسي لا يمكن تجاوزه."
    },
    {
      rule: "07 — العمل في الأماكن المحصورة",
      q: "ما المطلوب بخصوص خطة الإنقاذ عند العمل في الأماكن المحصورة؟",
      options: ["وضع خطة بعد الانتهاء من العمل","التأكد من وجود خطة إنقاذ وجاهزية تنفيذها قبل البدء","الاعتماد على فريق الطوارئ العام فقط","ليست ضرورية إذا كان المكان صغيراً"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التأكد من وجود خطة إنقاذ جاهزة للتنفيذ قبل البدء بالعمل.",
      feedback_wrong: "✗ خطأ! يجب أن تكون خطة الإنقاذ موجودة وجاهزة للتنفيذ قبل أي عمل في مكان محصور."
    },
    {
      rule: "07 — العمل في الأماكن المحصورة",
      q: "أي من التالي يُعتبر تصرفاً خاطئاً عند العمل في الأماكن المحصورة؟",
      options: ["اختبار المحيط الجوي قبل الدخول","وجود مراقب بالموقع","الدخول لإنقاذ زميل بدون جهاز تنفس أو خطة إنقاذ","الحصول على تصريح عمل"],
      correct: 2,
      feedback_correct: "✓ صحيح! الدخول لإنقاذ شخص بدون معدات مناسبة قد يؤدي لوقوع ضحايا إضافية — اتبع خطة الإنقاذ.",
      feedback_wrong: "✗ خطأ! محاولة الإنقاذ بدون معدات مناسبة وخطة هو أخطر تصرف ممكن في الأماكن المحصورة."
    },
    {
      rule: "07 — العمل في الأماكن المحصورة",
      q: "لماذا يجب الحصول على تصريح للعمل في الأماكن المحصورة؟",
      options: ["لأغراض التوثيق فقط","لضمان اتخاذ جميع احتياطات السلامة والتحقق من جاهزية المكان","لأن المشرف يطلب ذلك فقط","ليس ضرورياً إذا كان العمل روتينياً"],
      correct: 1,
      feedback_correct: "✓ صحيح! التصريح يضمن اتخاذ جميع الاحتياطات والتحقق من أن المكان آمن للدخول.",
      feedback_wrong: "✗ خطأ! التصريح يضمن التحقق من جميع إجراءات السلامة قبل الدخول."
    }
  ];

  var rule8Questions = [
    {
      rule: "08 — العمل في منطقة الخطر",
      q: "ما المبدأ الأساسي للعمل في منطقة الخطر؟",
      options: ["العمل بحذر دون اتخاذ إجراءات إضافية","أبقِ نفسك والآخرين بعيداً عن منطقة الخطر","الاعتماد على معدات الحماية فقط","العمل بسرعة لتقليل التعرض للخطر"],
      correct: 1,
      feedback_correct: "✓ صحيح! المبدأ الأساسي هو إبقاء نفسك والآخرين بعيداً عن منطقة الخطر.",
      feedback_wrong: "✗ خطأ! يجب إبقاء نفسك والآخرين بعيداً عن منطقة الخطر في جميع الأوقات."
    },
    {
      rule: "08 — العمل في منطقة الخطر",
      q: "أي من المخاطر التالية يجب أن تتمركز بعيداً عنها؟",
      options: ["الأجسام المتحركة والمركبات فقط","الأجسام المتحركة، المركبات، انطلاق الضغط المحبوس، والأجسام المتساقطة","المركبات فقط","الأجسام المتساقطة فقط"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب تجنب جميع هذه المخاطر: الأجسام المتحركة، المركبات، انطلاق الضغط المحبوس، والأجسام المتساقطة.",
      feedback_wrong: "✗ خطأ! يجب التمركز بعيداً عن جميع المخاطر بما فيها الأجسام المتحركة والمركبات والضغط المحبوس والأجسام المتساقطة."
    },
    {
      rule: "08 — العمل في منطقة الخطر",
      q: "ما الإجراء الصحيح بخصوص الحواجز ومناطق الحظر؟",
      options: ["تجاهلها إذا كانت تعيق العمل","إنشاء الحواجز ومناطق الحظر والالتزام بها","وضعها فقط عند وجود المشرف","إنشاؤها بعد الانتهاء من العمل"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب إنشاء الحواجز ومناطق الحظر والالتزام بها لحماية الجميع.",
      feedback_wrong: "✗ خطأ! يجب إنشاء الحواجز ومناطق الحظر والالتزام بها دائماً."
    },
    {
      rule: "08 — العمل في منطقة الخطر",
      q: "ماذا يجب فعله بخصوص الأجسام غير المثبتة في منطقة العمل؟",
      options: ["تركها في مكانها","اتخاذ إجراءات لتأمينها والإبلاغ عن الأجسام التي يحتمل سقوطها","نقلها بعيداً فقط إذا طلب المشرف","تغطيتها بقماش"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب تأمين الأجسام غير المثبتة والإبلاغ عن أي أجسام يحتمل سقوطها.",
      feedback_wrong: "✗ خطأ! يجب اتخاذ إجراءات فورية لتأمين الأجسام غير المثبتة والإبلاغ عنها."
    },
    {
      rule: "08 — العمل في منطقة الخطر",
      q: "ما المطلوب بخصوص الخراطيم المضغوطة قبل بدء العمل؟",
      options: ["التأكد من أنها متصلة فقط","التأكد من أن جميع الخراطيم المضغوطة مزودة بأداة فحص","فحصها مرة واحدة في الأسبوع","ليس ضرورياً فحصها"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التأكد من أن جميع الخراطيم المضغوطة مزودة بأداة فحص قبل بدء العمل.",
      feedback_wrong: "✗ خطأ! يجب التأكد من تزويد جميع الخراطيم المضغوطة بأداة فحص قبل البدء بالعمل."
    },
    {
      rule: "08 — العمل في منطقة الخطر",
      q: "لماذا يجب الابتعاد عن الضغط المحبوس في منطقة العمل؟",
      options: ["لأنه يسبب ضوضاء فقط","لأن انطلاقه المفاجئ قد يسبب إصابات خطيرة أو وفاة","لأنه يعيق حركة العمل","ليس خطيراً إذا كنت ترتدي معدات الحماية"],
      correct: 1,
      feedback_correct: "✓ صحيح! انطلاق الضغط المحبوس بشكل مفاجئ يمكن أن يسبب إصابات خطيرة أو وفاة.",
      feedback_wrong: "✗ خطأ! الضغط المحبوس خطر جسيم — انطلاقه المفاجئ قد يسبب إصابات خطيرة أو وفاة."
    },
    {
      rule: "08 — العمل في منطقة الخطر",
      q: "أي من التالي يُعتبر تصرفاً خاطئاً في منطقة الخطر؟",
      options: ["إنشاء حواجز حول منطقة العمل","الوقوف تحت حمولة معلقة بالرافعة","تأمين الأجسام غير المثبتة","فحص الخراطيم المضغوطة"],
      correct: 1,
      feedback_correct: "✓ صحيح! الوقوف تحت حمولة معلقة خطر مميت — يجب الابتعاد دائماً عن مسار الأحمال المعلقة.",
      feedback_wrong: "✗ خطأ! الوقوف تحت حمولة معلقة هو من أخطر التصرفات التي قد تؤدي للوفاة."
    },
    {
      rule: "08 — العمل في منطقة الخطر",
      q: "ماذا يجب أن تفعل إذا لاحظت عدم وجود حواجز حول منطقة عمل خطرة؟",
      options: ["الاستمرار بالعمل مع توخي الحذر","إنشاء الحواجز فوراً أو الإبلاغ عن الوضع","تنبيه الزملاء شفهياً فقط","تجاهل الأمر لأنه مسؤولية قسم السلامة"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب إنشاء الحواجز فوراً أو الإبلاغ عن الوضع لحماية الجميع.",
      feedback_wrong: "✗ خطأ! عدم وجود حواجز يعرض الجميع للخطر — يجب التصرف فوراً."
    }
  ];

  var rule9Questions = [
    {
      rule: "09 — عمليات الرفع",
      q: "ما المبدأ الأساسي لعمليات الرفع؟",
      options: ["رفع الحمولات بأسرع طريقة ممكنة","خطط لعمليات الرفع والتحكم في المنطقة","الاعتماد على خبرة المشغل فقط","البدء بالرفع ثم التخطيط لاحقاً"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التخطيط لعمليات الرفع والتحكم في المنطقة قبل البدء.",
      feedback_wrong: "✗ خطأ! المبدأ الأساسي هو التخطيط لعمليات الرفع والتحكم في المنطقة."
    },
    {
      rule: "09 — عمليات الرفع",
      q: "ماذا يجب التأكد منه قبل البدء بعملية الرفع بخصوص المعدة والحمولة؟",
      options: ["أن المعدة متوفرة فقط","أن المعدة والحمولة قد تم فحصهما وأنهما مناسبتان للغرض","أن الحمولة خفيفة الوزن","أن المعدة جديدة"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التأكد من أن المعدة والحمولة قد تم فحصهما وأنهما مناسبتان للغرض.",
      feedback_wrong: "✗ خطأ! يجب فحص المعدة والحمولة والتأكد من مناسبتهما للغرض قبل البدء."
    },
    {
      rule: "09 — عمليات الرفع",
      q: "ما القاعدة بخصوص استخدام معدات الرفع؟",
      options: ["استخدام أي معدة متاحة","استخدام فقط المعدات التي تدربت على استخدامها","استخدام المعدات الأحدث دائماً","يمكن للجميع استخدام أي معدة"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب استخدام فقط المعدات التي تدربت على استخدامها لضمان السلامة.",
      feedback_wrong: "✗ خطأ! يجب عدم استخدام أي معدة رفع إلا إذا تدربت على استخدامها."
    },
    {
      rule: "09 — عمليات الرفع",
      q: "ما المطلوب بخصوص عمليات الرفع الحرجة؟",
      options: ["تنفيذها بسرعة","وجود خطة رفع وإجراء تقييم مخاطر لعملية الرفع الحرجة","الاكتفاء بتعليمات شفهية","لا تختلف عن عمليات الرفع العادية"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب وجود خطة رفع وإجراء تقييم مخاطر لعملية الرفع الحرجة.",
      feedback_wrong: "✗ خطأ! عمليات الرفع الحرجة تتطلب خطة رفع وتقييم مخاطر مفصل."
    },
    {
      rule: "09 — عمليات الرفع",
      q: "ما الإجراء الصحيح بخصوص الحواجز ومناطق الحظر أثناء عمليات الرفع؟",
      options: ["وضعها فقط عند وجود المشرف","أضع والتزم بالحواجز ومناطق الحظر","ليست ضرورية للرفعات الصغيرة","وضعها بعد الانتهاء من الرفع"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب وضع الحواجز ومناطق الحظر والالتزام بها أثناء عمليات الرفع.",
      feedback_wrong: "✗ خطأ! وضع الحواجز ومناطق الحظر والالتزام بها إجراء إلزامي أثناء الرفع."
    },
    {
      rule: "09 — عمليات الرفع",
      q: "ما القاعدة بخصوص المشي تحت الحمولة المعلقة؟",
      options: ["مسموح إذا كانت الحمولة خفيفة","لا أمشي أبداً تحت حمولة معلقة","مسموح مع ارتداء الخوذة","مسموح إذا كان المشغل موجوداً"],
      correct: 1,
      feedback_correct: "✓ صحيح! لا يجب المشي أبداً تحت حمولة معلقة — هذه قاعدة لا تقبل الاستثناء.",
      feedback_wrong: "✗ خطأ! المشي تحت حمولة معلقة محظور تماماً في جميع الأحوال."
    },
    {
      rule: "09 — عمليات الرفع",
      q: "أي من التالي يُعتبر تصرفاً خاطئاً أثناء عمليات الرفع؟",
      options: ["فحص المعدة والحمولة قبل الرفع","إعداد خطة رفع للعمليات الحرجة","استخدام معدة رفع لم تتدرب على استخدامها","وضع حواجز حول منطقة الرفع"],
      correct: 2,
      feedback_correct: "✓ صحيح! استخدام معدة لم تتدرب عليها يعرضك ويعرض الآخرين لخطر كبير.",
      feedback_wrong: "✗ خطأ! استخدام معدات رفع بدون تدريب مناسب هو تصرف خاطئ وخطير."
    },
    {
      rule: "09 — عمليات الرفع",
      q: "لماذا يُعد التخطيط المسبق لعملية الرفع أمراً ضرورياً؟",
      options: ["لتوثيق العمل فقط","لأنه مطلب إداري فقط","لتحديد المخاطر وضمان مناسبة المعدات والحمولة وحماية المنطقة","ليس ضرورياً للرفعات الروتينية"],
      correct: 2,
      feedback_correct: "✓ صحيح! التخطيط يضمن تحديد المخاطر ومناسبة المعدات وحماية المنطقة والعاملين.",
      feedback_wrong: "✗ خطأ! التخطيط ضروري لتحديد المخاطر وضمان سلامة المعدات والحمولة والمنطقة."
    }
  ];

  var rule10Questions = [
    {
      rule: "10 — قيادة المركبات أو المعدات",
      q: "ما المبدأ الأساسي لقيادة المركبات أو المعدات؟",
      options: ["القيادة بسرعة لإنجاز العمل","اتباع تعليمات القيادة الآمنة","الاعتماد على الخبرة الشخصية فقط","القيادة حسب الظروف بدون قواعد محددة"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب اتباع تعليمات القيادة الآمنة في جميع الأوقات.",
      feedback_wrong: "✗ خطأ! المبدأ الأساسي هو اتباع تعليمات القيادة الآمنة دائماً."
    },
    {
      rule: "10 — قيادة المركبات أو المعدات",
      q: "ما القاعدة بخصوص حزام الأمان أثناء القيادة؟",
      options: ["ربطه فقط على الطرق السريعة","ربط حزام الأمان دائماً","ربطه فقط عند وجود رقابة","ليس ضرورياً داخل مواقع العمل"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب ربط حزام الأمان دائماً بدون استثناء.",
      feedback_wrong: "✗ خطأ! حزام الأمان يجب ربطه دائماً في جميع الأوقات والظروف."
    },
    {
      rule: "10 — قيادة المركبات أو المعدات",
      q: "ما التصرف الصحيح بخصوص حدود السرعة وظروف الطريق؟",
      options: ["تجاوز حدود السرعة إذا كان الطريق فارغاً","لا أتجاوز حدود السرعة وأهدئ السرعة لظروف الطريق","القيادة بأقصى سرعة مسموحة دائماً","تخفيف السرعة فقط عند وجود رقابة"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب عدم تجاوز حدود السرعة وتهدئة السرعة حسب ظروف الطريق.",
      feedback_wrong: "✗ خطأ! يجب الالتزام بحدود السرعة وتعديلها حسب ظروف الطريق."
    },
    {
      rule: "10 — قيادة المركبات أو المعدات",
      q: "ما القاعدة بخصوص استخدام الهاتف والأجهزة أثناء القيادة؟",
      options: ["مسموح لفترات قصيرة","لا أستخدم الهاتف أو أعمل على تشغيل الأجهزة أثناء القيادة","مسموح عند استخدام السماعة","مسموح أثناء التوقف المؤقت فقط"],
      correct: 1,
      feedback_correct: "✓ صحيح! يُمنع استخدام الهاتف أو تشغيل الأجهزة أثناء القيادة منعاً تاماً.",
      feedback_wrong: "✗ خطأ! استخدام الهاتف أو تشغيل أي أجهزة أثناء القيادة ممنوع تماماً."
    },
    {
      rule: "10 — قيادة المركبات أو المعدات",
      q: "ما المطلوب بخصوص حالة السائق أثناء القيادة؟",
      options: ["أن يكون قادراً على الإمساك بالمقود فقط","أن يكون لائقاً ومنتبهاً وفي حالة تأهب تام أثناء القيادة","أن يكون صاحياً فقط","أن يكون حاصلاً على رخصة فقط"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب أن تكون لائقاً ومنتبهاً وفي حالة تأهب تام أثناء القيادة.",
      feedback_wrong: "✗ خطأ! القيادة تتطلب أن تكون لائقاً ومنتبهاً وفي حالة تأهب تام."
    },
    {
      rule: "10 — قيادة المركبات أو المعدات",
      q: "ما القاعدة بخصوص التخطيط للرحلة؟",
      options: ["التخطيط فقط للرحلات الطويلة","أخطط دائماً لرحلتي","ليس ضرورياً للمسافات القصيرة","التخطيط عند توفر الوقت فقط"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب التخطيط دائماً للرحلة مهما كانت المسافة.",
      feedback_wrong: "✗ خطأ! التخطيط للرحلة إجراء إلزامي في جميع الأوقات."
    },
    {
      rule: "10 — قيادة المركبات أو المعدات",
      q: "ما الإجراء الصحيح بخصوص المسافة بينك وبين المركبة التي أمامك؟",
      options: ["تقليل المسافة لتوفير الوقت","أحافظ دائماً على مسافة آمنة بيني وبين المركبة التي أمامي","المسافة مهمة فقط على الطرق السريعة","الاقتراب مسموح إذا كانت السرعة منخفضة"],
      correct: 1,
      feedback_correct: "✓ صحيح! يجب المحافظة دائماً على مسافة آمنة بينك وبين المركبة التي أمامك.",
      feedback_wrong: "✗ خطأ! المحافظة على مسافة آمنة واجبة في جميع الأوقات والسرعات."
    },
    {
      rule: "10 — قيادة المركبات أو المعدات",
      q: "أي من التالي يُعتبر تصرفاً خاطئاً أثناء قيادة المركبات أو المعدات؟",
      options: ["ربط حزام الأمان","الالتزام بحدود السرعة","الرد على مكالمة هاتفية أثناء القيادة","التخطيط للرحلة مسبقاً"],
      correct: 2,
      feedback_correct: "✓ صحيح! الرد على مكالمة هاتفية أثناء القيادة ممنوع — يشتت الانتباه ويعرض الجميع للخطر.",
      feedback_wrong: "✗ خطأ! استخدام الهاتف أثناء القيادة من أخطر التصرفات التي تهدد سلامة الجميع."
    }
  ];

  var currentQuestions = [];
  var currentQuestion = 0;
  var score = 0;
  var answers = [];
  var currentMode = '';
  var employeeName = '';
  var employeeId = '';
  var quizStartTime = null;

  var quizMeta = {
    rule1:  { num: '01', name: 'عزل الطاقة', title: 'اختبار عزل الطاقة', desc: 'التحقق من العزل وعدم وجود أي طاقة قبل بدء العمل' },
    rule2:  { num: '02', name: 'تصريح العمل', title: 'اختبار تصريح العمل', desc: 'العمل بتصريح ساري المفعول إذا تطلب العمل ذلك' },
    rule3:  { num: '03', name: 'معدات الحماية الشخصية', title: 'اختبار معدات الحماية الشخصية', desc: 'ارتداء واستخدام معدات الحماية الشخصية المناسبة للمهمة' },
    rule4:  { num: '04', name: 'العمل على المرتفعات', title: 'اختبار العمل على المرتفعات', desc: 'احمِ نفسك من السقوط عند العمل على المرتفعات' },
    rule5:  { num: '05', name: 'تجاوز وسائل تحكم السلامة', title: 'اختبار تجاوز وسائل تحكم السلامة', desc: 'الحصول على إذن قبل تجاوز أو تعطيل وسائل تحكم السلامة' },
    rule6:  { num: '06', name: 'العمل الساخن', title: 'اختبار العمل الساخن', desc: 'السيطرة على المواد القابلة للاشتعال ومصادر الاشتعال' },
    rule7:  { num: '07', name: 'العمل في الأماكن المحصورة', title: 'اختبار العمل في الأماكن المحصورة', desc: 'الحصول على إذن قبل دخول مكان محصور' },
    rule8:  { num: '08', name: 'العمل في منطقة الخطر', title: 'اختبار العمل في منطقة الخطر', desc: 'أبقِ نفسك والآخرين بعيداً عن منطقة الخطر' },
    rule9:  { num: '09', name: 'عمليات الرفع', title: 'اختبار عمليات الرفع', desc: 'خطط لعمليات الرفع والتحكم في المنطقة' },
    rule10: { num: '10', name: 'قيادة المركبات أو المعدات', title: 'اختبار قيادة المركبات أو المعدات', desc: 'اتبع تعليمات القيادة الآمنة' },
    all:    { num: '⚡', name: 'اختبار شامل', title: 'اختبار جميع القواعد', desc: 'القواعد ٠١ إلى ١٠ — ٨٠ سؤال' }
  };

  var questionSets = {
    rule1: rule1Questions, rule2: rule2Questions, rule3: rule3Questions,
    rule4: rule4Questions, rule5: rule5Questions, rule6: rule6Questions,
    rule7: rule7Questions, rule8: rule8Questions, rule9: rule9Questions,
    rule10: rule10Questions
  };

  var ruleInfoData = {
    rule1: {
      icon: '⚡', color: '#e74c3c',
      facts: [
        { icon: '🔌', text: 'عزل الطاقة يشمل الكهربائية والهيدروليكية والهوائية والحرارية والميكانيكية والكيميائية' },
        { icon: '💀', text: 'الصعق الكهربائي هو السبب الرابع للوفيات في بيئة العمل عالمياً' },
        { icon: '🔒', text: 'نظام القفل والعلامة (LOTO) يمنع ٩٠٪ من حوادث الطاقة غير المتوقعة' }
      ]
    },
    rule2: {
      icon: '📋', color: '#3498db',
      facts: [
        { icon: '📝', text: 'تصريح العمل هو وثيقة رسمية تضمن تقييم المخاطر قبل بدء أي عمل خطير' },
        { icon: '⏰', text: 'التصريح له مدة صلاحية محددة ويجب تجديده إذا تغيرت ظروف العمل' },
        { icon: '👥', text: 'يجب أن يوقّع على التصريح جميع الأطراف المعنية: المنفذ والمشرف ومسؤول السلامة' }
      ]
    },
    rule3: {
      icon: '🦺', color: '#27ae60',
      facts: [
        { icon: '🪖', text: 'معدات الحماية الشخصية هي خط الدفاع الأخير بعد جميع إجراءات السلامة الأخرى' },
        { icon: '👁️', text: 'إصابات العيون تمثل ٢٠٪ من إصابات العمل — نظارات السلامة تمنع ٩٠٪ منها' },
        { icon: '📏', text: 'المعدات يجب أن تكون بالمقاس الصحيح — المعدات غير المناسبة قد تكون أخطر من عدمها' }
      ]
    },
    rule4: {
      icon: '🪜', color: '#8e44ad',
      facts: [
        { icon: '📊', text: 'السقوط من المرتفعات هو السبب الأول للوفيات في قطاع البناء والصناعة' },
        { icon: '📐', text: 'أي ارتفاع ١.٨ متر أو أكثر يتطلب حماية من السقوط حسب المعايير الدولية' },
        { icon: '🪢', text: 'حزام الأمان الكامل (Full Harness) يوزع قوة السقوط على الجسم ويقلل الإصابات بنسبة ٩٥٪' }
      ]
    },
    rule5: {
      icon: '🚫', color: '#e67e22',
      facts: [
        { icon: '🛡️', text: 'وسائل تحكم السلامة تشمل: الحواجز، أجهزة الإنذار، صمامات الأمان، وأنظمة الإيقاف الطارئ' },
        { icon: '⚖️', text: 'تجاوز أي وسيلة سلامة بدون إذن رسمي يعتبر مخالفة جسيمة قد تؤدي للفصل' },
        { icon: '📋', text: 'إذا كان لا بد من التجاوز، يجب وجود تقييم مخاطر مكتوب وموافقة الإدارة المختصة' }
      ]
    },
    rule6: {
      icon: '🔥', color: '#d35400',
      facts: [
        { icon: '🌡️', text: 'العمل الساخن يشمل: اللحام، القطع، الطحن، وأي عمل ينتج شرر أو لهب مكشوف' },
        { icon: '💨', text: 'الأبخرة القابلة للاشتعال يمكن أن تنتقل لمسافات بعيدة وتشتعل من مصدر بعيد' },
        { icon: '🧯', text: 'يجب وجود طفاية حريق مناسبة ومراقب حريق أثناء وبعد العمل الساخن بـ ٣٠ دقيقة' }
      ]
    },
    rule7: {
      icon: '🕳️', color: '#2c3e50',
      facts: [
        { icon: '🫁', text: 'نقص الأكسجين في الأماكن المحصورة يمكن أن يسبب فقدان الوعي خلال ثوانٍ معدودة' },
        { icon: '📡', text: 'يجب فحص الغازات قبل الدخول: الأكسجين، الغازات السامة، والغازات القابلة للاشتعال' },
        { icon: '🆘', text: 'يجب وجود مراقب خارجي وخطة إنقاذ جاهزة قبل دخول أي مكان محصور' }
      ]
    },
    rule8: {
      icon: '⚠️', color: '#c0392b',
      facts: [
        { icon: '🚧', text: 'منطقة الخطر هي أي منطقة يمكن أن تصل إليها معدات متحركة أو أحمال معلقة' },
        { icon: '👀', text: 'التواصل البصري مع مشغّل المعدات ضروري — إذا لم تره فهو لا يراك' },
        { icon: '🔶', text: 'الحواجز والعلامات التحذيرية يجب أن تكون واضحة ومرئية من جميع الاتجاهات' }
      ]
    },
    rule9: {
      icon: '🏗️', color: '#1a5276',
      facts: [
        { icon: '📋', text: 'كل عملية رفع تحتاج خطة مكتوبة تشمل: الوزن، نصف القطر، وقدرة الرافعة' },
        { icon: '⚖️', text: 'تجاوز حمولة الرافعة حتى بنسبة ١٠٪ يمكن أن يؤدي لانقلابها بالكامل' },
        { icon: '🚷', text: 'يمنع منعاً باتاً المرور أو الوقوف تحت الأحمال المعلقة مهما كانت الظروف' }
      ]
    },
    rule10: {
      icon: '🚗', color: '#16a085',
      facts: [
        { icon: '📱', text: 'استخدام الهاتف أثناء القيادة يزيد احتمال الحوادث ٤ أضعاف حتى مع السماعة' },
        { icon: '🪪', text: 'يجب التأكد من صلاحية الرخصة وأن السائق مؤهل لنوع المركبة أو المعدة' },
        { icon: '🔍', text: 'فحص المركبة قبل التشغيل يكتشف ٨٠٪ من الأعطال التي تسبب الحوادث' }
      ]
    }
  };

  var pendingInfoMode = '';

  function showRuleInfo(mode) {
    pendingInfoMode = mode;
    var meta = quizMeta[mode];
    var info = ruleInfoData[mode];
    if (!meta || !info) { showRegister(mode); return; }

    document.getElementById('rinfoNum').textContent = meta.num;
    document.getElementById('rinfoName').textContent = meta.name;
    document.getElementById('rinfoHeader').style.background = 'linear-gradient(170deg, ' + info.color + ' 0%, ' + info.color + '99 50%, #1a1a2e 100%)';

    var bodyHTML = '';
    info.facts.forEach(function(f) {
      bodyHTML += '<div class="rinfo-fact">' +
        '<div class="rinfo-fact-icon">' + f.icon + '</div>' +
        '<div class="rinfo-fact-text">' + f.text + '</div>' +
        '</div>';
    });
    document.getElementById('rinfoBody').innerHTML = bodyHTML;
    document.getElementById('rinfoOverlay').classList.add('visible');
  }

  function closeRuleInfo() {
    document.getElementById('rinfoOverlay').classList.remove('visible');
  }

  function proceedToRegister() {
    closeRuleInfo();
    showRegister(pendingInfoMode);
  }

  function showRegister(mode) {
    currentMode = mode;
    var meta = quizMeta[mode] || quizMeta.all;
    document.getElementById('regQuizTag').textContent = '📝 ' + meta.title;

    document.getElementById('regName').value = employeeName;
    document.getElementById('regId').value = employeeId;
    document.getElementById('regName').classList.remove('error');
    document.getElementById('regId').classList.remove('error');
    document.getElementById('regNameErr').classList.remove('show');
    document.getElementById('regIdErr').classList.remove('show');

    document.getElementById('homeScreen').classList.add('hidden');
    document.getElementById('registerScreen').classList.add('visible');
    document.getElementById('quizScreen').classList.remove('visible');
    document.getElementById('resultsScreen').classList.remove('visible');
  }

  function goHomeFromReg() {
    document.getElementById('registerScreen').classList.remove('visible');
    document.getElementById('homeScreen').classList.remove('hidden');
  }

  function submitRegistration() {
    var nameEl = document.getElementById('regName');
    var idEl = document.getElementById('regId');
    var nameVal = nameEl.value.trim();
    var idVal = idEl.value.trim();
    var valid = true;

    nameEl.classList.remove('error');
    idEl.classList.remove('error');
    document.getElementById('regNameErr').classList.remove('show');
    document.getElementById('regIdErr').classList.remove('show');

    if (!nameVal) {
      nameEl.classList.add('error');
      document.getElementById('regNameErr').classList.add('show');
      valid = false;
    }
    if (!idVal) {
      idEl.classList.add('error');
      document.getElementById('regIdErr').classList.add('show');
      valid = false;
    }

    if (!valid) return;

    employeeName = nameVal;
    employeeId = idVal;
    document.getElementById('registerScreen').classList.remove('visible');
    startQuiz(currentMode);
  }

  function startQuiz(mode) {
    currentMode = mode;
    currentQuestion = 0;
    score = 0;
    answers = [];
    quizStartTime = new Date();

    var meta = quizMeta[mode] || quizMeta.all;

    if (mode === 'all') {
      currentQuestions = [].concat(rule1Questions, rule2Questions, rule3Questions, rule4Questions, rule5Questions, rule6Questions, rule7Questions, rule8Questions, rule9Questions, rule10Questions);
    } else {
      currentQuestions = (questionSets[mode] || []).slice();
    }

    // Shuffle questions randomly
    for (var i = currentQuestions.length - 1; i > 0; i--) {
      var j = Math.floor(Math.random() * (i + 1));
      var temp = currentQuestions[i];
      currentQuestions[i] = currentQuestions[j];
      currentQuestions[j] = temp;
    }

    document.getElementById('ruleNum').textContent = meta.num;
    document.getElementById('ruleName').textContent = meta.name;
    document.getElementById('quizTitle').textContent = meta.title;
    document.getElementById('quizDesc').textContent = meta.desc;

    document.getElementById('scoreDisplay').textContent = '٠';
    document.getElementById('homeScreen').classList.add('hidden');
    document.getElementById('registerScreen').classList.remove('visible');
    document.getElementById('quizScreen').classList.add('visible');
    document.getElementById('resultsScreen').classList.remove('visible');
    renderQuestion();
  }

  function openStopModal() {
    document.getElementById('stopOverlay').classList.add('visible');
  }
  function closeStopModal() {
    document.getElementById('stopOverlay').classList.remove('visible');
  }

  function goHome() {
    document.getElementById('homeScreen').classList.remove('hidden');
    document.getElementById('registerScreen').classList.remove('visible');
    document.getElementById('quizScreen').classList.remove('visible');
    document.getElementById('quizScreen').style.display = '';
    document.getElementById('resultsScreen').classList.remove('visible');
  }

  function renderQuestion() {
    var q = currentQuestions[currentQuestion];
    var total = currentQuestions.length;

    document.getElementById('questionCounter').textContent =
      'السؤال ' + toArabic(currentQuestion + 1) + ' من ' + toArabic(total);
    document.getElementById('progressFill').style.width =
      ((currentQuestion / total) * 100) + '%';
    document.getElementById('questionLabel').textContent =
      'السؤال ' + (ordinals[currentQuestion] || toArabic(currentQuestion + 1));
    document.getElementById('questionText').textContent = q.q;
    document.getElementById('ruleTag').textContent = q.rule;

    if (currentMode === 'all') {
      document.getElementById('ruleTag').style.display = 'inline-block';
    } else {
      document.getElementById('ruleTag').style.display = 'none';
    }

    var optionsList = document.getElementById('optionsList');
    optionsList.innerHTML = '';
    var labels = ['أ', 'ب', 'ج', 'د'];

    q.options.forEach(function(opt, i) {
      var btn = document.createElement('button');
      btn.className = 'option-btn';
      btn.innerHTML = '<span class="option-icon">' + labels[i] + '</span><span>' + opt + '</span>';
      btn.addEventListener('click', function() { selectAnswer(i); });
      optionsList.appendChild(btn);
    });

    document.getElementById('feedbackBox').className = 'feedback-box';
    document.getElementById('feedbackBox').textContent = '';
    document.getElementById('nextBtn').className = 'next-btn';
  }

  function selectAnswer(idx) {
    var q = currentQuestions[currentQuestion];
    var btns = document.querySelectorAll('.option-btn');
    var isCorrect = idx === q.correct;

    btns.forEach(function(btn, i) {
      btn.classList.add('disabled');
      if (i === q.correct) btn.classList.add('correct');
      else if (i === idx && !isCorrect) btn.classList.add('wrong');
    });

    var fb = document.getElementById('feedbackBox');
    if (isCorrect) {
      score++;
      fb.className = 'feedback-box correct-feedback';
      fb.textContent = q.feedback_correct;
    } else {
      fb.className = 'feedback-box wrong-feedback';
      fb.textContent = q.feedback_wrong;
    }

    answers.push({ questionIdx: currentQuestion, selected: idx, correct: isCorrect });
    document.getElementById('scoreDisplay').textContent = toArabic(score);
    document.getElementById('nextBtn').className = 'next-btn visible';
  }

  function nextQuestion() {
    currentQuestion++;
    if (currentQuestion < currentQuestions.length) {
      document.getElementById('questionCard').style.animation = 'none';
      void document.getElementById('questionCard').offsetHeight;
      document.getElementById('questionCard').style.animation = 'cardEnter 0.5s ease-out';
      renderQuestion();
    } else {
      showResults();
    }
  }

  function showResults() {
    document.getElementById('quizScreen').classList.remove('visible');
    document.getElementById('quizScreen').style.display = 'none';
    var rs = document.getElementById('resultsScreen');
    rs.classList.add('visible');

    // Show employee info
    document.getElementById('resultEmpName').textContent = employeeName;
    document.getElementById('resultEmpId').textContent = 'الرقم الوظيفي: ' + employeeId;

    var total = currentQuestions.length;
    var pct = Math.round((score / total) * 100);

    document.getElementById('resultCircle').style.setProperty('--pct', pct + '%');
    document.getElementById('resultScore').textContent = toArabic(score);
    document.getElementById('resultTotal').textContent = 'من ' + toArabic(total);

    if (pct === 100) {
      document.getElementById('resultTitle').textContent = 'ممتاز! درجة كاملة 🏆';
      document.getElementById('resultMsg').textContent = 'أنت ملتزم تماماً بقواعد السلامة. استمر في الحفاظ على سلامتك وسلامة زملائك.';
    } else if (pct >= 75) {
      document.getElementById('resultTitle').textContent = 'أداء جيد جداً 👏';
      document.getElementById('resultMsg').textContent = 'لديك معرفة جيدة. راجع الإجابات الخاطئة لتعزيز معلوماتك.';
    } else if (pct >= 50) {
      document.getElementById('resultTitle').textContent = 'تحتاج لمراجعة 📖';
      document.getElementById('resultMsg').textContent = 'معرفتك تحتاج لتحسين. راجع القواعد وأعد الاختبار.';
    } else {
      document.getElementById('resultTitle').textContent = 'يجب إعادة التدريب ⚠️';
      document.getElementById('resultMsg').textContent = 'سلامتك مهمة! يرجى مراجعة القواعد بالكامل وإعادة الاختبار.';
    }

    var summaryHTML = '';
    answers.forEach(function(a) {
      var iconClass = a.correct ? 'correct-icon' : 'wrong-icon';
      var icon = a.correct ? '✓' : '✗';
      summaryHTML += '<div class="summary-item">' +
        '<div class="summary-icon ' + iconClass + '">' + icon + '</div>' +
        '<span>' + currentQuestions[a.questionIdx].q + '</span></div>';
    });
    document.getElementById('summaryList').innerHTML = summaryHTML;
  }

  function restartQuiz() {
    startQuiz(currentMode);
  }

  function exportResults() {
    var total = currentQuestions.length;
    var pct = Math.round((score / total) * 100);
    var meta = quizMeta[currentMode] || quizMeta.all;
    var endTime = new Date();
    var duration = quizStartTime ? Math.round((endTime - quizStartTime) / 60000) : 0;

    var now = new Date();
    var dateStr = now.getFullYear() + '/' + String(now.getMonth()+1).padStart(2,'0') + '/' + String(now.getDate()).padStart(2,'0');
    var timeStr = String(now.getHours()).padStart(2,'0') + ':' + String(now.getMinutes()).padStart(2,'0');

    var txt = '═══════════════════════════════════════\n';
    txt += '       نتيجة اختبار قواعد الحفاظ على الحياة\n';
    txt += '═══════════════════════════════════════\n\n';
    txt += '👷 بيانات الموظف:\n';
    txt += '   الاسم: ' + employeeName + '\n';
    txt += '   الرقم الوظيفي: ' + employeeId + '\n\n';
    txt += '📝 بيانات الاختبار:\n';
    txt += '   نوع الاختبار: ' + meta.title + '\n';
    txt += '   التاريخ: ' + dateStr + '\n';
    txt += '   الوقت: ' + timeStr + '\n';
    txt += '   المدة: ' + (duration > 0 ? duration + ' دقيقة' : 'أقل من دقيقة') + '\n\n';
    txt += '📊 النتيجة:\n';
    txt += '   الدرجة: ' + score + ' / ' + total + '\n';
    txt += '   النسبة: ' + pct + '%\n';
    txt += '   التقييم: ';
    if (pct === 100) txt += 'ممتاز - درجة كاملة\n';
    else if (pct >= 75) txt += 'أداء جيد جداً\n';
    else if (pct >= 50) txt += 'يحتاج لمراجعة\n';
    else txt += 'يجب إعادة التدريب\n';
    txt += '\n───────────────────────────────────────\n';
    txt += '   تفاصيل الإجابات:\n';
    txt += '───────────────────────────────────────\n\n';

    answers.forEach(function(a, i) {
      var q = currentQuestions[a.questionIdx];
      var status = a.correct ? '✅ صحيح' : '❌ خطأ';
      txt += (i+1) + '. ' + q.q + '\n';
      txt += '   الإجابة: ' + q.options[a.selected] + ' — ' + status + '\n';
      if (!a.correct) {
        txt += '   الإجابة الصحيحة: ' + q.options[q.correct] + '\n';
      }
      txt += '\n';
    });

    txt += '═══════════════════════════════════════\n';

    var blob = new Blob([txt], { type: 'text/plain;charset=utf-8' });
    var url = URL.createObjectURL(blob);
    var a = document.createElement('a');
    a.href = url;
    a.download = 'نتيجة_اختبار_' + employeeId + '_' + dateStr.replace(/\//g, '-') + '.txt';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
  }

  // Enter key on registration inputs
  document.getElementById('regName').addEventListener('keydown', function(e) {
    if (e.key === 'Enter') { document.getElementById('regId').focus(); }
  });
  document.getElementById('regId').addEventListener('keydown', function(e) {
    if (e.key === 'Enter') { submitRegistration(); }
  });
  // Clear error on typing
  document.getElementById('regName').addEventListener('input', function() {
    this.classList.remove('error');
    document.getElementById('regNameErr').classList.remove('show');
  });
  document.getElementById('regId').addEventListener('input', function() {
    this.classList.remove('error');
    document.getElementById('regIdErr').classList.remove('show');
  });

  // Dark mode
  if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
    document.documentElement.classList.add('dark');
  }
  window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', function(e) {
    if (e.matches) { document.documentElement.classList.add('dark'); }
    else { document.documentElement.classList.remove('dark'); }
  });
</script>
</body>
</html>
