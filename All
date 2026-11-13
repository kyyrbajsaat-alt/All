<!DOCTYPE html>
<html lang="kk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ӘМАТ / СЗПТ — Әлеуметтік маңызы бар азық-түлік бағасының мониторингі</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; background-color: #0b1320; color: #e2e8f0; }
        .card { background-color: #131c2e; border: 1px solid #1e293b; border-radius: 0.75rem; }
        .input-dark { background-color: #0f172a; border: 1px solid #334155; color: #f8fafc; }
        .input-dark:focus { outline: none; border-color: #38bdf8; }
        .tab-active { background-color: #0284c7; color: #ffffff; }
        .tab-inactive { color: #94a3b8; }
        .tab-inactive:hover { background-color: #1e293b; color: #f8fafc; }
    </style>
</head>
<body class="min-h-screen flex flex-col">

    <!-- Top Header -->
    <header class="border-b border-slate-800 bg-[#0f172a]/90 sticky top-0 z-30 backdrop-blur">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="w-9 h-9 rounded-lg bg-sky-500/20 border border-sky-500/40 flex items-center justify-center text-sky-400 font-bold">
                    ӘМ
                </div>
                <div>
                    <div class="flex items-center space-x-2">
                        <span class="text-xs font-semibold tracking-wider text-sky-400 uppercase">ХАКАТОН 2026 / 03 КЕЙС</span>
                    </div>
                    <h1 class="text-sm sm:text-base font-bold text-white leading-tight">Әлеуметтік маңызы бар азық-түлік бағасының мониторингі (ӘМАТ / СЗПТ)</h1>
                </div>
            </div>

            <!-- Role Switcher -->
            <div class="flex items-center space-x-2">
                <span class="hidden md:inline text-xs text-slate-400">Рөл:</span>
                <select id="roleSelect" onchange="changeRole()" class="input-dark text-xs sm:text-sm rounded-lg px-3 py-1.5 font-medium">
                    <option value="specialist">Мониторинг маманы</option>
                    <option value="analyst" selected>Талдаушы</option>
                    <option value="head">Жауапты басшы</option>
                </select>
            </div>
        </div>
    </header>

    <!-- Disclaimer Banner -->
    <div class="bg-amber-500/10 border-b border-amber-500/20 px-4 py-2">
        <div class="max-w-7xl mx-auto flex items-center justify-between text-xs text-amber-300">
            <span>⚠️ <strong>Ескерту:</strong> Бұл жүйедегі ескертулер мен ауытқулар тек тексеруге негіз болады. Жүйе заң бұзушылық туралы автоматты қорытынды шығармайды.</span>
            <span id="roleBadge" class="hidden sm:inline-block px-2 py-0.5 rounded bg-sky-500/20 text-sky-300 font-medium">Талдаушы режимі</span>
        </div>
    </div>

    <!-- Navigation Tabs -->
    <div class="max-w-7xl mx-auto w-full px-4 sm:px-6 lg:px-8 pt-6">
        <nav class="flex flex-wrap gap-2 border-b border-slate-800 pb-4">
            <button onclick="switchTab('dashboard')" id="tab-dashboard" class="tab-active px-4 py-2 rounded-lg text-sm font-medium transition">
                1. Аналитика және Салыстыру
            </button>
            <button onclick="switchTab('entry')" id="tab-entry" class="tab-inactive px-4 py-2 rounded-lg text-sm font-medium transition">
                2. Баға енгізу және Біріздендіру
            </button>
            <button onclick="switchTab('anomalies')" id="tab-anomalies" class="tab-inactive px-4 py-2 rounded-lg text-sm font-medium transition flex items-center space-x-2">
                <span>3. Ауытқуларды тексеру</span>
                <span id="anomalyCountBadge" class="px-1.5 py-0.5 text-xs rounded-full bg-rose-500/20 text-rose-400 font-semibold">0</span>
            </button>
            <button onclick="switchTab('directories')" id="tab-directories" class="tab-inactive px-4 py-2 rounded-lg text-sm font-medium transition">
                4. Анықтамалықтар
            </button>
        </nav>
    </div>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto w-full px-4 sm:px-6 lg:px-8 py-6 flex-1">

        <!-- TAB 1: DASHBOARD -->
        <section id="view-dashboard" class="space-y-6">
            <!-- Filters -->
            <div class="card p-4 grid grid-cols-1 sm:grid-cols-3 gap-4">
                <div>
                    <label class="block text-xs text-slate-400 mb-1">ӘМАТ тауары</label>
                    <select id="filterProduct" onchange="renderDashboard()" class="input-dark w-full rounded-lg px-3 py-2 text-sm"></select>
                </div>
                <div>
                    <label class="block text-xs text-slate-400 mb-1">Аумақ (Қала / Аудан)</label>
                    <select id="filterRegion" onchange="renderDashboard()" class="input-dark w-full rounded-lg px-3 py-2 text-sm">
                        <option value="ALL">Барлық аумақтар</option>
                    </select>
                </div>
                <div>
                    <label class="block text-xs text-slate-400 mb-1">Бақылау кезеңі</label>
                    <select id="filterPeriod" onchange="renderDashboard()" class="input-dark w-full rounded-lg px-3 py-2 text-sm">
                        <option value="ALL">Барлық күндер</option>
                        <option value="2026-11-14">14.11.2026 (Бүгін)</option>
                        <option value="2026-11-07">07.11.2026 (Өткен апта)</option>
                    </select>
                </div>
            </div>

            <!-- KPI Cards -->
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                <div class="card p-5">
                    <div class="text-xs text-slate-400 uppercase tracking-wider">Ең төменгі баға (Min)</div>
                    <div id="kpiMin" class="text-2xl font-bold text-emerald-400 mt-2">— ₸</div>
                    <div id="kpiMinUnit" class="text-xs text-slate-500 mt-1">Біріздендірілген өлшем</div>
                </div>
                <div class="card p-5 border-sky-500/40">
                    <div class="text-xs text-sky-400 uppercase tracking-wider font-semibold">Медианалық баға (Median)</div>
                    <div id="kpiMedian" class="text-2xl font-bold text-white mt-2">— ₸</div>
                    <div class="text-xs text-slate-500 mt-1">Негізгі салыстыру эталоны</div>
                </div>
                <div class="card p-5">
                    <div class="text-xs text-slate-400 uppercase tracking-wider">Ең жоғарғы баға (Max)</div>
                    <div id="kpiMax" class="text-2xl font-bold text-rose-400 mt-2">— ₸</div>
                    <div id="kpiMaxStore" class="text-xs text-slate-500 mt-1">—</div>
                </div>
                <div class="card p-5">
                    <div class="text-xs text-slate-400 uppercase tracking-wider">Жазбалар саны / Ауытқу</div>
                    <div class="flex items-baseline space-x-2 mt-2">
                        <span id="kpiTotal" class="text-2xl font-bold text-white">0</span>
                        <span id="kpiAlerts" class="text-sm font-semibold text-amber-400">(0 ескерту)</span>
                    </div>
                    <div class="text-xs text-slate-500 mt-1">Медианадан >10% жоғары</div>
                </div>
            </div>

            <!-- Chart & Table -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <div class="card p-5 lg:col-span-1 flex flex-col justify-between">
                    <div>
                        <h3 class="text-sm font-semibold text-white mb-1">Сауда нүктелері бойынша салыстыру</h3>
                        <p class="text-xs text-slate-400 mb-4">Біріздендірілген баға (теңге / базалық бірлік)</p>
                    </div>
                    <div class="relative h-64">
                        <canvas id="priceChart"></canvas>
                    </div>
                </div>

                <div class="card p-5 lg:col-span-2 overflow-x-auto">
                    <div class="flex items-center justify-between mb-4">
                        <h3 class="text-sm font-semibold text-white">Біріздендірілген бағалар тізілімі</h3>
                        <button onclick="exportCSV()" class="text-xs bg-slate-800 hover:bg-slate-700 text-sky-400 px-3 py-1.5 rounded-lg border border-slate-700 transition">
                            CSV жүктеу
                        </button>
                    </div>
                    <table class="w-full text-left border-collapse text-sm">
                        <thead>
                            <tr class="border-b border-slate-800 text-xs text-slate-400 uppercase">
                                <th class="py-2.5 px-3">Сауда нүктесі / Аумақ</th>
                                <th class="py-2.5 px-3">Күні</th>
                                <th class="py-2.5 px-3">Бастапқы қаптама</th>
                                <th class="py-2.5 px-3">Бірізді баға</th>
                                <th class="py-2.5 px-3">Ауытқу</th>
                            </tr>
                        </thead>
                        <tbody id="dashboardTableBody" class="divide-y divide-slate-800/70"></tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- TAB 2: DATA ENTRY & STANDARDIZATION -->
        <section id="view-entry" class="hidden space-y-6">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <!-- Manual Entry Form -->
                <div class="card p-6">
                    <h2 class="text-base font-bold text-white mb-1">Қолмен баға енгізу</h2>
                    <p class="text-xs text-slate-400 mb-5">Жүйе қаптама салмағын/көлемін автоматты түрде 1 кг, 1 литр немесе 1 данаға келтіреді.</p>

                    <form onsubmit="addPriceRecord(event)" class="space-y-4">
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-xs text-slate-400 mb-1">Тауар</label>
                                <select id="entryProduct" onchange="updateConversionPreview()" class="input-dark w-full rounded-lg px-3 py-2 text-sm" required></select>
                            </div>
                            <div>
                                <label class="block text-xs text-slate-400 mb-1">Сауда нүктесі</label>
                                <select id="entryStore" class="input-dark w-full rounded-lg px-3 py-2 text-sm" required></select>
                            </div>
                        </div>

                        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                            <div>
                                <label class="block text-xs text-slate-400 mb-1">Қаптама көлемі</label>
                                <input type="number" step="any" min="0.01" id="entryQty" value="900" oninput="updateConversionPreview()" class="input-dark w-full rounded-lg px-3 py-2 text-sm" required>
                            </div>
                            <div>
                                <label class="block text-xs text-slate-400 mb-1">Өлшем бірлігі</label>
                                <select id="entryUnit" onchange="updateConversionPreview()" class="input-dark w-full rounded-lg px-3 py-2 text-sm">
                                    <option value="g" selected>грамм (г)</option>
                                    <option value="kg">килограмм (кг)</option>
                                    <option value="ml">миллилитр (мл)</option>
                                    <option value="l">литр (л)</option>
                                    <option value="pcs">дана (шт)</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-xs text-slate-400 mb-1">Қаптама бағасы (₸)</label>
                                <input type="number" step="any" min="1" id="entryPrice" value="450" oninput="updateConversionPreview()" class="input-dark w-full rounded-lg px-3 py-2 text-sm" required>
                            </div>
                        </div>

                        <div>
                            <label class="block text-xs text-slate-400 mb-1">Бақылау күні</label>
                            <input type="date" id="entryDate" value="2026-11-14" class="input-dark w-full rounded-lg px-3 py-2 text-sm" required>
                        </div>

                        <!-- Live Calculation Box -->
                        <div class="p-4 rounded-lg bg-sky-500/10 border border-sky-500/30 flex items-center justify-between">
                            <div>
                                <div class="text-xs text-sky-300">Біріздендірілген есептік баға:</div>
                                <div id="conversionFormula" class="text-xs text-slate-400 mt-0.5">900 г үшін 450 ₸ → 1 кг</div>
                            </div>
                            <div id="conversionResult" class="text-xl font-bold text-sky-400">500 ₸/кг</div>
                        </div>

                        <div id="entryFeedback" class="hidden text-xs p-3 rounded-lg"></div>

                        <button type="submit" class="w-full bg-sky-600 hover:bg-sky-500 text-white font-semibold py-2.5 rounded-lg text-sm transition">
                            Тексеру және Тізілімге қосу
                        </button>
                    </form>
                </div>

                <!-- Batch File Upload & Validation -->
                <div class="card p-6 flex flex-col justify-between">
                    <div>
                        <h2 class="text-base font-bold text-white mb-1">Файлдан пакеттік жүктеу және Валидация</h2>
                        <p class="text-xs text-slate-400 mb-5">CSV/Excel деректерін жүктеу кезінде қайталанған және қате жазбалар автоматты сүзіледі.</p>

                        <div class="border-2 border-dashed border-slate-700 rounded-xl p-6 text-center hover:border-sky-500/50 transition">
                            <p class="text-sm text-slate-300 font-medium mb-2">Мониторинг файлын таңдаңыз (.csv)</p>
                            <p class="text-xs text-slate-500 mb-4">Формат: тауар_коды;дүкен_коды;күні;көлем;бірлік;баға</p>
                            <input type="file" id="csvFileInput" accept=".csv" onchange="handleFileUpload(event)" class="hidden">
                            <div class="flex flex-wrap justify-center gap-3">
                                <button type="button" onclick="document.getElementById('csvFileInput').click()" class="bg-slate-800 hover:bg-slate-700 text-white px-4 py-2 rounded-lg text-xs font-medium border border-slate-600 transition">
                                    Файл таңдау
                                </button>
                                <button type="button" onclick="simulateBatchImport()" class="bg-sky-500/20 hover:bg-sky-500/30 text-sky-300 px-4 py-2 rounded-lg text-xs font-medium border border-sky-500/40 transition">
                                    Тесттік файлды жүктеу (қателермен)
                                </button>
                            </div>
                        </div>

                        <div id="validationLog" class="mt-5 space-y-2">
                            <div class="text-xs text-slate-400 font-semibold">Валидация журналы:</div>
                            <div id="validationMessages" class="text-xs text-slate-500 bg-slate-900/80 p-3 rounded-lg border border-slate-800 max-h-48 overflow-y-auto space-y-1.5">
                                Жүктеу күтілуде...
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- TAB 3: ANOMALIES & VERIFICATION -->
        <section id="view-anomalies" class="hidden space-y-6">
            <div class="card p-5">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-5">
                    <div>
                        <h2 class="text-base font-bold text-white">Тексеруді қажет ететін ауытқулар</h2>
                        <p class="text-xs text-slate-400">Медианалық бағадан +10%-дан жоғары ауытқыған жазбалар тізімі. Сарапшы қорытындысын енгізіңіз.</p>
                    </div>
                </div>

                <div id="anomaliesList" class="space-y-4"></div>
            </div>
        </section>

        <!-- TAB 4: DIRECTORIES -->
        <section id="view-directories" class="hidden space-y-6">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Products Directory -->
                <div class="card p-5">
                    <h3 class="text-base font-bold text-white mb-1">ӘМАТ тауарларының анықтамалығы</h3>
                    <p class="text-xs text-slate-400 mb-4">Біріздендірілген базалық өлшем бірліктері бекітілген</p>
                    <form onsubmit="addProduct(event)" class="flex gap-2 mb-4">
                        <input type="text" id="newProdName" placeholder="Тауар атауы (мыс: Қарақұмық)" class="input-dark flex-1 rounded-lg px-3 py-1.5 text-xs" required>
                        <select id="newProdBase" class="input-dark rounded-lg px-2 py-1.5 text-xs">
                            <option value="кг">кг</option>
                            <option value="л">л</option>
                            <option value="дана">дана</option>
                        </select>
                        <button type="submit" class="bg-sky-600 hover:bg-sky-500 text-white px-3 py-1.5 rounded-lg text-xs font-medium">Қосу</button>
                    </form>
                    <ul id="productDirList" class="divide-y divide-slate-800 text-sm"></ul>
                </div>

                <!-- Stores Directory -->
                <div class="card p-5">
                    <h3 class="text-base font-bold text-white mb-1">Сауда нүктелерінің анықтамалығы</h3>
                    <p class="text-xs text-slate-400 mb-4">Дүкендер, супермаркеттер және базарлар</p>
                    <form onsubmit="addStore(event)" class="flex gap-2 mb-4">
                        <input type="text" id="newStoreName" placeholder="Нүкте атауы (мыс: Small №4)" class="input-dark flex-1 rounded-lg px-3 py-1.5 text-xs" required>
                        <input type="text" id="newStoreRegion" placeholder="Аумақ (мыс: Қызылорда қ.)" class="input-dark w-36 rounded-lg px-3 py-1.5 text-xs" required>
                        <button type="submit" class="bg-sky-600 hover:bg-sky-500 text-white px-3 py-1.5 rounded-lg text-xs font-medium">Қосу</button>
                    </form>
                    <ul id="storeDirList" class="divide-y divide-slate-800 text-sm"></ul>
                </div>
            </div>
        </section>

    </main>

    <script>
        let products = [
            { id: 'P1', name: 'Қант (құмшекер)', baseUnit: 'кг' },
            { id: 'P2', name: 'Күнбағыс майы', baseUnit: 'л' },
            { id: 'P3', name: 'Бірінші сұрыпты бидай ұны', baseUnit: 'кг' },
            { id: 'P4', name: 'Тауық жұмыртқасы (1 санат)', baseUnit: 'дана' },
            { id: 'P5', name: 'Күріш (ақталған)', baseUnit: 'кг' }
        ];

        let stores = [
            { id: 'S1', name
