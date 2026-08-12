<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PM & JSA Management App</title>

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>

    <style>
        @media print {
            .no-print {
                display: none !important;
            }
            body {
                background: #ffffff !important;
                padding: 0 !important;
                margin: 0 !important;
            }
            .print-container {
                box-shadow: none !important;
                border: none !important;
                padding: 0 !important;
            }
            input, select, textarea {
                border: none !important;
                background: transparent !important;
                outline: none !important;
                box-shadow: none !important;
            }
            table {
                page-break-inside: auto;
            }
            tr {
                page-break-inside: avoid;
                page-break-after: auto;
            }
            thead {
                display: table-header-group;
            }
        }
    </style>
</head>

<body class="bg-slate-100 font-sans text-slate-800 min-h-screen">

    <!-- =========================================================
         HALAMAN LOGIN
    ========================================================== -->
    <div id="loginScreen" class="flex items-center justify-center min-h-screen p-4">
        <div class="bg-white p-6 sm:p-8 rounded-xl shadow-md border border-slate-200 w-full max-w-md space-y-6">
            <div class="text-center">
                <h1 class="text-xl sm:text-2xl font-bold text-slate-900">
                    Login Sistem
                </h1>
                <p class="text-xs sm:text-sm text-slate-500 mt-1">
                    PM & JSA Management Application
                </p>
            </div>

            <div id="errorMessage" class="hidden p-3 bg-red-100 text-red-700 text-xs rounded-md font-medium text-center">
                Nama pengguna atau kode masuk salah!
            </div>

            <form onsubmit="handleLogin(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold uppercase text-slate-600 mb-1">
                        Nama Pengguna
                    </label>
                    <input type="text" id="username" placeholder="Masukkan nama pengguna" required class="w-full border border-slate-300 rounded-lg p-2.5 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>

                <div>
                    <label class="block text-xs font-semibold uppercase text-slate-600 mb-1">
                        Kode Masuk
                    </label>
                    <input type="password" id="password" placeholder="Masukkan kode masuk" required class="w-full border border-slate-300 rounded-lg p-2.5 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>

                <button type="submit" class="w-full py-2.5 bg-blue-600 hover:bg-blue-700 text-white font-medium rounded-lg text-sm transition-all shadow-sm">
                    Masuk Aplikasi
                </button>
            </form>
        </div>
    </div>


    <!-- =========================================================
         HALAMAN UTAMA
    ========================================================== -->
    <div id="appScreen" class="hidden p-3 sm:p-6 md:p-8">
        <div class="max-w-6xl mx-auto space-y-6">

            <!-- HEADER -->
            <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 no-print bg-white p-4 sm:p-6 rounded-xl shadow-sm border border-slate-200">
                <div>
                    <h1 class="text-xl sm:text-2xl font-bold text-slate-900">
                        PM & JSA Management
                    </h1>
                    <p class="text-xs sm:text-sm text-slate-500 mt-1">
                        Formulir pemeriksaan pemeliharaan dan analisis keselamatan kerja.
                    </p>
                </div>
==============
                <div class="flex flex-wrap items-center gap-2 sm:gap-3">
                    <button onclick="window.print()" class="flex-1 sm:flex-none px-4 py-2 bg-blue-600 hover:bg-blue-700 text-white font-medium rounded-lg text-xs sm:text-sm transition-all shadow-sm">
                        Download PDF / Cetak
                    </button>
                    <button onclick="handleLogout()" class="px-4 py-2 bg-slate-200 hover:bg-slate-300 text-slate-700 font-medium rounded-lg text-xs sm:text-sm transition-all">
                        Keluar
                    </button>
                </div>
            </div>
	=========	                
                <!-- SECTION INSPEKSI TEKNIS -->
                <div class="space-y-4">
                    <div class="bg-slate-900 text-white p-4 rounded-lg">
                        <h1 class="text-lg sm:text-xl font-bold uppercase tracking-wide">Checklist Inspeksi Teknis</h1>
                        <p class="text-slate-400 text-xs sm:text-sm mt-1">Centang setiap poin setelah prosedur pemeriksaan selesai dilakukan.</p>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <!-- 1. Engine -->
                        <div class="border border-slate-200 rounded-lg p-4 bg-slate-50">
                            <div class="flex items-center gap-2 border-b border-slate-200 pb-2 mb-3">
                                <span class="bg-blue-950 text-white text-xs font-bold px-2 py-0.5 rounded">01</span>
                                <h3 class="font-bold text-slate-900 text-sm uppercase">Inspeksi Engine</h3>
                            </div>
                            <div class="space-y-2">
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Cairan & Filter:</strong> Oli mesin, filter oli, fuel filter, dan filter udara.</span>
                                </label>
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Pendingin:</strong> Level coolant, selang radiator, v-belt, & kebersihan radiator.</span>
                                </label>
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Kondisi Fisik:</strong> Kebocoran oli, rembesan solar, mounting & knalpot.</span>
                                </label>
                            </div>
                        </div>

                        <!-- 2. Hidrolik -->
                        <div class="border border-slate-200 rounded-lg p-4 bg-slate-50">
                            <div class="flex items-center gap-2 border-b border-slate-200 pb-2 mb-3">
                                <span class="bg-blue-950 text-white text-xs font-bold px-2 py-0.5 rounded">02</span>
                                <h3 class="font-bold text-slate-900 text-sm uppercase">Sistem Hidrolik</h3>
                            </div>
                            <div class="space-y-2">
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Cairan & Filter:</strong> Level oli hidrolik, kuras endapan air, & filter hidrolik.</span>
                                </label>
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Komponen:</strong> Hydraulic pump, valve block, selang, & silinder hidrolik.</span>
                                </label>
                            </div>
                        </div>

                        <!-- 3. Final Drive & Undercarriage -->
                        <div class="border border-slate-200 rounded-lg p-4 bg-slate-50">
                            <div class="flex items-center gap-2 border-b border-slate-200 pb-2 mb-3">
                                <span class="bg-blue-950 text-white text-xs font-bold px-2 py-0.5 rounded">03</span>
                                <h3 class="font-bold text-slate-900 text-sm uppercase">Final Drive & Undercarriage</h3>
                            </div>
                            <div class="space-y-2">
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Pelumasan:</strong> Level oli dan penggantian oli final drive.</span>
                                </label>
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Mekanis:</strong> Floating seal, track tension, track shoe, & roller.</span>
                                </label>
                            </div>
                        </div>

                        <!-- 4. Transmission & Swing -->
                        <div class="border border-slate-200 rounded-lg p-4 bg-slate-50">
                            <div class="flex items-center gap-2 border-b border-slate-200 pb-2 mb-3">
                                <span class="bg-blue-950 text-white text-xs font-bold px-2 py-0.5 rounded">04</span>
                                <h3 class="font-bold text-slate-900 text-sm uppercase">Transmission & Swing</h3>
                            </div>
                            <div class="space-y-2">
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Swing Gearbox:</strong> Level oli, pelumas swing bearing, & swing brake.</span>
                                </label>
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Travel System:</strong> Respon pedal/tuas travel, pergerakan halus tanpa bunyi.</span>
                                </label>
                            </div>
                        </div>

                        <!-- 5. GET -->
                        <div class="border border-slate-200 rounded-lg p-4 bg-slate-50">
                            <div class="flex items-center gap-2 border-b border-slate-200 pb-2 mb-3">
                                <span class="bg-blue-950 text-white text-xs font-bold px-2 py-0.5 rounded">05</span>
                                <h3 class="font-bold text-slate-900 text-sm uppercase">Inspeksi GET</h3>
                            </div>
                            <div class="space-y-2">
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Bucket & Teeth:</strong> Keausan/retakan kuku bucket, adapter, side cutter.</span>
                                </label>
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Pengunci:</strong> Kekencangan pin pengunci kuku bucket.</span>
                                </label>
                            </div>
                        </div>

                        <!-- 6. Kelistrikan -->
                        <div class="border border-slate-200 rounded-lg p-4 bg-slate-50">
                            <div class="flex items-center gap-2 border-b border-slate-200 pb-2 mb-3">
                                <span class="bg-blue-950 text-white text-xs font-bold px-2 py-0.5 rounded">06</span>
                                <h3 class="font-bold text-slate-900 text-sm uppercase">Kelistrikan & Panel</h3>
                            </div>
                            <div class="space-y-2">
                                <label class="flex items-start gap-2 text-xs sm:text-sm text-slate-700 cursor-pointer">
                                    <input type="checkbox" class="mt-1 min-w-[16px] h-4 text-amber-600 rounded border-slate-300">
                                    <span><strong class="text-slate-900">Kelistrikan:</strong> Aki, tegangan alternator, perkabelan, & indikator panel.</span>
                                </label>
                            </div>
                        </div>
                    </div>
                </div>

 <!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
  <meta name="theme-color" content="#0f172a" />
  <title>PM Parts Checklist</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          screens: { xs: '360px' }
        }
      }
    };
  </script>
  <style>
    * { box-sizing: border-box; }
    html, body { margin:0; padding:0; width:100%; min-height:100%; }
    body { overflow-x:hidden; background:#f8fafc; }
    button, input, select { font:inherit; }
    .safe-bottom { padding-bottom: max(1rem, env(safe-area-inset-bottom)); }
    .mobile-card { display:none; }
    @media (max-width: 639px) {
      .desktop-table { display:none; }
      .mobile-card { display:block; }
      .page-pad { padding-left:12px; padding-right:12px; }
      .title { font-size:1.05rem; line-height:1.25rem; }
      .control-grid { grid-template-columns:1fr; }
      .stat-grid { grid-template-columns:repeat(2,minmax(0,1fr)); }
    }
    @media (min-width: 640px) {
      .desktop-table { display:block; }
      .mobile-card { display:none; }
    }
    .no-scrollbar::-webkit-scrollbar { display:none; }
    .no-scrollbar { scrollbar-width:none; }
	
	 
  </style>
</head>
<body class="text-slate-500">
  <header class="sticky top-0 z-30 bg-white-900 text-white shadow-lg">
    <div class="mx-auto w-full max-w-7xl page-pad px-4 sm:px-6 py-3 sm:py-4">
      <div class="flex items-center justify-between gap-3">
        <div class="min-w-0">
		</div>
		
 <div class="w-full bg-blue-950 text-white p-5 rounded-2xl shadow-md">
  <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-6">
    
    <!-- Sisi Kiri: Input / No. MO -->
    <div class="flex items-center gap-3 w-full md:w-auto">
      <div class="font-semibold text-sm whitespace-nowrap">
        No. MO<span class="ml-1">:</span>
      </div>
      <div class="relative w-full md:w-64">
        <input 
          type="text" 
          placeholder="Ketik No. MO" 
          class="w-full bg-blue-900/40 border border-blue-700/60 rounded-lg px-3 py-2 text-sm text-white placeholder-gray-400 focus:outline-none focus:border-blue-400"
        />
      </div>
    </div>

    <!-- Sisi Kanan: Nomor Dokumen & No Revisi -->
    <div class="text-xs md:text-sm w-full md:w-auto">
      <div class="grid grid-cols-[85px_10px_1fr] gap-x-2 gap-y-1">
        <span class="text-gray-300">Nomor Dokumen</span>
        <span>:</span>
        <span class="font-semibold text-white">BAMSF:PERA:8.5.1:03:05</span>
        
        <span class="text-gray-300">No Revisi</span>
        <span>:</span>
        <span class="font-semibold text-white">1</span>
      </div>
    </div>
  </div>
</div>
</div>
<!-- Informasi Pekerjaan -->
<div class="mt-4 bg-blue-950/80 border border-blue-800/60 rounded-xl p-4 shadow-inner">

  <div class="space-y-3">
  
  <!-- No Unit -->
    <div class="grid grid-cols-[95px_10px_minmax(0,1fr)] md:grid-cols-[110px_10px_auto] gap-x-2 items-center">
      <span class="text-gray-300">Nomor Unit</span>
      <span class="text-gray-400">:</span>

      <input
        type="text"
        name="No_Unit"
        placeholder="Nomor Unit"
        class="w-full md:w-64 bg-blue-900/70 border border-blue-700
               rounded-lg px-3 py-2 text-sm text-white
               placeholder-gray-400
               focus:outline-none focus:ring-2 focus:ring-blue-500
               focus:border-blue-500"
      />
    </div>

    <!-- Nama Mekanik -->
    <div class="grid grid-cols-[95px_10px_minmax(0,1fr)] md:grid-cols-[110px_10px_auto] gap-x-2 items-center">
      <span class="text-gray-300">Nama Mekanik</span>
      <span class="text-gray-400">:</span>

      <input
        type="text"
        name="nama_mekanik"
        placeholder="Nama mekanik"
        class="w-full md:w-64 bg-blue-900/70 border border-blue-700
               rounded-lg px-3 py-2 text-sm text-white
               placeholder-gray-400
               focus:outline-none focus:ring-2 focus:ring-blue-500
               focus:border-blue-500"
      />
    </div>


    <!-- Nama Forman -->
    <div class="grid grid-cols-[95px_10px_minmax(0,1fr)] md:grid-cols-[110px_10px_auto] gap-x-2 items-center">
      <span class="text-gray-300">Nama Forman</span>
      <span class="text-gray-400">:</span>

      <input
        type="text"
        name="nama_forman"
        placeholder="Nama forman"
        class="w-full md:w-64 bg-blue-900/70 border border-blue-700
               rounded-lg px-3 py-2 text-sm text-white
               placeholder-gray-400
               focus:outline-none focus:ring-2 focus:ring-blue-500
               focus:border-blue-500"
      />
    </div>


    <!-- Hari -->
    <div class="grid grid-cols-[95px_10px_minmax(0,1fr)] md:grid-cols-[110px_10px_auto] gap-x-2 items-center">
      <span class="text-gray-300">Hari</span>
      <span class="text-gray-400">:</span>

      <input
        type="text"
        id="hari_pekerjaan"
        name="hari_pekerjaan"
        readonly
        class="w-full md:w-64 bg-blue-900/70 border border-blue-700
               rounded-lg px-3 py-2 text-sm text-white
               cursor-not-allowed"
      />
    </div>


    <!-- Tanggal -->
    <div class="grid grid-cols-[95px_10px_minmax(0,1fr)] md:grid-cols-[110px_10px_auto] gap-x-2 items-center">
      <span class="text-gray-300">Tanggal</span>
      <span class="text-gray-400">:</span>

      <input
        type="text"
        id="tanggal_pekerjaan"
        name="tanggal_pekerjaan"
        readonly
        class="w-full md:w-64 bg-blue-900/70 border border-blue-700
               rounded-lg px-3 py-2 text-sm text-white
               cursor-not-allowed"
      />
    </div>


    <!-- Jam -->
    <div class="grid grid-cols-[95px_10px_minmax(0,1fr)] md:grid-cols-[110px_10px_auto] gap-x-2 items-center">
      <span class="text-gray-300">Jam</span>
      <span class="text-gray-400">:</span>

      <input
        type="text"
        id="jam_pekerjaan"
        name="jam_pekerjaan"
        readonly
        class="w-full md:w-64 bg-blue-900/70 border border-blue-700
               rounded-lg px-3 py-2 text-sm text-white
               cursor-not-allowed"
      />
    </div>

  </div>
</div>


<!-- Otomatis Hari, Tanggal & Jam -->
<script>
  function updateWaktuPekerjaan() {
    const sekarang = new Date();

    // Nama hari Bahasa Indonesia
    const namaHari = [
      "Minggu",
      "Senin",
      "Selasa",
      "Rabu",
      "Kamis",
      "Jumat",
      "Sabtu"
    ];

    // Nama bulan Bahasa Indonesia
    const namaBulan = [
      "Januari",
      "Februari",
      "Maret",
      "April",
      "Mei",
      "Juni",
      "Juli",
      "Agustus",
      "September",
      "Oktober",
      "November",
      "Desember"
    ];

    const hari = namaHari[sekarang.getDay()];
    const tanggal = sekarang.getDate();
    const bulan = namaBulan[sekarang.getMonth()];
    const tahun = sekarang.getFullYear();

    const jam = String(sekarang.getHours()).padStart(2, "0");
    const menit = String(sekarang.getMinutes()).padStart(2, "0");

    // Isi otomatis
    document.getElementById("hari_pekerjaan").value = hari;

    document.getElementById("tanggal_pekerjaan").value =
      `${tanggal} ${bulan} ${tahun}`;

    document.getElementById("jam_pekerjaan").value =
      `${jam}:${menit}`;
  }

  // Jalankan saat halaman dibuka
  updateWaktuPekerjaan();

  // Update setiap 1 menit
  setInterval(updateWaktuPekerjaan, 60000);
</script>
======

    <!-- TAILWIND CSS -->
    <script src="https://cdn.tailwindcss.com"></script>

    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            font-family: Arial, Helvetica, sans-serif;
        }

        /* ==================================================
           TABEL LAPTOP
        ================================================== */

        table {
            border-collapse: collapse;
            width: 100%;
        }

        th,
        td {
            border: 1px solid #64748b;
        }

        /* ==================================================
           MOBILE
        ================================================== */

        @media (max-width: 767px) {

            .desktop-table {
                display: none !important;
            }

            .mobile-card {
                display: block !important;
            }

        }

        @media (min-width: 768px) {

            .desktop-table {
                display: block !important;
            }

            .mobile-card {
                display: none !important;
            }

        }
    </style>
</head>


<body class="bg-slate-100 min-h-screen">


    <!-- =====================================================
         CONTAINER UTAMA
    ====================================================== -->

    <div class="w-full max-w-7xl mx-auto px-3 sm:px-5 lg:px-8 py-4">

        <!-- =====================================================
             NAMA MODEL
        ====================================================== -->

<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>PM PART EXCAVATOR</title>

<script src="https://cdn.tailwindcss.com"></script>

<style>

    * {
        box-sizing: border-box;
    }

    body {
        margin: 0;
        padding: 0;
        font-family: Arial, Helvetica, sans-serif;
        background: #f1f5f9;
    }

    /* =========================================
       TABEL UTAMA
    ========================================= */

    .table-wrapper {
        width: 100%;
        overflow: hidden;
    }

    table {
        width: 100%;
        table-layout: fixed;
        border-collapse: collapse;
    }

    th,
    td {
        border: 1px solid #64748b;
        text-align: center;
        vertical-align: middle;
        padding: 4px 3px;
        line-height: 1.15;
    }

    th {
        background: #cbd5e1;
        font-weight: bold;
    }

    /* =========================================
       LEBAR KOLOM
    ========================================= */

    .col-nama {
        width: 31%;
        text-align: left;
    }

    .col-part {
        width: 19%;
    }

    .col-jumlah {
        width: 7%;
    }

    .col-satuan {
        width: 7%;
    }

    .col-pm {
        width: 9%;
    }


    /* =========================================
       TAMPILAN HP
    ========================================= */

    @media (max-width: 600px) {

        body {
            background: black;
        }

        .container {
            padding: 4px !important;
        }

        .judul {
            padding: 6px !important;
            margin-bottom: 5px !important;
        }

        .judul h1 {
            font-size: 12px !important;
        }

        .judul p {
            font-size: 8px !important;
        }

        .model-box {
            padding: 5px !important;
            margin-bottom: 5px !important;
        }

        .model-box label {
            font-size: 8px !important;
        }

        .model-box select {
            font-size: 10px !important;
            padding: 5px !important;
            height: 30px;
        }

        .model-info {
            padding: 5px 7px !important;
            margin-bottom: 5px !important;
        }

        .model-info .judul-model {
            font-size: 8px !important;
        }

        .model-info .nama-model {
            font-size: 12px !important;
        }

        table {
            font-size: 7px;
        }

        th,
        td {
            padding: 3px 2px;
            height: 24px;
        }

        th {
            font-size: 7px;
        }

        td {
            font-size: 7px;
        }

        .nama-komponen {
            font-size: 7px;
            word-break: normal;
            overflow-wrap: break-word;
        }

        .part-number {
            font-size: 6.5px;
            word-break: break-word;
        }

        .check {
            font-size: 11px;
            font-weight: bold;
        }

        .keterangan {
            display: none;
        }

    }


    /* =========================================
       HP SANGAT KECIL
    ========================================= */

    @media (max-width: 380px) {

        table {
            font-size: 6px;
        }

        th,
        td {
            padding: 2px 1px;
            height: 21px;
        }

        th {
            font-size: 6px;
        }

        td {
            font-size: 6px;
        }

        .nama-komponen {
            font-size: 6px;
        }

        .part-number {
            font-size: 5.8px;
        }

        .check {
            font-size: 9px;
        }

    }



        /* =========================================
           TABEL PADAT UNTUK HP
        ========================================= */

        .compact-table {
            font-size: 9px;
            line-height: 1;
        }

        .compact-table td,
        .compact-table th {
            padding: 4px 2px;
            height: 24px;
        }


        /* =========================================
           DESKTOP
        ========================================= */

        @media (min-width: 768px) {

            .compact-table {
                font-size: 13px;
            }

            .compact-table td,
            .compact-table th {
                padding: 8px 6px;
                height: auto;
            }

        }

    </style>

</head>


<!DOCTYPE html>
<html lang="id">

<head>
    <meta charset="UTF-8">

    <meta
        name="viewport"
        content="width=device-width, initial-scale=1.0">

    <title>Maintenance Parts</title>

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>

    <style>

        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: #f3f4f6;
        }

        /* =========================================
           TABEL PADAT UNTUK HP
        ========================================= */

        .compact-table {
            font-size: 9px;
            line-height: 1;
        }

        .compact-table td,
        .compact-table th {
            padding: 4px 2px;
            height: 24px;
        }


        /* =========================================
           DESKTOP
        ========================================= */

        @media (min-width: 768px) {

            .compact-table {
                font-size: 13px;
            }

            .compact-table td,
            .compact-table th {
                padding: 8px 6px;
                height: auto;
            }

        }

    </style>

</head>


<body>


<!-- =====================================================
     HEADER
====================================================== -->

<header class="bg-[#003B5C] text-white shadow">

    <div class="max-w-7xl mx-auto px-3 py-2">

        <div class="flex items-center justify-between">

            <div>

                <h1 class="font-bold text-base md:text-xl">
                    MAINTENANCE PARTS
                </h1>

                <p class="text-[9px] md:text-xs text-blue-200">
                    Preventive Maintenance
                </p>

            </div>


            <div
                class="
                    bg-[#FFD100]
                    text-black
                    font-bold
                    px-2
                    py-1
                    rounded
                    text-xs
                ">

                PM

            </div>

        </div>

    </div>

</header>



<!-- =====================================================
     MAIN
====================================================== -->

<main class="max-w-7xl mx-auto">


    <!-- =================================================
         PILIH MODEL
    ================================================== -->

    <div class="bg-white p-2 border-b">

        <div class="relative">


            <!-- TOMBOL MODEL -->

            <button
                onclick="toggleModelMenu()"
                id="modelButton"
                class="
                    w-full
                    flex
                    items-center
                    justify-between
                    bg-[#003B5C]
                    text-white
                    rounded
                    px-3
                    py-2
                    text-xs
                    font-bold
                ">

                <span id="selectedModel">
                    EC480DL
                </span>

                <span id="arrow">
                    ▼
                </span>

            </button>



            <!-- =========================================
                 MENU MODEL
            ========================================== -->

            <div
                id="modelMenu"
                class="
                    hidden
                    absolute
                    left-0
                    right-0
                    top-full
                    mt-1
                    bg-white
                    border
                    border-gray-200
                    rounded
                    shadow-lg
                    z-50
                    overflow-hidden
                ">


                <!-- EC480DL -->

                <button
                    onclick="selectModel('EC480DL')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    EC480DL

                </button>


                <!-- EC210D -->

                <button
                    onclick="selectModel('EC210D')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    EC210D

                </button>


                <!-- EW205D -->

                <button
                    onclick="selectModel('EW205D')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    EW205D
					
					 <!-- D8R -->

                <button
                    onclick="selectModel('D8R')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    D8R
					
					 <!-- D6R -->

                <button
                    onclick="selectModel('D6R')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    D6R
					
					<!-- D5R -->

                <button
                    onclick="selectModel('D5R')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    D5R
					
					<!-- 924K -->

                <button
                    onclick="selectModel('924K')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    924K
					
						<!-- 313 -->

                <button
                    onclick="selectModel('313')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    313
					
						<!-- 14M3 -->

                <button
                    onclick="selectModel('14M3')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    14M3
					
					<!-- CS79 -->

                <button
                    onclick="selectModel('CS79')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    CS79
					
						<!-- PR776 -->

                <button
                    onclick="selectModel('PR776')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    PR776
					
					<!-- PR756 -->

                <button
                    onclick="selectModel('PR756')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    PR756
					
						<!-- L538 -->

                <button
                    onclick="selectModel('L538')"
                    class="
                        w-full
                        text-left
                        px-3
                        py-2.5
                        text-black
                        font-bold
                        hover:bg-blue-50
                    ">

                    L538
					


                </button>

            </div>

        </div>

    </div>



    <!-- =================================================
         INFO MODEL
    ================================================== -->

    <div
        class="
            bg-gray-50
            px-2
            py-1
            flex
            items-center
            justify-between
        ">

        <span
            id="modelTitle"
            class="
                font-bold
                text-xs
                text-[#003B5C]
            ">

            EC480DL

        </span>


        <span
            id="totalData"
            class="
                text-[9px]
                text-gray-500
            ">

            23 data

        </span>

    </div>



    <!-- =================================================
         TABLE
    ================================================== -->

    <div
        id="tableContainer"
        class="
            bg-blue-200
            overflow-black
        ">

        <table
            class="
                w-full
                table-fixed
                compact-table
                border-collapse
            ">


            <!-- =========================================
                 HEADER TABLE
            ========================================== -->

            <thead>

                <tr
                    class="
                        bg-black
                        text-black
                    ">


                    <!-- NO -->

                    <th
                        class="
                            w-[5%]
                            text-black
                            border-r
                            border-blue-800
                        ">

                        No

                    </th>


                    <!-- KOMPONEN -->

                    <th
                        class="
                            w-[28%]
                            text-left
                            border-r
                            border-blue-800
                        ">

                        Komponen

                    </th>


                    <!-- PART NUMBER -->

                    <th
                        class="
                            w-[25%]
                            text-left
                            border-r
                            border-black
                        ">

                        Part Number

                    </th>


                    <!-- QTY -->

                    <th
                        class="Text black"
                            w-[9%]
                            text-black
                            border-black
                            border-black
                        ">

                        Qty

                    </th>


                    <!-- SATUAN -->

                    <th
                        class="
                            w-[7%]
                            text-center
                            border-r
                            border-blue-800
                        ">

                        Sat

                    </th>


                    <!-- PM250 -->

                    <th
                        class="
                            w-[6.75%]
                            text-center
                            border-r
                            border-blue-800
                        ">

                        250

                    </th>


                    <!-- PM500 -->

                    <th
                        class="
                            w-[6.75%]
                            text-center
                            border-r
                            border-blue-800
                        ">

                        500

                    </th>


                    <!-- PM1000 -->

                    <th
                        class="
                            w-[6.75%]
                            text-center
                            border-r
                            border-blue-800
                        ">

                        1K

                    </th>


                    <!-- PM2000 -->

                    <th
                        class="
                            w-[6.75%]
                            text-center
                        ">

                        2K

                    </th>

                </tr>

            </thead>



            <!-- =========================================
                 DATA
            ========================================== -->

            <tbody
                id="tableBody"
                class="
                    divide-y
                    divide-black
                ">

            </tbody>


        </table>

    </div>



    <!-- =================================================
         DATA KOSONG
    ================================================== -->

    <div
        id="noData"
        class="
            hidden
            bg-white
            text-black
            p-8
            text-gray-400
        ">

        Data tidak tersedia.

    </div>


</main>



<!-- =====================================================
     JAVASCRIPT
====================================================== -->

<script>


/* ========================================================
   DATABASE
======================================================== */


const database = {


    /* =====================================================
       EC480DL
    ===================================================== */

    EC480DL: [

        {
            no: 1,
            nama: "SOS ENGINE",
            part: "SOS",
            qty: 1,
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },

        {
            no: 2,
            nama: "SOS SWING LH RH",
            part: "SOS",
            qty: 2,
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },

        {
            no: 3,
            nama: "HYDRAULIC",
            part: "SOS",
            qty: 1,
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },

        {
            no: 4,
            nama: "F/D LH RH",
            part: "SOS",
            qty: 2,
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },

        {
            no: 5,
            nama: "FUEL FILTER W/S",
            part: "VOE-11110683",
            qty: 1,
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },

        {
            no: 6,
            nama: "ULTRA DIESEL ENGINE OIL",
            part: "VOE-15067404",
            qty: 55,
            sat: "LTR",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },

        {
            no: 7,
            nama: "FUEL FILTER",
            part: "VOE-54315806",
            qty: 1,
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },

        {
            no: 8,
            nama: "OIL FILTER BY PASS",
            part: "VOE-21707132",
            qty: 1,
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },

        {
            no: 9,
            nama: "OIL FILTER",
            part: "VOE-17533661",
            qty: 2,
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },

        {
            no: 10,
            nama: "RACOR",
            part: "VOE-14622355",
            qty: 1,
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },

        {
            no: 11,
            nama: "GEAR OIL HD SAE 80W-90",
            part: "VOE-15067515",
            qty: 1,
            sat: "PAIL",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },

        {
            no: 12,
            nama: "FILTER",
            part: "VOE-14689735",
            qty: 1,
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },

        {
            no: 13,
            nama: "PILOT FILTER",
            part: "VOE-14750655",
            qty: 1,
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },

        {
            no: 14,
            nama: "PILOT FILTER",
            part: "VOE-14711981",
            qty: 1,
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },

        {
            no: 15,
            nama: "FILTER",
            part: "VOE-15052786",
            qty: 1,
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },

        {
            no: 16,
            nama: "AIR FILTER 11033998",
            part: "VOE-17500260",
            qty: 1,
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },

        {
            no: 17,
            nama: "GEAR OIL HD SAE 85W-140",
            part: "VOE-15067629",
            qty: 20,
            sat: "LTR",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },

        {
            no: 18,
            nama: "CARTRIDGE",
            part: "VOE-14530993",
            qty: 1,
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },

        {
            no: 19,
            nama: "SAFETY FILTER 1103399",
            part: "VOE-17500263",
            qty: 1,
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },

        {
            no: 20,
            nama: "BREATHER AIR FILTER",
            part: "VOE-11172907",
            qty: 1,
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },

        {
            no: 21,
            nama: "FILTER",
            part: "VOE-14530989",
            qty: 1,
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },

        {
            no: 22,
            nama: "ELEMENT",
            part: "VOE-14690316",
            qty: 1,
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },

        {
            no: 23,
            nama: "VOLVO HYDR OIL SAE 68",
            part: "VOE-15058191",
            qty: 270,
            sat: "LTR",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        }

    ],


    /* =====================================================
       EC210D
    ===================================================== */

    EC210D: [

        {
            no: 1,
            nama: "SOS ENGINE",
            part: "SOS",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 2,
            nama: "SOS F/D LH RH",
            part: "SOS",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
		{
            no: 3,
            nama: "OIL FILTER",
            part: "VOE-17535679",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 4,
            nama: "FUEL FILTER",
            part: "VOE-54315408",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 5,
            nama: "RACOR",
            part: "2020TM-OR",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 6,
            nama: "FUEL FILTER",
            part: "VOE-11110683",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
		{
            no: 7,
            nama: "ENGINE OIL",
            part: "VOE-15067404",
            qty: "25",
            sat: "LTR",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 8,
            nama: "TRACK GEARBOX OIL 85W-140",
            part: "VOE-15067629",
            qty: "20",
            sat: "LTR",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 9,
            nama: "SOS HYD",
            part: "SOS",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
		{
            no: 10,
            nama: "SOS SWING",
            part: "SOS",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
				{
            no: 11,
            nama: "AIR CLEANER",
            part: "VOE-17500253",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
			{
            no: 12,
            nama: "SAFETY FILTER",
            part: "VOE-17500251",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
			{
            no: 13,
            nama: "SWING OIL",
            part: "VOE-15067515",
            qty: "1",
            sat: "PAIL",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
			{
            no: 14,
            nama: "AIR FILTER OUTER",
            part: "VOE-15052786",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
			{
            no: 15,
            nama: "AIR FILTER INNER",
            part: "VOE-14689735",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
			{
            no: 16,
            nama: "HYDRAULIC OIL",
            part: "VOE-15058191",
            qty: "208",
            sat: "LTR",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },
			{
            no: 17,
            nama: "RETURN FILTER",
            part: "VOE-14688861",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },
		{
            no: 18,
            nama: "BREATHER",
            part: "VOE-14596399",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },
			{
            no: 19,
            nama: "STRAINER HYD",
            part: "SA-1141-00010",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },
			{
            no: 20,
            nama: "BREATHER",
            part: "VOE-11172907",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },
		
	
    ],


    /* =====================================================
       EW205D
    ===================================================== */

    EW205D: [

        {
            no: 1,
            nama: "SOS ENGINE",
            part: "SOS",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 2,
            nama: "OIL FILTER",
            part: "VOE-17535679",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 3,
            nama: "FUEL FILTER",
            part: "VOE-54315408",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 4,
            nama: "PRIMARY FILTER",
            part: "VOE-11110683",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 5,
            nama: "FILTER ELEMENT",
            part: "VEO-14622355",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 6,
            nama: "ENGINE OIL",
            part: "VOE-15067404",
            qty: "25",
            sat: "LTR",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
		{
            no: 7,
            nama: "RACOR",
            part: "2020TM-OR",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
		{
            no: 8,
            nama: "SOS TRAVEL GEAR BOX T/M",
            part: "SOS",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 9,
            nama: "SOS SWING",
            part: "SOS",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
		{
            no: 10,
            nama: "SOS AXLE OIL RH LH",
            part: "SOS",
            qty: "2",
            sat: "EA",
            pm250: false,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 11,
            nama: "SOS HYD OIL",
            part: "SOS",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
			{
            no: 12,
            nama: "SOS F/D RH LH",
            part: "SOS",
            qty: "4",
            sat: "EA",
            pm250: false,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
		{
            no: 13,
            nama: "AXLE OIL",
            part: "VOE-15067515",
            qty: "1",
            sat: "PILE",
            pm250: false,
            pm500: true,
            pm1000: true,
            pm2000: true
        },
		
		{
            no: 14,
            nama: "SWING GEARBOX OIL",
            part: "VOE-15067515",
            qty: "1",
            sat: "PILE",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
		{
            no: 15,
            nama: "SASFETY FILTER",
            part: "VEO-17500251/VOE-11110176",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
		{
            no: 16,
            nama: "AIR FILTER",
            part: "VEO-17500253/VOE-11110175",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
			{
            no: 17,
            nama: "HYD FILTER",
            part: "VEO-14750647/VOE-14688861",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
		{
            no: 18,
            nama: "FILTER ELEMENT",
            part: "VOE-14711981",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
			{
            no: 19,
            nama: "FILTER CARTRIDGE",
            part: "VOE-14750657",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
        },
			{
            no: 20,
            nama: "TRAVEL GEARBOX OIL",
            part: "VOE-15067629",
            qty: "5",
            sat: "LTR",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },
		{
            no: 21,
            nama: "HYDRAULIC OIL",
            part: "VOE-15058191",
            qty: "148",
            sat: "LTR",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true
        },
    ],
	/* =====================================================
       D8R
    ===================================================== */

		D8R: [
			{
			no:1,
			nama:"SOS ENGINE",
			part:"SOS",
			qty:"1",
			sat:"EA",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:2,
			nama:"SOS F/D LH RH",
			part:"SOS",
			qty:"2",
			sat:"EA",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:3,
			nama:"ENGINE OIL FILTER",
			part:"1R-0716",
			qty:"1",
			sat:"EA",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:4,
			nama:"DEO15W40-5 LIT",
			part:"3E-9848",
			qty:"42",
			sat:"LTR",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:5,
			nama:"FILTER-FUEL ",
			part:"1R-0749",
			qty:"1",
			sat:"EA",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:6,
			nama:"FILTER AS-WATER SEP",
			part:"326-1642",
			qty:"1",
			sat:"EA",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:7,
			nama:"RACOR",
			part:"2020TM-OR",
			qty:"1",
			sat:"EA",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:8,
			nama:"SOS HYD",
			part:"SOS",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:9,
			nama:"SOS T/M",
			part:"SOS",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:10,
			nama:"HYDRAULIC FILTER",
			part:"1R-0777",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:11,
			nama:"GASKET",
			part:"9H-6454",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:12,
			nama:"SEAL-O-RING",
			part:"5H-6733",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:13,
			nama:"FILTER-OIL  ",
			part:"465-6506",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:14,
			nama:"FILTER ELEMENT",
			part:"571-5253",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:16,
			nama:"BREATHER",
			part:"9G-5127",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:true,
			pm2000:true
			},

			{
			no:16,
			nama:"TDTO 30-20 LIT",
			part:"7X-7855",
			qty:"170",
			sat:"LTR",
			pm250:false,
			pm500:false,
			pm1000:true,
			pm2000:true
			},

			{
			no:17,
			nama:"SEAL-O-RING ",
			part:"6F-0711",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:true,
			pm2000:true
			},

			{
			no:18,
			nama:"FILTER ELEMENT AS-AIR",
			part:"6I-2505",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:true,
			pm2000:true
			},

			{
			no:19,
			nama:"FILTER GP-CAB AIR ",
			part:"396-7087",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:true,
			pm2000:true
			},

			{
			no:20,
			nama:"FILTER-CAB AIR",
			part:"112-7448",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:true,
			pm2000:true
			},

			{
			no:21,
			nama:"SEAL ",
			part:"5P-5678",
			qty:"2",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:false,
			pm2000:true
			},

			{
			no:22,
			nama:"TDTO-50 20L",
			part:"7X-7858",
			qty:"24",
			sat:"LTR",
			pm250:false,
			pm500:false,
			pm1000:false,
			pm2000:true
			},

			{
			no:23,
			nama:"HYDO ADV 30-20L",
			part:"319-5921",
			qty:"100",
			sat:"LTR",
			pm250:false,
			pm500:false,
			pm1000:false,
			pm2000:true
			},

			{
			no:24,
			nama:"RECEIVER DRYER ",
			part:"106-5534",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:false,
			pm2000:true
			},

			{
			no:25,
			nama:"FILTER ELEMENT AS-AIR",
			part:"6I-2506",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:false,
			pm2000:true
			},
	],
	
    /* =====================================================
       D6R
    ===================================================== */

    D6R: [

        {
            no: 1,
            nama: "SOS ENGINE",
            part: "SOS",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
		},
		{
            no: 2,
            nama: "SOS F/D LH RH",
            part: "SOS",
            qty: "2",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true
		},
		{
            no: 3,
            nama: "SEPARATOR",
            part: "438-5386",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true,
		},
		{
            no: 4,
            nama: "FUEL FILTER",
            part: "1R-0762",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true,
		},
		{
            no: 5,
            nama: "RACOR",
            part: "2020TM-OR",
            qty: "1",
            sat: "EA",
            pm250: true,
            pm500: true,
            pm1000: true,
            pm2000: true,
		},
		{
            no: 6,
            nama: "FILTER OLI",
            part: "465-6506",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: true,
            pm1000: true,
            pm2000: true,
		},
		{
            no: 7,
            nama: "ENGINE OIL FILTER",
            part: "1R-1808",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: true,
            pm1000: true,
            pm2000: true,
		},
		{
            no: 8,
            nama: "ENGINE OIL",
            part: "3E-9840",
            qty: "28",
            sat: "LTR",
            pm250: false,
            pm500: true,
            pm1000: true,
            pm2000: true,
		},
				{
            no: 9,
            nama: "SOS HYD",
            part: "SOS",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
		},
		{
            no: 10,
            nama: "SOS T/M",
            part: "SOS",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true
		},
		{
            no: 11,
            nama: "TDTO 30",
            part: "7X-7855",
            qty: "140",
            sat: "LTR",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true,
		},
		{
            no: 12,
            nama: "FILTER ELEMENT",
            part: "571-5253",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true,
		},
		{
            no: 13,
            nama: "GASKET",
            part: "3S-7781",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true,
		},
		{
            no: 14,
            nama: "BREATHER AS",
            part: "9G-5127",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true,
		},
		{
            no: 15,
            nama: "FILTER ELEMENT",
            part: "6I-2501",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: true,
            pm2000: true,
		},
		{
            no: 16,
            nama: "TDTO 50-20",
            part: "7X-7858",
            qty: "28",
            sat: "LTR",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true,
		},
		{
            no: 17,
            nama: "HYDO 30",
            part: "319-5921",
            qty: "60",
            sat: "LTR",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true,
		},
			{
            no: 18,
            nama: "RECEIVER DRYER",
            part: "106-5534",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true,
		},
			{
            no: 19,
            nama: "FILTER GP CAB AIR",
            part: "396-7087",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true,
		},
			{
            no: 20,
            nama: "FILTER CAB AIR",
            part: "112-7448",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true,
		},
			{
            no: 21,
            nama: "FILTER ELEMENT",
            part: "6I-2502",
            qty: "1",
            sat: "EA",
            pm250: false,
            pm500: false,
            pm1000: false,
            pm2000: true,
		},
		
	],
		
	
	
	/* =====================================================
       D5R
    ===================================================== */

		D5R: [
			{
			no:1,
			nama:"SOS ENGINE",
			part:"SOS",
			qty:"1",
			sat:"EA",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:2,
			nama:"SOS F/D LH RH",
			part:"SOS",
			qty:"2",
			sat:"EA",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:3,
			nama:"SEPARATOR",
			part:"438-5386",
			qty:"1",
			sat:"EA",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:4,
			nama:"FUEL FILTER",
			part:"360-8960",
			qty:"2",
			sat:"EA",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:5,
			nama:"RACOR",
			part:"2020TM-OR",
			qty:"1",
			sat:"EA",
			pm250:true,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:6,
			nama:"SOS HYD",
			part:"SOS",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:7,
			nama:"SOS T/M",
			part:"SOS",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:8,
			nama:"ENGINE OIL FILTER",
			part:"462-1171",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:9,
			nama:"DEO15W40-5 LIT",
			part:"3E-9848",
			qty:"16",
			sat:"LTR",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:10,
			nama:"FILTER-OIL ",
			part:"126-1818",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:11,
			nama:"HYD AND TM FILTER",
			part:"389-1076",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:12,
			nama:"SEAL O RING",
			part:"095-1678",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:13,
			nama:"FILTER ELEMENT",
			part:"337-5270",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:true,
			pm1000:true,
			pm2000:true
			},

			{
			no:14,
			nama:" GASKET  ",
			part:"3S-7781",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:true,
			pm2000:true
			},

			{
			no:15,
			nama:"BREATHER AS ",
			part:"9G-5127",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:true,
			pm2000:true
			},

			{
			no:16,
			nama:"FILTER ELEMENT ",
			part:"346-6693",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:true,
			pm2000:true
			},

			{
			no:17,
			nama:"TDTO 50-20 LIT",
			part:"7X-7858",
			qty:"14",
			sat:"LTR",
			pm250:false,
			pm500:false,
			pm1000:false,
			pm2000:true
			},

			{
			no:18,
			nama:"HYDO ADV 30-20L",
			part:"319-5921",
			qty:"65",
			sat:"LTR",
			pm250:false,
			pm500:false,
			pm1000:false,
			pm2000:true
			},

			{
			no:19,
			nama:"RECEIVER DRYER ",
			part:"106-5534",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:false,
			pm2000:true
			},

			{
			no:20,
			nama:"FILTER GP-CAB AIR ",
			part:"396-7087",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:false,
			pm2000:true
			},

			{
			no:21,
			nama:"FILTER-CAB AIR ",
			part:"112-7448",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:false,
			pm2000:true
			},

			{
			no:22,
			nama:"FILTER ELEMENT  SEC",
			part:"346-6694",
			qty:"1",
			sat:"EA",
			pm250:false,
			pm500:false,
			pm1000:false,
			pm2000:true
			},
		
	],
	/* =====================================================
       924K
    ===================================================== */

		'924K': [
		{
no:1,
nama:"SOS ENGINE",
part:"SOS",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:2,
nama:"SOS HYD",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:3,
nama:"SOS T/M",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:4,
nama:"SOS FRONT D/F ",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:5,
nama:"SOS REAR D/F ",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:6,
nama:"RACOR",
part:"2020TM-OR",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:7,
nama:"FILTER-ENGINE OIL ",
part:"462-1171",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:8,
nama:"CAT DEO CH4 20L",
part:"3E-9848",
qty:"20",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:9,
nama:"SEPARATOR",
part:"391-3764",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:10,
nama:"FUEL FILTER",
part:"360-8960",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:11,
nama:"FILTER AS-HY",
part:"144-6691",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:12,
nama:"PRIMARY AIR FILTER",
part:"256-7902",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:13,
nama:"TDTO 50-20 LIT",
part:"7X-7858",
qty:"50",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:14,
nama:"HYD OIL FILTER",
part:"421-5481",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:15,
nama:"FILTER AS",
part:"273-5711",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:16,
nama:"BREATHER",
part:"258-2829",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:17,
nama:"SEC AIR FILTER",
part:"256-7903",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:18,
nama:"HYDO ADV 30-20L",
part:"319-5921",
qty:"10",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:19,
nama:"HYDO ADV 10-20L       ",
part:"309-6942",
qty:"90",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},
],
	/* =====================================================
       313
    ===================================================== */

		'313': [
		{
no:1,
nama:"SOS OIL ENGINE",
part:"SOS",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:2,
nama:"SEAL-O-RING",
part:"7M-8485",
qty:"2",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:3,
nama:"RACOR",
part:"2020TM-OR",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:4,
nama:"SOS OIL F/D RH LH",
part:"SOS",
qty:"2",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:5,
nama:"SOS OIL HYD",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:6,
nama:"SOS OIL SWING ",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:7,
nama:"SOS OIL T/M",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:8,
nama:"FILTER AS-ENGINE OIL",
part:"1R-1807",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:9,
nama:"CAT DEO CH4 20L",
part:"3E-9848",
qty:"16",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:10,
nama:"ELEMENT AS",
part:"1R-1804",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:11,
nama:"SEAL-O-RING",
part:"207-2757",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:12,
nama:"FILTER AS",
part:"438-5386",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:13,
nama:"ELEMENT",
part:"093-7521",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:14,
nama:"FILTER AS",
part:"5I-8670",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:15,
nama:"TDTO 50-20 LIT",
part:"7X-7858",
qty:"12",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:16,
nama:"FILTER ELEMENT AS-AIR",
part:"131-8902",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:17,
nama:"FILTER ELEMENT AS-AIR",
part:"131-8903",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:18,
nama:"FILTER ELEMENT",
part:"245-7823",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:19,
nama:"FILTER ELEMENT",
part:"293-1184",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:20,
nama:"ELEMENT",
part:"398-7171",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:21,
nama:"RECEIVER AS",
part:"176-1902",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:22,
nama:"HYD0 ADV10-20 L",
part:"309-6942",
qty:"104",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},			
],
	/* =====================================================
       14M3
    ===================================================== */

		'14M3': [	
		{
no:1,
nama:"SOS ENGINE",
part:"SOS",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:2,
nama:"ELEMENT FUEL",
part:"436-7077",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:3,
nama:"ELEMENT-FUEL",
part:"500-0480",
qty:"2",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:4,
nama:"SOS WHEAL BEARING LH RH",
part:"SOS",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:5,
nama:"SOS T/M",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:6,
nama:"SOS TANDEM RH LH",
part:"SOS",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:7,
nama:"SOS CIRCLE",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:8,
nama:"SOS HYD",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:9,
nama:"RACOR",
part:"2020TM-OR",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:10,
nama:"DEO15W40-20 LIT       ",
part:"3E-9848",
qty:"40",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:11,
nama:"FILTER-ENGINE OIL",
part:"500-0483",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:12,
nama:"FILTER",
part:"9R-9925",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:13,
nama:"FILTER ELEMENT",
part:"389-1076",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:14,
nama:"SCREEN(HYDRAULIC)",
part:"338-3540",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:15,
nama:"BREATHER",
part:"4H-6112",
qty:"2",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:16,
nama:"FILTER-MAGNETIC",
part:"328-3655",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:17,
nama:"FILTER ELEMENT AS-AIR",
part:"6I-2505",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:18,
nama:"BREATHER AS",
part:"183-3873",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:19,
nama:"TDTO 30-20 LIT        ",
part:"9X-6466",
qty:"90",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:20,
nama:"GO 80W90-20 LIT       ",
part:"7X-7867",
qty:"10",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:21,
nama:"TDTO 50-20 LIT        ",
part:"7X-7858",
qty:"200",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:22,
nama:"FILTER ELEMENT AS-AIR",
part:"6I-2506",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:23,
nama:"FILTER ELEMENT-CAB AIR",
part:"149-1912",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:24,
nama:"FILTER ELEMENT-AIR",
part:"211-2660",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:25,
nama:"HYDO ADV 10-20L       ",
part:"309-6942",
qty:"100",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},				
	],
	/* =====================================================
       CS79
    ===================================================== */

		'CS79': [
		
		{
no:1,
nama:"SOS DIFFERNTIAL",
part:"SOS",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:2,
nama:"CAP & PROBE GP",
part:"177-9343",
qty:"3",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:3,
nama:"GREASE CARTIDGE",
part:"TU-H004C",
qty:"2",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:4,
nama:"RACOR",
part:"2020TM-OR",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:5,
nama:"SOS VIBRO ",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:6,
nama:"SOS HYD",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:7,
nama:"SOS ENGINE",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:8,
nama:"SOS F/D LH RH",
part:"SOS",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:9,
nama:"SOS FD DRUM LH RH",
part:"SOS",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:10,
nama:"FILTER ENGINE OIL",
part:"462-1171",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:11,
nama:"SEAL O RING (PLUG)",
part:"8L-2786",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:12,
nama:"FUEL FILTER (INLINE)",
part:"525-6205",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:13,
nama:"FILTER AS-WATER SEP",
part:"439-5037",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:14,
nama:"FILTER ELEMENT FUEL",
part:"360-8960",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:15,
nama:"CAT DEO CH4 20L",
part:"3E-9848",
qty:"20",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:16,
nama:"SEAL O RING (PLUG)",
part:"6V-6228",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},
{
no:17,
nama:"SEAL O RING (PLUG)",
part:"5J-2974",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:18,
nama:"SEAL O RING (PLUG DRAIN)",
part:"151-7517",
qty:"2",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:19,
nama:"SEAL O RING (FD DRUM)",
part:"151-7516",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:20,
nama:"FILTER ELEMENT AS-OIL",
part:"389-1085",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:21,
nama:"SEAL O RING",
part:"95-1671",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:22,
nama:"SEAL O RING (PLUG)",
part:"6V-5048",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:23,
nama:"BREATHER",
part:"183-3873",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:24,
nama:"CARTRIDGE",
part:"567-4704",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:25,
nama:"CAT TDTO-50 20L",
part:"7X-7858",
qty:"40",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:26,
nama:"CAT HYDO Adv 30 20L",
part:"319-5921",
qty:"50",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:27,
nama:"FILTER ELEMENT AS-AIR (PRIMARY)",
part:"256-7902",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:28,
nama:"FILTER ELEMENT-CAB AIR",
part:"282-5340",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:29,
nama:"SEAL (BONDED)(VALVE COVER)",
part:"527-1641",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:30,
nama:"KIT DRAIN (FUEL FILTER)",
part:"362-5412",
qty:"2",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:31,
nama:"KIT CAP FUEL TANK FILTER",
part:"350-7735",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:32,
nama:"SEAL O RING",
part:"3K-0360",
qty:"3",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},				
		],
		
	/* =====================================================
       PR776
    ===================================================== */

		'PR776': [
		{
no:1,
nama:"SOS ENGINE",
part:"SOS",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:2,
nama:"SOS F/D LH RH",
part:"SOS",
qty:"2",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:3,
nama:"SOS HYD",
part:"SOS",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:4,
nama:"SOS POWER TRAIN",
part:"SOS",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:5,
nama:"SOS REPLINISHING LH RH",
part:"SOS",
qty:"2",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:6,
nama:"SOS SLIP RING LH RH",
part:"SOS",
qty:"2",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:7,
nama:"SOS SPLITTER BOX",
part:"SOS",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:8,
nama:"ENGINE OIL PERTAMINA",
part:"15W-40",
qty:"93",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:9,
nama:"FUEL FILTER INSERT PRE-ASS",
part:"10135462",
qty:"2",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:10,
nama:"FUEL PRE FILTER",
part:"10149977",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:11,
nama:"ENGINE OIL FILTER",
part:"11427521",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:12,
nama:"FILTER INSERT",
part:"12403708",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:13,
nama:"COVER SEAL",
part:"11002875",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:14,
nama:"FILTER INSERT",
part:"10802779",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:15,
nama:"SEAL KIT",
part:"11827718",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},
{
no:16,
nama:"FILTER ELEMENT",
part:"11067781",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:17,
nama:"SEAL KIT",
part:"11651342",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:18,
nama:"FUEL ELEMENT FILT GRIFFIN 2020TM",
part:"2020TM-OR",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:19,
nama:"SLIP RING OIL  PERTAMINA",
part:"15W-40",
qty:"13,5",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:20,
nama:"SPLITTER BOX OIL  PERTAMINA",
part:"85W-140 GL.05",
qty:"16",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:21,
nama:"TRAVEL GEAR BOX OIL PERTAMINA",
part:"85W-140 GL.05",
qty:"86",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:22,
nama:"AXEL BEARING  PERTAMINA",
part:"85W-140 GL.05",
qty:"10",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:23,
nama:"O-RING",
part:"7380627",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:24,
nama:"BRAKE UNIT TRAVEL MOTOR PERTAMINA",
part:"15W-40",
qty:"0,6",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:25,
nama:"TRAVEL GEAR CARRIER PERTAMINA",
part:"ISO VG 100",
qty:"56",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:26,
nama:"V RIPPED BELT",
part:"11347044",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:27,
nama:"V RIPPED BELT",
part:"11005218",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:28,
nama:"MAIN FILTER ELEMENT",
part:"12248978",
qty:"2",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:29,
nama:"SAFETY ELEMENT",
part:"12248979",
qty:"2",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:30,
nama:"AIR FILTER",
part:"12254531",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:31,
nama:"RECIRCULATION FILTER",
part:"93517017",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:32,
nama:"HYDRAULIC OIL  PERTAMINA",
part:"15W-40",
qty:"320",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},
	
		],
		/* =====================================================
       PR756
    ===================================================== */

		'PR756': [
		{
no:1,
nama:"SOS OIL ENGINE",
part:"SOS",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:2,
nama:"SOS F/D LH RH",
part:"SOS",
qty:"2",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:3,
nama:"FILTER OLI",
part:"10297295",
qty:"2",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:4,
nama:"FILTER ELEMENT",
part:"11081663",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:5,
nama:"FUEL FINE FILTER",
part:"12820742",
qty:"2",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:6,
nama:"RACOR",
part:"2020TM-OR",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:7,
nama:"ENGINE OIL PERTAMINA",
part:"15W-40",
qty:"45",
sat:"LTR",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:8,
nama:"SOS HYD",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:9,
nama:"SOS POWER TRAIN",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:10,
nama:"SOS REPLINISING LH RH",
part:"SOS",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:11,
nama:"SOS SLIP RING LH RH",
part:"SOS",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:12,
nama:"SOS SPLITTER BOX",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:13,
nama:"FILTER ELEMENT",
part:"10663110",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:14,
nama:"FILTER INSERT",
part:"10802779",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:15,
nama:"ENGINE BREATHER FILTER",
part:"12886226",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:16,
nama:"SEAL KIT",
part:"11651342",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:17,
nama:"SLIP RING OIL PERTAMINA",
part:"ISO VG 100",
qty:"13,3",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:18,
nama:"TREVEL GEAR OIL PERTAMINA",
part:"85W-140 GL.5",
qty:"44",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:19,
nama:"SPILITER BOX OIL PERTAMINA",
part:"85W-140 GL.5",
qty:"8,5",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:20,
nama:"AIR CLEANER MAIN",
part:"11647528",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:21,
nama:"AIR CLEANER SAFETY",
part:"11231229",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:22,
nama:"FILTER",
part:"12228886",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:23,
nama:"V-BELT CHECK OR REPLACE",
part:"11482412",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:24,
nama:"HYDRAULIC OIL PERTAMINA",
part:"ISO VG 100",
qty:"152",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},
	
		],
		
		/* =====================================================
       L538
    ===================================================== */

		'L538': [
		{
no:1,
nama:"SOS ENGINE",
part:"SOS",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:2,
nama:"CARTRIDGE FINE-FILTER ",
part:"7091068",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:3,
nama:"CARTRIDGE PRE-FILTER ",
part:"7091069",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:4,
nama:"OIL FILTER ",
part:"7090561",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:5,
nama:" RACOR ",
part:"2020TM-OR",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:6,
nama:" ENGINE OIL PERTAMINA",
part:"15W-40",
qty:"14,7",
sat:"LTR",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:7,
nama:"SEAL ",
part:"7090235",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:8,
nama:"SEAL KIT ",
part:"7090529",
qty:"1",
sat:"EA",
pm250:true,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:9,
nama:"SOS D/F REAR FRONT",
part:"SOS",
qty:"2",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:10,
nama:"SOS HUB RH LH",
part:"SOS",
qty:"4",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:11,
nama:"SOS HYD",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:12,
nama:"SOS T/M",
part:"SOS",
qty:"1",
sat:"EA",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:13,
nama:"TRANSMISSION OIL ATF GULF",
part:"ATF 5W-20",
qty:"3,8",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:14,
nama:"FRONT AXLE DIFF OIL GULF",
part:"SAE 90 GL.05",
qty:"16,3",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:15,
nama:"REAR AXLE DIFF OILAR  GULF",
part:"SAE 90 GL.05",
qty:"15",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},
{
no:16,
nama:"FRONT AXLE WHEEL HUBS GULF",
part:"SAE 90 GL.05",
qty:"2,6",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:17,
nama:"REAR AXLE WHEEL HUBS GULF",
part:"SAE 90 GL.05",
qty:"2,6",
sat:"LTR",
pm250:false,
pm500:true,
pm1000:true,
pm2000:true
},

{
no:18,
nama:"REAR AXLE DIFF OIL GULF",
part:"SAE 90 GL.05",
qty:"15",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:19,
nama:"AIR FILTER ",
part:"12232137",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:20,
nama:"FIBRE GLASS FILTER ELEMENT ",
part:"10293870",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:21,
nama:"MAIN ELEMENT ",
part:"7412732",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:22,
nama:"O-RING 7,59X2,6 ",
part:"7090004",
qty:"4",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:23,
nama:"O-RING DIN 3771 110X4,00 ",
part:"7004419",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:24,
nama:"O-RING ISO 3601-1 113,89X3,53 ",
part:"7015616",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:25,
nama:"PARTICULATE FILTER ",
part:"10815373",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:26,
nama:"PREFILTER ",
part:"93014155",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:27,
nama:"PREFILTER ",
part:"93013612",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:28,
nama:"SEAL ",
part:"7091060",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:29,
nama:"SEALING RING 67X78X2 ",
part:"7408457",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:30,
nama:"WHIP",
part:"12923959",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:31,
nama:"FILTER AC",
part:"10492693",
qty:"2",
sat:"EA",
pm250:false,
pm500:false,
pm1000:true,
pm2000:true
},

{
no:32,
nama:"V-BELT",
part:"10650070",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:33,
nama:"AERATION FILTER 2µM ",
part:"10222403",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:34,
nama:"LOCKING ELEMENT ",
part:"7412733",
qty:"1",
sat:"EA",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

{
no:35,
nama:"HYDRAULIC OIL PEERTAMINA",
part:"ISO VG 100",
qty:"110",
sat:"LTR",
pm250:false,
pm500:false,
pm1000:false,
pm2000:true
},

		
		
		],
	
};



/* ========================================================
   MODEL AKTIF
======================================================== */

let currentModel = "EC480DL";



/* ========================================================
   BUKA / TUTUP MENU MODEL
======================================================== */

function toggleModelMenu() {

    const menu =
        document.getElementById("modelMenu");

    const arrow =
        document.getElementById("arrow");


    menu.classList.toggle("hidden");


    if (menu.classList.contains("hidden")) {

        arrow.innerText = "▼";

    } else {

        arrow.innerText = "▲";

    }

}



/* ========================================================
   PILIH MODEL
======================================================== */

function selectModel(model) {

    currentModel = model;


    /* Ganti nama model */

    document
        .getElementById("selectedModel")
        .innerText = model;


    document
        .getElementById("modelTitle")
        .innerText = model;


    /* Tutup menu */

    document
        .getElementById("modelMenu")
        .classList.add("hidden");


    document
        .getElementById("arrow")
        .innerText = "▼";


    /* Render data */

    renderData();

}



/* ========================================================
   ICON PM
======================================================== */

function pmIcon(active) {

    if (active) {

        return `
            <span
                class="
                    inline-flex
                    items-center
                    justify-center
                    w-[13px]
                    h-[13px]
                    md:w-5
                    md:h-5
                    rounded-full
                    bg-green-100
                    text-green-600
                    font-bold
                    text-[8px]
                    md:text-xs
                ">

                ✓

            </span>
        `;

    }


    return `
        <span class="text-gray-200">
            •
        </span>
    `;

}



/* ========================================================
   TAMPILKAN DATA
======================================================== */

function renderData() {

    const tbody =
        document.getElementById("tableBody");

    const noData =
        document.getElementById("noData");

    const totalData =
        document.getElementById("totalData");


    /* Ambil data sesuai model */

    const data =
        database[currentModel];


    /* Jumlah data */

    totalData.innerText =
        data.length + " data";


    /* Jika tidak ada data */

    if (!data || data.length === 0) {

        tbody.innerHTML = "";

        noData.classList.remove("hidden");

        return;

    }


    noData.classList.add("hidden");


    /* Buat tabel */

    tbody.innerHTML = data.map(item => `

        <tr
            class="
                hover:bg-blue-50
                border-b
                border-gray-100
            ">


            <!-- =========================
                 NOMOR
            ========================== -->

            <td
                class="
                    text-black
                    text-black
                    border-r
                    border-gray-100
                ">

                ${item.no}

            </td>


            <!-- =========================
                 NAMA KOMPONEN
            ========================== -->

            <td
                class="
                    font-semibold
                    text-gray-800
                    truncate
                    max-w-0
                    border-r
                    border-gray-100
                "
                title="${item.nama}">

                ${item.nama}

            </td>


            <!-- =========================
                 PART NUMBER
            ========================== -->

            <td
                class="
                    font-mono
                    text-black
                    truncate
                    max-w-0
                    border-r
                    border-gray-100
                "
                title="${item.part}">

                ${item.part}

            </td>


            <!-- =========================
                 QTY
            ========================== -->

            <td
                class="
                    text-black
                    font-semibold-black
                    border-black
                    border-gray-100
                ">

                ${item.qty}

            </td>


            <!-- =========================
                 SATUAN
            ========================== -->

            <td
                class="
                    text-black
                    text-black
                    border-r
                    border-gray-100
                ">

                ${item.sat}

            </td>


            <!-- =========================
                 PM250
            ========================== -->

            <td
                class="
                    text-center
                    border-r
                    border-gray-100
                ">

                ${pmIcon(item.pm250)}

            </td>


            <!-- =========================
                 PM500
            ========================== -->

            <td
                class="
                    text-center
                    border-r
                    border-gray-100
                ">

                ${pmIcon(item.pm500)}

            </td>


            <!-- =========================
                 PM1000
            ========================== -->

            <td
                class="
                    text-center
                    border-r
                    border-gray-100
                ">

                ${pmIcon(item.pm1000)}

            </td>


            <!-- =========================
                 PM2000
            ========================== -->

            <td
                class="text-center">

                ${pmIcon(item.pm2000)}

            </td>


        </tr>

    `).join("");

}



/* ========================================================
   KLIK DI LUAR MENU
======================================================== */

document.addEventListener("click", function(event) {

    const menu =
        document.getElementById("modelMenu");

    const button =
        document.getElementById("modelButton");


    if (
        !menu.contains(event.target) &&
        !button.contains(event.target)
    ) {

        menu.classList.add("hidden");

        document
            .getElementById("arrow")
            .innerText = "▼";

    }

});



/* ========================================================
   JALANKAN SAAT HALAMAN DIBUKA
======================================================== */

renderData();


</script>


</body>

</html>


                <!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Job Safety Analysis (JSA)</title>
  <!-- CDN Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest"></script>
</head>
<body class="bg-slate-100 text-slate-800 font-sans min-h-screen pb-10">

  <!-- Container Utama (Maksimal Lebar HP / Tablet) -->
  <div class="max-w-md mx-auto sm:max-w-xl md:max-w-3xl lg:max-w-5xl px-4 py-6">

    <div class="w-full bg-blue-950 text-white p-5 rounded-2xl shadow-md">
  <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-1">
    
<div class="w-full bg-blue-950 text-white p-5 rounded-2xl shadow-md">
  <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-1">

   <!-- Header JSA -->
<div class="w-full flex flex-col md:flex-row md:items-center md:justify-between gap-4">

  <!-- Bagian Kiri: Judul & Subjudul -->
  <div class="flex items-center gap-3 min-w-0">
    
    <div class="shrink-0 p-2 bg-blue-900/50 rounded-xl text-amber-400">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-7 w-7 md:h-8 md:w-8"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
        stroke-width="2"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"
        />
      </svg>
    </div>

    <div class="min-w-0">
      <h1 class="text-base sm:text-lg md:text-xl font-bold tracking-wide leading-tight">
        JOB SAFETY ANALYSIS (JSA)
      </h1>

      <p class="text-[10px] sm:text-xs md:text-sm text-gray-300 leading-tight mt-1">
        Dokumen Prosedur &amp; Keselamatan Kerja Terpadu
      </p>
    </div>

  </div>


  <!-- Bagian Kanan: Nomor Dokumen -->
  <div class="w-full md:w-auto text-xs sm:text-sm">
    
    <div class="grid grid-cols-[75px_8px_minmax(0,1fr)] md:grid-cols-[85px_10px_auto] gap-x-2 gap-y-1">

      <span class="text-gray-300">No. Dokumen</span>
      <span>:</span>
      <span class="font-semibold text-white break-all md:whitespace-nowrap">
        BAMSF:KPK3L:8.5.1:09:03
      </span>

      <span class="text-gray-300">No. Revisi</span>
      <span>:</span>
      <span class="font-semibold text-white">
        0
      </span>

    </div>

  </div>

</div>
  </div>
</div>
  </div>
</div>

  </div>
</div>

    <!-- APD Wajib Section -->
    <section class="bg-blue-950 border border-amber-200 rounded-xl p-4 ">
      <div class="flex items-center gap-2 mb-3">
        <i data-lucide="hard-hat" class="w-5 h-5 text-amber-600"></i>
		
        <h2 class="text-sm font-bold text-white uppercase tracking-wider">APD Wajib</h2>
      </div>
      <div class="flex flex-wrap gap-2">
        <span class="text-white text-xs font-semibold px-2.5 py-1 rounded-md">
          SAFETY HELMET
        </span>
        <span class="text-white text-xs font-semibold px-2.5 py-1 rounded-md">
          SAFETY GOGGLES
        </span>
        <span class="text-white text-xs font-semibold px-2.5 py-1 rounded-md">
          SAFETY SHOES
        </span>
        <span class="text-white text-xs font-semibold px-2.5 py-1 rounded-md">
          ROMPI PANTUL
        </span>
        <span class="text-white text-xs font-semibold px-2.5 py-1 rounded-md">
          SARUNG TANGAN
        </span>
      </div>
    </section>

    <!-- List Tahapan Pekerjaan (Mobile Cards) -->
    <div class="space-y-4">

      <!-- 1. Menyiapkan Tools -->
      <div class="bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
        <div class="bg-blue-950 text-white px-4 py-3 flex items-center gap-3">
          <span class="bg-amber-500 text-slate-900 font-extrabold rounded-lg w-7 h-7 flex items-center justify-center text-sm shadow">1</span>
          <h3 class="font-bold text-base">Menyiapkan Tools</h3>
        </div>
        <div class="p-4 space-y-4">
          <!-- Sub 1.1 -->
          <div class="border-l-2 border-amber-500 pl-3 space-y-2">
            <div class="flex items-center gap-2 text-rose-700 font-semibold text-xs uppercase">
              <i data-lucide="alert-triangle" class="w-4 h-4"></i>
              <span>1.1 Identifikasi Bahaya: Kejatuhan</span>
            </div>
            <ul class="text-xs text-slate-700 space-y-1.5 pl-1">
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">1.1.1</span>
                <span>Perhatikan peletakan tools dan pastikan aman</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">1.1.2</span>
                <span>Letakkan tools pada tempat yang mudah dijangkau</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">1.1.3</span>
                <span>Gunakan alat angkat yang sesuai jika diperlukan</span>
              </li>
            </ul>
          </div>

          <!-- Sub 1.2 -->
          <div class="border-l-2 border-amber-500 pl-3 space-y-2">
            <div class="flex items-center gap-2 text-rose-700 font-semibold text-xs uppercase">
              <i data-lucide="alert-triangle" class="w-4 h-4"></i>
              <span>1.2 Identifikasi Bahaya: Tergores</span>
            </div>
            <ul class="text-xs text-slate-700 space-y-1.5 pl-1">
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">1.2.1</span>
                <span>Gunakan sarung tangan untuk memegang tools</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">1.2.2</span>
                <span>Lakukan perbaikan tools, jika ditemukan ada yang tidak aman</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">1.2.3</span>
                <span>Ganti tools jika sudah tidak standard</span>
              </li>
            </ul>
          </div>

          <!-- Sub 1.3 -->
          <div class="border-l-2 border-amber-500 pl-3 space-y-2">
            <div class="flex items-center gap-2 text-rose-700 font-semibold text-xs uppercase">
              <i data-lucide="alert-triangle" class="w-4 h-4"></i>
              <span>1.3 Identifikasi Bahaya: Pinggang Sakit</span>
            </div>
            <ul class="text-xs text-slate-700 space-y-1.5 pl-1">
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">1.3.1</span>
                <span>Perhatikan posisi tubuh waktu mengangkat. Bila berat minta bantuan rekan sekerja atau gunakan alat angkat.</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- 2. Menyiapkan part atau suku cadang -->
      <div class="bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
        <div class="bg-blue-950 text-white px-4 py-3 flex items-center gap-3">
          <span class="bg-amber-500 text-slate-900 font-extrabold rounded-lg w-7 h-7 flex items-center justify-center text-sm shadow">2</span>
          <h3 class="font-bold text-base">Menyiapkan Part atau Suku Cadang</h3>
        </div>
        <div class="p-4 space-y-4">
          <!-- Sub 2.1 -->
          <div class="border-l-2 border-amber-500 pl-3 space-y-2">
            <div class="flex items-center gap-2 text-rose-700 font-semibold text-xs uppercase">
              <i data-lucide="alert-triangle" class="w-4 h-4"></i>
              <span>2.1 Identifikasi Bahaya: Kejatuhan</span>
            </div>
            <ul class="text-xs text-slate-700 space-y-1.5 pl-1">
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">2.1.1</span>
                <span>Persiapkan part pada satu tempat atau baki</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">2.1.2</span>
                <span>Gunakan sarung tangan untuk memegang part</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- 3. Pekerjaan Service Unit -->
      <div class="bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
        <div class="bg-blue-950 text-white px-4 py-3 flex items-center gap-3">
          <span class="bg-amber-500 text-slate-900 font-extrabold rounded-lg w-7 h-7 flex items-center justify-center text-sm shadow">3</span>
          <h3 class="font-bold text-base">Pekerjaan Service Unit</h3>
        </div>
        <div class="p-4 space-y-4">
          <!-- Sub 3.1 -->
          <div class="border-l-2 border-amber-500 pl-3 space-y-2">
            <div class="flex items-center gap-2 text-rose-700 font-semibold text-xs uppercase">
              <i data-lucide="alert-triangle" class="w-4 h-4"></i>
              <span>3.1 Identifikasi Bahaya: Kejatuhan</span>
            </div>
            <ul class="text-xs text-slate-700 space-y-1.5 pl-1">
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">3.1.1</span>
                <span>Jangan ada dibawah komponen yang sudah diangkat</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">3.1.2</span>
                <span>Pastikan meletakkan komponen, spare part dan tool ditempat yang aman</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">3.1.3</span>
                <span>Gunakan alat lifting yang sesuai dengan SWL</span>
              </li>
            </ul>
          </div>

          <!-- Sub 3.2 -->
          <div class="border-l-2 border-amber-500 pl-3 space-y-2">
            <div class="flex items-center gap-2 text-rose-700 font-semibold text-xs uppercase">
              <i data-lucide="alert-triangle" class="w-4 h-4"></i>
              <span>3.2 Identifikasi Bahaya: Terjepit</span>
            </div>
            <ul class="text-xs text-slate-700 space-y-1.5 pl-1">
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">3.2.1</span>
                <span>Perhatikan posisi tubuh dan anggota badan saat bekerja</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">3.2.2</span>
                <span>Lakukan komunikasi sesama rekan kerja pada saat bekerja</span>
              </li>
            </ul>
          </div>

          <!-- Sub 3.3 -->
          <div class="border-l-2 border-amber-500 pl-3 space-y-2">
            <div class="flex items-center gap-2 text-rose-700 font-semibold text-xs uppercase">
              <i data-lucide="alert-triangle" class="w-4 h-4"></i>
              <span>3.3 Identifikasi Bahaya: Tergores</span>
            </div>
            <ul class="text-xs text-slate-700 space-y-1.5 pl-1">
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">3.3.1</span>
                <span>Gunakan sarung tangan pada saat bekerja</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">3.3.2</span>
                <span>Lakukan perbaikan tools, jika ditemukan ada yang tidak aman</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">3.3.3</span>
                <span>Ganti tools jika tidak standard</span>
              </li>
            </ul>
          </div>

          <!-- Sub 3.4 -->
          <div class="border-l-2 border-amber-500 pl-3 space-y-2">
            <div class="flex items-center gap-2 text-rose-700 font-semibold text-xs uppercase">
              <i data-lucide="alert-triangle" class="w-4 h-4"></i>
              <span>3.4 Identifikasi Bahaya: Pinggang Sakit</span>
            </div>
            <ul class="text-xs text-slate-700 space-y-1.5 pl-1">
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">3.4.1</span>
                <span>Perhatikan posisi tubuh waktu mengangkat. Bila berat minta bantuan rekan sekerja atau gunakan alat angkat.</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- 4. Mencuci Unit -->
      <div class="bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
        <div class="bg-blue-950 text-white px-4 py-3 flex items-center gap-3">
          <span class="bg-amber-500 text-slate-900 font-extrabold rounded-lg w-7 h-7 flex items-center justify-center text-sm shadow">4</span>
          <h3 class="font-bold text-base">Mencuci Unit</h3>
        </div>
        <div class="p-4 space-y-4">
          <!-- Sub 4.1 -->
          <div class="border-l-2 border-amber-500 pl-3 space-y-2">
            <div class="flex items-center gap-2 text-rose-700 font-semibold text-xs uppercase">
              <i data-lucide="alert-triangle" class="w-4 h-4"></i>
              <span>4.1 Identifikasi Bahaya: Terpeleset</span>
            </div>
            <ul class="text-xs text-slate-700 space-y-1.5 pl-1">
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">4.1.1</span>
                <span>Pastikan area kerja bersih dari serakan sampah dan spare part bekas</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">4.1.2</span>
                <span>Gunakan APD</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">4.1.3</span>
                <span>Gunakan mantel anti air agar tidak terkena semburan balik air</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">4.1.4</span>
                <span>Pastikan posisi pijakan saat melakukan pencucian unit.</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- 5. Ground Test Unit -->
      <div class="bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
        <div class="bg-blue-950 text-white px-4 py-3 flex items-center gap-3">
          <span class="bg-amber-500 text-slate-900 font-extrabold rounded-lg w-7 h-7 flex items-center justify-center text-sm shadow">5</span>
          <h3 class="font-bold text-base">Ground Test Unit</h3>
        </div>
        <div class="p-4 space-y-4">
          <!-- Sub 5.1 -->
          <div class="border-l-2 border-amber-500 pl-3 space-y-2">
            <div class="flex items-center gap-2 text-rose-700 font-semibold text-xs uppercase">
              <i data-lucide="alert-triangle" class="w-4 h-4"></i>
              <span>5.1 Identifikasi Bahaya: Unit Menabrak</span>
            </div>
            <ul class="text-xs text-slate-700 space-y-1.5 pl-1">
              <li class="flex items-start gap-2">
                <span class="font-mono text-slate-400">5.1.1</span>
                <span>Pastikan pada saat ground test unit, tidak ada sarana, alat support di sekitar unit radius 30 meter</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

    </div>

    <!-- Footer -->
    <footer class="mt-6 text-center text-xs text-slate-400">
      <p>Job Safety Analysis • Optimised for Mobile View</p>
    </footer>

  </div>

  <script>
    lucide.createIcons();
  </script>
</body>
</html>
                </div>

                <!-- TANDA TANGAN -->
                <div class="pt-6 border-t border-slate-200">
                    <h2 class="text-black font-semibold uppercase text-slate-500 mb-6 tracking-wider">
                        Persetujuan & Tanda Tangan PTBA
                    </h2>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6 text-center">
                        <div>
                            <div class="h-20 sm:h-24 border-b border-dashed border-slate-300"></div>
                            <p class="mt-2 font-medium text-xs sm:text-sm text-slate-800">
                                Sub-Section Head Production Heavy Equipment GET & Undercarriage
                            </p>
                            <input type="text" name="nama_sub_section_head" placeholder="Ketik nama..." class="mt-1 w-full border-0 border-b border-slate-300 bg-transparent text-xs sm:text-sm text-slate-700 text-center focus:border-blue-500 focus:ring-0">
                        </div>

                        <div>
                            <div class="h-20 sm:h-24 border-b border-dashed border-slate-300"></div>
                            <p class="mt-2 font-medium text-xs sm:text-sm text-slate-800">
                                Supervisor / K3
                            </p>
                            <input type="text" name="nama_supervisor" placeholder="Ketik nama..." class="mt-1 w-full border-0 border-b border-slate-300 bg-transparent text-xs sm:text-sm text-slate-700 text-center focus:border-blue-500 focus:ring-0">
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </div>

    <!-- JAVASCRIPT -->
    <script>
        const pmData = {
            "PR756": {
                "PM250": [
                    { part_name: "SOS ENGINE", part_number: "SOS", qty: 1, satuan: "EA" },
                    { part_name: "SOS F/D RH LH", part_number: "SOS", qty: 2, satuan: "EA" },
                    { part_name: "EASY-CHANGE FILTER", part_number: "10297295", qty: 2, satuan: "EA" },
                    { part_name: "FILTER ELEMENT", part_number: "11081663", qty: 1, satuan: "EA" },
                    { part_name: "FUEL FINE FILTER", part_number: "12820742", qty: 2, satuan: "EA" },
                    { part_name: "RACOR", part_number: "P552020TM", qty: 1, satuan: "EA" },
                    { part_name: "ENGINE OIL PERTAMINA", part_number: "PERTAMINA ENGINE 15W-40", qty: 45, satuan: "LTR" }
                ]
            }
        };

        function handleLogin(event) {
            event.preventDefault();
            const user = document.getElementById("username").value.trim();
            const pass = document.getElementById("password").value;
            const errorMsg = document.getElementById("errorMessage");

            if (user === "admin" && pass === "PMSEM2") {
                errorMsg.classList.add("hidden");
                document.getElementById("loginScreen").classList.add("hidden");
                document.getElementById("appScreen").classList.remove("hidden");
            } else {
                errorMsg.classList.remove("hidden");
            }
        }

        function handleLogout() {
            document.getElementById("username").value = "";
            document.getElementById("password").value = "";
            document.getElementById("appScreen").classList.add("hidden");
            document.getElementById("loginScreen").classList.remove("hidden");
        }

        function updatePmChecklist() {
            const model = document.getElementById("modelSelect").value;
            const jenisPm = document.getElementById("jenisPmSelect").value;
            const tbody = document.getElementById("pmTableBody");

            if (!model) {
                tbody.innerHTML = `<tr><td colspan="7" class="p-4 text-center text-slate-400 italic">Silakan pilih Model Unit di atas untuk memuat daftar item PM.</td></tr>`;
                return;
            }

            const items = pmData[model] && pmData[model][jenisPm] ? pmData[model][jenisPm] : [];

            if (items.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" class="p-4 text-center text-slate-400 italic">Belum ada data part untuk Model <b>${model}</b> (${jenisPm}).<br>Silakan gunakan tombol "+ Tambah Komponen" untuk menambahkan manual.</td></tr>`;
                return;
            }

            let html = "";
            items.forEach((item, index) => {
                html += `
                    <tr class="border-b border-slate-200">
                        <td class="p-2 border-r border-slate-200 text-center font-medium nomor-pm">${index + 1}</td>
                        <td class="p-2 border-r border-slate-200"><input type="text" value="${escapeHtml(item.part_name)}" class="w-full p-1 bg-transparent border-0 focus:ring-0 text-xs sm:text-sm"></td>
                        <td class="p-2 border-r border-slate-200 text-center"><input type="text" value="${escapeHtml(item.part_number)}" class="w-full p-1 bg-transparent border-0 focus:ring-0 text-xs sm:text-sm text-center font-mono"></td>
                        <td class="p-2 border-r border-slate-200 text-center"><input type="text" value="${item.qty} ${item.satuan}" class="w-full p-1 bg-transparent border-0 focus:ring-0 text-xs sm:text-sm text-center"></td>
                        <td class="p-2 border-r border-slate-200 text-center">
                            <select class="w-full border border-slate-300 rounded p-1 bg-white focus:ring-1 focus:ring-blue-500 text-xs sm:text-sm">
                                <option value="OK">OK</option>
                                <option value="NOK">NOK</option>
                                <option value="NA">N/A</option>
                            </select>
                        </td>
                        <td class="p-2 border-r border-slate-200"><input type="text" placeholder="Catatan..." class="w-full p-1 border border-slate-200 rounded text-xs sm:text-sm"></td>
                        <td class="p-2 text-center no-print"><button onclick="removeRow(this)" class="text-red-500 hover:text-red-700 font-bold">×</button></td>
                    </tr>
                `;
            });
            tbody.innerHTML = html;
            renumberPmRows();
        }

        function addPmRow() {
            const tbody = document.getElementById("pmTableBody");
            const existingRows = tbody.querySelectorAll("tr");
            if (existingRows.length === 1 && existingRows[0].querySelector("td[colspan='7']")) {
                tbody.innerHTML = "";
            }

            const row = document.createElement("tr");
            row.className = "border-b border-slate-200";
            row.innerHTML = `
                <td class="p-2 border-r border-slate-200 text-center font-medium nomor-pm">-</td>
                <td class="p-2 border-r border-slate-200"><input type="text" placeholder="Nama Part..." class="w-full p-1 bg-transparent border-0 focus:ring-0 text-xs sm:text-sm"></td>
                <td class="p-2 border-r border-slate-200 text-center"><input type="text" placeholder="Part Number" class="w-full p-1 bg-transparent border-0 focus:ring-0 text-xs sm:text-sm text-center font-mono"></td>
                <td class="p-2 border-r border-slate-200 text-center"><input type="text" placeholder="1 EA" class="w-full p-1 bg-transparent border-0 focus:ring-0 text-xs sm:text-sm text-center"></td>
                <td class="p-2 border-r border-slate-200 text-center">
                    <select class="w-full border border-slate-300 rounded p-1 bg-white text-xs sm:text-sm"><option value="OK">OK</option><option value="NOK">NOK</option><option value="NA">N/A</option></select>
                </td>
                <td class="p-2 border-r border-slate-200"><input type="text" placeholder="Catatan..." class="w-full p-1 border border-slate-200 rounded text-xs sm:text-sm"></td>
                <td class="p-2 text-center no-print"><button onclick="removeRow(this)" class="text-red-500 hover:text-red-700 font-bold">×</button></td>
            `;
            tbody.appendChild(row);
            renumberPmRows();
        }

        function renumberPmRows() {
            const rows = document.querySelectorAll("#pmTableBody tr");
            let nomor = 1;
            rows.forEach(row => {
                const cell = row.querySelector(".nomor-pm");
                if (cell) {
                    cell.textContent = nomor;
                    nomor++;
                }
            });
        }

        function addJsaRow() {
            const tableBody = document.querySelector("#jsaTable tbody");
            const row = document.createElement("tr");
            row.className = "border-b border-slate-200";
            row.innerHTML = `
                <td class="p-2 border-r border-slate-200 text-center font-bold">-</td>
                <td class="p-2 border-r border-slate-200"><input type="text" placeholder="Langkah Kerja..." class="w-full p-1 bg-transparent border-0 focus:ring-0 text-xs sm:text-sm"></td>
                <td class="p-2 border-r border-slate-200 text-center font-mono"><input type="text" placeholder="0.0" class="w-full p-1 bg-transparent border-0 focus:ring-0 text-xs sm:text-sm text-center"></td>
                <td class="p-2 border-r border-slate-200"><input type="text" placeholder="Potensi Bahaya..." class="w-full p-1 bg-transparent border-0 focus:ring-0 text-xs sm:text-sm"></td>
                <td class="p-2 border-r border-slate-200 text-center font-mono"><input type="text" placeholder="0.0.0" class="w-full p-1 bg-transparent border-0 focus:ring-0 text-xs sm:text-sm text-center"></td>
                <td class="p-2 border-r border-slate-200"><textarea placeholder="Pengendalian..." rows="2" class="w-full p-1 bg-transparent border border-slate-200 rounded text-xs sm:text-sm"></textarea></td>
                <td class="p-2 text-center no-print"><button onclick="removeRow(this)" class="text-red-500 hover:text-red-700 font-bold">×</button></td>
            `;
            tableBody.appendChild(row);
        }

        function removeRow(button) {
            const row = button.closest("tr");
            if (row) {
                row.remove();
                renumberPmRows();
            }
        }

        function escapeHtml(value) {
            if (!value) return "";
            return String(value).replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
        }

        window.addEventListener("DOMContentLoaded", function () {
            const tanggal = document.getElementById("tanggalJam");
            if (tanggal) {
                const now = new Date();
                now.setMinutes(now.getMinutes() - now.getTimezoneOffset());
                tanggal.value = now.toISOString().slice(0, 16);
            }
        });
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikasi Kamera Dokumentasi</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 20px; background: #f0f2f5; }
        video, canvas { width: 100%; max-width: 400px; border-radius: 10px; margin-top: 10px; }
        button { padding: 12px 20px; font-size: 16px; background: #007bff; color: white; border: none; border-radius: 5px; cursor: pointer; margin-top: 10px; }
        button:hover { background: #0056b3; }
    </style>
</head>
<body>

    <h2>Kamera Dokumentasi</h2>
    
    <!-- Tampilan Kamera -->
    <video id="video" autoplay playsinline></video>
    <br>
    <button id="capture-btn">Ambil Foto</button>

    <!-- Hasil Foto -->
    <h3>Hasil Dokumentasi:</h3>
    <canvas id="canvas" style="display:none;"></canvas>
    <img id="photo" alt="Hasil foto akan muncul di sini" style="display:none;">

    <script>
        const video = document.getElementById('video');
        const canvas = document.getElementById('canvas');
        const photo = document.getElementById('photo');
        const captureBtn = document.getElementById('capture-btn');

        // Mengaktifkan kamera HP
        async function initCamera() {
            try {
                const stream = await navigator.mediaDevices.getUserMedia({ 
                    video: { facingMode: 'environment' } // 'environment' untuk kamera belakang
                });
                video.srcObject = stream;
            } catch (err) {
                alert("Gagal mengakses kamera: " + err);
            }
        }

        // Mengambil foto
        captureBtn.addEventListener('click', () => {
            const context = canvas.getContext('2d');
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;
            context.drawImage(video, 0, 0, canvas.width, canvas.height);
            
            // Konversi ke format gambar
            const dataUrl = canvas.toDataURL('image/png');
            photo.setAttribute('src', dataUrl);
            photo.style.display = 'block';
        });

        // Jalankan kamera saat halaman dibuka
        initCamera();
    </script>

</body>
</html>
