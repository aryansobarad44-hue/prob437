<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Probability & Statistics – 25EMAB104</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:wght@300;400;500;600&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #f5f3ee; --surface: #ffffff; --ink: #1a1714; --muted: #6b6560;
  --accent: #2d5f8a; --accent2: #e85d26; --accent3: #3a9e6f; --gold: #c49a1f;
  --border: #ddd9d3; --unit1: #2d5f8a; --unit2: #3a9e6f; --unit3: #e85d26;
}
* { margin:0; padding:0; box-sizing:border-box; }
html { scroll-behavior: smooth; }
body { font-family:'DM Sans',sans-serif; background:var(--bg); color:var(--ink); }

nav {
  position:sticky; top:0; z-index:200;
  background:var(--ink);
  display:flex; align-items:center; justify-content:space-between;
  padding:0 28px; height:54px;
  box-shadow:0 2px 16px rgba(0,0,0,0.3);
}
.nav-logo { font-family:'DM Serif Display',serif; color:#fff; font-size:17px; white-space:nowrap; }
.nav-links { display:flex; gap:4px; flex-wrap:wrap; }
.nav-links a {
  color:rgba(255,255,255,0.65); text-decoration:none; font-size:12px;
  font-weight:500; padding:5px 10px; border-radius:4px;
  transition:all 0.18s; letter-spacing:0.04em; text-transform:uppercase;
}
.nav-links a:hover { color:#fff; background:rgba(255,255,255,0.12); }
.nav-links a.active { color:#fff; background:rgba(255,255,255,0.2); }

.page { display:none; min-height:100vh; animation: fadeIn 0.3s ease both; }
.page.active { display:block; }
@keyframes fadeIn { from{opacity:0;transform:translateY(8px)} to{opacity:1;transform:translateY(0)} }

/* HERO */
.hero {
  min-height:100vh; display:flex; flex-direction:column;
  align-items:center; justify-content:center;
  padding:80px 32px; text-align:center; position:relative;
  background:
    radial-gradient(ellipse 80% 60% at 20% 80%, rgba(45,95,138,0.13) 0%, transparent 60%),
    radial-gradient(ellipse 60% 50% at 80% 20%, rgba(232,93,38,0.10) 0%, transparent 60%),
    var(--bg);
  overflow:hidden;
}
.hero::before {
  content:''; position:absolute; inset:0;
  background-image:linear-gradient(var(--border) 1px,transparent 1px),linear-gradient(90deg,var(--border) 1px,transparent 1px);
  background-size:48px 48px; opacity:0.35; pointer-events:none;
}
.course-badge {
  display:inline-flex; align-items:center; gap:8px;
  background:var(--ink); color:var(--gold);
  font-family:'JetBrains Mono',monospace; font-size:12px; font-weight:600;
  letter-spacing:0.12em; padding:6px 16px; border-radius:2px;
  margin-bottom:32px; position:relative; z-index:1;
}
.hero-title {
  font-family:'DM Serif Display',serif;
  font-size:clamp(38px,7vw,84px); line-height:1.05;
  letter-spacing:-0.02em; max-width:820px; margin-bottom:16px;
  position:relative; z-index:1;
}
.hero-title em { font-style:italic; color:var(--accent); }
.hero-subtitle { font-size:17px; color:var(--muted); font-weight:300; margin-bottom:44px; position:relative; z-index:1; }
.student-card {
  background:var(--surface); border:1.5px solid var(--border); border-radius:12px;
  padding:24px 34px; display:inline-flex; flex-direction:column; gap:4px;
  text-align:left; box-shadow:0 4px 32px rgba(0,0,0,0.07);
  position:relative; z-index:1; min-width:300px;
}
.s-label { font-size:10px; text-transform:uppercase; letter-spacing:0.1em; color:var(--muted); font-weight:600; }
.s-value { font-size:20px; font-weight:600; font-family:'DM Serif Display',serif; margin-bottom:12px; }
.meta-row { display:flex; gap:20px; flex-wrap:wrap; margin-top:4px; }
.meta { display:flex; flex-direction:column; gap:2px; }
.meta .s-label { font-size:9px; }
.meta .val { font-family:'JetBrains Mono',monospace; font-size:13px; color:var(--accent); font-weight:600; }
.course-stats {
  display:flex; margin-top:36px; position:relative; z-index:1;
  border:1.5px solid var(--border); border-radius:10px; overflow:hidden;
  background:var(--surface); box-shadow:0 2px 16px rgba(0,0,0,0.06);
}
.stat-item { padding:16px 26px; text-align:center; border-right:1.5px solid var(--border); }
.stat-item:last-child { border-right:none; }
.stat-num { font-family:'DM Serif Display',serif; font-size:28px; }
.stat-lbl { font-size:11px; text-transform:uppercase; letter-spacing:0.08em; color:var(--muted); margin-top:2px; }
.toc-grid {
  display:grid; grid-template-columns:repeat(3,1fr); gap:12px;
  margin-top:44px; max-width:840px; width:100%; position:relative; z-index:1;
}
.toc-card {
  background:var(--surface); border:1.5px solid var(--border);
  border-radius:10px; padding:18px 20px; text-align:left;
  cursor:pointer; transition:all 0.2s; box-shadow:0 2px 8px rgba(0,0,0,0.04);
}
.toc-card:hover { transform:translateY(-3px); box-shadow:0 8px 28px rgba(0,0,0,0.1); }
.toc-unit { font-size:10px; font-weight:700; letter-spacing:0.1em; text-transform:uppercase; margin-bottom:4px; }
.toc-ch { font-family:'DM Serif Display',serif; font-size:16px; line-height:1.3; }
.toc-hrs { font-family:'JetBrains Mono',monospace; font-size:11px; color:var(--muted); margin-top:6px; }
.u1c{color:var(--unit1);} .u2c{color:var(--unit2);} .u3c{color:var(--unit3);}

/* CHAPTER PAGE */
.ch-page { max-width:940px; margin:0 auto; padding:52px 32px 80px; }
.ch-topbar {
  display:flex; align-items:center; justify-content:space-between;
  margin-bottom:36px; padding-bottom:18px; border-bottom:2px solid var(--border);
  flex-wrap:wrap; gap:12px;
}
.ch-badge { display:flex; align-items:center; gap:10px; }
.ch-unit-pill {
  font-family:'JetBrains Mono',monospace; font-size:11px; font-weight:700;
  letter-spacing:0.1em; text-transform:uppercase; padding:5px 12px;
  border-radius:4px; color:#fff;
}
.u1{background:var(--unit1);} .u2{background:var(--unit2);} .u3{background:var(--unit3);}
.ch-num { font-family:'JetBrains Mono',monospace; font-size:13px; color:var(--muted); font-weight:600; }
.ch-hrs-badge { background:var(--ink); color:#fff; font-family:'JetBrains Mono',monospace; font-size:12px; padding:5px 12px; border-radius:4px; }
.ch-title { font-family:'DM Serif Display',serif; font-size:clamp(30px,5vw,50px); line-height:1.1; margin-bottom:10px; }
.ch-intro { font-size:15px; color:var(--muted); line-height:1.75; max-width:700px; margin-bottom:40px; }
.content-section { margin-bottom:48px; }
.section-heading { font-family:'DM Serif Display',serif; font-size:23px; margin-bottom:16px; padding-bottom:8px; border-bottom:1.5px solid var(--border); }
.subsection-heading { font-size:14px; font-weight:600; color:var(--ink); margin:20px 0 8px; text-transform:uppercase; letter-spacing:0.06em; }
p.body-text { font-size:14px; line-height:1.78; color:#2e2a27; margin-bottom:12px; }
.def-box { background:#f0f5fb; border-left:4px solid var(--accent); border-radius:0 8px 8px 0; padding:14px 18px; margin:14px 0; }
.def-box.green { background:#f0f7f2; border-left-color:var(--accent3); }
.def-box.orange { background:#fff4f0; border-left-color:var(--accent2); }
.def-title { font-size:10px; font-weight:700; letter-spacing:0.1em; text-transform:uppercase; color:var(--accent); margin-bottom:4px; }
.def-box.green .def-title{color:var(--accent3);} .def-box.orange .def-title{color:var(--accent2);}
.def-text { font-size:14px; line-height:1.7; }
.formula-box { background:var(--ink); color:#fff; border-radius:10px; padding:18px 22px; margin:14px 0; font-family:'JetBrains Mono',monospace; }
.formula-label { font-size:10px; letter-spacing:0.12em; text-transform:uppercase; color:var(--gold); margin-bottom:8px; }
.formula { font-size:14px; line-height:1.9; }
.key-list { list-style:none; margin:12px 0; }
.key-list li { padding:9px 12px 9px 34px; position:relative; font-size:14px; line-height:1.6; border-bottom:1px solid var(--border); }
.key-list li:last-child{border-bottom:none;}
.key-list li::before{content:'→';position:absolute;left:12px;color:var(--accent);font-weight:700;}
.key-list.green li::before{color:var(--accent3);} .key-list.orange li::before{color:var(--accent2);}
.two-col { display:grid; grid-template-columns:1fr 1fr; gap:14px; margin:14px 0; }
.info-card { background:var(--surface); border:1.5px solid var(--border); border-radius:10px; padding:16px; }
.info-card-title { font-weight:600; font-size:13px; margin-bottom:7px; }
.info-card p { font-size:13px; line-height:1.65; color:var(--muted); }
.example-box { background:#fdfbf7; border:1.5px solid #e6e0d4; border-radius:10px; padding:16px 20px; margin:14px 0; }
.example-label { font-size:10px; font-weight:700; letter-spacing:0.1em; text-transform:uppercase; color:var(--gold); margin-bottom:6px; }
.example-box p { font-size:14px; line-height:1.7; }
.content-table { width:100%; border-collapse:collapse; margin:14px 0; font-size:13px; }
.content-table th { background:var(--ink); color:#fff; padding:9px 13px; text-align:left; font-size:11px; letter-spacing:0.06em; text-transform:uppercase; }
.content-table td { padding:9px 13px; border-bottom:1px solid var(--border); }
.content-table tr:last-child td{border-bottom:none;}
.content-table tr:nth-child(even) td{background:rgba(0,0,0,0.02);}
.lab-section { background:#f0f7f2; border:1.5px solid #b8e0c8; border-radius:12px; padding:22px 26px; margin-top:36px; }
.lab-section.orange{background:#fff4f0;border-color:#f4bca4;}
.lab-top { font-size:11px; font-weight:700; letter-spacing:0.1em; text-transform:uppercase; color:var(--accent3); margin-bottom:9px; }
.lab-section.orange .lab-top{color:var(--accent2);}
.lab-section h3 { font-family:'DM Serif Display',serif; font-size:19px; margin-bottom:9px; }
.lab-section p{font-size:14px;line-height:1.7;}
.lab-list{list-style:none;margin-top:10px;}
.lab-list li{padding:6px 0 6px 20px;position:relative;font-size:14px;border-bottom:1px dashed #c5e0cb;}
.lab-section.orange .lab-list li{border-bottom-color:#f4c9b7;}
.lab-list li:last-child{border-bottom:none;}
.lab-list li::before{content:'◆';position:absolute;left:0;font-size:8px;color:var(--accent3);top:10px;}
.lab-section.orange .lab-list li::before{color:var(--accent2);}
.ch-nav { display:flex; justify-content:space-between; align-items:center; margin-top:52px; padding-top:24px; border-top:2px solid var(--border); gap:10px; flex-wrap:wrap; }
.ch-nav-btn { display:flex; align-items:center; gap:8px; background:var(--surface); border:1.5px solid var(--border); border-radius:8px; padding:11px 18px; cursor:pointer; transition:all 0.2s; text-decoration:none; color:var(--ink); font-size:14px; font-weight:500; }
.ch-nav-btn:hover{background:var(--ink);color:#fff;border-color:var(--ink);}

/* BOOKS */
.books-page{background:var(--ink);min-height:100vh;padding:60px 32px;}
.books-inner{max-width:900px;margin:0 auto;}
.books-heading{font-family:'DM Serif Display',serif;font-size:34px;color:var(--gold);margin-bottom:26px;}
.book-list{display:grid;gap:13px;margin-bottom:44px;}
.book-item{background:rgba(255,255,255,0.06);border:1px solid rgba(255,255,255,0.1);border-radius:10px;padding:16px 20px;display:flex;gap:15px;}
.book-num{font-family:'JetBrains Mono',monospace;font-size:20px;color:var(--gold);font-weight:600;flex-shrink:0;}
.book-text{font-size:14px;line-height:1.65;color:rgba(255,255,255,0.8);}
footer{background:#111;color:rgba(255,255,255,0.4);text-align:center;padding:22px;font-size:12px;letter-spacing:0.05em;}
footer strong{color:rgba(255,255,255,0.7);}

@media(max-width:640px){
  .toc-grid{grid-template-columns:1fr 1fr;}
  .two-col{grid-template-columns:1fr;}
  .ch-page{padding:32px 16px 60px;}
  .course-stats{flex-direction:column;}
  .stat-item{border-right:none;border-bottom:1.5px solid var(--border);}
  .stat-item:last-child{border-bottom:none;}
  nav{padding:0 12px;}
  .nav-links a{padding:4px 7px;font-size:10px;}
}
</style>
</head>
<body>

<nav>
  <span class="nav-logo">P&amp;S · 25EMAB104</span>
  <div class="nav-links">
    <a href="#" onclick="showPage('home');return false" id="nav-home" class="active">Home</a>
    <a href="#" onclick="showPage('ch1');return false" id="nav-ch1">Ch 1</a>
    <a href="#" onclick="showPage('ch2');return false" id="nav-ch2">Ch 2</a>
    <a href="#" onclick="showPage('ch3');return false" id="nav-ch3">Ch 3</a>
    <a href="#" onclick="showPage('ch4');return false" id="nav-ch4">Ch 4</a>
    <a href="#" onclick="showPage('ch5');return false" id="nav-ch5">Ch 5</a>
    <a href="#" onclick="showPage('ch6');return false" id="nav-ch6">Ch 6</a>
    <a href="#" onclick="showPage('books');return false" id="nav-books">Books</a>
  </div>
</nav>

<!-- HOME -->
<div class="page active" id="page-home">
<section class="hero">
  <div class="course-badge">25EMAB104 &nbsp;·&nbsp; KLE Tech University</div>
  <h1 class="hero-title">Probability<br>&amp; <em>Statistics</em></h1>
  <p class="hero-subtitle">Complete Study Notes &nbsp;·&nbsp; CS AI &nbsp;·&nbsp; Semester 2</p>
  <div class="student-card">
    <span class="s-label">Student</span>
    <span class="s-value">Shrishail Sobarad</span>
    <div class="meta-row">
      <div class="meta"><span class="s-label">USN</span><span class="val">02FE25BCI037</span></div>
      <div class="meta"><span class="s-label">Branch</span><span class="val">CS AI</span></div>
      <div class="meta"><span class="s-label">Semester</span><span class="val">2nd</span></div>
    </div>
  </div>
  <div class="course-stats">
    <div class="stat-item"><div class="stat-num">3</div><div class="stat-lbl">Credits</div></div>
    <div class="stat-item"><div class="stat-num">100</div><div class="stat-lbl">Total Marks</div></div>
    <div class="stat-item"><div class="stat-num">45</div><div class="stat-lbl">Teaching Hrs</div></div>
    <div class="stat-item"><div class="stat-num">6</div><div class="stat-lbl">Chapters</div></div>
  </div>
  <div class="toc-grid">
    <div class="toc-card" onclick="showPage('ch1')"><div class="toc-unit u1c">Unit I · Ch 01</div><div class="toc-ch">Description of Data</div><div class="toc-hrs">10 hrs</div></div>
    <div class="toc-card" onclick="showPage('ch2')"><div class="toc-unit u1c">Unit I · Ch 02</div><div class="toc-ch">Probability</div><div class="toc-hrs">07 hrs</div></div>
    <div class="toc-card" onclick="showPage('ch3')"><div class="toc-unit u2c">Unit II · Ch 03</div><div class="toc-ch">Random Variables &amp; Distributions</div><div class="toc-hrs">08 hrs</div></div>
    <div class="toc-card" onclick="showPage('ch4')"><div class="toc-unit u2c">Unit II · Ch 04</div><div class="toc-ch">Statistical Inference I</div><div class="toc-hrs">10 hrs</div></div>
    <div class="toc-card" onclick="showPage('ch5')"><div class="toc-unit u3c">Unit III · Ch 05</div><div class="toc-ch">Correlation &amp; Regression</div><div class="toc-hrs">05 hrs</div></div>
    <div class="toc-card" onclick="showPage('ch6')"><div class="toc-unit u3c">Unit III · Ch 06</div><div class="toc-ch">Statistical Inference II</div><div class="toc-hrs">05 hrs</div></div>
  </div>
</section>
</div>

<!-- CHAPTER 1 -->
<div class="page" id="page-ch1">
<div class="ch-page">
  <div class="ch-topbar">
    <div class="ch-badge"><span class="ch-unit-pill u1">Unit I</span><span class="ch-num">Chapter 01</span></div>
    <span class="ch-hrs-badge">10 hrs</span>
  </div>
  <h1 class="ch-title">Description of Data</h1>
  <p class="ch-intro">This chapter introduces the foundational concepts of statistics — what data is, how it is classified, and how to summarize and visualize it using numerical and graphical methods.</p>

  <div class="content-section">
    <h2 class="section-heading">1.1 Introduction to Data &amp; Types of Variables</h2>
    <p class="body-text">Data is a collection of facts, measurements, or observations. In statistics, data is classified by its nature and level of measurement.</p>
    <div class="two-col">
      <div class="info-card"><div class="info-card-title">Qualitative (Categorical)</div><p>Non-numeric data representing categories or labels. E.g., Gender, Blood Group, Grade (A/B/C).</p></div>
      <div class="info-card"><div class="info-card-title">Quantitative (Numerical)</div><p>Numeric data that can be measured or counted. E.g., Height, Weight, Marks, Temperature.</p></div>
    </div>
    <table class="content-table">
      <tr><th>Scale</th><th>Description</th><th>Example</th><th>Operations</th></tr>
      <tr><td>Nominal</td><td>Named categories, no order</td><td>Gender, Blood group</td><td>= , ≠</td></tr>
      <tr><td>Ordinal</td><td>Ordered categories, unequal gaps</td><td>Ranks, Letter grades</td><td>&lt; , &gt;</td></tr>
      <tr><td>Interval</td><td>Equal gaps, no true zero</td><td>Temperature (°C), IQ</td><td>+, −</td></tr>
      <tr><td>Ratio</td><td>Equal gaps, true zero exists</td><td>Height, Weight, Age</td><td>+, −, ×, ÷</td></tr>
    </table>
  </div>

  <div class="content-section">
    <h2 class="section-heading">1.2 Measures of Central Tendency</h2>
    <h3 class="subsection-heading">Arithmetic Mean</h3>
    <p class="body-text">Sum of all observations divided by the number of observations. Sensitive to outliers.</p>
    <div class="formula-box">
      <div class="formula-label">Simple Mean</div>
      <div class="formula">x̄ = (x₁ + x₂ + ... + xₙ) / n = Σxᵢ / n</div>
    </div>
    <div class="formula-box">
      <div class="formula-label">Weighted Mean</div>
      <div class="formula">x̄_w = Σ(wᵢ · xᵢ) / Σwᵢ &nbsp;&nbsp;&nbsp; [wᵢ = weight of xᵢ]</div>
    </div>
    <div class="example-box">
      <div class="example-label">Example</div>
      <p>Marks: 70, 80, 90 → Mean = (70+80+90)/3 = <strong>80</strong><br>Weighted (w = 1,2,3): x̄_w = (70+160+270)/6 = 500/6 ≈ <strong>83.3</strong></p>
    </div>

    <h3 class="subsection-heading">Median</h3>
    <div class="def-box"><div class="def-title">Definition</div><div class="def-text">The middle value in sorted data. For even n: average of two middle values. Not affected by outliers. Best for skewed distributions.</div></div>
    <ul class="key-list">
      <li>Odd n: Median = value at position (n+1)/2</li>
      <li>Even n: Median = average of values at n/2 and (n/2)+1</li>
      <li>Preferred over mean when data has extreme values</li>
    </ul>

    <h3 class="subsection-heading">Mode</h3>
    <div class="def-box"><div class="def-title">Definition</div><div class="def-text">The most frequently occurring value. A dataset can be unimodal, bimodal, or multimodal. If no value repeats, there is no mode.</div></div>

    <h3 class="subsection-heading">Quartiles</h3>
    <table class="content-table">
      <tr><th>Quartile</th><th>Position</th><th>Meaning</th></tr>
      <tr><td>Q1 (25th percentile)</td><td>(n+1)/4</td><td>25% of data is below Q1</td></tr>
      <tr><td>Q2 (50th percentile)</td><td>Median</td><td>50% of data is below Q2</td></tr>
      <tr><td>Q3 (75th percentile)</td><td>3(n+1)/4</td><td>75% of data is below Q3</td></tr>
    </table>
    <div class="def-box"><div class="def-title">IQR – Interquartile Range</div><div class="def-text">IQR = Q3 − Q1. Measures spread of the middle 50%. Outliers: values below Q1 − 1.5×IQR or above Q3 + 1.5×IQR.</div></div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">1.3 Measures of Dispersion</h2>
    <div class="formula-box">
      <div class="formula-label">Population Variance</div>
      <div class="formula">σ² = Σ(xᵢ − μ)² / N</div>
    </div>
    <div class="formula-box">
      <div class="formula-label">Sample Variance &amp; Standard Deviation</div>
      <div class="formula">s² = Σ(xᵢ − x̄)² / (n−1)<br>s = √[Σ(xᵢ − x̄)² / (n−1)]</div>
    </div>
    <div class="formula-box">
      <div class="formula-label">Coefficient of Variation (CV)</div>
      <div class="formula">CV = (s / x̄) × 100%<br><br>Lower CV → more consistent. Higher CV → more variable.</div>
    </div>
    <div class="example-box">
      <div class="example-label">Example</div>
      <p>Dataset: 4, 8, 6, 5, 3 &nbsp;(n=5)<br>
      x̄ = 26/5 = 5.2<br>
      Σ(xᵢ−x̄)² = (4−5.2)²+(8−5.2)²+(6−5.2)²+(5−5.2)²+(3−5.2)² = 1.44+7.84+0.64+0.04+4.84 = 14.8<br>
      s² = 14.8/4 = <strong>3.7</strong> &nbsp;·&nbsp; s = √3.7 ≈ <strong>1.92</strong></p>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">1.4 Skewness</h2>
    <div class="two-col">
      <div class="info-card"><div class="info-card-title">Positive Skew (Right Skewed)</div><p>Long tail on the right. Mean &gt; Median &gt; Mode. E.g., income distribution.</p></div>
      <div class="info-card"><div class="info-card-title">Negative Skew (Left Skewed)</div><p>Long tail on the left. Mean &lt; Median &lt; Mode. E.g., age at retirement.</p></div>
    </div>
    <div class="formula-box">
      <div class="formula-label">Pearson's Coefficient of Skewness</div>
      <div class="formula">Sk = 3(Mean − Median) / Standard Deviation<br><br>Sk &gt; 0 → Right skewed &nbsp;·&nbsp; Sk &lt; 0 → Left skewed &nbsp;·&nbsp; Sk = 0 → Symmetric</div>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">1.5 Data Visualization</h2>
    <h3 class="subsection-heading">Histogram</h3>
    <p class="body-text">A bar graph for continuous data where bars represent class intervals. Bar heights = frequencies. Bars touch each other (no gaps). Reveals distribution shape, skewness, and modality.</p>

    <h3 class="subsection-heading">Box Plot (Box-and-Whisker)</h3>
    <p class="body-text">Displays five-number summary: Minimum, Q1, Median (Q2), Q3, Maximum. Whiskers extend to min/max (within 1.5×IQR). Points beyond whiskers are outliers.</p>
    <ul class="key-list">
      <li>Box width = IQR (Q3 − Q1) — shows middle 50% spread</li>
      <li>Line inside box = Median</li>
      <li>Outliers shown as individual dots (•) beyond whiskers</li>
      <li>Excellent for comparing distributions across groups side-by-side</li>
    </ul>

    <h3 class="subsection-heading">Normal Q-Q Plot</h3>
    <div class="def-box"><div class="def-title">Purpose</div><div class="def-text">Checks if data follows a normal distribution. Sample quantiles (Y-axis) are plotted against theoretical normal quantiles (X-axis). If points fall on a straight diagonal line → data is approximately normal.</div></div>
    <ul class="key-list">
      <li>Straight diagonal line → approximately normal distribution</li>
      <li>S-shaped curve → heavy-tailed or light-tailed distribution</li>
      <li>Curved upward → positive skew; curved downward → negative skew</li>
      <li>Used before applying t-tests, ANOVA, regression (which assume normality)</li>
    </ul>
  </div>

  <div class="lab-section">
    <div class="lab-top">⚗️ Lab Session · 12 hrs</div>
    <h3>Data Handling &amp; Visualization</h3>
    <p>Hands-on implementation using R / Python:</p>
    <ul class="lab-list">
      <li>Importing datasets from CSV; exploring with summary() / describe()</li>
      <li>Computing mean, median, mode, variance, SD, CV</li>
      <li>Plotting histograms with frequency and density curves</li>
      <li>Drawing box plots and identifying outliers using IQR rule</li>
      <li>Constructing Q-Q plots to assess normality (qqnorm in R)</li>
      <li>Measuring and interpreting skewness coefficient</li>
    </ul>
  </div>

  <div class="ch-nav">
    <a href="#" class="ch-nav-btn" onclick="showPage('home');return false">⌂ &nbsp;Home</a>
    <a href="#" class="ch-nav-btn" onclick="showPage('ch2');return false">Chapter 2 &nbsp;→</a>
  </div>
</div>
</div>

<!-- CHAPTER 2 -->
<div class="page" id="page-ch2">
<div class="ch-page">
  <div class="ch-topbar">
    <div class="ch-badge"><span class="ch-unit-pill u1">Unit I</span><span class="ch-num">Chapter 02</span></div>
    <span class="ch-hrs-badge">07 hrs</span>
  </div>
  <h1 class="ch-title">Probability</h1>
  <p class="ch-intro">Probability is the mathematical framework for quantifying uncertainty. It forms the backbone of statistical inference, machine learning, and decision-making under uncertainty.</p>

  <div class="content-section">
    <h2 class="section-heading">2.1 Basic Definitions</h2>
    <div class="def-box"><div class="def-title">Experiment</div><div class="def-text">Any process that generates a well-defined outcome. E.g., tossing a coin, rolling a die, drawing a card.</div></div>
    <div class="def-box"><div class="def-title">Sample Space (S)</div><div class="def-text">The set of all possible outcomes. Coin: S = {H, T}. Die: S = {1,2,3,4,5,6}. Two coins: S = {HH, HT, TH, TT}.</div></div>
    <div class="def-box"><div class="def-title">Event (E)</div><div class="def-text">Any subset of the sample space. Getting even number on die: E = {2,4,6}. Events can be simple (one outcome) or compound (multiple outcomes).</div></div>
    <div class="formula-box">
      <div class="formula-label">Classical Probability</div>
      <div class="formula">P(E) = n(E) / n(S) = Favourable outcomes / Total outcomes<br><br>Axioms: &nbsp;0 ≤ P(E) ≤ 1 &nbsp;·&nbsp; P(S)=1 &nbsp;·&nbsp; P(∅)=0 &nbsp;·&nbsp; P(E') = 1−P(E)</div>
    </div>
    <div class="example-box">
      <div class="example-label">Example</div>
      <p>Rolling a fair die: P(even) = 3/6 = 1/2 &nbsp;·&nbsp; P(prime) = P({2,3,5}) = 3/6 = 1/2<br>Drawing a card: P(King) = 4/52 = 1/13 &nbsp;·&nbsp; P(Red) = 26/52 = 1/2</p>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">2.2 Rules of Probability</h2>
    <h3 class="subsection-heading">Addition Rule</h3>
    <div class="formula-box">
      <div class="formula-label">General Addition Rule</div>
      <div class="formula">P(A ∪ B) = P(A) + P(B) − P(A ∩ B)<br><br>If A and B mutually exclusive (A ∩ B = ∅):<br>P(A ∪ B) = P(A) + P(B)</div>
    </div>
    <div class="example-box">
      <div class="example-label">Example</div>
      <p>P(King or Heart) = P(King) + P(Heart) − P(King of Hearts) = 4/52 + 13/52 − 1/52 = <strong>16/52 ≈ 0.308</strong></p>
    </div>

    <h3 class="subsection-heading">Multiplication Rule &amp; Conditional Probability</h3>
    <div class="formula-box">
      <div class="formula-label">Conditional Probability</div>
      <div class="formula">P(A | B) = P(A ∩ B) / P(B) &nbsp;&nbsp; [P(B) ≠ 0]</div>
    </div>
    <div class="formula-box">
      <div class="formula-label">General Multiplication Rule</div>
      <div class="formula">P(A ∩ B) = P(A) · P(B | A)<br><br>If A and B are independent: P(B|A) = P(B)<br>P(A ∩ B) = P(A) · P(B)</div>
    </div>
    <div class="example-box">
      <div class="example-label">Example – Conditional</div>
      <p>Bag has 3 red, 2 blue balls. Draw 2 without replacement.<br>
      P(both red) = P(R₁) × P(R₂|R₁) = (3/5) × (2/4) = 6/20 = <strong>0.3</strong></p>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">2.3 Bayes' Theorem</h2>
    <div class="def-box"><div class="def-title">Concept</div><div class="def-text">Bayes' theorem updates the probability of a hypothesis as new evidence is observed. It reverses conditional probabilities: "Given B happened, what's the probability A caused it?"</div></div>
    <div class="formula-box">
      <div class="formula-label">Bayes' Theorem</div>
      <div class="formula">P(Aᵢ | B) = P(B | Aᵢ) · P(Aᵢ) / Σⱼ [P(B | Aⱼ) · P(Aⱼ)]<br><br>Posterior ∝ Likelihood × Prior</div>
    </div>
    <table class="content-table">
      <tr><th>Term</th><th>Meaning</th></tr>
      <tr><td>P(Aᵢ) — Prior</td><td>Initial probability of Aᵢ before seeing evidence</td></tr>
      <tr><td>P(B|Aᵢ) — Likelihood</td><td>Probability of evidence B given Aᵢ is true</td></tr>
      <tr><td>P(Aᵢ|B) — Posterior</td><td>Updated probability of Aᵢ after seeing evidence B</td></tr>
      <tr><td>P(B) — Evidence</td><td>Total probability of observing B (normalizing constant)</td></tr>
    </table>
    <div class="example-box">
      <div class="example-label">Classic Example – Medical Test</div>
      <p>Disease prevalence = 1%. Test accuracy = 99% (both sensitivity and specificity).<br>
      P(D) = 0.01, P(+|D) = 0.99, P(+|D') = 0.01<br>
      P(D|+) = (0.99×0.01) / [(0.99×0.01)+(0.01×0.99)] = 0.0099/0.0198 = <strong>0.5 (50%)</strong><br>
      <em>Even with a 99% accurate test, there's only 50% chance of actually having the disease due to the low base rate — this is the "base rate fallacy".</em></p>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">2.4 Bayesian Classification</h2>
    <p class="body-text">Naïve Bayes is a probabilistic classifier based on Bayes' theorem with the "naïve" assumption that all features are conditionally independent given the class label.</p>
    <div class="formula-box">
      <div class="formula-label">Naïve Bayes Classifier</div>
      <div class="formula">P(C | x₁,...,xₙ) ∝ P(C) · Π P(xᵢ | C)<br><br>Predicted class = argmax_C [P(C) · Π P(xᵢ | C)]</div>
    </div>
    <ul class="key-list">
      <li>Spam filtering: classify email as spam/not-spam based on word frequencies</li>
      <li>Text classification: sentiment analysis, topic categorisation</li>
      <li>Medical diagnosis: predict disease from symptoms</li>
      <li>Despite "naïve" assumption, works surprisingly well in practice</li>
      <li>Variants: Gaussian NB (continuous), Multinomial NB (text counts), Bernoulli NB (binary features)</li>
    </ul>
  </div>

  <div class="ch-nav">
    <a href="#" class="ch-nav-btn" onclick="showPage('ch1');return false">← &nbsp;Chapter 1</a>
    <a href="#" class="ch-nav-btn" onclick="showPage('home');return false">⌂ Home</a>
    <a href="#" class="ch-nav-btn" onclick="showPage('ch3');return false">Chapter 3 &nbsp;→</a>
  </div>
</div>
</div>

<!-- CHAPTER 3 -->
<div class="page" id="page-ch3">
<div class="ch-page">
  <div class="ch-topbar">
    <div class="ch-badge"><span class="ch-unit-pill u2">Unit II</span><span class="ch-num">Chapter 03</span></div>
    <span class="ch-hrs-badge">08 hrs</span>
  </div>
  <h1 class="ch-title">Random Variables &amp; Probability Distributions</h1>
  <p class="ch-intro">A random variable maps outcomes of a random experiment to numerical values. Probability distributions describe how probability is distributed over these values.</p>

  <div class="content-section">
    <h2 class="section-heading">3.1 Random Variables</h2>
    <div class="def-box"><div class="def-title">Definition</div><div class="def-text">A random variable X is a function X: S → ℝ that assigns a real number to each outcome in the sample space S.</div></div>
    <div class="two-col">
      <div class="info-card"><div class="info-card-title">Discrete Random Variable</div><p>Countable values. E.g., X = number of heads in 5 tosses ∈ {0,1,2,3,4,5}. Described by PMF: P(X=x).</p></div>
      <div class="info-card"><div class="info-card-title">Continuous Random Variable</div><p>Uncountably infinite values in an interval. E.g., X = height of a student ∈ (0, ∞). Described by PDF: f(x).</p></div>
    </div>
    <div class="formula-box">
      <div class="formula-label">Expected Value (Mean) and Variance</div>
      <div class="formula">E[X] = Σ x·P(X=x) &nbsp;[Discrete]<br>E[X] = ∫ x·f(x) dx &nbsp;[Continuous]<br><br>Var(X) = E[X²] − (E[X])² = E[(X−μ)²]<br>SD = σ = √Var(X)</div>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">3.2 Binomial Distribution</h2>
    <div class="def-box"><div class="def-title">Conditions (Bernoulli Trials)</div><div class="def-text">Fixed n trials. Each trial: only two outcomes (success/failure). Constant probability of success p. Trials are independent. X counts number of successes.</div></div>
    <div class="formula-box">
      <div class="formula-label">X ~ B(n, p)</div>
      <div class="formula">P(X = k) = C(n,k) · pᵏ · (1−p)ⁿ⁻ᵏ &nbsp;&nbsp; k = 0,1,...,n<br><br>E[X] = np &nbsp;&nbsp;&nbsp; Var(X) = np(1−p)</div>
    </div>
    <div class="example-box">
      <div class="example-label">Example</div>
      <p>Toss a fair coin 10 times. P(exactly 6 heads):<br>
      P(X=6) = C(10,6) × (0.5)⁶ × (0.5)⁴ = 210 × (1/1024) ≈ <strong>0.205</strong><br>
      Mean = 10×0.5 = 5 &nbsp;·&nbsp; SD = √(10×0.5×0.5) = √2.5 ≈ 1.58</p>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">3.3 Poisson Distribution</h2>
    <div class="def-box"><div class="def-title">When to Use</div><div class="def-text">Counts events occurring in a fixed interval of time or space when events occur independently at a constant average rate λ. E.g., calls per hour, defects per metre, accidents per day.</div></div>
    <div class="formula-box">
      <div class="formula-label">X ~ Poisson(λ)</div>
      <div class="formula">P(X = k) = e⁻λ · λᵏ / k! &nbsp;&nbsp; k = 0,1,2,...<br><br>E[X] = λ &nbsp;&nbsp;&nbsp; Var(X) = λ &nbsp;&nbsp;&nbsp; (Mean = Variance)</div>
    </div>
    <div class="example-box">
      <div class="example-label">Example</div>
      <p>Calls arrive at λ=3/hour. P(exactly 5 calls in 1 hour):<br>
      P(X=5) = e⁻³ × 3⁵ / 5! = 0.0498 × 243/120 ≈ <strong>0.1008</strong></p>
    </div>
    <p class="body-text">Binomial → Poisson when n is large and p is very small (np = λ remains constant).</p>
  </div>

  <div class="content-section">
    <h2 class="section-heading">3.4 Normal Distribution</h2>
    <div class="def-box"><div class="def-title">Properties</div><div class="def-text">Symmetric, bell-shaped continuous distribution. Completely determined by mean μ (location) and standard deviation σ (spread). Most common distribution due to the Central Limit Theorem.</div></div>
    <div class="formula-box">
      <div class="formula-label">X ~ N(μ, σ²)</div>
      <div class="formula">f(x) = (1/σ√(2π)) · exp[−(x−μ)²/2σ²]<br><br>Standard Normal: Z = (X − μ)/σ &nbsp;~&nbsp; N(0,1)<br><br>Empirical Rule: μ±1σ → 68% &nbsp;·&nbsp; μ±2σ → 95% &nbsp;·&nbsp; μ±3σ → 99.7%</div>
    </div>
    <ul class="key-list green">
      <li>Mean = Median = Mode (perfect symmetry)</li>
      <li>Total area under curve = 1</li>
      <li>Curve extends from −∞ to +∞ (asymptotic to x-axis)</li>
      <li>Z-table used to find probabilities for any normal distribution</li>
    </ul>
    <div class="example-box">
      <div class="example-label">Example – Z Score</div>
      <p>Exam scores: μ=70, σ=10. What % of students score above 85?<br>
      Z = (85−70)/10 = 1.5 &nbsp;→&nbsp; P(Z &lt; 1.5) = 0.9332<br>
      P(X &gt; 85) = 1 − 0.9332 = <strong>6.68%</strong></p>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">3.5 Bivariate Distribution</h2>
    <p class="body-text">When two random variables X and Y are observed simultaneously, we study their joint probability distribution.</p>
    <div class="formula-box">
      <div class="formula-label">Joint PMF (Discrete) &amp; Marginal Distributions</div>
      <div class="formula">Joint: P(X=x, Y=y) = p(x,y) &nbsp;&nbsp; ΣΣ p(x,y) = 1<br><br>Marginal of X: P(X=x) = Σ_y p(x,y)<br>Marginal of Y: P(Y=y) = Σ_x p(x,y)</div>
    </div>
    <div class="formula-box">
      <div class="formula-label">Covariance</div>
      <div class="formula">Cov(X,Y) = E[XY] − E[X]·E[Y]<br>Cov(X,Y) = E[(X−μx)(Y−μy)]<br><br>Independent X,Y → Cov(X,Y) = 0 (but converse not always true)</div>
    </div>
    <div class="def-box green"><div class="def-title">Interpretation</div><div class="def-text">Cov &gt; 0: X and Y increase together. Cov &lt; 0: X increases, Y decreases. Cov = 0: no linear relationship. Covariance is scale-dependent; use correlation coefficient (r) for comparison.</div></div>
  </div>

  <div class="lab-section">
    <div class="lab-top">⚗️ Lab Session · 10 hrs</div>
    <h3>Probability Distributions &amp; Hypothesis Testing</h3>
    <ul class="lab-list">
      <li>Simulating Binomial, Poisson, Normal distributions in R/Python</li>
      <li>Plotting PMF/PDF and CDF curves</li>
      <li>Computing probabilities using dbinom(), dpois(), dnorm()</li>
      <li>Z-score calculation and standard normal table usage</li>
      <li>Joint probability tables and marginal distributions</li>
      <li>Computing and interpreting covariance</li>
    </ul>
  </div>

  <div class="ch-nav">
    <a href="#" class="ch-nav-btn" onclick="showPage('ch2');return false">← &nbsp;Chapter 2</a>
    <a href="#" class="ch-nav-btn" onclick="showPage('home');return false">⌂ Home</a>
    <a href="#" class="ch-nav-btn" onclick="showPage('ch4');return false">Chapter 4 &nbsp;→</a>
  </div>
</div>
</div>

<!-- CHAPTER 4 -->
<div class="page" id="page-ch4">
<div class="ch-page">
  <div class="ch-topbar">
    <div class="ch-badge"><span class="ch-unit-pill u2">Unit II</span><span class="ch-num">Chapter 04</span></div>
    <span class="ch-hrs-badge">10 hrs</span>
  </div>
  <h1 class="ch-title">Statistical Inference I</h1>
  <p class="ch-intro">Statistical inference draws conclusions about a population using sample data. This chapter covers sampling design, hypothesis testing, confidence intervals, and the P-value approach.</p>

  <div class="content-section">
    <h2 class="section-heading">4.1 Sampling Methods</h2>
    <p class="body-text">A sample is a representative subset of a population. Good sampling minimises bias and allows valid inference.</p>
    <table class="content-table">
      <tr><th>Method</th><th>How it works</th><th>Use Case</th></tr>
      <tr><td><strong>SRSWR</strong></td><td>Each unit drawn at random; returned before next draw. Duplicates possible.</td><td>Theoretical analysis, bootstrapping</td></tr>
      <tr><td><strong>SRSWOR</strong></td><td>Each unit drawn at random; not returned. No duplicates. Most common in practice.</td><td>Surveys, quality control</td></tr>
      <tr><td><strong>Stratified</strong></td><td>Population split into strata (subgroups). Random sample taken from each stratum proportionally.</td><td>When population has known subgroups (e.g., age groups)</td></tr>
      <tr><td><strong>Cluster</strong></td><td>Population split into clusters (natural groups). Entire clusters chosen at random.</td><td>Geographically dispersed populations</td></tr>
    </table>
    <div class="def-box"><div class="def-title">Sampling Distribution</div><div class="def-text">The distribution of a statistic (e.g., sample mean x̄) over all possible samples of size n. By the Central Limit Theorem, x̄ ~ N(μ, σ²/n) for large n regardless of the population distribution.</div></div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">4.2 Hypothesis Testing</h2>
    <div class="two-col">
      <div class="info-card"><div class="info-card-title">Null Hypothesis (H₀)</div><p>Default claim, no effect, no difference. E.g., H₀: μ = 50. We attempt to reject this using evidence.</p></div>
      <div class="info-card"><div class="info-card-title">Alternative Hypothesis (H₁)</div><p>Claim we want to support. H₁: μ ≠ 50 (two-tailed), μ &gt; 50 or μ &lt; 50 (one-tailed).</p></div>
    </div>
    <table class="content-table">
      <tr><th>Decision Made</th><th>H₀ Actually True</th><th>H₀ Actually False</th></tr>
      <tr><td>Reject H₀</td><td>❌ Type I Error (probability = α)</td><td>✅ Correct (Power = 1−β)</td></tr>
      <tr><td>Fail to Reject H₀</td><td>✅ Correct</td><td>❌ Type II Error (probability = β)</td></tr>
    </table>
    <h3 class="subsection-heading">Steps in Hypothesis Testing</h3>
    <ul class="key-list green">
      <li><strong>Step 1:</strong> State H₀ and H₁ clearly</li>
      <li><strong>Step 2:</strong> Choose significance level α (typically 0.05 or 0.01)</li>
      <li><strong>Step 3:</strong> Select appropriate test statistic (Z, t, χ², F)</li>
      <li><strong>Step 4:</strong> Compute test statistic from sample data</li>
      <li><strong>Step 5:</strong> Find p-value or compare with critical value</li>
      <li><strong>Step 6:</strong> Decision — Reject H₀ if p-value &lt; α (or test stat &gt; critical)</li>
      <li><strong>Step 7:</strong> State conclusion in plain language within the problem context</li>
    </ul>
  </div>

  <div class="content-section">
    <h2 class="section-heading">4.3 Test Statistics for Means &amp; Proportions</h2>
    <div class="formula-box">
      <div class="formula-label">Z-test: Single Mean (σ known)</div>
      <div class="formula">Z = (x̄ − μ₀) / (σ/√n) &nbsp;~&nbsp; N(0,1)</div>
    </div>
    <div class="formula-box">
      <div class="formula-label">t-test: Single Mean (σ unknown)</div>
      <div class="formula">t = (x̄ − μ₀) / (s/√n) &nbsp;~&nbsp; t(n−1 df)</div>
    </div>
    <div class="formula-box">
      <div class="formula-label">Z-test: Difference of Means</div>
      <div class="formula">Z = (x̄₁ − x̄₂) / √(σ₁²/n₁ + σ₂²/n₂)</div>
    </div>
    <div class="formula-box">
      <div class="formula-label">Z-test: Single Proportion</div>
      <div class="formula">Z = (p̂ − p₀) / √(p₀(1−p₀)/n) &nbsp;&nbsp;&nbsp; where p̂ = x/n</div>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">4.4 Confidence Intervals</h2>
    <div class="def-box"><div class="def-title">Definition</div><div class="def-text">A 95% CI means: if we repeated the sampling procedure many times, 95% of constructed intervals would contain the true parameter. The interval either contains the true value or it doesn't — probability applies to the procedure, not the specific interval.</div></div>
    <div class="formula-box">
      <div class="formula-label">CI for Mean (σ known)</div>
      <div class="formula">x̄ ± z_{α/2} · (σ/√n)<br><br>90% CI: z = 1.645 &nbsp;·&nbsp; 95% CI: z = 1.960 &nbsp;·&nbsp; 99% CI: z = 2.576</div>
    </div>
    <div class="formula-box">
      <div class="formula-label">CI for Mean (σ unknown)</div>
      <div class="formula">x̄ ± t_{α/2, n−1} · (s/√n)</div>
    </div>
    <div class="formula-box">
      <div class="formula-label">Sample Size Determination</div>
      <div class="formula">n = (z_{α/2} · σ / E)² &nbsp;&nbsp; [E = desired margin of error]</div>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">4.5 P-value Approach</h2>
    <div class="def-box"><div class="def-title">P-value Definition</div><div class="def-text">The probability of obtaining results as extreme as (or more extreme than) the observed data, assuming H₀ is true. A small p-value is evidence against H₀.</div></div>
    <table class="content-table">
      <tr><th>P-value Range</th><th>Evidence Against H₀</th></tr>
      <tr><td>p &gt; 0.10</td><td>Little or no evidence</td></tr>
      <tr><td>0.05 &lt; p ≤ 0.10</td><td>Weak evidence</td></tr>
      <tr><td>0.01 &lt; p ≤ 0.05</td><td>Moderate evidence (typically "significant")</td></tr>
      <tr><td>p ≤ 0.01</td><td>Strong evidence against H₀</td></tr>
    </table>
    <div class="example-box">
      <div class="example-label">Example</div>
      <p>A machine claims μ = 500g output. Sample of n=36: x̄ = 495g, σ = 12g.<br>
      Z = (495−500)/(12/√36) = −5/2 = −2.5<br>
      Two-tailed p-value = 2 × P(Z &lt; −2.5) = 2 × 0.0062 = <strong>0.0124 &lt; 0.05</strong><br>
      → Reject H₀. The machine is not producing 500g on average.</p>
    </div>
  </div>

  <div class="lab-section">
    <div class="lab-top">⚗️ Lab Session · 10 hrs</div>
    <h3>Hypothesis Testing in R/Python</h3>
    <ul class="lab-list">
      <li>One-sample z-test and t-test: t.test() in R, scipy.stats in Python</li>
      <li>Two-sample tests for difference of means</li>
      <li>Proportion tests: prop.test() in R</li>
      <li>Computing confidence intervals manually and using functions</li>
      <li>Visualising sampling distributions and rejection regions</li>
      <li>Interpreting p-values and stating conclusions</li>
    </ul>
  </div>

  <div class="ch-nav">
    <a href="#" class="ch-nav-btn" onclick="showPage('ch3');return false">← &nbsp;Chapter 3</a>
    <a href="#" class="ch-nav-btn" onclick="showPage('home');return false">⌂ Home</a>
    <a href="#" class="ch-nav-btn" onclick="showPage('ch5');return false">Chapter 5 &nbsp;→</a>
  </div>
</div>
</div>

<!-- CHAPTER 5 -->
<div class="page" id="page-ch5">
<div class="ch-page">
  <div class="ch-topbar">
    <div class="ch-badge"><span class="ch-unit-pill u3">Unit III</span><span class="ch-num">Chapter 05</span></div>
    <span class="ch-hrs-badge">05 hrs</span>
  </div>
  <h1 class="ch-title">Correlation &amp; Regression</h1>
  <p class="ch-intro">Correlation measures the strength and direction of a linear relationship between two variables. Regression builds predictive models to estimate one variable from another — or from many others.</p>

  <div class="content-section">
    <h2 class="section-heading">5.1 Correlation</h2>
    <div class="def-box"><div class="def-title">Key Principle</div><div class="def-text">Correlation measures association, NOT causation. Two variables can be strongly correlated due to a third "confounding" variable or pure coincidence (spurious correlation).</div></div>
    <div class="formula-box">
      <div class="formula-label">Pearson's Correlation Coefficient (r)</div>
      <div class="formula">r = Σ(xᵢ−x̄)(yᵢ−ȳ) / √[Σ(xᵢ−x̄)² · Σ(yᵢ−ȳ)²]<br>r = Cov(X,Y) / (σ_x · σ_y) &nbsp;&nbsp;&nbsp; −1 ≤ r ≤ 1</div>
    </div>
    <table class="content-table">
      <tr><th>r value</th><th>Interpretation</th></tr>
      <tr><td>r = +1</td><td>Perfect positive linear correlation</td></tr>
      <tr><td>0.7 ≤ r &lt; 1</td><td>Strong positive correlation</td></tr>
      <tr><td>0 &lt; r &lt; 0.7</td><td>Moderate/weak positive correlation</td></tr>
      <tr><td>r = 0</td><td>No linear correlation</td></tr>
      <tr><td>−0.7 &lt; r &lt; 0</td><td>Moderate/weak negative correlation</td></tr>
      <tr><td>r = −1</td><td>Perfect negative linear correlation</td></tr>
    </table>
  </div>

  <div class="content-section">
    <h2 class="section-heading">5.2 Simple Linear Regression</h2>
    <div class="def-box"><div class="def-title">Least Squares Method</div><div class="def-text">Finds the line ŷ = β₀ + β₁x that minimises the Sum of Squared Errors (SSE = Σ(yᵢ − ŷᵢ)²). This line is the best linear unbiased estimator (BLUE).</div></div>
    <div class="formula-box">
      <div class="formula-label">Estimated Regression Coefficients</div>
      <div class="formula">β̂₁ = Σ(xᵢ−x̄)(yᵢ−ȳ) / Σ(xᵢ−x̄)² = Sxy / Sxx<br><br>β̂₀ = ȳ − β̂₁x̄ &nbsp;&nbsp;&nbsp; (line passes through (x̄, ȳ))</div>
    </div>
    <div class="formula-box">
      <div class="formula-label">Coefficient of Determination (R²)</div>
      <div class="formula">R² = SSR/SST = 1 − SSE/SST &nbsp;&nbsp;&nbsp; 0 ≤ R² ≤ 1<br><br>SST = Σ(yᵢ−ȳ)² &nbsp;[Total] &nbsp;&nbsp; SSR = Σ(ŷᵢ−ȳ)² &nbsp;[Regression]<br>SSE = Σ(yᵢ−ŷᵢ)² &nbsp;[Residual/Error]</div>
    </div>
    <p class="body-text">R² = 0.85 means 85% of variation in Y is explained by the regression model. The remaining 15% is unexplained (residual).</p>

    <h3 class="subsection-heading">ANOVA Table for Regression</h3>
    <table class="content-table">
      <tr><th>Source</th><th>SS</th><th>df</th><th>MS</th><th>F-statistic</th></tr>
      <tr><td>Regression</td><td>SSR</td><td>k</td><td>MSR = SSR/k</td><td>F = MSR/MSE</td></tr>
      <tr><td>Residual (Error)</td><td>SSE</td><td>n−k−1</td><td>MSE = SSE/(n−k−1)</td><td>—</td></tr>
      <tr><td>Total</td><td>SST</td><td>n−1</td><td>—</td><td>—</td></tr>
    </table>
    <p class="body-text">H₀: β₁=0 (no linear relationship). Reject H₀ if F &gt; F_critical or p &lt; α → model is significant.</p>
    <div class="example-box">
      <div class="example-label">Example</div>
      <p>Study hours (x) vs Exam marks (y) for 5 students.<br>
      x: 1,2,3,4,5 &nbsp;·&nbsp; y: 50,55,65,70,80<br>
      x̄=3, ȳ=64 &nbsp;·&nbsp; Sxy=35, Sxx=10<br>
      β̂₁ = 35/10 = <strong>3.5</strong> &nbsp;·&nbsp; β̂₀ = 64 − 3.5×3 = <strong>53.5</strong><br>
      Regression line: ŷ = 53.5 + 3.5x &nbsp;→ each extra study hour adds 3.5 marks.</p>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">5.3 Multiple Linear Regression</h2>
    <div class="formula-box">
      <div class="formula-label">Multiple Regression Model</div>
      <div class="formula">Y = β₀ + β₁x₁ + β₂x₂ + ... + βₖxₖ + ε<br><br>Matrix form: Y = Xβ + ε<br>β̂ = (XᵀX)⁻¹ Xᵀy</div>
    </div>
    <ul class="key-list orange">
      <li>Each βᵢ = partial slope — change in Y per unit increase in xᵢ (holding all other xⱼ constant)</li>
      <li>Adjusted R² = 1 − [(1−R²)(n−1)/(n−k−1)] — penalises for adding unnecessary predictors</li>
      <li>Check: multicollinearity (VIF &gt; 10 is problematic), residual normality, homoscedasticity</li>
      <li>Dummy variables for categorical predictors (k categories → k−1 dummies)</li>
    </ul>
  </div>

  <div class="content-section">
    <h2 class="section-heading">5.4 Logistic Regression</h2>
    <div class="def-box orange"><div class="def-title">When to Use</div><div class="def-text">When Y is binary (0 or 1): pass/fail, disease/no disease, spam/not spam. Linear regression fails here because predicted values can exceed [0,1]. Logistic regression models P(Y=1|X).</div></div>
    <div class="formula-box">
      <div class="formula-label">Logistic (Sigmoid) Function</div>
      <div class="formula">P(Y=1|X) = 1/(1 + e⁻ᶻ) &nbsp;&nbsp; where z = β₀ + β₁x₁ + ... + βₖxₖ<br><br>Log-odds (Logit): ln[P/(1−P)] = β₀ + β₁x₁ + ...<br><br>Decision: predict Y=1 if P ≥ 0.5, else Y=0</div>
    </div>
    <ul class="key-list orange">
      <li>eᵝ¹ = odds ratio — multiplicative change in odds per unit increase in x₁</li>
      <li>Parameters estimated by Maximum Likelihood Estimation (MLE), not least squares</li>
      <li>Evaluated using confusion matrix: accuracy, precision, recall, F1-score</li>
      <li>Fundamental algorithm in binary classification in machine learning</li>
    </ul>
  </div>

  <div class="lab-section orange">
    <div class="lab-top">⚗️ Lab Session · 08 hrs</div>
    <h3>Regression Analysis</h3>
    <ul class="lab-list">
      <li>Scatter plots and Pearson correlation coefficient</li>
      <li>Simple linear regression: lm() in R / LinearRegression in sklearn</li>
      <li>ANOVA table for regression: anova(lm_model) in R</li>
      <li>Residual diagnostics: normality, heteroscedasticity, influential points</li>
      <li>Multiple regression with ANOVA approach</li>
      <li>Logistic regression: glm(family=binomial) in R, confusion matrix evaluation</li>
    </ul>
  </div>

  <div class="ch-nav">
    <a href="#" class="ch-nav-btn" onclick="showPage('ch4');return false">← &nbsp;Chapter 4</a>
    <a href="#" class="ch-nav-btn" onclick="showPage('home');return false">⌂ Home</a>
    <a href="#" class="ch-nav-btn" onclick="showPage('ch6');return false">Chapter 6 &nbsp;→</a>
  </div>
</div>
</div>

<!-- CHAPTER 6 -->
<div class="page" id="page-ch6">
<div class="ch-page">
  <div class="ch-topbar">
    <div class="ch-badge"><span class="ch-unit-pill u3">Unit III</span><span class="ch-num">Chapter 06</span></div>
    <span class="ch-hrs-badge">05 hrs</span>
  </div>
  <h1 class="ch-title">Statistical Inference II</h1>
  <p class="ch-intro">This chapter covers non-parametric tests and goodness-of-fit procedures for categorical data — tools for when parametric assumptions (normality, equal variance) cannot be met.</p>

  <div class="content-section">
    <h2 class="section-heading">6.1 Chi-Square Test for Independence</h2>
    <div class="def-box"><div class="def-title">Purpose</div><div class="def-text">Tests whether two categorical variables are statistically independent (not associated). Data is arranged in a contingency table of observed frequencies.</div></div>
    <div class="formula-box">
      <div class="formula-label">Chi-Square Test Statistic</div>
      <div class="formula">χ² = Σᵢ Σⱼ (Oᵢⱼ − Eᵢⱼ)² / Eᵢⱼ<br><br>Eᵢⱼ = (Row i total × Column j total) / Grand total N<br><br>df = (r−1)(c−1) for r×c table</div>
    </div>
    <ul class="key-list orange">
      <li>H₀: The two categorical variables are independent</li>
      <li>H₁: The two variables are associated (dependent)</li>
      <li>Reject H₀ if χ² &gt; χ²_critical (from table) or p-value &lt; α</li>
      <li>Assumption: all expected frequencies Eᵢⱼ ≥ 5 (merge cells if violated)</li>
    </ul>
    <div class="example-box">
      <div class="example-label">Example – 2×2 Contingency Table</div>
      <p>Testing whether smoking is associated with lung disease (n=200):</p>
      <table class="content-table" style="margin-top:8px;">
        <tr><th></th><th>Disease</th><th>No Disease</th><th>Total</th></tr>
        <tr><td>Smoker</td><td>O=40, E=25</td><td>O=60, E=75</td><td>100</td></tr>
        <tr><td>Non-smoker</td><td>O=10, E=25</td><td>O=90, E=75</td><td>100</td></tr>
        <tr><td>Total</td><td>50</td><td>150</td><td>200</td></tr>
      </table>
      <p style="margin-top:8px;">χ² = (40−25)²/25 + (60−75)²/75 + (10−25)²/25 + (90−75)²/75 = 9+3+9+3 = <strong>24</strong><br>
      df = (2−1)(2−1) = 1 &nbsp;·&nbsp; χ²_critical(0.05,1) = 3.841<br>
      24 &gt;&gt; 3.841 → <strong>Reject H₀. Smoking and lung disease are significantly associated.</strong></p>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">6.2 m × n Contingency Table</h2>
    <p class="body-text">The chi-square test generalises directly to tables with any number of rows (m) and columns (n).</p>
    <table class="content-table">
      <tr><th></th><th>B₁</th><th>B₂</th><th>…</th><th>Bₙ</th><th>Row Total</th></tr>
      <tr><td>A₁</td><td>O₁₁</td><td>O₁₂</td><td>…</td><td>O₁ₙ</td><td>R₁</td></tr>
      <tr><td>A₂</td><td>O₂₁</td><td>O₂₂</td><td>…</td><td>O₂ₙ</td><td>R₂</td></tr>
      <tr><td>…</td><td>…</td><td>…</td><td>…</td><td>…</td><td>…</td></tr>
      <tr><td>Col Total</td><td>C₁</td><td>C₂</td><td>…</td><td>Cₙ</td><td>N</td></tr>
    </table>
    <div class="formula-box">
      <div class="formula-label">Expected Frequency &amp; Degrees of Freedom</div>
      <div class="formula">Eᵢⱼ = Rᵢ × Cⱼ / N<br><br>df = (m−1)(c−1) &nbsp;&nbsp; where m=rows, c=columns</div>
    </div>
  </div>

  <div class="content-section">
    <h2 class="section-heading">6.3 Choosing a Test Procedure</h2>
    <table class="content-table">
      <tr><th>Situation</th><th>Appropriate Test</th></tr>
      <tr><td>Single mean vs known μ₀ (σ known)</td><td>Z-test</td></tr>
      <tr><td>Single mean vs known μ₀ (σ unknown)</td><td>One-sample t-test</td></tr>
      <tr><td>Two independent means</td><td>Two-sample t-test / Z-test</td></tr>
      <tr><td>Single proportion vs known p₀</td><td>Z-test for proportion</td></tr>
      <tr><td>Association between two categorical variables</td><td>Chi-square test of independence</td></tr>
      <tr><td>Does data fit a distribution?</td><td>Chi-square goodness-of-fit</td></tr>
      <tr><td>Does data follow a continuous distribution?</td><td>Kolmogorov-Smirnov (KS) test</td></tr>
    </table>
  </div>

  <div class="content-section">
    <h2 class="section-heading">6.4 Goodness of Fit Test</h2>
    <div class="def-box orange"><div class="def-title">Purpose</div><div class="def-text">Tests whether observed data comes from a specified theoretical distribution (Uniform, Normal, Poisson, Binomial, etc.).</div></div>
    <div class="formula-box">
      <div class="formula-label">Chi-Square Goodness-of-Fit</div>
      <div class="formula">χ² = Σᵢ (Oᵢ − Eᵢ)² / Eᵢ &nbsp;&nbsp; i = 1,2,...,k<br><br>H₀: Data follows the specified distribution<br>H₁: Data does not follow that distribution<br><br>df = k−1 (or k−1−p if p parameters estimated from data)</div>
    </div>
    <div class="example-box">
      <div class="example-label">Example – Fair Die Test</div>
      <p>A die is rolled 120 times. Expected frequency = 120/6 = 20 for each face.</p>
      <table class="content-table" style="margin-top:8px;">
        <tr><th>Face</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th><th>6</th></tr>
        <tr><td>Observed (O)</td><td>25</td><td>17</td><td>15</td><td>23</td><td>20</td><td>20</td></tr>
        <tr><td>Expected (E)</td><td>20</td><td>20</td><td>20</td><td>20</td><td>20</td><td>20</td></tr>
      </table>
      <p style="margin-top:8px;">χ² = (25)²/20 + (−3)²/20 + (−5)²/20 + (3)²/20 + 0 + 0 = 25/20+9/20+25/20+9/20 = <strong>3.4</strong><br>
      df = 5 &nbsp;·&nbsp; χ²_critical(0.05,5) = 11.07<br>
      3.4 &lt; 11.07 → <strong>Fail to reject H₀. No evidence that the die is unfair.</strong></p>
    </div>
    <ul class="key-list orange">
      <li>All expected frequencies must be ≥ 5 (merge adjacent classes if needed)</li>
      <li>If parameters estimated from data: subtract one df per estimated parameter</li>
      <li>Can test for Poisson, Binomial, Normal, Uniform, Exponential fit</li>
      <li>Kolmogorov-Smirnov (KS) test is an alternative for continuous distributions — does not require grouping into bins</li>
    </ul>
  </div>

  <div class="lab-section orange">
    <div class="lab-top">⚗️ Lab Session · 08 hrs (combined with Ch 5)</div>
    <h3>Chi-Square Tests in R/Python</h3>
    <ul class="lab-list">
      <li>Constructing contingency tables: table() / pd.crosstab()</li>
      <li>Chi-square test of independence: chisq.test() in R</li>
      <li>Computing expected frequencies and χ² statistic manually</li>
      <li>Goodness-of-fit for Uniform and Poisson distributions</li>
      <li>Kolmogorov-Smirnov test: ks.test() in R</li>
      <li>Visualising residuals from contingency table analysis</li>
    </ul>
  </div>

  <div class="ch-nav">
    <a href="#" class="ch-nav-btn" onclick="showPage('ch5');return false">← &nbsp;Chapter 5</a>
    <a href="#" class="ch-nav-btn" onclick="showPage('home');return false">⌂ Home</a>
    <a href="#" class="ch-nav-btn" onclick="showPage('books');return false">Books &nbsp;→</a>
  </div>
</div>
</div>

<!-- BOOKS PAGE -->
<div class="page" id="page-books">
<div class="books-page">
  <div class="books-inner">
    <h2 class="books-heading">📚 Text Books</h2>
    <div class="book-list">
      <div class="book-item"><span class="book-num">01</span><span class="book-text">Douglas C Montgomery, George C Runger — <strong>Applied Statistics for Engineers</strong>, 5th Edition, John Wiley and Sons</span></div>
      <div class="book-item"><span class="book-num">02</span><span class="book-text">Walpole, Myers, Myers, Ye — <strong>Probability and Statistics for Engineers and Scientists</strong>, 9th Edition, Prentice Hall</span></div>
      <div class="book-item"><span class="book-num">03</span><span class="book-text">J. Susan Milton, Jesse C. Arnold — <strong>Introduction to Probability and Statistics</strong>, 4th Ed, TATA McGraw-Hill Edition 2007</span></div>
    </div>
    <h2 class="books-heading" style="margin-top:40px;">📖 Reference Books</h2>
    <div class="book-list">
      <div class="book-item"><span class="book-num">R1</span><span class="book-text">Jiawei Han, Micheline Kamber — <strong>Data Mining: Concepts and Techniques</strong>, Morgan Kaufmann Publishers, 2005</span></div>
      <div class="book-item"><span class="book-num">R2</span><span class="book-text">Gupta S C and Kapoor V K — <strong>Fundamentals of Mathematical Statistics</strong>, 1ed, Sultan Chand &amp; Sons, New Delhi, 2000</span></div>
      <div class="book-item"><span class="book-num">R3</span><span class="book-text">Sheldon M. Ross — <strong>Introduction to Probability and Statistics for Engineers and Scientists</strong></span></div>
    </div>
    <div style="margin-top:44px;text-align:center;">
      <a href="#" onclick="showPage('home');return false" class="ch-nav-btn" style="display:inline-flex;background:rgba(255,255,255,0.1);border-color:rgba(255,255,255,0.2);color:#fff;">⌂ &nbsp;Back to Home</a>
    </div>
  </div>
</div>
<footer>
  <strong>Shrishail Sobarad</strong> &nbsp;·&nbsp; 02FE25BCI037 &nbsp;·&nbsp; CS AI – Semester 2 &nbsp;·&nbsp; KLE Tech University &nbsp;·&nbsp; 25EMAB104
</footer>
</div>

<script>
function showPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-links a').forEach(a => a.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  const navEl = document.getElementById('nav-' + id);
  if (navEl) navEl.classList.add('active');
  window.scrollTo({ top: 0, behavior: 'smooth' });
}
// Arrow key navigation
const pageOrder = ['home','ch1','ch2','ch3','ch4','ch5','ch6','books'];
document.addEventListener('keydown', e => {
  const cur = pageOrder.findIndex(p => document.getElementById('page-'+p).classList.contains('active'));
  if (e.key === 'ArrowRight' && cur < pageOrder.length-1) showPage(pageOrder[cur+1]);
  if (e.key === 'ArrowLeft' && cur > 0) showPage(pageOrder[cur-1]);
});
</script>
</body>
</html>
