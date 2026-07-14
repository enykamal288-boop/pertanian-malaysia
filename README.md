[index.html](https://github.com/user-attachments/files/29993745/index.html)
# pertanian-malaysia<!DOCTYPE html>
<html lang="ms">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Papan Pemuka Pertanian Malaysia — Banci Pertanian 2024</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,500;0,9..144,600;0,9..144,700;1,9..144,500&family=IBM+Plex+Sans:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css" />
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.4/chart.umd.min.js"></script>

<style>
  :root{
    --hijau-rimba:#123524;
    --hijau-rimba-2:#1a4531;
    --hijau-daun:#2f6b45;
    --emas-padi:#d9a92b;
    --emas-padi-terang:#f1c85c;
    --tanah-liat:#a3502e;
    --kertas:#f6f1e4;
    --kertas-pudar:#efe7d3;
    --teks-terang:#f6f2e6;
    --teks-muted:#c9d3c6;
    --garis:rgba(246,242,230,0.14);
    --font-display:'Fraunces', serif;
    --font-body:'IBM Plex Sans', sans-serif;
    --font-mono:'IBM Plex Mono', monospace;
  }
  *{box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    margin:0;
    background:var(--hijau-rimba);
    color:var(--teks-terang);
    font-family:var(--font-body);
    line-height:1.55;
  }
  a{color:var(--emas-padi-terang);}

  /* ---------- Motif padi (signature element) ---------- */
  .motif-padi{
    display:flex;
    align-items:center;
    gap:10px;
    opacity:0.85;
    margin:2.2rem 0;
  }
  .motif-padi .garis{flex:1;height:1px;background:linear-gradient(90deg,transparent,var(--emas-padi),transparent);}
  .motif-padi svg{width:34px;height:34px;flex-shrink:0;}

  /* ---------- Header ---------- */
  header.hero{
    position:relative;
    padding:4.6rem 6vw 3.4rem;
    background:
      radial-gradient(ellipse 90% 70% at 15% -10%, rgba(217,169,43,0.16), transparent 60%),
      radial-gradient(ellipse 70% 60% at 100% 0%, rgba(47,107,69,0.5), transparent 55%),
      var(--hijau-rimba);
    border-bottom:1px solid var(--garis);
    overflow:hidden;
  }
  header.hero::before{
    content:"";
    position:absolute; inset:0;
    background-image:repeating-linear-gradient(115deg, rgba(246,242,230,0.035) 0px, rgba(246,242,230,0.035) 1px, transparent 1px, transparent 64px);
    pointer-events:none;
  }
  .eyebrow{
    font-family:var(--font-mono);
    letter-spacing:0.14em;
    text-transform:uppercase;
    font-size:0.72rem;
    color:var(--emas-padi-terang);
    display:flex; align-items:center; gap:10px;
  }
  .eyebrow::before{content:"❖"; color:var(--emas-padi);}
  h1.judul{
    font-family:var(--font-display);
    font-weight:600;
    font-size:clamp(2.2rem, 5vw, 4rem);
    line-height:1.04;
    margin:0.6rem 0 0.9rem;
    max-width:16ch;
  }
  h1.judul em{font-style:italic; color:var(--emas-padi-terang); font-weight:500;}
  .subjudul{
    max-width:62ch;
    font-size:1.05rem;
    color:var(--teks-muted);
  }
  .hero-meta{
    margin-top:2.4rem;
    display:flex; flex-wrap:wrap; gap:2.2rem;
    font-family:var(--font-mono);
    font-size:0.78rem;
    color:var(--teks-muted);
  }
  .hero-meta strong{color:var(--teks-terang); display:block; font-family:var(--font-body); font-size:0.95rem; font-weight:600;}

  /* ---------- Layout umum ---------- */
  main{max-width:1240px; margin:0 auto; padding:0 6vw;}
  section{padding:3.6rem 0;}
  .label-seksyen{
    font-family:var(--font-mono);
    text-transform:uppercase;
    letter-spacing:0.12em;
    font-size:0.72rem;
    color:var(--emas-padi-terang);
    margin-bottom:0.6rem;
  }
  h2.tajuk-seksyen{
    font-family:var(--font-display);
    font-size:clamp(1.5rem,2.6vw,2.1rem);
    font-weight:600;
    margin:0 0 0.5rem;
  }
  p.keterangan-seksyen{
    color:var(--teks-muted);
    max-width:72ch;
    margin:0 0 2rem;
  }

  /* ---------- KPI ---------- */
  .kpi-grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
    gap:1px;
    background:var(--garis);
    border:1px solid var(--garis);
    border-radius:14px;
    overflow:hidden;
  }
  .kpi{
    background:var(--hijau-rimba-2);
    padding:1.5rem 1.4rem;
  }
  .kpi .angka{
    font-family:var(--font-mono);
    font-size:clamp(1.5rem,2.4vw,2rem);
    font-weight:600;
    color:var(--emas-padi-terang);
    display:block;
  }
  .kpi .ket{font-size:0.82rem; color:var(--teks-muted); margin-top:0.35rem;}

  /* ---------- Panel umum ---------- */
  .panel{
    background:var(--hijau-rimba-2);
    border:1px solid var(--garis);
    border-radius:16px;
    padding:1.6rem;
  }
  .grid-2{display:grid; grid-template-columns:1.35fr 1fr; gap:1.3rem;}
  @media (max-width:860px){.grid-2{grid-template-columns:1fr;}}

  /* ---------- Peta ---------- */
  #peta{height:480px; border-radius:12px; overflow:hidden; background:#0c2318;}
  .peta-kawalan{
    display:flex; align-items:center; justify-content:space-between; flex-wrap:wrap; gap:0.8rem;
    margin-bottom:1rem;
  }
  select#pilihMetrik{
    background:var(--hijau-rimba);
    color:var(--teks-terang);
    border:1px solid var(--garis);
    padding:0.55rem 0.8rem;
    border-radius:8px;
    font-family:var(--font-body);
    font-size:0.85rem;
  }
  .legenda{display:flex; align-items:center; gap:0.5rem; font-family:var(--font-mono); font-size:0.72rem; color:var(--teks-muted);}
  .legenda .swatch{width:16px;height:12px;border-radius:2px;}
  .peta-nota{font-size:0.78rem; color:var(--teks-muted); margin-top:0.8rem;}
  .leaflet-popup-content-wrapper{background:var(--hijau-rimba); color:var(--teks-terang); border-radius:10px;}
  .leaflet-popup-tip{background:var(--hijau-rimba);}
  .popup-negeri{font-family:var(--font-display); font-size:1.05rem; margin:0 0 4px;}
  .popup-baris{font-family:var(--font-mono); font-size:0.78rem; color:var(--teks-muted); margin:2px 0;}
  .popup-baris b{color:var(--emas-padi-terang);}
  #petaFallback{display:none; padding:2rem; text-align:center; color:var(--teks-muted); font-size:0.9rem;}

  /* ---------- Jadual negeri ---------- */
  .jadual-wrap{overflow-x:auto; border:1px solid var(--garis); border-radius:14px;}
  table{width:100%; border-collapse:collapse; font-size:0.86rem;}
  thead th{
    text-align:left;
    font-family:var(--font-mono);
    text-transform:uppercase;
    font-size:0.68rem;
    letter-spacing:0.08em;
    color:var(--emas-padi-terang);
    background:var(--hijau-rimba-2);
    padding:0.85rem 1rem;
    position:sticky; top:0;
  }
  tbody td{padding:0.75rem 1rem; border-top:1px solid var(--garis);}
  tbody tr:hover{background:rgba(217,169,43,0.06);}
  td.angka, th.angka{font-family:var(--font-mono); text-align:right;}
  .tanda-belum{color:var(--teks-muted); font-style:italic; font-size:0.82rem;}
  .bar-mini{height:6px; border-radius:3px; background:var(--garis); margin-top:6px; overflow:hidden;}
  .bar-mini > i{display:block; height:100%; background:linear-gradient(90deg,var(--emas-padi),var(--emas-padi-terang));}

  /* ---------- Carta ---------- */
  .carta-box{position:relative; height:340px;}
  .carta-box.pendek{height:260px;}

  /* ---------- Kad fokus ---------- */
  .fokus-grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(150px,1fr)); gap:1px; background:var(--garis); border:1px solid var(--garis); border-radius:14px; overflow:hidden; margin-bottom:1.4rem;}
  .fokus-kad{background:var(--hijau-rimba-2); padding:1.2rem;}
  .fokus-kad .angka{font-family:var(--font-mono); font-size:1.35rem; color:var(--emas-padi-terang); font-weight:600;}
  .fokus-kad .ket{font-size:0.78rem; color:var(--teks-muted); margin-top:0.3rem;}

  /* ---------- Huraian analisis ---------- */
  .analisis{
    columns:1;
    font-size:0.98rem;
  }
  .analisis h3{
    font-family:var(--font-display);
    font-weight:600;
    font-size:1.2rem;
    color:var(--emas-padi-terang);
    margin:1.6rem 0 0.5rem;
  }
  .analisis p{color:#e7e2d2; margin:0 0 1rem;}
  .analisis p:first-of-type::first-letter{
    font-family:var(--font-display);
    font-size:3rem;
    float:left;
    line-height:0.8;
    padding:0.1rem 0.5rem 0 0;
    color:var(--emas-padi-terang);
  }
  .petikan-stat{
    border-left:3px solid var(--emas-padi);
    padding:0.2rem 0 0.2rem 1rem;
    margin:1.4rem 0;
    color:var(--teks-muted);
    font-size:0.9rem;
  }

  /* ---------- Footer / sumber ---------- */
  footer{
    border-top:1px solid var(--garis);
    padding:3rem 6vw 3.5rem;
    background:var(--hijau-rimba-2);
  }
  footer h4{font-family:var(--font-display); font-size:1.1rem; margin:0 0 0.9rem; color:var(--emas-padi-terang);}
  .sumber-list{list-style:none; margin:0; padding:0; display:grid; grid-template-columns:repeat(auto-fit,minmax(260px,1fr)); gap:0.6rem 2rem; font-size:0.83rem; color:var(--teks-muted);}
  .sumber-list li{padding-left:1.1rem; position:relative;}
  .sumber-list li::before{content:"›"; position:absolute; left:0; color:var(--emas-padi);}
  .disclaimer{margin-top:1.8rem; font-size:0.78rem; color:var(--teks-muted); max-width:80ch; border-top:1px dashed var(--garis); padding-top:1.2rem;}
  .footer-bawah{margin-top:1.8rem; font-family:var(--font-mono); font-size:0.72rem; color:var(--teks-muted); display:flex; justify-content:space-between; flex-wrap:wrap; gap:0.5rem;}

  @media (max-width:600px){
    header.hero{padding:3.4rem 5vw 2.4rem;}
    section{padding:2.4rem 0;}
  }
</style>
</head>
<body>

<header class="hero">
  <div class="eyebrow">Papan Pemuka Data Terbuka · Sektor Pertanian</div>
  <h1 class="judul">Peta hasil bumi <em>Malaysia</em>, negeri demi negeri.</h1>
  <p class="subjudul">Gambaran data pertanian kebangsaan — pendapatan sektor, keluasan tanaman utama, hasil padi dan kelapa sawit — disusun daripada Banci Pertanian 2024 (DOSM) dan sumber rasmi lain, disemak dan disahkan sebelum dipaparkan.</p>
  <div class="hero-meta">
    <div><strong>RM186.43 bilion</strong>pendapatan sektor pertanian negara, 2023</div>
    <div><strong>1.03 juta</strong>pegangan pertanian berdaftar</div>
    <div><strong>16 negeri</strong>+ WP diliputi peta interaktif</div>
    <div><strong>Julai 2026</strong>dashboard disusun · rujukan data 2022–2023</div>
  </div>
</header>

<main>

  <!-- ================= KPI ================= -->
  <section id="kpi">
    <div class="kpi-grid">
      <div class="kpi"><span class="angka">RM186.43B</span><span class="ket">Pendapatan sektor pertanian negara (2023)</span></div>
      <div class="kpi"><span class="angka">RM92.68B</span><span class="ket">Sumbangan kelapa sawit — 49.7% pendapatan pertanian negara</span></div>
      <div class="kpi"><span class="angka">5.65 juta ha</span><span class="ket">Keluasan tanaman kelapa sawit negara (2023)</span></div>
      <div class="kpi"><span class="angka">2.19 juta tan</span><span class="ket">Pengeluaran padi negara setahun</span></div>
      <div class="kpi"><span class="angka">1.03 juta</span><span class="ket">Pegangan pertanian — 98% diusahakan individu</span></div>
    </div>
  </section>

  <div class="motif-padi"><div class="garis"></div>
    <svg viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M50 95V45" stroke="#d9a92b" stroke-width="3" stroke-linecap="round"/>
      <path d="M50 55C40 45 30 40 25 25C38 28 46 38 50 48" fill="#2f6b45"/>
      <path d="M50 55C60 45 70 40 75 25C62 28 54 38 50 48" fill="#2f6b45"/>
      <ellipse cx="50" cy="30" rx="7" ry="14" fill="#f1c85c"/>
      <ellipse cx="42" cy="18" rx="5" ry="10" fill="#f1c85c" transform="rotate(-25 42 18)"/>
      <ellipse cx="58" cy="18" rx="5" ry="10" fill="#f1c85c" transform="rotate(25 58 18)"/>
    </svg>
  <div class="garis"></div></div>

  <!-- ================= PETA ================= -->
  <section id="peta-seksyen">
    <div class="label-seksyen">Peta Interaktif</div>
    <h2 class="tajuk-seksyen">Pendapatan sektor pertanian mengikut negeri</h2>
    <p class="keterangan-seksyen">Peta jalan (street map) interaktif berasaskan Leaflet/OpenStreetMap. Warna lebih gelap menunjukkan pendapatan sektor pertanian lebih tinggi (RM bilion, tahun rujukan 2023). Klik atau sentuh sesebuah negeri untuk butiran penuh.</p>

    <div class="panel">
      <div class="peta-kawalan">
        <select id="pilihMetrik">
          <option value="pendapatan">Pendapatan sektor pertanian (RM bilion, 2023)</option>
        </select>
        <div class="legenda">
          <span>Rendah</span>
          <span class="swatch" style="background:#3c4a34"></span>
          <span class="swatch" style="background:#6b7d3f"></span>
          <span class="swatch" style="background:#a89a3a"></span>
          <span class="swatch" style="background:#d9a92b"></span>
          <span class="swatch" style="background:#f1c85c"></span>
          <span>Tinggi</span>
          <span style="margin-left:10px; opacity:0.6;">■ Kelabu = belum diterbitkan</span>
        </div>
      </div>
      <div id="peta"></div>
      <div id="petaFallback">Peta tidak dapat dimuatkan (sempadan negeri gagal diambil dari sumber luar). Sila lihat jadual penuh dan carta di bawah — semua data tetap tersedia.</div>
      <p class="peta-nota">Sempadan negeri: geoBoundaries.org (ODbL) · Peta jalan: OpenStreetMap contributors. Data pendapatan tersedia untuk 8 daripada 16 negeri setakat laporan negeri Banci Pertanian 2024 diterbitkan (April 2026); baki negeri akan dikemas kini apabila laporan rasmi masing-masing terbit.</p>
    </div>
  </section>

  <!-- ================= RANKING + PECAHAN TANAMAN ================= -->
  <section id="carta-utama">
    <div class="label-seksyen">Analisis Perbandingan</div>
    <h2 class="tajuk-seksyen">Kedudukan negeri &amp; struktur pendapatan tanaman</h2>
    <p class="keterangan-seksyen">Johor, Sarawak, Sabah dan Pahang kekal peneraju pendapatan pertanian negara; kelapa sawit pula mendominasi struktur pendapatan tanaman kebangsaan berbanding komoditi lain.</p>

    <div class="grid-2">
      <div class="panel">
        <strong style="font-family:var(--font-display); font-size:1.05rem;">Kedudukan negeri ikut pendapatan pertanian 2023</strong>
        <div class="carta-box"><canvas id="cartaRanking"></canvas></div>
      </div>
      <div class="panel">
        <strong style="font-family:var(--font-display); font-size:1.05rem;">Pendapatan tanaman kebangsaan ikut jenis</strong>
        <div class="carta-box"><canvas id="cartaJenisTanaman"></canvas></div>
      </div>
    </div>
  </section>

  <!-- ================= FOKUS PADI ================= -->
  <section id="fokus-padi">
    <div class="label-seksyen">Fokus Komoditi · 01</div>
    <h2 class="tajuk-seksyen">Padi — jelapang beras negara</h2>
    <p class="keterangan-seksyen">Kedah kekal jelapang padi utama negara, tetapi Selangor lebih cekap dari segi kebolehpasaran hasil.</p>

    <div class="fokus-grid">
      <div class="fokus-kad"><div class="angka">789,444 t</div><div class="ket">Pengeluaran padi Kedah/tahun — tertinggi negara</div></div>
      <div class="fokus-kad"><div class="angka">246,405 t</div><div class="ket">Pengeluaran padi Selangor/tahun — kedua tertinggi</div></div>
      <div class="fokus-kad"><div class="angka">99.4%</div><div class="ket">Kadar jualan padi Selangor (tertinggi negara)</div></div>
      <div class="fokus-kad"><div class="angka">~65%</div><div class="ket">Kadar sara diri beras negara (import baki 35%)</div></div>
      <div class="fokus-kad"><div class="angka">RM3.84B</div><div class="ket">Sumbangan padi kepada pendapatan pertanian negara</div></div>
    </div>

    <div class="panel">
      <strong style="font-family:var(--font-display); font-size:1.05rem;">Keluasan tanaman padi — 4 negeri jelapang utama (2022)</strong>
      <div class="carta-box pendek"><canvas id="cartaPadi"></canvas></div>
    </div>
  </section>

  <!-- ================= FOKUS SAWIT ================= -->
  <section id="fokus-sawit">
    <div class="label-seksyen">Fokus Komoditi · 02</div>
    <h2 class="tajuk-seksyen">Kelapa sawit — tulang belakang pertanian negara</h2>
    <p class="keterangan-seksyen">Sabah dan Sarawak menguasai keluasan tanaman sawit negara; Perak pula mencatatkan hasil buah tandan segar (BTS) tertinggi per hektar.</p>

    <div class="fokus-grid">
      <div class="fokus-kad"><div class="angka">1.58 juta ha</div><div class="ket">Keluasan sawit Sarawak — terbesar negara</div></div>
      <div class="fokus-kad"><div class="angka">1.54 juta ha</div><div class="ket">Keluasan sawit Sabah — kedua terbesar</div></div>
      <div class="fokus-kad"><div class="angka">16.70 t/ha</div><div class="ket">Purata hasil BTS negara 2024 (naik drpd 15.79, 2023)</div></div>
      <div class="fokus-kad"><div class="angka">21.01 t/ha</div><div class="ket">Hasil BTS tertinggi — Perak</div></div>
      <div class="fokus-kad"><div class="angka">12.33 t/ha</div><div class="ket">Hasil BTS terendah — Kelantan</div></div>
    </div>

    <div class="panel">
      <strong style="font-family:var(--font-display); font-size:1.05rem;">Taburan keluasan sawit — Semenanjung berbanding Sabah &amp; Sarawak (2023)</strong>
      <div class="carta-box pendek"><canvas id="cartaSawit"></canvas></div>
      <p class="peta-nota">Jumlah keluasan negara 2023: 5,652,569 ha, menyusut ~22,000 ha berbanding 2022 (5,674,742 ha) berikutan dasar had keluasan maksimum 6.5 juta ha dan tumpuan kepada tanaman semula berbanding pembukaan tanah baharu. Pekebun kecil persendirian menguasai 822,073 ha (14.5%), purata 3.9 ha seorang.</p>
    </div>
  </section>

  <!-- ================= PERBELANJAAN SUBSEKTOR ================= -->
  <section id="perbelanjaan">
    <div class="label-seksyen">Struktur Kos</div>
    <h2 class="tajuk-seksyen">Perbelanjaan sektor pertanian mengikut subsektor</h2>
    <p class="keterangan-seksyen">Daripada jumlah perbelanjaan sektor pertanian negara RM67.89 bilion (2023), subsektor tanaman mencatatkan perbelanjaan tertinggi.</p>
    <div class="panel">
      <div class="carta-box pendek"><canvas id="cartaPerbelanjaan"></canvas></div>
    </div>
  </section>

  <!-- ================= JADUAL NEGERI ================= -->
  <section id="jadual-seksyen">
    <div class="label-seksyen">Data Penuh</div>
    <h2 class="tajuk-seksyen">Jadual pendapatan sektor pertanian ikut negeri</h2>
    <p class="keterangan-seksyen">Susunan menurun ikut pendapatan sektor pertanian 2023. Negeri bertanda "Belum diterbitkan" belum mempunyai laporan Banci Pertanian 2024 peringkat negeri pada masa dashboard ini disusun.</p>
    <div class="jadual-wrap">
      <table>
        <thead>
          <tr>
            <th>Negeri</th>
            <th class="angka">Pendapatan pertanian (RM bilion, 2023)</th>
            <th>Subsektor tanaman</th>
            <th class="angka">Pegangan pertanian</th>
            <th>Catatan</th>
          </tr>
        </thead>
        <tbody id="badanJadual"></tbody>
      </table>
    </div>
  </section>

  <!-- ================= HURAIAN ANALISIS ================= -->
  <section id="analisis-seksyen">
    <div class="label-seksyen">Huraian &amp; Analisis</div>
    <h2 class="tajuk-seksyen">Membaca corak pertanian negara</h2>

    <div class="analisis">
      <p>Data Banci Pertanian 2024 yang diterbitkan secara berperingkat oleh Jabatan Perangkaan Malaysia (DOSM) memberi gambaran paling terkini dan menyeluruh tentang struktur ekonomi pertanian negara sejak banci sebelumnya. Pada tahun rujukan 2023, sektor pertanian negara mencatatkan pendapatan keseluruhan RM186.43 bilion, dengan subsektor tanaman menyumbang RM132.06 bilion atau lebih 70 peratus daripada jumlah tersebut — mengesahkan bahawa tanaman kekal sebagai enjin utama ekonomi pertanian Malaysia berbanding ternakan, perikanan, akuakultur mahupun perhutanan.</p>

      <h3>Sawit: satu tanaman, hampir separuh pendapatan</h3>
      <p>Daripada jumlah pendapatan subsektor tanaman itu, kelapa sawit bersendirian menyumbang RM92.68 bilion — bersamaan hampir 50 peratus daripada keseluruhan pendapatan sektor pertanian negara dan lebih 70 peratus daripada pendapatan subsektor tanaman sahaja. Jurang antara sawit dengan tanaman kedua tertinggi, buah-buahan (RM14.15 bilion), amat ketara. Struktur ini menjelaskan mengapa Sabah dan Sarawak — dua negeri dengan keluasan sawit terbesar, masing-masing melebihi 1.5 juta hektar — turut muncul antara tiga negeri berpendapatan pertanian tertinggi negara, bersama Johor yang turut didominasi tanaman sawit dalam keluasan bertanamnya yang melebihi 837,000 hektar.</p>
      <p>Namun pergantungan tinggi kepada satu komoditi turut membawa risiko konsentrasi. Dasar kerajaan yang mengehadkan keluasan maksimum tanaman sawit kepada 6.5 juta hektar dan menggalakkan tanaman semula berbanding pembukaan tanah baharu — tercermin pada penyusutan keluasan negara daripada 5,674,742 hektar (2022) kepada 5,652,569 hektar (2023) — menunjukkan hala tuju dasar kini lebih tertumpu kepada peningkatan produktiviti per hektar berbanding perluasan kawasan. Jurang hasil buah tandan segar (BTS) antara Perak (21.01 tan/ha) dan Kelantan (12.33 tan/ha) turut menunjukkan ruang besar untuk penambahbaikan amalan pertanian baik di sesetengah negeri.</p>

      <h3>Padi: konsentrasi geografi dan cabaran sara diri</h3>
      <p>Berbeza daripada sawit yang tersebar luas di Semenanjung dan Borneo, pengeluaran padi jauh lebih tertumpu. Kedah bersendirian menyumbang 789,444 tan metrik padi setahun — jauh mengatasi Selangor di kedudukan kedua dengan 246,405 tan metrik — mengukuhkan status Kedah sebagai jelapang padi negara menerusi kawasan pengairan Lembaga Kemajuan Pertanian Muda (MADA). Menariknya, walaupun keluasan dan pengeluaran Kedah jauh lebih besar, Selangor mencatatkan kadar jualan hasil tertinggi negara (99.4 peratus daripada pengeluaran berjaya dipasarkan), berbanding Kedah pada kadar 75.95 peratus — mencerminkan kelebihan Selangor dari segi kedekatan pasaran dan rantaian bekalan berbanding kelebihan semula jadi Kedah dari segi keluasan sawah.</p>
      <p>Pada peringkat negara, kadar sara diri beras kekal sekitar 65 peratus, bermakna hampir satu pertiga keperluan beras negara masih bergantung kepada import daripada negara seperti India, Pakistan, Myanmar, Thailand dan Kemboja. Ini menjadikan padi bukan sekadar isu ekonomi tetapi juga isu keterjaminan makanan negara — walaupun sumbangannya kepada pendapatan pertanian (RM3.84 bilion) jauh lebih kecil berbanding sawit.</p>

      <h3>Jurang pendapatan antara negeri dan antara jenis pegangan</h3>
      <p>Data yang tersedia setakat ini menunjukkan jurang ketara antara negeri berpendapatan pertanian tertinggi (Johor, RM30.15 bilion) dengan negeri terendah dalam senarai yang telah diterbitkan (Terengganu, RM5.98 bilion) — perbezaan lebih lima kali ganda. Struktur pegangan turut menunjukkan ketidakseimbangan: pegangan pertanian yang diusahakan oleh pertubuhan (syarikat, ladang korporat) hanya merupakan 2 peratus daripada jumlah 1.03 juta pegangan berdaftar, namun menyumbang 73 peratus daripada jumlah pendapatan sektor pertanian negara. Sebaliknya, 98 peratus pegangan yang diusahakan secara individu — kebanyakannya pekebun kecil dan petani keluarga — hanya berkongsi baki 27 peratus pendapatan. Corak ini konsisten di peringkat negeri; di Johor misalnya, subsektor tanaman menyumbang 73.5 peratus pendapatan pertanian negeri, manakala di Pahang angka itu lebih tinggi lagi pada 88.7 peratus.</p>

      <div class="petikan-stat">Nota metodologi: laporan Banci Pertanian 2024 peringkat negeri diterbitkan secara berperingkat oleh DOSM sepanjang 2025–2026. Setakat dashboard ini disusun, lapan daripada enam belas negeri/WP telah menerbitkan angka pendapatan pertanian lengkap. Baki negeri akan dikemas kini apabila laporan rasmi masing-masing diterbitkan.</div>

      <h3>Kesimpulan ringkas</h3>
      <p>Secara keseluruhan, landskap pertanian Malaysia memaparkan dua wajah serentak: sebuah industri komoditi eksport bernilai tinggi yang diterajui sawit dan disokong oleh ladang korporat berskala besar di Sabah, Sarawak dan Johor; dan satu lagi sistem pertanian sara diri serta separa komersil berskala kecil — terutamanya padi dan tanaman makanan — yang tertumpu di kawasan seperti Kedah, Perak dan Kelantan, dengan margin pendapatan yang jauh lebih nipis. Dasar pertanian negara pada masa hadapan berkemungkinan perlu mengimbangi dua keutamaan berbeza ini: mengekalkan daya saing eksport sawit sambil mengukuhkan keterjaminan makanan domestik menerusi sektor padi dan tanaman makanan.</p>
    </div>
  </section>

</main>

<footer>
  <h4>Sumber data &amp; rujukan</h4>
  <ul class="sumber-list">
    <li>Jabatan Perangkaan Malaysia (DOSM) — Laporan Banci Pertanian 2024, peringkat kebangsaan &amp; negeri (rujukan tahun 2023), diterbitkan berperingkat 2025–2026 · dosm.gov.my</li>
    <li>DOSM / data.gov.my — OpenDOSM, dataset "Keluasan dan Pengeluaran Tanaman mengikut Negeri", 2017–2022</li>
    <li>Lembaga Minyak Sawit Malaysia (MPOB) — statistik keluasan &amp; hasil BTS kelapa sawit 2023–2024</li>
    <li>Malaysian Palm Oil Green Conservation Foundation (MPOGCF) — infografik keluasan tanaman sawit mengikut negeri</li>
    <li>Liputan media rasmi pelancaran Laporan Banci Pertanian 2024 Negeri — Bernama, portal kerajaan negeri &amp; MKN</li>
    <li>geoBoundaries.org — sempadan geografi ADM1 Malaysia (lesen ODbL) · OpenStreetMap contributors</li>
  </ul>
  <p class="disclaimer">Dashboard ini disusun untuk tujuan gambaran dan pendidikan berdasarkan angka yang disemak daripada sumber terbuka rasmi di atas pada tarikh penyusunan. Sesetengah data negeri masih belum diterbitkan sepenuhnya oleh DOSM dan ditanda secara jelas dalam peta serta jadual. Untuk keputusan dasar, rujukan komersil atau penerbitan rasmi, sila rujuk terus penerbitan asal di dosm.gov.my dan data.gov.my kerana angka mungkin disemak semula dari semasa ke semasa.</p>
  <div class="footer-bawah">
    <span>Papan Pemuka Pertanian Malaysia · disusun 14 Julai 2026</span>
    <span>Reka bentuk: Leaflet + Chart.js · Data: sumber terbuka kerajaan Malaysia</span>
  </div>
</footer>

<script>
/* ======================================================================
   DATA PERTANIAN NEGERI — disahkan daripada Banci Pertanian 2024 (DOSM)
   dan sumber rasmi lain yang disenaraikan dalam footer.
   ====================================================================== */
const dataNegeri = {
  "Johor":            { pendapatan: 30.15, tanamanPct: 73.5, pegangan: 106003, catatan: "Pendapatan tertinggi negara · keluasan bertanam >837,000 ha, sawit dominan · guna tenaga 210,575 orang" },
  "Sarawak":          { pendapatan: 29.18, tanamanPct: null, pegangan: null,   catatan: "Keluasan sawit terbesar negara (1.58 juta ha)" },
  "Sabah":            { pendapatan: 28.22, tanamanPct: null, pegangan: null,   catatan: "Keluasan sawit kedua terbesar negara (1.54 juta ha)" },
  "Pahang":           { pendapatan: 27.12, tanamanPct: 88.7, pegangan: null,   catatan: "Guna tenaga pertanian 193,216 orang (79.4% subsektor tanaman)" },
  "Perak":            { pendapatan: 17.69, tanamanPct: 52.8, pegangan: null,   catatan: "Hasil BTS sawit tertinggi negara (21.01 t/ha) · peneraju akuakultur ikan air tawar" },
  "Selangor":         { pendapatan: 8.68,  tanamanPct: null, pegangan: 37579,  catatan: "Kadar jualan padi tertinggi negara (99.4%)" },
  "Kelantan":         { pendapatan: 7.84,  tanamanPct: 84.8, pegangan: null,   catatan: "Hasil BTS sawit terendah negara (12.33 t/ha)" },
  "Terengganu":       { pendapatan: 5.98,  tanamanPct: 76.0, pegangan: 73089,  catatan: "Keluasan bertanam 227,904 ha — sawit, getah, padi, buah-buahan" },
  "Kedah":            { pendapatan: null,  tanamanPct: null, pegangan: null,   catatan: "Jelapang padi negara — 789,444 t padi/tahun (data padi sahaja tersedia)" },
  "Melaka":           { pendapatan: null,  tanamanPct: null, pegangan: null,   catatan: "Laporan negeri belum diterbitkan" },
  "Negeri Sembilan":  { pendapatan: null,  tanamanPct: null, pegangan: null,   catatan: "Laporan negeri belum diterbitkan" },
  "Perlis":           { pendapatan: null,  tanamanPct: null, pegangan: null,   catatan: "Laporan negeri belum diterbitkan" },
  "Pulau Pinang":     { pendapatan: null,  tanamanPct: null, pegangan: null,   catatan: "Laporan negeri belum diterbitkan" },
  "W.P. Kuala Lumpur":{ pendapatan: null,  tanamanPct: null, pegangan: null,   catatan: "Kawasan bandar — aktiviti pertanian komersil terhad" },
  "W.P. Labuan":      { pendapatan: null,  tanamanPct: null, pegangan: null,   catatan: "Laporan negeri belum diterbitkan" },
  "W.P. Putrajaya":   { pendapatan: null,  tanamanPct: null, pegangan: null,   catatan: "Tiada aktiviti pertanian komersil (DOSM)" }
};

// Alias untuk padanan nama dari fail GeoJSON (geoBoundaries) ke dataNegeri
const aliasNegeri = {
  "johor":"Johor","kedah":"Kedah","kelantan":"Kelantan","melaka":"Melaka","malacca":"Melaka",
  "negeri sembilan":"Negeri Sembilan","pahang":"Pahang","perak":"Perak","perlis":"Perlis",
  "pulau pinang":"Pulau Pinang","penang":"Pulau Pinang","sabah":"Sabah","sarawak":"Sarawak",
  "selangor":"Selangor","terengganu":"Terengganu",
  "kuala lumpur":"W.P. Kuala Lumpur","w.p. kuala lumpur":"W.P. Kuala Lumpur","wilayah persekutuan kuala lumpur":"W.P. Kuala Lumpur",
  "labuan":"W.P. Labuan","w.p. labuan":"W.P. Labuan","wilayah persekutuan labuan":"W.P. Labuan",
  "putrajaya":"W.P. Putrajaya","w.p. putrajaya":"W.P. Putrajaya","wilayah persekutuan putrajaya":"W.P. Putrajaya"
};
function padankanNama(namaMentah){
  if(!namaMentah) return null;
  const bersih = namaMentah.toLowerCase().trim();
  if(aliasNegeri[bersih]) return aliasNegeri[bersih];
  for(const k in aliasNegeri){ if(bersih.includes(k)) return aliasNegeri[k]; }
  return null;
}

function warnaIkutNilai(v){
  if(v===null||v===undefined) return "#3a4038"; // kelabu = belum diterbitkan
  if(v < 8)  return "#3c4a34";
  if(v < 15) return "#6b7d3f";
  if(v < 20) return "#a89a3a";
  if(v < 28) return "#d9a92b";
  return "#f1c85c";
}

/* ---------------- PETA ---------------- */
(function initPeta(){
  const peta = L.map('peta', {scrollWheelZoom:false, zoomControl:true}).setView([4.2, 108.5], 5.3);
  L.tileLayer('https://{s}.basemaps.cartocdn.com/dark_nolabels/{z}/{x}/{y}{r}.png', {
    attribution:'&copy; OpenStreetMap contributors &copy; CARTO',
    subdomains:'abcd', maxZoom:12
  }).addTo(peta);

  const urlGeo = "https://raw.githubusercontent.com/wmgeolab/geoBoundaries/9469f09/releaseData/gbOpen/MYS/ADM1/geoBoundaries-MYS-ADM1_simplified.geojson";

  fetch(urlGeo).then(r=>{ if(!r.ok) throw new Error('gagal'); return r.json(); }).then(geo=>{
    const layer = L.geoJSON(geo, {
      style: feature=>{
        const namaProp = feature.properties.shapeName || feature.properties.name || feature.properties.NAME_1 || "";
        const kunci = padankanNama(namaProp);
        const nilai = kunci && dataNegeri[kunci] ? dataNegeri[kunci].pendapatan : null;
        return {
          fillColor: warnaIkutNilai(nilai),
          fillOpacity: 0.82,
          color: "#f6f2e6",
          weight: 0.8,
          opacity: 0.5
        };
      },
      onEachFeature:(feature, lyr)=>{
        const namaProp = feature.properties.shapeName || feature.properties.name || feature.properties.NAME_1 || "Negeri";
        const kunci = padankanNama(namaProp);
        const d = kunci ? dataNegeri[kunci] : null;
        const namaPaparan = kunci || namaProp;
        let html = `<div class="popup-negeri">${namaPaparan}</div>`;
        if(d && d.pendapatan!==null){
          html += `<div class="popup-baris">Pendapatan pertanian: <b>RM${d.pendapatan.toFixed(2)} bilion</b> (2023)</div>`;
          if(d.tanamanPct) html += `<div class="popup-baris">Subsektor tanaman: <b>${d.tanamanPct}%</b> drpd pendapatan</div>`;
          if(d.pegangan) html += `<div class="popup-baris">Pegangan pertanian: <b>${d.pegangan.toLocaleString('ms-MY')}</b></div>`;
          html += `<div class="popup-baris" style="max-width:220px; margin-top:6px;">${d.catatan}</div>`;
        } else {
          html += `<div class="popup-baris">Data pendapatan: <b>belum diterbitkan</b></div>`;
          if(d && d.catatan) html += `<div class="popup-baris" style="max-width:220px;">${d.catatan}</div>`;
        }
        lyr.bindPopup(html);
        lyr.on('mouseover', ()=> lyr.setStyle({fillOpacity:1, weight:1.6}));
        lyr.on('mouseout',  ()=> lyr.setStyle({fillOpacity:0.82, weight:0.8}));
      }
    }).addTo(peta);
    try{ peta.fitBounds(layer.getBounds(), {padding:[18,18]}); }catch(e){}
  }).catch(err=>{
    document.getElementById('peta').style.display='none';
    document.getElementById('petaFallback').style.display='block';
    console.warn('Gagal memuatkan GeoJSON negeri:', err);
  });
})();

/* ---------------- WARNA CHART.JS SEPADAN TEMA ---------------- */
Chart.defaults.color = "#c9d3c6";
Chart.defaults.font.family = "'IBM Plex Sans', sans-serif";
Chart.defaults.borderColor = "rgba(246,242,230,0.12)";

/* ---------------- CARTA: RANKING NEGERI ---------------- */
(function(){
  const senarai = Object.entries(dataNegeri)
    .filter(([,v])=>v.pendapatan!==null)
    .sort((a,b)=>b[1].pendapatan-a[1].pendapatan);
  new Chart(document.getElementById('cartaRanking'), {
    type:'bar',
    data:{
      labels: senarai.map(s=>s[0]),
      datasets:[{
        label:'RM bilion',
        data: senarai.map(s=>s[1].pendapatan),
        backgroundColor: senarai.map(s=>warnaIkutNilai(s[1].pendapatan)),
        borderRadius:5, maxBarThickness:26
      }]
    },
    options:{
      indexAxis:'y',
      plugins:{legend:{display:false}, tooltip:{callbacks:{label:c=>`RM${c.raw} bilion`}}},
      scales:{ x:{grid:{color:'rgba(246,242,230,0.08)'}, ticks:{callback:v=>'RM'+v+'B'}}, y:{grid:{display:false}} }
    }
  });
})();

/* ---------------- CARTA: JENIS TANAMAN ---------------- */
new Chart(document.getElementById('cartaJenisTanaman'), {
  type:'bar',
  data:{
    labels:['Kelapa sawit','Buah-buahan','Sayur-sayuran','Getah','Padi','Nanas'],
    datasets:[{
      data:[92.68,14.15,10.90,4.27,3.84,2.33],
      backgroundColor:['#f1c85c','#d9a92b','#a89a3a','#6b7d3f','#3c4a34','#a3502e'],
      borderRadius:5
    }]
  },
  options:{
    plugins:{legend:{display:false}, tooltip:{callbacks:{label:c=>`RM${c.raw} bilion`}}},
    scales:{ y:{grid:{color:'rgba(246,242,230,0.08)'}, ticks:{callback:v=>'RM'+v+'B'}}, x:{grid:{display:false}} }
  }
});

/* ---------------- CARTA: PADI IKUT NEGERI (keluasan 2022) ---------------- */
new Chart(document.getElementById('cartaPadi'), {
  type:'bar',
  data:{
    labels:['Kedah','Sarawak','Perak','Kelantan'],
    datasets:[{
      label:'Keluasan tanaman padi (ribu ha, 2022)',
      data:[213.7, 77.7, 74.6, 74.0],
      backgroundColor:'#d9a92b', borderRadius:5, maxBarThickness:44
    }]
  },
  options:{
    plugins:{legend:{display:false}, tooltip:{callbacks:{label:c=>`${c.raw} ribu ha`}}},
    scales:{ y:{grid:{color:'rgba(246,242,230,0.08)'}, ticks:{callback:v=>v+'k ha'}}, x:{grid:{display:false}} }
  }
});

/* ---------------- CARTA: TABURAN SAWIT ---------------- */
new Chart(document.getElementById('cartaSawit'), {
  type:'doughnut',
  data:{
    labels:['Semenanjung Malaysia (2.52 juta ha · 44.6%)','Sabah & Sarawak (3.13 juta ha · 55.4%)'],
    datasets:[{ data:[2518883,3133685], backgroundColor:['#6b7d3f','#f1c85c'], borderColor:'#1a4531', borderWidth:3 }]
  },
  options:{
    plugins:{ legend:{position:'bottom', labels:{boxWidth:12, padding:16}},
      tooltip:{callbacks:{label:c=>`${c.label}: ${(c.raw/1e6).toFixed(2)} juta ha`}} }
  }
});

/* ---------------- CARTA: PERBELANJAAN SUBSEKTOR ---------------- */
new Chart(document.getElementById('cartaPerbelanjaan'), {
  type:'bar',
  data:{
    labels:['Tanaman','Ternakan','Perikanan tangkapan','Perhutanan & pembalakan','Akuakultur'],
    datasets:[{
      data:[41.53,17.00,5.03,2.57,1.76],
      backgroundColor:['#f1c85c','#d9a92b','#a89a3a','#6b7d3f','#3c4a34'],
      borderRadius:5
    }]
  },
  options:{
    indexAxis:'y',
    plugins:{legend:{display:false}, tooltip:{callbacks:{label:c=>`RM${c.raw} bilion`}}},
    scales:{ x:{grid:{color:'rgba(246,242,230,0.08)'}, ticks:{callback:v=>'RM'+v+'B'}}, y:{grid:{display:false}} }
  }
});

/* ---------------- JADUAL PENUH ---------------- */
(function(){
  const badan = document.getElementById('badanJadual');
  const susunan = Object.entries(dataNegeri).sort((a,b)=>{
    const pa = a[1].pendapatan===null ? -1 : a[1].pendapatan;
    const pb = b[1].pendapatan===null ? -1 : b[1].pendapatan;
    return pb-pa;
  });
  const maks = 30.15;
  susunan.forEach(([nama, d])=>{
    const tr = document.createElement('tr');
    const pendapatanHtml = d.pendapatan!==null
      ? `RM${d.pendapatan.toFixed(2)}B<div class="bar-mini"><i style="width:${(d.pendapatan/maks*100).toFixed(0)}%"></i></div>`
      : `<span class="tanda-belum">Belum diterbitkan</span>`;
    tr.innerHTML = `
      <td><strong>${nama}</strong></td>
      <td class="angka">${pendapatanHtml}</td>
      <td>${d.tanamanPct? d.tanamanPct+'%' : '<span class="tanda-belum">—</span>'}</td>
      <td class="angka">${d.pegangan? d.pegangan.toLocaleString('ms-MY') : '<span class="tanda-belum">—</span>'}</td>
      <td style="color:var(--teks-muted); font-size:0.82rem;">${d.catatan}</td>
    `;
    badan.appendChild(tr);
  });
})();
</script>
</body>
</html>
