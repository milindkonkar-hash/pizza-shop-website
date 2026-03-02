# pizza-shop-website
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pizza Shop | Home</title>
  <meta name="description" content="Pizza Shop - Explore newcomers, offers, and delicious pizzas with fast add-to-cart ordering.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Archivo:wght@600;700&family=Manrope:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #ffffff;
      --ink: #14243a;
      --muted: #6f7f91;
      --blue: #006491;
      --red: #e31837;
      --line: #e4edf5;
      --card: #ffffff;
      --shadow: 0 14px 32px rgba(20, 36, 58, 0.1);
      --radius: 20px;
      --maxw: 1240px;
      --topbar-height: 74px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      font-family: "Manrope", "Segoe UI", sans-serif;
      background: var(--bg);
      color: var(--ink);
      line-height: 1.5;
      overflow-x: hidden;
    }

    body.cart-open {
      overflow: hidden;
    }

    body.drawer-open {
      overflow: hidden;
    }

    body.auth-locked {
      overflow: hidden;
    }

    body.order-flow-open {
      overflow: hidden;
    }

    body.track-order-open {
      overflow: hidden;
    }

    img {
      display: block;
      width: 100%;
      object-fit: cover;
    }

    .container {
      width: min(var(--maxw), 92vw);
      margin: 0 auto;
    }

    @keyframes navFadeSlide {
      from {
        opacity: 0;
        transform: translateY(-14px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    [data-scroll-animate] {
      opacity: 0;
      transform: translate3d(0, 24px, 0);
      transition: opacity 0.65s ease, transform 0.65s cubic-bezier(0.22, 1, 0.36, 1);
      transition-delay: var(--scroll-anim-delay, 0ms);
      will-change: opacity, transform;
    }

    [data-scroll-animate][data-slide-from="left"] {
      transform: translate3d(-30px, 0, 0);
    }

    [data-scroll-animate][data-slide-from="right"] {
      transform: translate3d(30px, 0, 0);
    }

    [data-scroll-animate].in-view {
      opacity: 1;
      transform: translate3d(0, 0, 0);
    }

    .topbar {
      position: sticky;
      top: 0;
      z-index: 40;
      background: rgba(255, 255, 255, 0.56);
      backdrop-filter: blur(14px) saturate(120%);
      -webkit-backdrop-filter: blur(14px) saturate(120%);
      border-bottom: 1px solid rgba(190, 210, 228, 0.65);
      animation: navFadeSlide 0.55s cubic-bezier(0.22, 1, 0.36, 1) both;
    }

    .topbar-inner {
      min-height: var(--topbar-height);
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 16px;
    }

    .brand {
      text-decoration: none;
      color: var(--ink);
      font-family: "Archivo", sans-serif;
      font-size: clamp(1.4rem, 2.2vw, 2rem);
      letter-spacing: 0.01em;
    }

    .brand span {
      color: var(--red);
    }

    .top-links {
      display: flex;
      align-items: center;
      gap: clamp(12px, 2vw, 24px);
      list-style: none;
    }

    .top-links a {
      text-decoration: none;
      font-weight: 600;
      color: #36506d;
      font-size: 0.94rem;
    }

    .cart-trigger {
      border: 0;
      cursor: pointer;
      border-radius: 999px;
      padding: 10px 16px;
      color: #ffffff;
      font-weight: 700;
      letter-spacing: 0.01em;
      background: linear-gradient(90deg, var(--blue), var(--red));
      display: inline-flex;
      align-items: center;
      gap: 10px;
      box-shadow: 0 10px 22px rgba(0, 100, 145, 0.24);
    }

    .cart-trigger span {
      min-width: 26px;
      height: 26px;
      border-radius: 50%;
      background: #ffffff;
      color: #10253b;
      display: grid;
      place-items: center;
      font-size: 0.82rem;
    }

    .top-actions {
      display: inline-flex;
      align-items: center;
      gap: 10px;
    }

    .user-pill {
      border: 1px solid rgba(178, 204, 226, 0.72);
      border-radius: 999px;
      padding: 8px 12px;
      font-size: 0.82rem;
      color: #1f4465;
      background: rgba(245, 251, 255, 0.48);
      backdrop-filter: blur(10px) saturate(120%);
      -webkit-backdrop-filter: blur(10px) saturate(120%);
      box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.35);
      max-width: 240px;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }

    .logout-trigger {
      border: 1px solid #cbd9e7;
      border-radius: 999px;
      padding: 9px 14px;
      background: #ffffff;
      color: #153454;
      font-weight: 700;
      cursor: pointer;
    }

    .auth-overlay {
      position: fixed;
      inset: 0;
      z-index: 120;
      display: grid;
      place-items: center;
      padding: 22px;
      background:
        radial-gradient(circle at 6% 8%, rgba(0, 100, 145, 0.32), transparent 44%),
        radial-gradient(circle at 88% 12%, rgba(227, 24, 55, 0.28), transparent 48%),
        linear-gradient(145deg, rgba(9, 24, 39, 0.9), rgba(10, 34, 53, 0.82));
      backdrop-filter: blur(10px);
    }

    .auth-overlay.hidden {
      display: none;
    }

    .auth-shell {
      width: min(540px, 96vw);
      background:
        linear-gradient(160deg, rgba(0, 100, 145, 0.06), rgba(227, 24, 55, 0.07)),
        #ffffff;
      border: 1px solid rgba(198, 218, 236, 0.94);
      border-radius: 24px;
      box-shadow:
        0 26px 68px rgba(6, 23, 37, 0.42),
        0 10px 24px rgba(17, 44, 69, 0.18);
      padding: 24px 24px 20px;
      display: grid;
      gap: 14px;
      animation: authPop 0.28s ease-out;
    }

    @keyframes authPop {
      from {
        transform: translateY(10px) scale(0.985);
        opacity: 0;
      }
      to {
        transform: translateY(0) scale(1);
        opacity: 1;
      }
    }

    .auth-title {
      font-family: "Archivo", sans-serif;
      font-size: clamp(1.3rem, 2.4vw, 1.52rem);
      color: #102a44;
      margin: 0;
    }

    .auth-subtitle {
      color: #4e6983;
      font-size: 0.92rem;
      margin: 4px 0 0;
      line-height: 1.55;
    }

    .auth-switch {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      border-radius: 14px;
      padding: 4px;
      background: #edf3f9;
      border: 1px solid #d2e0ee;
      gap: 4px;
    }

    .auth-switch-btn {
      border: 0;
      border-radius: 10px;
      padding: 10px 12px;
      font-size: 0.88rem;
      font-weight: 700;
      color: #3f5d78;
      background: transparent;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .auth-switch-btn.is-active {
      color: #ffffff;
      background: linear-gradient(90deg, var(--blue), var(--red));
      box-shadow: 0 10px 20px rgba(0, 100, 145, 0.24);
    }

    .auth-pane {
      display: none;
      gap: 10px;
    }

    .auth-pane.is-active {
      display: grid;
    }

    .auth-grid {
      display: grid;
      gap: 10px;
    }

    .auth-group {
      display: grid;
      gap: 6px;
    }

    .auth-group label {
      font-weight: 700;
      font-size: 0.86rem;
      color: #163a5b;
      letter-spacing: 0.01em;
    }

    .auth-group input {
      width: 100%;
      border: 1px solid #bfd2e3;
      border-radius: 12px;
      padding: 11px 12px;
      font: inherit;
      color: #122d47;
      background: rgba(255, 255, 255, 0.97);
      transition: border-color 0.2s ease, box-shadow 0.2s ease, transform 0.2s ease;
    }

    .auth-group input:focus {
      outline: none;
      border-color: #1b77a3;
      box-shadow: 0 0 0 3px rgba(0, 100, 145, 0.15);
      transform: translateY(-1px);
    }

    .auth-submit {
      border: 0;
      border-radius: 12px;
      padding: 12px;
      font-size: 0.92rem;
      font-weight: 800;
      color: #ffffff;
      background: linear-gradient(92deg, #01628f, #e31837);
      box-shadow: 0 12px 24px rgba(0, 100, 145, 0.28);
      cursor: pointer;
      transition: transform 0.2s ease, box-shadow 0.2s ease;
    }

    .auth-submit:hover {
      transform: translateY(-1px);
      box-shadow: 0 16px 24px rgba(0, 100, 145, 0.24);
    }

    .auth-submit:disabled {
      opacity: 0.64;
      transform: none;
      box-shadow: none;
      cursor: not-allowed;
    }

    .auth-message {
      min-height: 20px;
      border-radius: 10px;
      padding: 8px 10px;
      font-size: 0.82rem;
      line-height: 1.4;
      display: none;
      border: 1px solid transparent;
    }

    .auth-message.show {
      display: block;
    }

    .auth-message.info {
      background: #e9f5fc;
      border-color: #c2def1;
      color: #1c5779;
    }

    .auth-message.success {
      background: #eaf8ef;
      border-color: #bfe7cb;
      color: #1c6a39;
    }

    .auth-message.error {
      background: #fdecef;
      border-color: #f6c3cc;
      color: #b11b34;
    }

    .auth-hint {
      font-size: 0.79rem;
      color: #556f88;
      background: #f1f7fc;
      border: 1px dashed #c1d6e8;
      border-radius: 11px;
      padding: 10px 11px;
      line-height: 1.45;
    }

    .drawer-tab-toggle {
      position: fixed;
      left: 0;
      top: 50%;
      transform: translateY(-50%);
      z-index: 82;
      border: 0;
      border-radius: 0 14px 14px 0;
      border-right: 1px solid rgba(255, 255, 255, 0.46);
      padding: 14px 10px;
      min-height: 132px;
      min-width: 52px;
      background: linear-gradient(180deg, #005f89, #e31837);
      color: #ffffff;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      box-shadow: 0 14px 24px rgba(10, 32, 52, 0.32);
      transition: left 0.26s ease, transform 0.2s ease, box-shadow 0.2s ease, padding 0.22s ease, min-height 0.22s ease, min-width 0.22s ease, border-radius 0.22s ease;
    }

    .drawer-tab-toggle:hover {
      transform: translateY(-50%) translateX(2px);
      box-shadow: 0 16px 28px rgba(10, 32, 52, 0.36);
    }

    .drawer-toggle-label {
      position: absolute;
      left: 50%;
      top: 50%;
      font-size: 0.78rem;
      font-weight: 800;
      text-transform: uppercase;
      white-space: nowrap;
      pointer-events: none;
      transition: opacity 0.2s ease, transform 0.24s ease, letter-spacing 0.2s ease;
    }

    .drawer-toggle-label.menu {
      letter-spacing: 0.08em;
      opacity: 1;
      transform: translate(-50%, -50%) rotate(90deg);
    }

    .drawer-toggle-label.close {
      letter-spacing: 0.02em;
      opacity: 0;
      transform: translate(-50%, -16%);
    }

    .drawer-tab-toggle.is-open {
      left: calc(clamp(240px, 25vw, 430px) - 24px);
      min-height: 40px;
      min-width: 84px;
      border-radius: 999px;
      border-right: 0;
      padding: 10px 14px;
      transform: translateY(-50%);
    }

    .drawer-tab-toggle.is-open .drawer-toggle-label.menu {
      opacity: 0;
      transform: translate(-50%, -84%) rotate(90deg);
    }

    .drawer-tab-toggle.is-open .drawer-toggle-label.close {
      opacity: 1;
      transform: translate(-50%, -50%);
    }

    .left-drawer {
      position: fixed;
      left: 0;
      top: 0;
      bottom: 0;
      width: clamp(240px, 25vw, 430px);
      z-index: 80;
      display: grid;
      grid-template-rows: auto auto auto 1fr;
      transform: translateX(-102%);
      transition: transform 0.28s cubic-bezier(0.22, 0.61, 0.36, 1);
      background:
        linear-gradient(166deg, rgba(1, 98, 143, 0.1), rgba(227, 24, 55, 0.09)),
        #f7fbff;
      border-right: 1px solid #d4e2f0;
      box-shadow: 0 20px 36px rgba(13, 38, 60, 0.24);
    }

    .left-drawer.open {
      transform: translateX(0);
    }

    .left-drawer-backdrop {
      position: fixed;
      inset: 0;
      z-index: 70;
      background: rgba(9, 28, 45, 0.35);
      opacity: 0;
      transition: opacity 0.2s ease;
    }

    .left-drawer-backdrop.show {
      opacity: 1;
    }

    .drawer-head {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 14px 14px 12px;
      border-bottom: 1px solid #d8e6f3;
      background: rgba(255, 255, 255, 0.74);
      backdrop-filter: blur(6px);
    }

    .drawer-head h3 {
      font-family: "Archivo", sans-serif;
      font-size: 1.02rem;
      letter-spacing: 0.01em;
      color: #143451;
      margin: 0;
    }

    .drawer-close {
      border: 0;
      width: 30px;
      height: 30px;
      border-radius: 999px;
      background: #e8f0f7;
      color: #204c6e;
      font-weight: 700;
      cursor: pointer;
    }

    .drawer-user-status {
      margin: 10px 14px 0;
      padding: 9px 10px;
      border-radius: 10px;
      border: 1px solid #c9d9e8;
      background: #eef5fb;
      color: #1d4f71;
      font-size: 0.8rem;
      line-height: 1.4;
    }

    .drawer-auth-actions {
      margin: 10px 14px 8px;
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 8px;
    }

    .drawer-auth-btn {
      border: 1px solid #c8d9e8;
      border-radius: 11px;
      background: #ffffff;
      color: #1c4e72;
      padding: 8px 8px;
      font-size: 0.78rem;
      font-weight: 700;
      cursor: pointer;
      transition: transform 0.2s ease, border-color 0.2s ease, box-shadow 0.2s ease;
    }

    .drawer-auth-btn:hover {
      transform: translateY(-1px);
      border-color: #97bddb;
      box-shadow: 0 8px 16px rgba(19, 53, 82, 0.14);
    }

    .drawer-auth-btn.signout {
      background: #ffeef1;
      border-color: #f2cad2;
      color: #a31f36;
    }

    .drawer-auth-btn:disabled {
      opacity: 0.55;
      cursor: not-allowed;
      transform: none;
      box-shadow: none;
    }

    .drawer-section-nav {
      margin: 2px 14px 0;
      display: grid;
      gap: 8px;
      border-top: 1px solid #dbe8f4;
      padding-top: 12px;
    }

    .drawer-section-btn {
      border: 1px solid #c6d8e8;
      border-radius: 11px;
      background: #ffffff;
      color: #1e4d71;
      text-align: left;
      padding: 9px 10px;
      font-size: 0.82rem;
      font-weight: 700;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .drawer-section-btn.active {
      color: #ffffff;
      border-color: transparent;
      background: linear-gradient(90deg, #01628f, #e31837);
      box-shadow: 0 10px 20px rgba(0, 100, 145, 0.22);
    }

    .drawer-content {
      padding: 12px 14px 18px;
      overflow-y: auto;
      display: grid;
    }

    .drawer-panel {
      display: none;
      align-content: start;
      gap: 10px;
    }

    .drawer-panel.active {
      display: grid;
    }

    .drawer-panel h4 {
      font-family: "Archivo", sans-serif;
      font-size: 0.96rem;
      color: #163a5c;
      margin: 0;
    }

    .drawer-note {
      font-size: 0.8rem;
      color: #4f6a84;
      margin: 0;
      line-height: 1.4;
    }

    .drawer-list {
      list-style: none;
      display: grid;
      gap: 8px;
      margin: 0;
      padding: 0;
    }

    .drawer-list li {
      border: 1px solid #d0deeb;
      background: #ffffff;
      border-radius: 10px;
      padding: 8px 9px;
      font-size: 0.79rem;
      color: #244c70;
      line-height: 1.4;
    }

    .drawer-order-list,
    .drawer-reward-list {
      list-style: none;
      margin: 0;
      padding: 0;
      display: grid;
      gap: 8px;
    }

    .drawer-order-item,
    .drawer-reward-item {
      border: 1px solid #cfdeeb;
      border-radius: 10px;
      background: #ffffff;
      padding: 9px 10px;
      display: grid;
      gap: 4px;
      font-size: 0.78rem;
      color: #1f4e72;
      line-height: 1.35;
    }

    .drawer-order-item strong,
    .drawer-reward-item strong {
      font-size: 0.8rem;
      color: #143a5d;
    }

    .drawer-empty {
      border: 1px dashed #bfd2e3;
      border-radius: 10px;
      background: #f1f7fc;
      color: #5a748d;
      font-size: 0.79rem;
      padding: 11px 10px;
    }

    .drawer-feedback-form {
      display: grid;
      gap: 8px;
    }

    .drawer-feedback-form textarea {
      width: 100%;
      min-height: 110px;
      resize: vertical;
      border: 1px solid #bfd2e3;
      border-radius: 10px;
      background: #ffffff;
      padding: 10px;
      font: inherit;
      color: #123755;
    }

    .drawer-feedback-form textarea:focus {
      outline: none;
      border-color: #1f7ca8;
      box-shadow: 0 0 0 3px rgba(0, 100, 145, 0.12);
    }

    .drawer-feedback-form button {
      border: 0;
      border-radius: 10px;
      padding: 10px 12px;
      font-weight: 700;
      color: #ffffff;
      background: linear-gradient(90deg, #01628f, #e31837);
      cursor: pointer;
    }

    .drawer-feedback-status {
      min-height: 18px;
      font-size: 0.76rem;
      color: #5d7389;
    }

    .hero-section {
      padding: 0;
    }

    .hero-section .container {
      width: 100%;
      max-width: 100%;
    }

    .hero-slider {
      position: relative;
      height: calc(100vh - var(--topbar-height));
      height: calc(100dvh - var(--topbar-height));
      border-radius: 0;
      overflow: hidden;
      border: 0;
      box-shadow: none;
      background: #eff5fb;
      isolation: isolate;
    }

    .slides-track {
      height: 100%;
      display: flex;
      transition: transform 0.7s cubic-bezier(0.22, 0.61, 0.36, 1);
      will-change: transform;
    }

    .slide {
      position: relative;
      flex: 0 0 100%;
      height: 100%;
    }

    .slide img {
      height: 100%;
      filter: saturate(1.06) contrast(1.04);
      transform: scale(1.06);
      transition: transform 0.9s ease;
    }

    .slide.active img {
      transform: scale(1);
    }

    .slide-overlay {
      position: absolute;
      inset: 0;
      background:
        linear-gradient(100deg, rgba(9, 31, 50, 0.76) 0%, rgba(9, 31, 50, 0.38) 46%, rgba(9, 31, 50, 0.16) 100%);
    }

    .slide-content {
      position: absolute;
      left: clamp(12px, 3vw, 26px);
      bottom: clamp(10px, 2.2vw, 18px);
      max-width: min(440px, 80vw);
      color: #ffffff;
      z-index: 3;
    }

    .slide-content > * {
      opacity: 0;
      transform: translateY(16px);
      transition: transform 0.45s ease, opacity 0.45s ease;
    }

    .slide.active .slide-content > * {
      opacity: 1;
      transform: translateY(0);
    }

    .slide.active .slide-content .badge { transition-delay: 120ms; }
    .slide.active .slide-content h1 { transition-delay: 190ms; }
    .slide.active .slide-content p { transition-delay: 270ms; }
    .slide.active .slide-content .slide-cta { transition-delay: 340ms; }

    .slide-content .badge {
      display: inline-flex;
      align-items: center;
      border-radius: 999px;
      padding: 6px 12px;
      margin-bottom: 12px;
      font-size: 0.78rem;
      letter-spacing: 0.04em;
      text-transform: uppercase;
      font-weight: 800;
      border: 1px solid rgba(255, 255, 255, 0.22);
      background: rgba(255, 255, 255, 0.16);
    }

    .slide-content .badge.offer {
      background: rgba(227, 24, 55, 0.82);
      border-color: rgba(227, 24, 55, 0.82);
    }

    .slide-content h1 {
      font-family: "Archivo", sans-serif;
      font-size: clamp(1rem, 1.9vw, 1.6rem);
      line-height: 1.14;
      margin-bottom: 6px;
    }

    .slide-content > p:not(.badge) {
      max-width: 52ch;
      font-size: clamp(0.72rem, 0.95vw, 0.9rem);
      color: rgba(255, 255, 255, 0.95);
      margin-bottom: 8px;
    }

    .slide-cta {
      text-decoration: none;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      border-radius: 999px;
      background: #ffffff;
      color: #11314f;
      font-weight: 700;
      padding: 7px 12px;
      font-size: 0.78rem;
    }

    .slide-cta::after {
      content: ">";
      font-weight: 800;
    }

    .slide-action-row {
      display: flex;
      align-items: center;
      gap: 8px;
      flex-wrap: wrap;
    }

    .offer-add-btn {
      border: 1px solid rgba(255, 255, 255, 0.8);
      background: rgba(255, 255, 255, 0.2);
      color: #ffffff;
      border-radius: 999px;
      padding: 7px 12px;
      font-size: 0.78rem;
      font-weight: 700;
      cursor: pointer;
      transition: transform 0.2s ease, background 0.2s ease;
    }

    .offer-add-btn:hover {
      transform: translateY(-1px);
      background: rgba(255, 255, 255, 0.28);
    }

    .slider-nav {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      z-index: 5;
      border: 0;
      border-radius: 999px;
      width: 42px;
      height: 42px;
      cursor: pointer;
      color: #163454;
      background: rgba(255, 255, 255, 0.92);
      display: grid;
      place-items: center;
      font-size: 1.2rem;
      box-shadow: 0 8px 14px rgba(9, 31, 50, 0.25);
    }

    .slider-nav.prev {
      left: 12px;
    }

    .slider-nav.next {
      right: 12px;
    }

    .slider-dots {
      position: absolute;
      bottom: 14px;
      left: 50%;
      transform: translateX(-50%);
      z-index: 6;
      display: flex;
      gap: 8px;
      padding: 6px 10px;
      border-radius: 999px;
      background: rgba(12, 33, 54, 0.46);
      backdrop-filter: blur(8px);
    }

    .slider-dots .dot {
      width: 10px;
      height: 10px;
      border-radius: 50%;
      border: 0;
      cursor: pointer;
      background: rgba(255, 255, 255, 0.46);
    }

    .slider-dots .dot.active {
      background: #ffffff;
      transform: scale(1.08);
    }

    .categories-section {
      padding: 8px 0 70px;
    }

    .section-head {
      margin-bottom: 18px;
    }

    .section-head h2 {
      font-family: "Archivo", sans-serif;
      font-size: clamp(1.5rem, 3vw, 2.35rem);
      letter-spacing: 0.01em;
      margin-bottom: 6px;
      color: #112d4a;
    }

    .section-head p {
      color: var(--muted);
      font-size: 0.98rem;
    }

    .category-tabs {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 12px;
      margin-bottom: 14px;
    }

    .category-tab {
      border: 1px solid var(--line);
      background: #ffffff;
      border-radius: 16px;
      overflow: hidden;
      padding: 0;
      text-align: left;
      cursor: pointer;
      transition: transform 0.22s ease, box-shadow 0.22s ease, border-color 0.22s ease;
      position: relative;
    }

    .category-tab img {
      width: 100%;
      height: clamp(94px, 11vw, 132px);
      object-fit: cover;
      transform: scale(1.03);
      transition: transform 0.35s ease;
    }

    .category-tab .tab-label {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px 12px;
      font-size: 0.92rem;
      color: #1a4264;
      font-weight: 700;
      background: #ffffff;
    }

    .category-tab .tab-label small {
      color: #5d7891;
      font-size: 0.76rem;
      font-weight: 700;
    }

    .category-tab:hover {
      transform: translateY(-1px);
      box-shadow: 0 8px 14px rgba(21, 54, 87, 0.12);
    }

    .category-tab:hover img {
      transform: scale(1.09);
    }

    .category-tab.active {
      border-color: rgba(0, 100, 145, 0.45);
      box-shadow: 0 10px 18px rgba(0, 100, 145, 0.24);
      transform: translateY(-2px);
    }

    .category-tab.active .tab-label {
      color: #ffffff;
      background: linear-gradient(90deg, var(--blue), var(--red));
    }

    .category-tab.active .tab-label small {
      color: rgba(255, 255, 255, 0.88);
    }

    .category-block {
      padding: 18px 0 8px;
      border-top: 1px solid var(--line);
      opacity: 0;
      transform: translateY(16px);
      transition: opacity 0.45s ease, transform 0.45s ease;
    }

    .category-block.revealed {
      opacity: 1;
      transform: translateY(0);
    }

    .category-content {
      max-height: 0;
      overflow: hidden;
      opacity: 0;
      transform: translateY(-10px);
      transition: max-height 0.55s ease, opacity 0.35s ease, transform 0.35s ease;
    }

    .category-block.is-open .category-content {
      opacity: 1;
      transform: translateY(0);
    }

    .category-head {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
      margin-bottom: 12px;
      cursor: pointer;
      position: relative;
      padding-right: 24px;
    }

    .category-head::after {
      content: "v";
      position: absolute;
      right: 0;
      color: #43607b;
      font-size: 1rem;
      transition: transform 0.3s ease;
    }

    .category-block.is-open .category-head::after {
      transform: rotate(180deg);
    }

    .category-head h3 {
      font-size: clamp(1.2rem, 2vw, 1.6rem);
      color: #16324f;
    }

    .category-head span {
      font-size: 0.88rem;
      font-weight: 700;
      color: #36506b;
      border: 1px solid var(--line);
      border-radius: 999px;
      padding: 6px 12px;
      background: #f8fbff;
    }

    .menu-grid {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 16px;
    }

    .menu-card {
      border: 1px solid var(--line);
      border-radius: 18px;
      background: var(--card);
      box-shadow: 0 8px 18px rgba(18, 36, 58, 0.08);
      overflow: hidden;
      display: flex;
      flex-direction: column;
      height: 100%;
      opacity: 0;
      transform: translateY(12px) scale(0.985);
      transition: opacity 0.42s ease, transform 0.42s ease;
      transition-delay: var(--item-delay, 0ms);
    }

    .category-block.is-open .menu-card {
      opacity: 1;
      transform: translateY(0) scale(1);
    }

    .menu-card img {
      height: 184px;
      flex-shrink: 0;
      background: #eef4fb;
    }

    .menu-content {
      padding: 14px;
      display: flex;
      flex-direction: column;
      flex: 1;
      min-height: 0;
    }

    .menu-content h4 {
      font-size: 1.06rem;
      color: #12314f;
      margin-bottom: 6px;
      line-height: 1.25;
    }

    .menu-content p {
      font-size: 0.88rem;
      color: var(--muted);
      margin-bottom: 14px;
      flex: 1;
    }

    .menu-bottom {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      margin-top: auto;
    }

    .price {
      font-weight: 800;
      color: #133656;
      font-size: 1.02rem;
    }

    .add-cart-btn {
      border: 0;
      cursor: pointer;
      border-radius: 10px;
      font-weight: 700;
      font-size: 0.86rem;
      color: #ffffff;
      background: linear-gradient(90deg, var(--blue), var(--red));
      padding: 9px 12px;
      transition: transform 0.2s ease, box-shadow 0.2s ease;
      box-shadow: 0 8px 15px rgba(0, 100, 145, 0.2);
      white-space: nowrap;
    }

    .add-cart-btn:hover {
      transform: translateY(-1px);
      box-shadow: 0 10px 18px rgba(0, 100, 145, 0.24);
    }

    .category-block.is-open .menu-card:hover {
      transform: translateY(-4px) scale(1.012);
      box-shadow: 0 16px 22px rgba(18, 36, 58, 0.14);
    }

    .footer {
      border-top: 1px solid var(--line);
      padding: 22px 0 34px;
      color: #5f7387;
      font-size: 0.9rem;
      text-align: center;
    }

    .cart-backdrop {
      position: fixed;
      inset: 0;
      z-index: 80;
      background: rgba(13, 26, 41, 0.42);
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.24s ease;
    }

    .cart-backdrop.show {
      opacity: 1;
      pointer-events: auto;
    }

    .cart-panel {
      position: fixed;
      right: 0;
      top: 0;
      width: min(380px, 94vw);
      height: 100dvh;
      z-index: 90;
      background: #ffffff;
      border-left: 1px solid var(--line);
      box-shadow: -16px 0 32px rgba(13, 26, 41, 0.18);
      transform: translateX(100%);
      transition: transform 0.3s ease;
      display: grid;
      grid-template-rows: auto auto 1fr auto;
    }

    .cart-panel.open {
      transform: translateX(0);
    }

    .cart-header {
      padding: 16px;
      border-bottom: 1px solid var(--line);
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
    }

    .cart-header h2 {
      font-size: 1.2rem;
      color: #173553;
    }

    .close-cart {
      border: 0;
      border-radius: 10px;
      background: #eaf3fb;
      color: #153553;
      padding: 8px 11px;
      cursor: pointer;
      font-weight: 700;
    }

    .cart-subtitle {
      padding: 10px 16px;
      color: #6b7e90;
      font-size: 0.86rem;
      border-bottom: 1px solid var(--line);
    }

    .cart-items {
      list-style: none;
      overflow: auto;
      padding: 12px 16px;
      display: grid;
      gap: 10px;
      align-content: start;
    }

    .empty-cart {
      border: 1px dashed #cfdeeb;
      border-radius: 12px;
      padding: 16px;
      color: #62809b;
      text-align: center;
      font-size: 0.92rem;
      background: #f9fcff;
    }

    .cart-item {
      border: 1px solid var(--line);
      border-radius: 12px;
      padding: 10px;
      display: grid;
      gap: 6px;
      background: #ffffff;
    }

    .cart-item-top {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      align-items: flex-start;
    }

    .cart-item h4 {
      font-size: 0.92rem;
      color: #12314f;
      line-height: 1.3;
    }

    .line-total {
      font-size: 0.89rem;
      font-weight: 700;
      color: #153b5d;
      white-space: nowrap;
    }

    .qty-row {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      border: 1px solid var(--line);
      border-radius: 999px;
      padding: 4px;
      width: fit-content;
    }

    .qty-btn {
      border: 0;
      width: 26px;
      height: 26px;
      border-radius: 50%;
      cursor: pointer;
      font-weight: 800;
      font-size: 0.95rem;
      color: #12314f;
      background: #edf5fc;
    }

    .qty-value {
      min-width: 18px;
      text-align: center;
      font-size: 0.9rem;
      font-weight: 700;
      color: #12314f;
    }

    .cart-footer {
      border-top: 1px solid var(--line);
      padding: 14px 16px 16px;
      display: grid;
      gap: 10px;
      background: #ffffff;
    }

    .total-row {
      display: flex;
      justify-content: space-between;
      color: #143351;
      font-size: 0.96rem;
    }

    .total-row strong {
      font-size: 1rem;
    }

    .checkout-btn {
      border: 0;
      border-radius: 12px;
      padding: 12px;
      font-weight: 700;
      color: #ffffff;
      background: linear-gradient(90deg, var(--blue), var(--red));
      cursor: pointer;
      transition: opacity 0.2s ease;
    }

    .checkout-btn:disabled {
      opacity: 0.42;
      cursor: not-allowed;
    }

    .order-flow-overlay,
    .tracking-overlay {
      position: fixed;
      inset: 0;
      z-index: 130;
      background: rgba(10, 26, 40, 0.56);
      backdrop-filter: blur(5px);
      display: grid;
      place-items: center;
      padding: 24px;
    }

    .tracking-overlay {
      z-index: 131;
    }

    .order-flow-overlay.hidden,
    .tracking-overlay.hidden {
      display: none;
    }

    .order-flow-shell,
    .tracking-shell {
      width: min(980px, 96vw);
      max-height: 92dvh;
      overflow: auto;
      background:
        linear-gradient(160deg, rgba(0, 100, 145, 0.06), rgba(227, 24, 55, 0.05)),
        #ffffff;
      border: 1px solid #d7e5f2;
      border-radius: 20px;
      box-shadow: 0 20px 52px rgba(10, 28, 44, 0.32);
      padding: 20px;
      display: grid;
      gap: 14px;
    }

    .order-flow-head,
    .tracking-head {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      align-items: center;
      border-bottom: 1px solid #dfebf6;
      padding-bottom: 10px;
    }

    .order-flow-head h2,
    .tracking-head h2 {
      font-family: "Archivo", sans-serif;
      color: #12314f;
      font-size: clamp(1.2rem, 2.3vw, 1.5rem);
    }

    .order-flow-close,
    .tracking-close {
      border: 0;
      border-radius: 10px;
      padding: 8px 12px;
      background: #e8f1fa;
      color: #12314f;
      font-weight: 700;
      cursor: pointer;
    }

    .order-flow-subtitle,
    .tracking-subtitle {
      color: #55708a;
      font-size: 0.9rem;
    }

    .order-flow-grid {
      display: grid;
      grid-template-columns: 1.1fr 0.9fr;
      gap: 14px;
    }

    .order-block {
      border: 1px solid #d4e2ef;
      border-radius: 14px;
      padding: 12px;
      background: #f9fcff;
      display: grid;
      gap: 10px;
      align-content: start;
    }

    .order-block h3 {
      color: #113552;
      font-size: 1rem;
    }

    .order-flow-items {
      list-style: none;
      display: grid;
      gap: 8px;
      max-height: 220px;
      overflow: auto;
      padding-right: 4px;
    }

    .order-flow-item {
      border: 1px solid #d8e6f3;
      border-radius: 10px;
      background: #ffffff;
      padding: 8px 9px;
      display: flex;
      justify-content: space-between;
      gap: 8px;
      font-size: 0.88rem;
      color: #143451;
    }

    .order-flow-item span:first-child {
      flex: 1;
    }

    .order-coupon-list,
    .order-mode-list {
      display: grid;
      gap: 8px;
    }

    .order-coupon-option,
    .order-mode-option {
      border: 1px solid #cdddec;
      border-radius: 10px;
      background: #ffffff;
      padding: 8px 10px;
      display: flex;
      gap: 8px;
      align-items: flex-start;
      color: #163a5b;
      font-size: 0.86rem;
    }

    .order-coupon-option input,
    .order-mode-option input {
      margin-top: 2px;
      accent-color: #006491;
    }

    .order-coupon-option small,
    .order-mode-option small {
      display: block;
      color: #607a93;
      margin-top: 2px;
      line-height: 1.3;
    }

    .order-coupon-option.is-disabled {
      opacity: 0.55;
    }

    .coupon-note {
      border: 1px dashed #c8d8e8;
      border-radius: 10px;
      background: #f1f7fc;
      padding: 8px 10px;
      font-size: 0.82rem;
      color: #476784;
      min-height: 36px;
    }

    .price-breakdown {
      border: 1px solid #d4e2ef;
      border-radius: 12px;
      background: #ffffff;
      padding: 10px;
      display: grid;
      gap: 8px;
    }

    .price-breakdown-row {
      display: flex;
      justify-content: space-between;
      color: #173553;
      font-size: 0.9rem;
    }

    .price-breakdown-row.discount {
      color: #1f6e3a;
    }

    .price-breakdown-row.total {
      border-top: 1px solid #d9e7f3;
      padding-top: 7px;
      font-weight: 800;
      font-size: 0.98rem;
    }

    .order-flow-actions {
      display: flex;
      justify-content: flex-end;
      gap: 10px;
    }

    .order-confirm-visual {
      display: grid;
      justify-items: center;
      gap: 8px;
      padding: 2px 0 0;
    }

    .order-confirm-visual.hidden {
      display: none;
    }

    .rotating-pizza-loader {
      width: 76px;
      aspect-ratio: 1;
      border-radius: 50%;
      position: relative;
      background:
        radial-gradient(circle at 50% 50%, #f9d07f 0 44%, #cd6d2f 45% 58%, #8f461f 59% 100%);
      box-shadow:
        0 10px 20px rgba(114, 62, 28, 0.28),
        inset 0 0 0 2px rgba(255, 255, 255, 0.34);
      animation: pizzaSpin 1.5s linear infinite;
      transform-origin: 50% 50%;
    }

    .rotating-pizza-loader::before {
      content: "";
      position: absolute;
      inset: 14%;
      border-radius: 50%;
      background:
        radial-gradient(circle at 22% 28%, #c82734 0 9%, transparent 10%),
        radial-gradient(circle at 65% 24%, #2f7e3e 0 8%, transparent 9%),
        radial-gradient(circle at 74% 63%, #c82734 0 10%, transparent 11%),
        radial-gradient(circle at 32% 70%, #2f7e3e 0 8%, transparent 9%),
        radial-gradient(circle at 50% 50%, rgba(250, 245, 206, 0.95) 0 65%, rgba(248, 193, 89, 0.88) 66% 100%);
    }

    .rotating-pizza-loader::after {
      content: "";
      position: absolute;
      inset: 21%;
      border-radius: 50%;
      background: conic-gradient(from 45deg, rgba(255, 255, 255, 0) 0 55%, rgba(255, 255, 255, 0.45) 70%, rgba(255, 255, 255, 0) 85% 100%);
      animation: pizzaShine 1.1s ease-in-out infinite;
    }

    .order-confirm-caption {
      font-size: 0.78rem;
      color: #53728e;
      text-align: center;
    }

    .order-flow-btn {
      border: 0;
      border-radius: 11px;
      padding: 10px 14px;
      font-weight: 700;
      cursor: pointer;
    }

    .order-flow-btn.secondary {
      background: #eaf2fa;
      color: #133451;
    }

    .order-flow-btn.primary {
      background: linear-gradient(90deg, var(--blue), var(--red));
      color: #ffffff;
      min-width: 170px;
    }

    .order-flow-btn:disabled {
      cursor: not-allowed;
      opacity: 0.58;
    }

    .order-confirm-status {
      min-height: 20px;
      font-size: 0.84rem;
      color: #1d5e81;
      text-align: right;
    }

    @keyframes pizzaSpin {
      from {
        transform: rotate(0deg);
      }

      to {
        transform: rotate(360deg);
      }
    }

    @keyframes pizzaShine {
      0%,
      100% {
        opacity: 0.35;
      }

      50% {
        opacity: 0.72;
      }
    }

    .tracking-meta {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 8px;
    }

    .tracking-pill {
      border: 1px solid #d5e4f1;
      border-radius: 10px;
      background: #f8fcff;
      padding: 8px 10px;
      color: #143451;
      font-size: 0.88rem;
    }

    .tracking-pill strong {
      display: block;
      color: #10324f;
      margin-top: 2px;
    }

    .tracking-steps {
      list-style: none;
      display: grid;
      gap: 10px;
      padding: 0;
      margin: 2px 0 0;
    }

    .tracking-step {
      border: 1px solid #d2e1ef;
      border-radius: 12px;
      padding: 10px 11px;
      background: #ffffff;
      color: #153958;
    }

    .tracking-step .step-title {
      font-weight: 700;
      display: block;
      margin-bottom: 2px;
    }

    .tracking-step .step-meta {
      font-size: 0.82rem;
      color: #55718a;
    }

    .tracking-step.active {
      border-color: #92bdd9;
      box-shadow: 0 0 0 3px rgba(0, 100, 145, 0.1);
      background: #f2f9ff;
    }

    .tracking-actions {
      display: flex;
      justify-content: flex-end;
      gap: 10px;
    }

    @media (max-width: 1050px) {
      .menu-grid {
        grid-template-columns: repeat(2, minmax(0, 1fr));
      }
    }

    @media (max-width: 760px) {
      .top-links {
        display: none;
      }

      .drawer-tab-toggle {
        top: auto;
        bottom: 14px;
        transform: none;
        border-radius: 999px;
        padding: 10px 14px;
        min-height: 0;
        min-width: 94px;
      }

      .drawer-tab-toggle:hover {
        transform: translateX(2px);
      }

      .drawer-tab-toggle.is-open {
        left: calc(min(86vw, 360px) - 72px);
        top: auto;
        bottom: 14px;
        transform: none;
      }

      .drawer-toggle-label.menu {
        transform: translate(-50%, -50%);
      }

      .drawer-tab-toggle.is-open .drawer-toggle-label.menu {
        transform: translate(-50%, -84%);
      }

      .left-drawer {
        width: min(86vw, 360px);
      }

      .auth-overlay {
        padding: 14px;
      }

      .auth-shell {
        padding: 18px 16px 16px;
        border-radius: 18px;
      }

      .auth-title {
        font-size: 1.22rem;
      }

      .auth-subtitle {
        font-size: 0.86rem;
      }

      .auth-switch-btn {
        padding: 9px 8px;
        font-size: 0.82rem;
      }

      .top-actions {
        gap: 8px;
      }

      .user-pill {
        display: none;
      }

      .logout-trigger {
        padding: 8px 12px;
        font-size: 0.82rem;
      }

      .hero-slider {
        height: calc(100vh - var(--topbar-height));
        height: calc(100dvh - var(--topbar-height));
      }

      .slide-content {
        max-width: 90vw;
        left: 10px;
        bottom: 8px;
      }

      .slide-content .badge {
        margin-bottom: 6px;
        padding: 4px 8px;
        font-size: 0.64rem;
      }

      .slide-content h1 {
        font-size: clamp(0.9rem, 4.2vw, 1.1rem);
        margin-bottom: 4px;
      }

      .slide-content > p:not(.badge) {
        display: none;
      }

      .slide-cta {
        padding: 6px 10px;
        font-size: 0.72rem;
      }

      .offer-add-btn {
        padding: 6px 10px;
        font-size: 0.72rem;
      }

      .slider-nav {
        width: 36px;
        height: 36px;
      }

      .menu-grid {
        grid-template-columns: 1fr;
      }

      .order-flow-overlay,
      .tracking-overlay {
        padding: 12px;
      }

      .order-flow-shell,
      .tracking-shell {
        border-radius: 16px;
        padding: 14px;
        width: min(100%, 100vw);
        max-height: 95dvh;
      }

      .order-flow-grid {
        grid-template-columns: 1fr;
      }

      .tracking-meta {
        grid-template-columns: 1fr;
      }

      .menu-card img {
        height: 210px;
      }

      .category-tabs {
        gap: 8px;
      }

      .category-tab {
        border-radius: 12px;
      }

      .category-tab .tab-label {
        padding: 9px 8px;
        font-size: 0.8rem;
      }

      .category-tab .tab-label small {
        font-size: 0.68rem;
      }
    }

    @media (prefers-reduced-motion: reduce) {
      .topbar {
        animation: none;
      }

      .rotating-pizza-loader,
      .rotating-pizza-loader::after {
        animation: none;
      }

      [data-scroll-animate] {
        opacity: 1;
        transform: none;
        transition: none;
      }
    }
  </style>
</head>
<body class="auth-locked">
  <div class="auth-overlay" id="authOverlay" role="dialog" aria-modal="true" aria-labelledby="pizzaLoginTitle">
    <div class="auth-shell">
      <div>
        <h2 class="auth-title" id="pizzaLoginTitle">Welcome to Pizza Shop</h2>
        <p class="auth-subtitle">Sign in to continue, or create an account to save your details for the next visit.</p>
      </div>

      <div class="auth-switch" role="tablist" aria-label="Authentication options">
        <button class="auth-switch-btn is-active" id="authSignInTab" type="button" role="tab" aria-selected="true" aria-controls="pizza-login-form" data-auth-view="signin">Sign In</button>
        <button class="auth-switch-btn" id="authSignUpTab" type="button" role="tab" aria-selected="false" aria-controls="pizza-signup-form" data-auth-view="signup">Sign Up</button>
      </div>

      <form class="auth-pane is-active" id="pizza-login-form" data-auth-pane="signin" role="tabpanel" aria-labelledby="authSignInTab">
        <div class="auth-grid">
          <div class="auth-group">
            <label for="pizza-login-email">Email Address</label>
            <input type="email" id="pizza-login-email" placeholder="user@example.com" required autocomplete="username">
          </div>
          <div class="auth-group">
            <label for="pizza-login-password">Password</label>
            <input type="password" id="pizza-login-password" placeholder="Enter your password" required autocomplete="current-password">
          </div>
        </div>
        <button class="auth-submit" id="pizzaSignInSubmit" type="submit">Sign In</button>
        <p class="auth-message" id="pizza-login-message"></p>
        <p class="auth-hint">Demo login available: <strong>user@example.com</strong> / <strong>password123</strong></p>
      </form>

      <form class="auth-pane" id="pizza-signup-form" data-auth-pane="signup" role="tabpanel" aria-labelledby="authSignUpTab" hidden>
        <div class="auth-grid">
          <div class="auth-group">
            <label for="pizza-signup-name">Full Name</label>
            <input type="text" id="pizza-signup-name" placeholder="Your name" required autocomplete="name">
          </div>
          <div class="auth-group">
            <label for="pizza-signup-email">Email Address</label>
            <input type="email" id="pizza-signup-email" placeholder="you@example.com" required autocomplete="email">
          </div>
          <div class="auth-group">
            <label for="pizza-signup-password">Create Password</label>
            <input type="password" id="pizza-signup-password" placeholder="Minimum 6 characters" required autocomplete="new-password">
          </div>
          <div class="auth-group">
            <label for="pizza-signup-confirm-password">Confirm Password</label>
            <input type="password" id="pizza-signup-confirm-password" placeholder="Re-enter password" required autocomplete="new-password">
          </div>
        </div>
        <button class="auth-submit" id="pizzaSignUpSubmit" type="submit">Create Account</button>
        <p class="auth-message" id="pizza-signup-message"></p>
        <p class="auth-hint">Accounts created here are stored in your browser for this device.</p>
      </form>
    </div>
  </div>

  <button class="drawer-tab-toggle" id="leftDrawerToggle" type="button" aria-controls="leftUtilityDrawer" aria-expanded="false" aria-label="Open side panel">
    <span class="drawer-toggle-label menu">Menu</span>
    <span class="drawer-toggle-label close">Close</span>
  </button>

  <aside class="left-drawer" id="leftUtilityDrawer" aria-hidden="true">
    <div class="drawer-head">
      <h3>Quick Access</h3>
      <button class="drawer-close" id="leftDrawerClose" type="button" aria-label="Close side panel">x</button>
    </div>
    <p class="drawer-user-status" id="drawerUserStatus">You are browsing as guest. Sign in to access personalized activity.</p>
    <div class="drawer-auth-actions">
      <button class="drawer-auth-btn" id="drawerSignInBtn" type="button">Sign In</button>
      <button class="drawer-auth-btn" id="drawerSignUpBtn" type="button">Sign Up</button>
      <button class="drawer-auth-btn signout" id="drawerSignOutBtn" type="button" disabled>Sign Out</button>
    </div>
    <nav class="drawer-section-nav" aria-label="Utility menu">
      <button class="drawer-section-btn active" type="button" data-drawer-section="coupons">Coupons &amp; Offers</button>
      <button class="drawer-section-btn" type="button" data-drawer-section="orders">Order History</button>
      <button class="drawer-section-btn" type="button" data-drawer-section="feedback">Feedback</button>
      <button class="drawer-section-btn" type="button" data-drawer-section="rewards">Reward History</button>
    </nav>
    <div class="drawer-content">
      <section class="drawer-panel active" data-drawer-panel="coupons">
        <h4>Coupons and Offers</h4>
        <p class="drawer-note">Apply these in checkout or ask support to validate current eligibility.</p>
        <ul class="drawer-list">
          <li><strong>WEEKEND20</strong><br>20% off on orders above Rs. 699.</li>
          <li><strong>CHEESE60</strong><br>Flat Rs. 60 off on orders above Rs. 499.</li>
          <li><strong>LATENIGHT50</strong><br>Flat Rs. 50 off after 10:00 PM.</li>
          <li><strong>Note</strong><br>Combo offer deals are not coupon eligible.</li>
        </ul>
      </section>
      <section class="drawer-panel" data-drawer-panel="orders">
        <h4>Order History</h4>
        <p class="drawer-note">Your most recent checkouts are listed here.</p>
        <ul class="drawer-order-list" id="drawerOrderHistoryList"></ul>
      </section>
      <section class="drawer-panel" data-drawer-panel="feedback">
        <h4>Feedback</h4>
        <p class="drawer-note">Share your experience so we can improve the pizza portal.</p>
        <form class="drawer-feedback-form" id="drawerFeedbackForm">
          <textarea id="drawerFeedbackText" placeholder="Write your feedback here..." required></textarea>
          <button type="submit">Submit Feedback</button>
          <p class="drawer-feedback-status" id="drawerFeedbackStatus"></p>
        </form>
      </section>
      <section class="drawer-panel" data-drawer-panel="rewards">
        <h4>Reward History</h4>
        <p class="drawer-note">Points are added when you complete an order.</p>
        <ul class="drawer-reward-list" id="drawerRewardHistoryList"></ul>
      </section>
    </div>
  </aside>
  <div class="left-drawer-backdrop" id="leftDrawerBackdrop" hidden></div>

  <header class="topbar">
    <div class="container topbar-inner">
      <a class="brand" href="#home"><span>Pizza</span> Shop</a>
      <ul class="top-links">
        <li><a href="#home">Home</a></li>
        <li><a href="#categories">Categories</a></li>
        <li><a href="#veg">Veg</a></li>
        <li><a href="#nonveg">Non Veg</a></li>
        <li><a href="#extras">Extras</a></li>
      </ul>
      <div class="top-actions">
        <div class="user-pill" id="userPill" hidden></div>
        <button class="logout-trigger" id="logoutBtn" type="button" hidden>Logout</button>
        <button class="cart-trigger" id="openCartBtn" type="button" aria-controls="cartPanel" aria-expanded="false">
          Cart
          <span id="cartCount">0</span>
        </button>
      </div>
    </div>
  </header>

  <main id="home">
    <section class="hero-section">
      <div class="container">
        <div class="hero-slider" id="heroSlider" aria-label="Newcomers and offers slides" data-scroll-animate data-anim-delay="80">
          <button class="slider-nav prev" id="prevSlide" type="button" aria-label="Previous slide">&#10094;</button>
          <button class="slider-nav next" id="nextSlide" type="button" aria-label="Next slide">&#10095;</button>

          <div class="slides-track" id="slidesTrack">
            <article class="slide active">
              <img src="https://images.unsplash.com/photo-1604382354936-07c5d9983bd3?auto=format&fit=crop&w=1800&q=80" alt="New paneer pizza offer">
              <div class="slide-overlay"></div>
              <div class="slide-content">
              <p class="badge">Newcomer</p>
              <h1>Paneer Royal Loaded - Intro Price Rs. 299</h1>
              <p>Try our newly launched paneer special with fresh capsicum, onion, and creamy makhani drizzle.</p>
              <div class="slide-action-row">
                <a class="slide-cta" href="#veg">Order Newcomer</a>
                <button class="offer-add-btn add-cart-btn" type="button" data-id="veg-2">Add to Cart</button>
              </div>
            </div>
          </article>

            <article class="slide">
              <img src="https://images.unsplash.com/photo-1513104890138-7c749659a591?auto=format&fit=crop&w=1800&q=80" alt="Buy one get one pizza offer">
              <div class="slide-overlay"></div>
              <div class="slide-content">
              <p class="badge offer">Offer</p>
              <h1>Buy 1 Get 1 Free On Medium Pizzas</h1>
              <p>Valid this week on all medium Veg and Non Veg pizzas. Add two pizzas to cart to enjoy this deal.</p>
              <div class="slide-action-row">
                <a class="slide-cta" href="#categories">View Menu</a>
                <button class="offer-add-btn add-cart-btn" type="button" data-id="nonveg-1">Add to Cart</button>
              </div>
            </div>
          </article>

            <article class="slide">
              <img src="https://images.unsplash.com/photo-1571407970349-bc81e7e96d47?auto=format&fit=crop&w=1800&q=80" alt="Stuffed crust newcomer pizza">
              <div class="slide-overlay"></div>
              <div class="slide-content">
              <p class="badge">Newcomer</p>
              <h1>Stuffed Crust Festival Starts At Rs. 349</h1>
              <p>Cheese-filled crust, rich toppings, and wood-baked aroma. Built for full-family nights.</p>
              <div class="slide-action-row">
                <a class="slide-cta" href="#nonveg">Try Stuffed Range</a>
                <button class="offer-add-btn add-cart-btn" type="button" data-id="nonveg-6">Add to Cart</button>
              </div>
            </div>
          </article>

            <article class="slide">
              <img src="https://images.unsplash.com/photo-1548365328-9f547fb0953e?auto=format&fit=crop&w=1800&q=80" alt="Family meal combo offer">
              <div class="slide-overlay"></div>
              <div class="slide-content">
              <p class="badge offer">Offer</p>
              <h1>Family Combo @ Rs. 799 With Extras</h1>
              <p>Get 2 regular pizzas, garlic breadsticks, and drinks at one value combo price.</p>
              <div class="slide-action-row">
                <a class="slide-cta" href="#extras">See Extras</a>
                <button class="offer-add-btn add-cart-btn" type="button" data-id="extra-1">Add to Cart</button>
              </div>
            </div>
          </article>

            <article class="slide">
              <img src="https://images.unsplash.com/photo-1594007654729-407eedc4be65?auto=format&fit=crop&w=1800&q=80" alt="Late night pizza delivery offer">
              <div class="slide-overlay"></div>
              <div class="slide-content">
              <p class="badge offer">Offer</p>
              <h1>Late Night Delivery Offer: Flat Rs. 100 Off</h1>
              <p>Order after 10 PM and save instantly. Perfect for work nights and game sessions.</p>
              <div class="slide-action-row">
                <a class="slide-cta" href="#categories">Start Order</a>
                <button class="offer-add-btn add-cart-btn" type="button" data-id="veg-1">Add to Cart</button>
              </div>
            </div>
          </article>
          </div>

          <div class="slider-dots" id="sliderDots" aria-label="Slider controls"></div>
        </div>
      </div>
    </section>

    <section class="categories-section" id="categories">
      <div class="container">
        <div class="section-head" data-scroll-animate data-slide-from="left" data-anim-delay="120">
          <h2>Categories</h2>
          <p>Scroll below and explore Veg, Non Veg, and Extras. Each category has 6 items with Add to Cart.</p>
        </div>

        <div class="category-tabs" role="tablist" aria-label="Pizza categories" data-scroll-animate data-slide-from="right" data-anim-delay="180">
          <button class="category-tab" type="button" role="tab" aria-selected="false" aria-controls="veg" data-tab-target="veg">
            <img src="https://images.unsplash.com/photo-1574071318508-1cdbab80d002?auto=format&fit=crop&w=1000&q=80" alt="Veg pizza category">
            <span class="tab-label">Veg <small>6 items</small></span>
          </button>
          <button class="category-tab" type="button" role="tab" aria-selected="false" aria-controls="nonveg" data-tab-target="nonveg">
            <img src="https://images.unsplash.com/photo-1513104890138-7c749659a591?auto=format&fit=crop&w=1000&q=80" alt="Non veg pizza category">
            <span class="tab-label">Non Veg <small>6 items</small></span>
          </button>
          <button class="category-tab" type="button" role="tab" aria-selected="false" aria-controls="extras" data-tab-target="extras">
            <img src="https://images.unsplash.com/photo-1619531038896-7c0d0ff0fe72?auto=format&fit=crop&w=1000&q=80" alt="Extras category">
            <span class="tab-label">Extras <small>6 items</small></span>
          </button>
        </div>

        <section class="category-block" id="veg" data-category="veg">
          <div class="category-head">
            <h3>Veg</h3>
            <span>6 Items</span>
          </div>
          <div class="category-content">
            <div class="menu-grid" id="vegGrid"></div>
          </div>
        </section>

        <section class="category-block" id="nonveg" data-category="nonveg">
          <div class="category-head">
            <h3>Non Veg</h3>
            <span>6 Items</span>
          </div>
          <div class="category-content">
            <div class="menu-grid" id="nonVegGrid"></div>
          </div>
        </section>

        <section class="category-block" id="extras" data-category="extras">
          <div class="category-head">
            <h3>Extras</h3>
            <span>6 Items</span>
          </div>
          <div class="category-content">
            <div class="menu-grid" id="extrasGrid"></div>
          </div>
        </section>
      </div>
    </section>
  </main>

  <footer class="footer" data-scroll-animate data-anim-delay="220">
    <div class="container">
      Pizza Shop (c) 2026 | Freshly baked, fast delivered.
    </div>
  </footer>

  <aside class="cart-panel" id="cartPanel" aria-hidden="true">
    <div class="cart-header">
      <h2>Your Cart</h2>
      <button class="close-cart" id="closeCartBtn" type="button">Close</button>
    </div>
    <p class="cart-subtitle">All selected pizzas and extras appear here.</p>
    <ul class="cart-items" id="cartItems"></ul>
    <div class="cart-footer">
      <div class="total-row">
        <span>Total Items</span>
        <strong id="totalItems">0</strong>
      </div>
      <div class="total-row">
        <span>Total Amount</span>
        <strong id="totalAmount">Rs. 0</strong>
      </div>
      <button class="checkout-btn" id="checkoutBtn" type="button" disabled>Proceed to Checkout</button>
    </div>
  </aside>
  <div class="cart-backdrop" id="cartBackdrop" hidden></div>

  <section class="order-flow-overlay hidden" id="orderFlowOverlay" role="dialog" aria-modal="true" aria-labelledby="orderFlowTitle">
    <div class="order-flow-shell">
      <div class="order-flow-head">
        <h2 id="orderFlowTitle">Finalize Your Order</h2>
        <button class="order-flow-close" id="closeOrderFlowBtn" type="button">Back to Cart</button>
      </div>
      <p class="order-flow-subtitle">Choose coupon, order type, and confirm. Combo offer deals do not allow coupons.</p>

      <div class="order-flow-grid">
        <section class="order-block">
          <h3>Selected Items</h3>
          <ul class="order-flow-items" id="orderFlowItems"></ul>
        </section>

        <section class="order-block">
          <h3>Coupons</h3>
          <div class="order-coupon-list">
            <label class="order-coupon-option" data-coupon-option>
              <input type="radio" name="orderCoupon" value="NONE" checked>
              <span>No Coupon<small>Pay regular order amount.</small></span>
            </label>
            <label class="order-coupon-option" data-coupon-option>
              <input type="radio" name="orderCoupon" value="WEEKEND20">
              <span>WEEKEND20<small>20% off on subtotal above Rs. 699.</small></span>
            </label>
            <label class="order-coupon-option" data-coupon-option>
              <input type="radio" name="orderCoupon" value="CHEESE60">
              <span>CHEESE60<small>Flat Rs. 60 off on subtotal above Rs. 499.</small></span>
            </label>
            <label class="order-coupon-option" data-coupon-option>
              <input type="radio" name="orderCoupon" value="LATENIGHT50">
              <span>LATENIGHT50<small>Flat Rs. 50 off after 10:00 PM.</small></span>
            </label>
          </div>
          <p class="coupon-note" id="orderCouponNote"></p>

          <h3>Order Type</h3>
          <div class="order-mode-list">
            <label class="order-mode-option">
              <input type="radio" name="orderMode" value="dine_in" checked>
              <span>Dine In<small>Eat at the restaurant.</small></span>
            </label>
            <label class="order-mode-option">
              <input type="radio" name="orderMode" value="take_away">
              <span>Take Away<small>Pick up from the store counter.</small></span>
            </label>
            <label class="order-mode-option">
              <input type="radio" name="orderMode" value="delivery">
              <span>Delivery<small>Delivered to your address.</small></span>
            </label>
          </div>

          <div class="price-breakdown">
            <div class="price-breakdown-row">
              <span>Subtotal</span>
              <strong id="orderFlowSubtotal">Rs. 0</strong>
            </div>
            <div class="price-breakdown-row discount">
              <span>Coupon Discount</span>
              <strong id="orderFlowDiscount">-Rs. 0</strong>
            </div>
            <div class="price-breakdown-row total">
              <span>Final Amount</span>
              <strong id="orderFlowFinalAmount">Rs. 0</strong>
            </div>
          </div>
        </section>
      </div>

      <div class="order-flow-actions">
        <button class="order-flow-btn secondary" id="orderFlowCancelBtn" type="button">Cancel</button>
        <button class="order-flow-btn primary" id="orderConfirmBtn" type="button">Confirm Order</button>
      </div>
      <div class="order-confirm-visual hidden" id="orderConfirmVisual" aria-hidden="true">
        <div class="rotating-pizza-loader"></div>
        <p class="order-confirm-caption">Chef is spinning your pizza into the oven...</p>
      </div>
      <p class="order-confirm-status" id="orderConfirmStatus"></p>
    </div>
  </section>

  <section class="tracking-overlay hidden" id="orderTrackingOverlay" role="dialog" aria-modal="true" aria-labelledby="trackingTitle">
    <div class="tracking-shell">
      <div class="tracking-head">
        <h2 id="trackingTitle">Track Your Order</h2>
        <button class="tracking-close" id="closeTrackingBtn" type="button">Close</button>
      </div>
      <p class="tracking-subtitle" id="trackingSubtitle">Your order is confirmed and being prepared.</p>
      <div class="tracking-meta">
        <p class="tracking-pill">Order ID<strong id="trackingOrderId">--</strong></p>
        <p class="tracking-pill">Order Type<strong id="trackingOrderType">--</strong></p>
        <p class="tracking-pill">Coupon Applied<strong id="trackingCoupon">None</strong></p>
        <p class="tracking-pill">Amount Paid<strong id="trackingAmount">Rs. 0</strong></p>
      </div>
      <ul class="tracking-steps">
        <li class="tracking-step active">
          <span class="step-title">Order Confirmed</span>
          <span class="step-meta" id="trackingStepConfirmedMeta">Just now</span>
        </li>
        <li class="tracking-step">
          <span class="step-title" id="trackingStepSecondaryTitle">Kitchen started</span>
          <span class="step-meta" id="trackingStepSecondaryMeta">Estimated update in a few minutes</span>
        </li>
        <li class="tracking-step">
          <span class="step-title" id="trackingStepFinalTitle">Ready soon</span>
          <span class="step-meta" id="trackingStepFinalMeta">Please keep this screen for reference</span>
        </li>
      </ul>
      <div class="tracking-actions">
        <button class="order-flow-btn secondary" id="startNewOrderBtn" type="button">Start New Order</button>
      </div>
    </div>
  </section>

  <script>
    const AUTH_USERS_KEY = "pizza_auth_users_v1";
    const AUTH_SESSION_KEY = "pizza_auth_session_v1";
    const ORDER_HISTORY_KEY = "pizza_order_history_v1";
    const REWARD_HISTORY_KEY = "pizza_reward_history_v1";
    const FEEDBACK_HISTORY_KEY = "pizza_feedback_history_v1";
    const BACKEND_PORT = "3000";
    const DEMO_USER = {
      email: "user@example.com",
      password: "password123",
      name: "Demo User"
    };
    const ORDER_CONFIRM_DELAY_MS = 5000;
    const ORDER_TYPE_LABELS = {
      dine_in: "Dine In",
      take_away: "Take Away",
      delivery: "Delivery"
    };

    const authOverlay = document.getElementById("authOverlay");
    const authSwitchButtons = Array.from(document.querySelectorAll(".auth-switch-btn"));
    const authPanes = Array.from(document.querySelectorAll(".auth-pane"));
    const loginForm = document.getElementById("pizza-login-form");
    const signupForm = document.getElementById("pizza-signup-form");
    const loginMessage = document.getElementById("pizza-login-message");
    const signupMessage = document.getElementById("pizza-signup-message");
    const signInSubmitBtn = document.getElementById("pizzaSignInSubmit");
    const signUpSubmitBtn = document.getElementById("pizzaSignUpSubmit");
    const loginEmailInput = document.getElementById("pizza-login-email");
    const loginPasswordInput = document.getElementById("pizza-login-password");
    const signupNameInput = document.getElementById("pizza-signup-name");
    const signupEmailInput = document.getElementById("pizza-signup-email");
    const signupPasswordInput = document.getElementById("pizza-signup-password");
    const signupConfirmInput = document.getElementById("pizza-signup-confirm-password");
    const userPill = document.getElementById("userPill");
    const logoutBtn = document.getElementById("logoutBtn");
    const drawerToggleBtn = document.getElementById("leftDrawerToggle");
    const drawerPanel = document.getElementById("leftUtilityDrawer");
    const drawerCloseBtn = document.getElementById("leftDrawerClose");
    const drawerBackdrop = document.getElementById("leftDrawerBackdrop");
    const drawerSectionButtons = Array.from(document.querySelectorAll(".drawer-section-btn"));
    const drawerPanels = Array.from(document.querySelectorAll(".drawer-panel"));
    const drawerSignInBtn = document.getElementById("drawerSignInBtn");
    const drawerSignUpBtn = document.getElementById("drawerSignUpBtn");
    const drawerSignOutBtn = document.getElementById("drawerSignOutBtn");
    const drawerUserStatus = document.getElementById("drawerUserStatus");
    const drawerOrderHistoryList = document.getElementById("drawerOrderHistoryList");
    const drawerRewardHistoryList = document.getElementById("drawerRewardHistoryList");
    const drawerFeedbackForm = document.getElementById("drawerFeedbackForm");
    const drawerFeedbackText = document.getElementById("drawerFeedbackText");
    const drawerFeedbackStatus = document.getElementById("drawerFeedbackStatus");
    const orderFlowOverlay = document.getElementById("orderFlowOverlay");
    const closeOrderFlowBtn = document.getElementById("closeOrderFlowBtn");
    const orderFlowCancelBtn = document.getElementById("orderFlowCancelBtn");
    const orderFlowItems = document.getElementById("orderFlowItems");
    const orderCouponNote = document.getElementById("orderCouponNote");
    const orderFlowSubtotal = document.getElementById("orderFlowSubtotal");
    const orderFlowDiscount = document.getElementById("orderFlowDiscount");
    const orderFlowFinalAmount = document.getElementById("orderFlowFinalAmount");
    const orderConfirmBtn = document.getElementById("orderConfirmBtn");
    const orderConfirmVisual = document.getElementById("orderConfirmVisual");
    const orderConfirmStatus = document.getElementById("orderConfirmStatus");
    const couponInputs = Array.from(document.querySelectorAll("input[name='orderCoupon']"));
    const couponOptionCards = Array.from(document.querySelectorAll("[data-coupon-option]"));
    const modeInputs = Array.from(document.querySelectorAll("input[name='orderMode']"));
    const orderTrackingOverlay = document.getElementById("orderTrackingOverlay");
    const closeTrackingBtn = document.getElementById("closeTrackingBtn");
    const startNewOrderBtn = document.getElementById("startNewOrderBtn");
    const trackingSubtitle = document.getElementById("trackingSubtitle");
    const trackingOrderId = document.getElementById("trackingOrderId");
    const trackingOrderType = document.getElementById("trackingOrderType");
    const trackingCoupon = document.getElementById("trackingCoupon");
    const trackingAmount = document.getElementById("trackingAmount");
    const trackingStepConfirmedMeta = document.getElementById("trackingStepConfirmedMeta");
    const trackingStepSecondaryTitle = document.getElementById("trackingStepSecondaryTitle");
    const trackingStepSecondaryMeta = document.getElementById("trackingStepSecondaryMeta");
    const trackingStepFinalTitle = document.getElementById("trackingStepFinalTitle");
    const trackingStepFinalMeta = document.getElementById("trackingStepFinalMeta");
    let currentSessionUser = null;
    let orderDraft = null;
    let confirmOrderTimer = null;
    let confirmOrderCountdown = null;

    function clearConfirmOrderTimers() {
      if (confirmOrderTimer) {
        clearTimeout(confirmOrderTimer);
        confirmOrderTimer = null;
      }
      if (confirmOrderCountdown) {
        clearInterval(confirmOrderCountdown);
        confirmOrderCountdown = null;
      }
    }

    function resetOrderConfirmState() {
      clearConfirmOrderTimers();
      orderConfirmBtn.disabled = false;
      closeOrderFlowBtn.disabled = false;
      orderFlowCancelBtn.disabled = false;
      orderFlowCancelBtn.textContent = "Cancel";
      orderConfirmVisual.classList.add("hidden");
      orderConfirmVisual.setAttribute("aria-hidden", "true");
      couponInputs.forEach((input) => {
        input.disabled = false;
      });
      modeInputs.forEach((input) => {
        input.disabled = false;
      });
    }

    function normalizeEmail(value) {
      return String(value || "").trim().toLowerCase();
    }

    function inferNameFromEmail(email) {
      const localPart = normalizeEmail(email).split("@")[0] || "guest";
      const formatted = localPart.replace(/[._-]+/g, " ").trim();
      return formatted
        .split(" ")
        .filter(Boolean)
        .map((piece) => piece.charAt(0).toUpperCase() + piece.slice(1))
        .join(" ") || "Guest";
    }

    function escapeHtml(value) {
      return String(value || "")
        .replace(/&/g, "&amp;")
        .replace(/</g, "&lt;")
        .replace(/>/g, "&gt;")
        .replace(/"/g, "&quot;")
        .replace(/'/g, "&#39;");
    }

    function formatDrawerINR(value) {
      return new Intl.NumberFormat("en-IN", {
        style: "currency",
        currency: "INR",
        maximumFractionDigits: 0
      }).format(Number(value) || 0);
    }

    function readListStorage(key) {
      try {
        const value = localStorage.getItem(key);
        if (!value) {
          return [];
        }
        const parsed = JSON.parse(value);
        return Array.isArray(parsed) ? parsed : [];
      } catch (error) {
        return [];
      }
    }

    function writeListStorage(key, values) {
      localStorage.setItem(key, JSON.stringify(values));
    }

    function getApiUrlCandidates(path) {
      const cleanPath = path.startsWith("/") ? path : `/${path}`;
      const localApi = `http://localhost:${BACKEND_PORT}${cleanPath}`;
      const sameOriginApi = cleanPath;
      const isFileProtocol = window.location.protocol === "file:";
      const isNonBackendPort = window.location.port && window.location.port !== BACKEND_PORT;
      if (isFileProtocol || isNonBackendPort) {
        return [localApi, sameOriginApi];
      }
      return [sameOriginApi, localApi];
    }

    async function apiRequest(path, options = {}) {
      const candidates = getApiUrlCandidates(path);
      let lastError = null;

      for (const url of candidates) {
        try {
          const response = await fetch(url, options);
          const raw = await response.text();
          let data = {};
          if (raw) {
            try {
              data = JSON.parse(raw);
            } catch (parseError) {
              data = {};
            }
          }

          if (!response.ok) {
            throw new Error(data.error || `Request failed (${response.status})`);
          }

          return data;
        } catch (error) {
          lastError = error;
        }
      }

      throw lastError || new Error(`API call failed for ${path}`);
    }

    function readLocalUsers() {
      try {
        const value = localStorage.getItem(AUTH_USERS_KEY);
        if (!value) {
          return [];
        }
        const parsed = JSON.parse(value);
        if (!Array.isArray(parsed)) {
          return [];
        }
        return parsed;
      } catch (error) {
        return [];
      }
    }

    function writeLocalUsers(users) {
      localStorage.setItem(AUTH_USERS_KEY, JSON.stringify(users));
    }

    function findLocalUser(email) {
      const normalized = normalizeEmail(email);
      if (!normalized) {
        return null;
      }
      return readLocalUsers().find((user) => normalizeEmail(user.email) === normalized) || null;
    }

    function saveSession(user) {
      localStorage.setItem(AUTH_SESSION_KEY, JSON.stringify({
        email: normalizeEmail(user.email),
        name: String(user.name || inferNameFromEmail(user.email)),
        source: String(user.source || "local")
      }));
    }

    function readSession() {
      try {
        const value = localStorage.getItem(AUTH_SESSION_KEY);
        if (!value) {
          return null;
        }
        const parsed = JSON.parse(value);
        const email = normalizeEmail(parsed?.email);
        if (!email) {
          return null;
        }
        return {
          email,
          name: String(parsed?.name || inferNameFromEmail(email)),
          source: String(parsed?.source || "local")
        };
      } catch (error) {
        return null;
      }
    }

    function clearSession() {
      localStorage.removeItem(AUTH_SESSION_KEY);
    }

    function openDrawer() {
      drawerPanel.classList.add("open");
      drawerPanel.setAttribute("aria-hidden", "false");
      drawerToggleBtn.classList.add("is-open");
      drawerToggleBtn.setAttribute("aria-expanded", "true");
      drawerToggleBtn.setAttribute("aria-label", "Close side panel");
      drawerBackdrop.hidden = false;
      requestAnimationFrame(() => drawerBackdrop.classList.add("show"));
      document.body.classList.add("drawer-open");
    }

    function closeDrawer() {
      drawerPanel.classList.remove("open");
      drawerPanel.setAttribute("aria-hidden", "true");
      drawerToggleBtn.classList.remove("is-open");
      drawerToggleBtn.setAttribute("aria-expanded", "false");
      drawerToggleBtn.setAttribute("aria-label", "Open side panel");
      drawerBackdrop.classList.remove("show");
      document.body.classList.remove("drawer-open");
      setTimeout(() => {
        if (!drawerBackdrop.classList.contains("show")) {
          drawerBackdrop.hidden = true;
        }
      }, 210);
    }

    function setDrawerSection(sectionKey) {
      const target = sectionKey || "coupons";
      drawerSectionButtons.forEach((button) => {
        const isActive = button.dataset.drawerSection === target;
        button.classList.toggle("active", isActive);
      });
      drawerPanels.forEach((panel) => {
        panel.classList.toggle("active", panel.dataset.drawerPanel === target);
      });
    }

    function renderOrderHistory() {
      const orders = readListStorage(ORDER_HISTORY_KEY);
      if (!orders.length) {
        drawerOrderHistoryList.innerHTML = `<li class="drawer-empty">No orders yet. Place your first order and checkout to populate history.</li>`;
        return;
      }

      drawerOrderHistoryList.innerHTML = orders.slice(0, 10).map((order) => {
        const orderId = escapeHtml(order.id || "Order");
        const created = new Date(order.placedAt || order.createdAt || Date.now());
        const dateLabel = Number.isNaN(created.getTime()) ? "Unknown date" : created.toLocaleString("en-IN");
        const amount = formatDrawerINR(order.amount || 0);
        const count = Number(order.itemCount) || 0;
        const modeLabel = ORDER_TYPE_LABELS[order.orderType] || "Order";
        const couponLabel = order.couponCode && order.couponCode !== "NONE" ? String(order.couponCode) : "No coupon";
        return `
          <li class="drawer-order-item">
            <strong>${orderId}</strong>
            <span>${count} item${count === 1 ? "" : "s"} - ${amount} (${escapeHtml(modeLabel)})</span>
            <span>${escapeHtml(couponLabel)}</span>
            <span>${escapeHtml(dateLabel)}</span>
          </li>
        `;
      }).join("");
    }

    function renderRewardHistory() {
      const rewards = readListStorage(REWARD_HISTORY_KEY);
      if (!rewards.length) {
        drawerRewardHistoryList.innerHTML = `<li class="drawer-empty">No rewards yet. Rewards will appear after completed checkouts.</li>`;
        return;
      }

      drawerRewardHistoryList.innerHTML = rewards.slice(0, 12).map((entry) => {
        const created = new Date(entry.createdAt || Date.now());
        const dateLabel = Number.isNaN(created.getTime()) ? "Unknown date" : created.toLocaleDateString("en-IN");
        const reason = escapeHtml(entry.reason || "Order reward");
        const points = Number(entry.points) || 0;
        return `
          <li class="drawer-reward-item">
            <strong>+${points} points</strong>
            <span>${reason}</span>
            <span>${dateLabel}</span>
          </li>
        `;
      }).join("");
    }

    function setDrawerFeedbackStatus(message, tone = "info") {
      if (!message) {
        drawerFeedbackStatus.textContent = "";
        drawerFeedbackStatus.style.color = "#5d7389";
        return;
      }
      drawerFeedbackStatus.textContent = message;
      if (tone === "error") {
        drawerFeedbackStatus.style.color = "#b11b34";
      } else if (tone === "success") {
        drawerFeedbackStatus.style.color = "#1c6a39";
      } else {
        drawerFeedbackStatus.style.color = "#1c5779";
      }
    }

    function syncDrawerAuthState(sessionUser) {
      if (sessionUser) {
        drawerUserStatus.textContent = `Signed in as ${sessionUser.name} (${sessionUser.email})`;
        drawerSignOutBtn.disabled = false;
      } else {
        drawerUserStatus.textContent = "You are browsing as guest. Sign in to access personalized activity.";
        drawerSignOutBtn.disabled = true;
      }
    }

    function openAuthModal(view = "signin") {
      authOverlay.classList.remove("hidden");
      document.body.classList.add("auth-locked");
      setAuthView(view);
    }

    function performSignOut() {
      clearSession();
      applySignedOutState();
    }

    function setAuthMessage(element, message, tone = "info") {
      if (!element) {
        return;
      }
      if (!message) {
        element.textContent = "";
        element.className = "auth-message";
        return;
      }
      element.textContent = message;
      element.className = `auth-message ${tone} show`;
    }

    function clearAuthMessages() {
      setAuthMessage(loginMessage, "");
      setAuthMessage(signupMessage, "");
    }

    function setAuthView(view) {
      const targetView = view === "signup" ? "signup" : "signin";

      authSwitchButtons.forEach((button) => {
        const isActive = button.dataset.authView === targetView;
        button.classList.toggle("is-active", isActive);
        button.setAttribute("aria-selected", String(isActive));
      });

      authPanes.forEach((pane) => {
        const isActive = pane.dataset.authPane === targetView;
        pane.classList.toggle("is-active", isActive);
        pane.hidden = !isActive;
      });

      clearAuthMessages();
    }

    function updateHeaderForUser(sessionUser) {
      userPill.textContent = `${sessionUser.name} (${sessionUser.email})`;
      userPill.hidden = false;
      logoutBtn.hidden = false;
    }

    function applySignedInState(sessionUser) {
      authOverlay.classList.add("hidden");
      document.body.classList.remove("auth-locked");
      currentSessionUser = sessionUser;
      updateHeaderForUser(sessionUser);
      syncDrawerAuthState(sessionUser);
    }

    function applySignedOutState() {
      authOverlay.classList.remove("hidden");
      document.body.classList.add("auth-locked");
      currentSessionUser = null;
      userPill.hidden = true;
      logoutBtn.hidden = true;
      loginForm.reset();
      signupForm.reset();
      setAuthView("signin");
      syncDrawerAuthState(null);
      if (drawerPanel.classList.contains("open")) {
        closeDrawer();
      }
    }

    function authenticateLocal(email, password) {
      const normalizedEmail = normalizeEmail(email);
      const rawPassword = String(password || "");

      if (normalizedEmail === DEMO_USER.email && rawPassword === DEMO_USER.password) {
        return { email: DEMO_USER.email, name: DEMO_USER.name, source: "demo" };
      }

      const localUser = findLocalUser(normalizedEmail);
      if (!localUser || String(localUser.password) !== rawPassword) {
        return null;
      }

      return {
        email: normalizedEmail,
        name: String(localUser.name || inferNameFromEmail(normalizedEmail)),
        source: "local"
      };
    }

    async function authenticateBackend(email, password) {
      const response = await apiRequest("/api/auth/login", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          email,
          password,
          role: "user"
        })
      });

      const resolvedEmail = normalizeEmail(response?.user?.email || email);
      return {
        email: resolvedEmail,
        name: String(response?.user?.name || inferNameFromEmail(resolvedEmail)),
        source: "backend"
      };
    }

    authSwitchButtons.forEach((button) => {
      button.addEventListener("click", () => setAuthView(button.dataset.authView));
    });

    drawerToggleBtn.addEventListener("click", () => {
      if (drawerPanel.classList.contains("open")) {
        closeDrawer();
      } else {
        openDrawer();
      }
    });

    drawerCloseBtn.addEventListener("click", closeDrawer);
    drawerBackdrop.addEventListener("click", closeDrawer);

    drawerSectionButtons.forEach((button) => {
      button.addEventListener("click", () => {
        setDrawerSection(button.dataset.drawerSection);
      });
    });

    drawerSignInBtn.addEventListener("click", () => {
      closeDrawer();
      openAuthModal("signin");
    });

    drawerSignUpBtn.addEventListener("click", () => {
      closeDrawer();
      openAuthModal("signup");
    });

    drawerSignOutBtn.addEventListener("click", performSignOut);

    drawerFeedbackForm.addEventListener("submit", (event) => {
      event.preventDefault();
      setDrawerFeedbackStatus("");

      const text = String(drawerFeedbackText.value || "").trim();
      if (text.length < 8) {
        setDrawerFeedbackStatus("Please enter at least 8 characters.", "error");
        return;
      }

      const feedbackEntries = readListStorage(FEEDBACK_HISTORY_KEY);
      feedbackEntries.unshift({
        message: text,
        submittedAt: new Date().toISOString()
      });
      writeListStorage(FEEDBACK_HISTORY_KEY, feedbackEntries.slice(0, 50));
      drawerFeedbackForm.reset();
      setDrawerFeedbackStatus("Feedback submitted. Thank you!", "success");
    });

    loginForm.addEventListener("submit", async (event) => {
      event.preventDefault();
      clearAuthMessages();

      const email = normalizeEmail(loginEmailInput.value);
      const password = String(loginPasswordInput.value || "");

      if (!email || !password) {
        setAuthMessage(loginMessage, "Enter both email and password.", "error");
        return;
      }

      signInSubmitBtn.disabled = true;
      signInSubmitBtn.textContent = "Signing In...";

      try {
        let sessionUser = null;

        try {
          sessionUser = await authenticateBackend(email, password);
        } catch (error) {
          sessionUser = authenticateLocal(email, password);

          if (!sessionUser) {
            const err = String(error?.message || "").toLowerCase();
            if (err.includes("invalid credentials")) {
              setAuthMessage(loginMessage, "Invalid credentials. Use your registered account or the demo login.", "error");
            } else {
              setAuthMessage(loginMessage, "Server unavailable. Use Sign Up to create a local account, then sign in.", "error");
            }
            return;
          }

          if (sessionUser.source === "demo") {
            setAuthMessage(loginMessage, "Signed in using demo account (offline mode).", "info");
          } else {
            setAuthMessage(loginMessage, "Signed in using your locally created account.", "info");
          }
        }

        saveSession(sessionUser);
        applySignedInState(sessionUser);
      } finally {
        signInSubmitBtn.disabled = false;
        signInSubmitBtn.textContent = "Sign In";
      }
    });

    signupForm.addEventListener("submit", (event) => {
      event.preventDefault();
      clearAuthMessages();

      const name = String(signupNameInput.value || "").trim();
      const email = normalizeEmail(signupEmailInput.value);
      const password = String(signupPasswordInput.value || "");
      const confirmPassword = String(signupConfirmInput.value || "");

      if (name.length < 2) {
        setAuthMessage(signupMessage, "Enter your full name (at least 2 characters).", "error");
        return;
      }

      if (!email || !email.includes("@") || !email.includes(".")) {
        setAuthMessage(signupMessage, "Enter a valid email address.", "error");
        return;
      }

      if (password.length < 6) {
        setAuthMessage(signupMessage, "Password must be at least 6 characters long.", "error");
        return;
      }

      if (password !== confirmPassword) {
        setAuthMessage(signupMessage, "Passwords do not match.", "error");
        return;
      }

      if (email === DEMO_USER.email) {
        setAuthMessage(signupMessage, "This email is reserved for demo login. Use a different email.", "error");
        return;
      }

      signUpSubmitBtn.disabled = true;
      signUpSubmitBtn.textContent = "Creating...";

      try {
        const users = readLocalUsers();
        const duplicate = users.some((user) => normalizeEmail(user.email) === email);
        if (duplicate) {
          setAuthMessage(signupMessage, "Account already exists. Please sign in.", "error");
          return;
        }

        const createdUser = {
          name,
          email,
          password,
          createdAt: new Date().toISOString()
        };
        users.unshift(createdUser);
        writeLocalUsers(users);

        const sessionUser = { email, name, source: "local" };
        saveSession(sessionUser);
        setAuthMessage(signupMessage, "Account created. You are now signed in.", "success");
        applySignedInState(sessionUser);
      } finally {
        signUpSubmitBtn.disabled = false;
        signUpSubmitBtn.textContent = "Create Account";
      }
    });

    logoutBtn.addEventListener("click", performSignOut);

    setDrawerSection("coupons");
    renderOrderHistory();
    renderRewardHistory();
    syncDrawerAuthState(null);
    setDrawerFeedbackStatus("");

    const existingSession = readSession();
    if (existingSession) {
      applySignedInState(existingSession);
    } else {
      applySignedOutState();
    }

    const menuData = {
      veg: [
        {
          id: "veg-1",
          name: "Margherita Classic",
          description: "Fresh tomato sauce, mozzarella, basil leaves.",
          price: 249,
          image: "https://images.unsplash.com/photo-1574071318508-1cdbab80d002?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "veg-2",
          name: "Paneer Tikka Supreme",
          description: "Paneer tikka cubes, onion, capsicum, smoky spices.",
          price: 329,
          image: "https://images.unsplash.com/photo-1628840042765-356cda07504e?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "veg-3",
          name: "Farm Fresh Delight",
          description: "Mushroom, sweet corn, tomato, onion and cheese.",
          price: 319,
          image: "https://images.unsplash.com/photo-1593560708920-61dd98c46a4e?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "veg-4",
          name: "Veggie Overload",
          description: "Double veggies, jalapeno, black olive, extra cheese.",
          price: 349,
          image: "https://images.unsplash.com/photo-1604382355076-af4b0eb60143?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "veg-5",
          name: "Corn & Cheese Burst",
          description: "Golden corn, mozzarella blend, creamy base sauce.",
          price: 289,
          image: "https://images.unsplash.com/photo-1565299507177-b0ac66763828?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "veg-6",
          name: "Tandoori Veg Special",
          description: "Tandoori sauce, paneer, onion, capsicum and herbs.",
          price: 339,
          image: "https://images.unsplash.com/photo-1600628422019-783d5ad7f111?auto=format&fit=crop&w=1200&q=80"
        }
      ],
      nonVeg: [
        {
          id: "nonveg-1",
          name: "Pepper Barbecue Chicken",
          description: "Barbecue chicken, onion, mozzarella, smoky drizzle.",
          price: 379,
          image: "https://images.unsplash.com/photo-1513104890138-7c749659a591?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "nonveg-2",
          name: "Chicken Dominator",
          description: "Loaded chicken toppings with rich tomato sauce.",
          price: 459,
          image: "https://images.unsplash.com/photo-1620374645356-6318d88f5b46?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "nonveg-3",
          name: "Chicken Sausage Fiesta",
          description: "Chicken sausage slices, onion, capsicum, oregano.",
          price: 369,
          image: "https://images.unsplash.com/photo-1541745537411-b8046dc6d66c?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "nonveg-4",
          name: "Keema Do Pyaza",
          description: "Spiced chicken keema, double onion, mozzarella.",
          price: 399,
          image: "https://images.unsplash.com/photo-1601924582970-9238bcb495d9?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "nonveg-5",
          name: "Peri Peri Chicken",
          description: "Peri peri chicken chunks, jalapeno and cheese.",
          price: 409,
          image: "https://images.unsplash.com/photo-1590947132387-155cc02f3212?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "nonveg-6",
          name: "Spicy Chicken Supreme",
          description: "Spicy chicken, red paprika, onion and chili flakes.",
          price: 429,
          image: "https://images.unsplash.com/photo-1611273426858-4506f43c9fce?auto=format&fit=crop&w=1200&q=80"
        }
      ],
      extras: [
        {
          id: "extra-1",
          name: "Family Combo Deal",
          description: "2 regular pizzas, garlic breadsticks, and drinks at combo pricing.",
          price: 799,
          isCombo: true,
          image: "https://images.unsplash.com/photo-1619531038896-7c0d0ff0fe72?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "extra-2",
          name: "Stuffed Garlic Bread",
          description: "Cheese stuffed bread with italian seasoning.",
          price: 199,
          image: "https://images.unsplash.com/photo-1509440159596-0249088772ff?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "extra-3",
          name: "Choco Lava Cake",
          description: "Warm dessert cake with molten chocolate center.",
          price: 129,
          image: "https://images.unsplash.com/photo-1541783245831-57d6fb0926d3?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "extra-4",
          name: "Cheesy Jalapeno Dip",
          description: "Creamy cheese dip with jalapeno kick.",
          price: 59,
          image: "https://images.unsplash.com/photo-1612198507804-53f29dcf8d13?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "extra-5",
          name: "Masala Cola (500ml)",
          description: "Chilled fizzy drink to pair with hot pizza.",
          price: 89,
          image: "https://images.unsplash.com/photo-1544145945-f90425340c7e?auto=format&fit=crop&w=1200&q=80"
        },
        {
          id: "extra-6",
          name: "Veg Pasta Italiano",
          description: "Creamy pasta with vegetables and herbs.",
          price: 179,
          image: "https://images.unsplash.com/photo-1621996346565-e3dbc646d9a9?auto=format&fit=crop&w=1200&q=80"
        }
      ]
    };

    const allItems = [
      ...menuData.veg,
      ...menuData.nonVeg,
      ...menuData.extras
    ];

    const itemLookup = new Map(allItems.map((item) => [item.id, item]));

    const formatINR = (value) => new Intl.NumberFormat("en-IN", {
      style: "currency",
      currency: "INR",
      maximumFractionDigits: 0
    }).format(value);

    function getSelectedCouponCode() {
      const selected = couponInputs.find((input) => input.checked);
      return selected ? selected.value : "NONE";
    }

    function getSelectedOrderMode() {
      const selected = modeInputs.find((input) => input.checked);
      return selected ? selected.value : "dine_in";
    }

    function isLateNightEligible() {
      const hour = new Date().getHours();
      return hour >= 22 || hour < 4;
    }

    function calculateCouponDiscount(subtotal, couponCode, comboBlocked) {
      if (comboBlocked || !subtotal) {
        return 0;
      }

      if (couponCode === "WEEKEND20" && subtotal >= 699) {
        return Math.round(subtotal * 0.2);
      }

      if (couponCode === "CHEESE60" && subtotal >= 499) {
        return 60;
      }

      if (couponCode === "LATENIGHT50" && isLateNightEligible()) {
        return 50;
      }

      return 0;
    }

    const vegGrid = document.getElementById("vegGrid");
    const nonVegGrid = document.getElementById("nonVegGrid");
    const extrasGrid = document.getElementById("extrasGrid");

    function cardTemplate(item) {
      return `
        <article class="menu-card">
          <img src="${item.image}" alt="${item.name}" loading="lazy">
          <div class="menu-content">
            <h4>${item.name}</h4>
            <p>${item.description}</p>
            <div class="menu-bottom">
              <span class="price">${formatINR(item.price)}</span>
              <button class="add-cart-btn" type="button" data-id="${item.id}">Add to Cart</button>
            </div>
          </div>
        </article>
      `;
    }

    function renderMenu() {
      vegGrid.innerHTML = menuData.veg.map(cardTemplate).join("");
      nonVegGrid.innerHTML = menuData.nonVeg.map(cardTemplate).join("");
      extrasGrid.innerHTML = menuData.extras.map(cardTemplate).join("");
    }

    renderMenu();

    const categoryTabs = Array.from(document.querySelectorAll(".category-tab"));
    const categoryBlocks = Array.from(document.querySelectorAll(".category-block"));
    const scrollAnimatedNodes = Array.from(document.querySelectorAll("[data-scroll-animate]"));

    function initializeScrollAnimations() {
      if (!scrollAnimatedNodes.length) {
        return;
      }

      scrollAnimatedNodes.forEach((element, index) => {
        const parsedDelay = Number(element.dataset.animDelay);
        const delay = Number.isFinite(parsedDelay) ? parsedDelay : Math.min(index * 90, 420);
        element.style.setProperty("--scroll-anim-delay", `${delay}ms`);
      });

      const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
      if (prefersReducedMotion || typeof IntersectionObserver !== "function") {
        scrollAnimatedNodes.forEach((element) => element.classList.add("in-view"));
        return;
      }

      const observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add("in-view");
            observer.unobserve(entry.target);
          }
        });
      }, {
        threshold: 0.14,
        rootMargin: "0px 0px -6% 0px"
      });

      scrollAnimatedNodes.forEach((element) => observer.observe(element));
    }

    function applyCardStagger() {
      document.querySelectorAll(".menu-grid").forEach((grid) => {
        grid.querySelectorAll(".menu-card").forEach((card, index) => {
          card.style.setProperty("--item-delay", `${index * 45}ms`);
        });
      });
    }

    function closeAllCategories() {
      categoryTabs.forEach((tab) => {
        tab.classList.remove("active");
        tab.setAttribute("aria-selected", "false");
      });

      categoryBlocks.forEach((block) => {
        block.classList.remove("is-open");
        const content = block.querySelector(".category-content");
        if (content) {
          content.style.maxHeight = "0px";
        }
      });
    }

    function setActiveCategory(categoryId, options = {}) {
      const { smoothScroll = false, toggleIfActive = false } = options;
      const openBlock = document.querySelector(".category-block.is-open");
      const isAlreadyOpen = openBlock && openBlock.id === categoryId;

      if (toggleIfActive && isAlreadyOpen) {
        closeAllCategories();
        return;
      }

      categoryTabs.forEach((tab) => {
        const isActive = tab.dataset.tabTarget === categoryId;
        tab.classList.toggle("active", isActive);
        tab.setAttribute("aria-selected", String(isActive));
      });

      categoryBlocks.forEach((block) => {
        const content = block.querySelector(".category-content");
        const isOpen = block.id === categoryId;
        block.classList.toggle("is-open", isOpen);
        if (!content) {
          return;
        }

        if (isOpen) {
          content.style.maxHeight = "5000px";
        } else {
          content.style.maxHeight = "0px";
        }
      });

      if (smoothScroll) {
        const target = document.getElementById(categoryId);
        if (target) {
          target.scrollIntoView({ behavior: "smooth", block: "start" });
        }
      }
    }

    function refreshOpenCategoryHeight() {
      document.querySelectorAll(".category-block.is-open .category-content").forEach((openContent) => {
        openContent.style.maxHeight = "5000px";
      });
    }

    function bindCategoryImageResizeFix() {
      document.querySelectorAll(".menu-grid img").forEach((image) => {
        if (!image.complete) {
          image.addEventListener("load", refreshOpenCategoryHeight, { once: true });
        }
      });
    }

    categoryTabs.forEach((tab) => {
      tab.addEventListener("click", () => {
        setActiveCategory(tab.dataset.tabTarget, { smoothScroll: true, toggleIfActive: true });
      });
    });

    document.querySelectorAll(".category-head").forEach((head) => {
      head.addEventListener("click", () => {
        const parent = head.closest(".category-block");
        if (parent) {
          setActiveCategory(parent.id, { toggleIfActive: true });
        }
      });
    });

    window.addEventListener("resize", refreshOpenCategoryHeight);
    window.addEventListener("load", refreshOpenCategoryHeight);

    const handleHashCategory = () => {
      const hash = window.location.hash.replace("#", "");
      if (["veg", "nonveg", "extras"].includes(hash)) {
        setActiveCategory(hash);
      } else {
        closeAllCategories();
      }
    };

    window.addEventListener("hashchange", handleHashCategory);

    const categoryRevealObserver = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add("revealed");
          categoryRevealObserver.unobserve(entry.target);
        }
      });
    }, { threshold: 0.16 });

    categoryBlocks.forEach((block) => categoryRevealObserver.observe(block));

    applyCardStagger();
    bindCategoryImageResizeFix();
    handleHashCategory();
    initializeScrollAnimations();

    const cart = new Map();
    const cartPanel = document.getElementById("cartPanel");
    const cartItems = document.getElementById("cartItems");
    const cartBackdrop = document.getElementById("cartBackdrop");
    const openCartBtn = document.getElementById("openCartBtn");
    const closeCartBtn = document.getElementById("closeCartBtn");
    const cartCount = document.getElementById("cartCount");
    const totalItems = document.getElementById("totalItems");
    const totalAmount = document.getElementById("totalAmount");
    const checkoutBtn = document.getElementById("checkoutBtn");

    function openCart() {
      cartPanel.classList.add("open");
      cartPanel.setAttribute("aria-hidden", "false");
      openCartBtn.setAttribute("aria-expanded", "true");
      cartBackdrop.hidden = false;
      requestAnimationFrame(() => cartBackdrop.classList.add("show"));
      document.body.classList.add("cart-open");
    }

    function closeCart() {
      cartPanel.classList.remove("open");
      cartPanel.setAttribute("aria-hidden", "true");
      openCartBtn.setAttribute("aria-expanded", "false");
      cartBackdrop.classList.remove("show");
      document.body.classList.remove("cart-open");
      setTimeout(() => {
        if (!cartBackdrop.classList.contains("show")) {
          cartBackdrop.hidden = true;
        }
      }, 220);
    }

    function addItem(id) {
      const currentQty = cart.get(id) || 0;
      cart.set(id, currentQty + 1);
      renderCart();
      openCart();
    }

    function updateQty(id, change) {
      const nextQty = (cart.get(id) || 0) + change;
      if (nextQty <= 0) {
        cart.delete(id);
      } else {
        cart.set(id, nextQty);
      }
      renderCart();
    }

    function renderCart() {
      const entries = Array.from(cart.entries());
      const itemsCount = entries.reduce((sum, entry) => sum + entry[1], 0);
      const amount = entries.reduce((sum, entry) => {
        const item = itemLookup.get(entry[0]);
        return sum + (item.price * entry[1]);
      }, 0);

      cartCount.textContent = String(itemsCount);
      totalItems.textContent = String(itemsCount);
      totalAmount.textContent = formatINR(amount);
      checkoutBtn.disabled = entries.length === 0;

      if (entries.length === 0) {
        cartItems.innerHTML = `<li class="empty-cart">Your cart is empty. Tap "Add to Cart" on any pizza.</li>`;
        return;
      }

      cartItems.innerHTML = entries.map((entry) => {
        const item = itemLookup.get(entry[0]);
        const qty = entry[1];
        const lineTotal = item.price * qty;
        return `
          <li class="cart-item">
            <div class="cart-item-top">
              <h4>${item.name}</h4>
              <span class="line-total">${formatINR(lineTotal)}</span>
            </div>
            <div class="qty-row">
              <button class="qty-btn" type="button" data-action="decrease" data-id="${item.id}">-</button>
              <span class="qty-value">${qty}</span>
              <button class="qty-btn" type="button" data-action="increase" data-id="${item.id}">+</button>
            </div>
          </li>
        `;
      }).join("");
    }

    function normalizeOrderEntries(entries) {
      return entries
        .filter((entry) => itemLookup.has(entry[0]) && Number(entry[1]) > 0)
        .map((entry) => [entry[0], Number(entry[1])]);
    }

    function buildOrderDraft(entries) {
      const normalizedEntries = normalizeOrderEntries(entries);
      const subtotal = normalizedEntries.reduce((sum, entry) => {
        const item = itemLookup.get(entry[0]);
        return sum + ((item ? item.price : 0) * entry[1]);
      }, 0);
      const itemCount = normalizedEntries.reduce((sum, entry) => sum + entry[1], 0);
      const hasComboDeal = normalizedEntries.some((entry) => {
        const item = itemLookup.get(entry[0]);
        return Boolean(item && item.isCombo);
      });
      return {
        entries: normalizedEntries,
        subtotal,
        itemCount,
        hasComboDeal,
        couponCode: "NONE",
        orderType: "dine_in",
        discount: 0,
        finalAmount: subtotal
      };
    }

    function syncCouponAvailability() {
      if (!orderDraft) {
        return;
      }

      couponOptionCards.forEach((card) => {
        const input = card.querySelector("input[name='orderCoupon']");
        if (!input) {
          return;
        }
        const shouldDisable = orderDraft.hasComboDeal && input.value !== "NONE";
        input.disabled = shouldDisable;
        card.classList.toggle("is-disabled", shouldDisable);
      });

      if (orderDraft.hasComboDeal) {
        const noneInput = couponInputs.find((input) => input.value === "NONE");
        if (noneInput) {
          noneInput.checked = true;
        }
      }
    }

    function getCouponFeedbackMessage() {
      if (!orderDraft) {
        return "";
      }

      if (orderDraft.hasComboDeal) {
        return "Combo offer deal selected. Coupons are disabled for this checkout.";
      }

      if (orderDraft.couponCode === "NONE") {
        return "Select a coupon to see instant savings on the final amount.";
      }

      if (orderDraft.couponCode === "WEEKEND20" && orderDraft.subtotal < 699) {
        return "WEEKEND20 requires a subtotal of at least Rs. 699.";
      }

      if (orderDraft.couponCode === "CHEESE60" && orderDraft.subtotal < 499) {
        return "CHEESE60 requires a subtotal of at least Rs. 499.";
      }

      if (orderDraft.couponCode === "LATENIGHT50" && !isLateNightEligible()) {
        return "LATENIGHT50 is valid after 10:00 PM.";
      }

      return `${orderDraft.couponCode} applied successfully.`;
    }

    function renderOrderFlow() {
      if (!orderDraft) {
        return;
      }

      orderFlowItems.innerHTML = orderDraft.entries.map((entry) => {
        const item = itemLookup.get(entry[0]);
        const name = item ? item.name : entry[0];
        const qty = entry[1];
        const lineTotal = (item ? item.price : 0) * qty;
        return `
          <li class="order-flow-item">
            <span>${escapeHtml(name)} x ${qty}</span>
            <strong>${formatINR(lineTotal)}</strong>
          </li>
        `;
      }).join("");

      orderDraft.couponCode = getSelectedCouponCode();
      orderDraft.orderType = getSelectedOrderMode();
      orderDraft.discount = calculateCouponDiscount(orderDraft.subtotal, orderDraft.couponCode, orderDraft.hasComboDeal);
      orderDraft.finalAmount = Math.max(0, orderDraft.subtotal - orderDraft.discount);

      orderFlowSubtotal.textContent = formatINR(orderDraft.subtotal);
      orderFlowDiscount.textContent = `-${formatINR(orderDraft.discount)}`;
      orderFlowFinalAmount.textContent = formatINR(orderDraft.finalAmount);
      orderCouponNote.textContent = getCouponFeedbackMessage();
    }

    function openOrderFlow(entries) {
      const nextDraft = buildOrderDraft(entries);
      if (!nextDraft.entries.length) {
        return;
      }

      orderDraft = nextDraft;
      couponInputs.forEach((input) => {
        input.disabled = false;
        input.checked = input.value === "NONE";
      });
      modeInputs.forEach((input) => {
        input.disabled = false;
        input.checked = input.value === "dine_in";
      });
      orderConfirmStatus.textContent = "";
      resetOrderConfirmState();
      syncCouponAvailability();
      renderOrderFlow();
      orderFlowOverlay.classList.remove("hidden");
      document.body.classList.add("order-flow-open");
    }

    function closeOrderFlow(options = {}) {
      const { reopenCart = false, allowCancelConfirming = false } = options;
      if (confirmOrderTimer) {
        if (!allowCancelConfirming) {
          return;
        }
        resetOrderConfirmState();
      }
      orderFlowOverlay.classList.add("hidden");
      document.body.classList.remove("order-flow-open");
      orderConfirmStatus.textContent = "";
      orderDraft = null;

      if (reopenCart && cart.size > 0) {
        openCart();
      }
    }

    function closeTrackingOverlay() {
      orderTrackingOverlay.classList.add("hidden");
      document.body.classList.remove("track-order-open");
    }

    function openTrackingOverlay(orderRecord) {
      const placedAt = new Date(orderRecord.placedAt || Date.now());
      const modeLabel = ORDER_TYPE_LABELS[orderRecord.orderType] || "Dine In";
      const couponLabel = orderRecord.couponCode && orderRecord.couponCode !== "NONE" ? orderRecord.couponCode : "No coupon";
      const modeConfig = {
        dine_in: {
          subtitle: "Your table order is confirmed and kitchen prep is underway.",
          secondTitle: "Table preparation started",
          secondMeta: "Chef team has started your meal.",
          finalTitle: "Serve at table in around 12 minutes",
          finalMeta: "Please stay near your table."
        },
        take_away: {
          subtitle: "Your take away order is being prepared and packed.",
          secondTitle: "Packing queue started",
          secondMeta: "Store team is preparing your pickup bag.",
          finalTitle: "Pickup in around 15 minutes",
          finalMeta: "Please reach the store counter with your order ID."
        },
        delivery: {
          subtitle: "Your delivery request is confirmed and rider allocation has started.",
          secondTitle: "Rider assignment in progress",
          secondMeta: "Dispatch team is assigning the nearest rider.",
          finalTitle: "Delivery in around 30 minutes",
          finalMeta: "Keep your phone reachable for rider updates."
        }
      }[orderRecord.orderType] || {
        subtitle: "Your order is confirmed.",
        secondTitle: "Order accepted",
        secondMeta: "Team is preparing your order.",
        finalTitle: "Ready soon",
        finalMeta: "Please track this order ID for updates."
      };

      trackingSubtitle.textContent = modeConfig.subtitle;
      trackingOrderId.textContent = orderRecord.id || "--";
      trackingOrderType.textContent = modeLabel;
      trackingCoupon.textContent = couponLabel;
      trackingAmount.textContent = formatINR(orderRecord.amount || 0);
      trackingStepConfirmedMeta.textContent = Number.isNaN(placedAt.getTime()) ? "Just now" : placedAt.toLocaleTimeString("en-IN");
      trackingStepSecondaryTitle.textContent = modeConfig.secondTitle;
      trackingStepSecondaryMeta.textContent = modeConfig.secondMeta;
      trackingStepFinalTitle.textContent = modeConfig.finalTitle;
      trackingStepFinalMeta.textContent = modeConfig.finalMeta;
      orderTrackingOverlay.classList.remove("hidden");
      document.body.classList.add("track-order-open");
    }

    function finalizeOrderWithDelay() {
      if (!orderDraft || !orderDraft.entries.length || confirmOrderTimer) {
        return;
      }

      renderOrderFlow();
      orderConfirmBtn.disabled = true;
      closeOrderFlowBtn.disabled = true;
      orderFlowCancelBtn.disabled = false;
      orderFlowCancelBtn.textContent = "Cancel Order";
      orderConfirmVisual.classList.remove("hidden");
      orderConfirmVisual.setAttribute("aria-hidden", "false");
      couponInputs.forEach((input) => {
        input.disabled = true;
      });
      modeInputs.forEach((input) => {
        input.disabled = true;
      });

      let secondsRemaining = Math.ceil(ORDER_CONFIRM_DELAY_MS / 1000);
      orderConfirmStatus.textContent = `Confirming order... ${secondsRemaining}s`;
      confirmOrderCountdown = setInterval(() => {
        secondsRemaining -= 1;
        if (secondsRemaining > 0) {
          orderConfirmStatus.textContent = `Confirming order... ${secondsRemaining}s`;
        }
      }, 1000);

      confirmOrderTimer = setTimeout(() => {
        resetOrderConfirmState();
        const placedOrder = recordCheckoutHistory(orderDraft.entries, orderDraft.finalAmount, {
          subtotal: orderDraft.subtotal,
          discount: orderDraft.discount,
          couponCode: orderDraft.couponCode,
          orderType: orderDraft.orderType,
          hasComboDeal: orderDraft.hasComboDeal
        });
        cart.clear();
        renderCart();
        closeCart();
        orderFlowOverlay.classList.add("hidden");
        document.body.classList.remove("order-flow-open");
        orderConfirmStatus.textContent = "";
        orderDraft = null;
        setDrawerSection("orders");
        openTrackingOverlay(placedOrder);
      }, ORDER_CONFIRM_DELAY_MS);
    }

    function recordCheckoutHistory(entries, amount, metadata = {}) {
      const now = new Date();
      const orderId = `ORD-${now.getTime().toString(36).toUpperCase()}`;
      const itemCount = entries.reduce((sum, entry) => sum + entry[1], 0);
      const safeAmount = Number(amount) || 0;
      const subtotal = Number(metadata.subtotal) || safeAmount;
      const discount = Math.max(0, Number(metadata.discount) || 0);
      const orderType = String(metadata.orderType || "dine_in");
      const couponCode = String(metadata.couponCode || "NONE");
      const hasComboDeal = Boolean(metadata.hasComboDeal);
      const orderRecord = {
        id: orderId,
        placedAt: now.toISOString(),
        itemCount,
        amount: safeAmount,
        subtotal,
        discount,
        couponCode,
        orderType,
        hasComboDeal,
        items: entries.map((entry) => {
          const item = itemLookup.get(entry[0]);
          return {
            id: entry[0],
            name: item ? item.name : entry[0],
            qty: entry[1]
          };
        })
      };

      const orders = readListStorage(ORDER_HISTORY_KEY);
      orders.unshift(orderRecord);
      writeListStorage(ORDER_HISTORY_KEY, orders.slice(0, 20));

      const pointsEarned = Math.max(5, Math.round(safeAmount / 20));
      const rewards = readListStorage(REWARD_HISTORY_KEY);
      rewards.unshift({
        points: pointsEarned,
        reason: `Reward for ${orderId}`,
        createdAt: now.toISOString()
      });
      writeListStorage(REWARD_HISTORY_KEY, rewards.slice(0, 40));

      renderOrderHistory();
      renderRewardHistory();
      return orderRecord;
    }

    renderCart();

    document.addEventListener("click", (event) => {
      const addButton = event.target.closest(".add-cart-btn");
      if (addButton) {
        addItem(addButton.dataset.id);
        return;
      }

      const qtyButton = event.target.closest(".qty-btn");
      if (qtyButton) {
        const action = qtyButton.dataset.action;
        const id = qtyButton.dataset.id;
        updateQty(id, action === "increase" ? 1 : -1);
      }
    });

    openCartBtn.addEventListener("click", openCart);
    closeCartBtn.addEventListener("click", closeCart);
    cartBackdrop.addEventListener("click", closeCart);
    couponInputs.forEach((input) => {
      input.addEventListener("change", () => {
        if (orderDraft) {
          renderOrderFlow();
        }
      });
    });
    modeInputs.forEach((input) => {
      input.addEventListener("change", () => {
        if (orderDraft) {
          renderOrderFlow();
        }
      });
    });
    closeOrderFlowBtn.addEventListener("click", () => closeOrderFlow({ reopenCart: true }));
    orderFlowCancelBtn.addEventListener("click", () => {
      const cancelingConfirm = Boolean(confirmOrderTimer);
      closeOrderFlow({ reopenCart: true, allowCancelConfirming: cancelingConfirm });
    });
    orderConfirmBtn.addEventListener("click", finalizeOrderWithDelay);
    closeTrackingBtn.addEventListener("click", closeTrackingOverlay);
    startNewOrderBtn.addEventListener("click", () => {
      closeTrackingOverlay();
      window.location.hash = "#categories";
    });
    checkoutBtn.addEventListener("click", () => {
      const entries = Array.from(cart.entries());
      if (!entries.length) {
        return;
      }
      closeCart();
      openOrderFlow(entries);
    });

    document.addEventListener("keydown", (event) => {
      if (event.key === "Escape") {
        if (!orderTrackingOverlay.classList.contains("hidden")) {
          closeTrackingOverlay();
          return;
        }
        if (!orderFlowOverlay.classList.contains("hidden")) {
          closeOrderFlow({ reopenCart: true });
          return;
        }
        closeCart();
        closeDrawer();
      }
    });

    const heroSlider = document.getElementById("heroSlider");
    const slidesTrack = document.getElementById("slidesTrack");
    const slides = Array.from(document.querySelectorAll(".slide"));
    const prevSlideBtn = document.getElementById("prevSlide");
    const nextSlideBtn = document.getElementById("nextSlide");
    const sliderDots = document.getElementById("sliderDots");

    let activeSlide = 0;
    let autoplay = null;

    slides.forEach((_, index) => {
      const dot = document.createElement("button");
      dot.type = "button";
      dot.className = `dot${index === 0 ? " active" : ""}`;
      dot.setAttribute("aria-label", `Go to slide ${index + 1}`);
      dot.addEventListener("click", () => {
        setSlide(index);
        restartAutoplay();
      });
      sliderDots.appendChild(dot);
    });

    const dots = Array.from(document.querySelectorAll(".slider-dots .dot"));

    function setSlide(index, animate = true) {
      activeSlide = (index + slides.length) % slides.length;
      if (slidesTrack) {
        slidesTrack.style.transition = animate ? "transform 0.7s cubic-bezier(0.22, 0.61, 0.36, 1)" : "none";
        slidesTrack.style.transform = `translateX(-${activeSlide * 100}%)`;
      }
      slides.forEach((slide, idx) => slide.classList.toggle("active", idx === activeSlide));
      dots.forEach((dot, idx) => dot.classList.toggle("active", idx === activeSlide));
    }

    function startAutoplay() {
      clearInterval(autoplay);
      autoplay = setInterval(() => setSlide(activeSlide + 1), 4500);
    }

    function restartAutoplay() {
      startAutoplay();
    }

    prevSlideBtn.addEventListener("click", () => {
      setSlide(activeSlide - 1);
      restartAutoplay();
    });

    nextSlideBtn.addEventListener("click", () => {
      setSlide(activeSlide + 1);
      restartAutoplay();
    });

    if (heroSlider) {
      heroSlider.addEventListener("mouseenter", () => clearInterval(autoplay));
      heroSlider.addEventListener("mouseleave", startAutoplay);
    }

    document.addEventListener("visibilitychange", () => {
      if (document.hidden) {
        clearInterval(autoplay);
      } else {
        startAutoplay();
      }
    });

    setSlide(0, false);
    requestAnimationFrame(() => {
      if (slidesTrack) {
        slidesTrack.style.transition = "transform 0.7s cubic-bezier(0.22, 0.61, 0.36, 1)";
      }
    });
    startAutoplay();
  </script>
</body>
</html>

