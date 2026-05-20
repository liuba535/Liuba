```html
<!DOCTYPE html>
<html lang="ro">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Canva Simulator - Proiectul Meu despre Cărți</title>
    <!-- Tailwind CSS pentru stilizare rapidă și modernă -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Fonturi speciale din Google Fonts pentru aspect editorial/literar -->
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400..900;1,400..900&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&family=Cinzel:wght@400;700&family=EB+Garamond:ital,wght@0,400..800;1,400..800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
        }
        .font-playfair {
            font-family: 'Playfair Display', serif;
        }
        .font-cinzel {
            font-family: 'Cinzel', serif;
        }
        .font-garamond {
            font-family: 'EB Garamond', serif;
        }
        /* Personalizare scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0f172a;
        }
        ::-webkit-scrollbar-thumb {
            background: #334155;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #475569;
        }
    </style>
</head>
<body class="bg-slate-900 text-slate-100 min-h-screen flex flex-col overflow-hidden">

    <!-- Bara de Navigare Superioară (Stil Canva) -->
    <header class="bg-slate-950 border-b border-slate-800 px-4 py-3 flex items-center justify-between z-10">
        <div class="flex items-center space-x-3">
            <!-- Logo Canva fictiv în gradient -->
            <div class="bg-gradient-to-tr from-purple-600 via-pink-500 to-blue-500 p-2 rounded-lg shadow-lg flex items-center justify-center">
                <span class="text-white font-extrabold tracking-wider text-xs">CANVA</span>
            </div>
            <div class="h-5 w-px bg-slate-800"></div>
            <div>
                <h1 class="text-sm font-semibold text-slate-200">Prezentare: Lumea Cărților</h1>
                <p class="text-[10px] text-slate-500 flex items-center">
                    <span class="w-2 h-2 rounded-full bg-emerald-500 inline-block mr-1 animate-pulse"></span> 
                    Salvat în browser local
                </p>
            </div>
        </div>

        <div class="flex items-center space-x-3">
            <!-- Selector de Temă Vizuală -->
            <div class="flex items-center bg-slate-900 border border-slate-800 rounded-lg p-1 text-xs">
                <span class="text-slate-400 px-2">Design:</span>
                <select id="themeSelect" onchange="changeTheme(this.value)" class="bg-slate-950 text-slate-200 border-none rounded p-1 focus:ring-1 focus:ring-purple-500 text-xs cursor-pointer focus:outline-none">
                    <option value="warm-cream">Warm Cream (Clasic)</option>
                    <option value="emerald-green">Emerald Library</option>
                    <option value="midnight-blue">Midnight Blue</option>
                    <option value="minimalist-white">Modern Minimalist</option>
                </select>
            </div>

            <!-- Buton Mod Prezentare -->
            <button onclick="openPresentation()" class="bg-gradient-to-r from-purple-600 to-pink-600 hover:from-purple-500 hover:to-pink-500 text-white text-xs font-semibold px-4 py-2 rounded-lg shadow-lg transition flex items-center space-x-1.5">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
                <span>Prezintă (16:9)</span>
            </button>

            <!-- Buton Export/Copiere Text -->
            <button onclick="toggleSummaryModal(true)" class="bg-slate-800 hover:bg-slate-700 text-slate-200 text-xs px-3 py-2 rounded-lg border border-slate-700 transition flex items-center space-x-1">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-purple-400" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 5H6a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2v-1M8 5a2 2 0 002 2h2a2 2 0 002-2M8 5a2 2 0 012-2h2a2 2 0 012 2m0 0h2a2 2 0 012 2v3m2 4H10m0 0l3-3m-3 3l3 3" /></svg>
                <span>Copiază Textul</span>
            </button>
        </div>
    </header>

    <!-- Spațiul Principal de Lucru -->
    <div class="flex flex-1 overflow-hidden">
        <!-- Panoul Lateral Stânga (Editor de Text) -->
        <aside class="w-80 bg-slate-950 border-r border-slate-800 flex flex-col overflow-y-auto p-4 shrink-0">
            <h2 class="text-xs font-bold uppercase tracking-wider text-purple-400 mb-4 flex items-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1.5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" /></svg>
                Personalizează Slide-ul
            </h2>

            <!-- Mesaj Ajutător -->
            <div class="bg-slate-900 border border-slate-800 rounded-xl p-3 mb-5 text-xs text-slate-300">
                <div class="font-semibold text-purple-400 mb-1 flex items-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5 mr-1" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" /></svg>
                    Instrucțiuni rapide:
                </div>
                <p class="leading-relaxed text-slate-400">Modifică textele de mai jos pentru a schimba instantaneu conținutul din slide-ul curent din dreapta.</p>
            </div>

            <!-- Intrări pentru Editare Text -->
            <div class="space-y-4">
                <div>
                    <label class="block text-[10px] font-bold text-slate-400 mb-1 uppercase tracking-wider">Titlu Slide</label>
                    <input type="text" id="editorTitle" oninput="updateSlideText('title', this.value)" class="w-full bg-slate-900 border border-slate-800 rounded-lg px-3 py-2 text-sm text-slate-100 focus:ring-2 focus:ring-purple-500 focus:outline-none transition">
                </div>

                <div>
                    <label class="block text-[10px] font-bold text-slate-400 mb-1 uppercase tracking-wider">Subtitlu / Sursă / Citat</label>
                    <input type="text" id="editorSubtitle" oninput="updateSlideText('subtitle', this.value)" class="w-full bg-slate-900 border border-slate-800 rounded-lg px-3 py-2 text-sm text-slate-100 focus:ring-2 focus:ring-purple-500 focus:outline-none transition">
                </div>

                <!-- Secțiune dinamică de conținut adițional -->
                <div class="border-t border-slate-800 pt-3">
                    <label class="block text-[10px] font-bold text-slate-400 mb-2 uppercase tracking-wider">Puncte Importante</label>
                    <div id="editorInputs" class="space-y-3">
                        <!-- Generat dinamic prin JS -->
                    </div>
                </div>

                <!-- Tipografia Proiectului -->
                <div class="border-t border-slate-800 pt-4">
                    <label class="block text-[10px] font-bold text-slate-400 mb-2 uppercase tracking-wider">Stil Font Proiect</label>
                    <div class="grid grid-cols-2 gap-2">
                        <button onclick="changeFont('playfair')" class="bg-slate-900 hover:bg-slate-800 border border-slate-800 rounded-lg p-2 text-center text-xs text-slate-300 font-semibold">
                            Serif Clasic
                        </button>
                        <button onclick="changeFont('jakarta')" class="bg-slate-900 hover:bg-slate-800 border border-slate-800 rounded-lg p-2 text-center text-xs text-slate-300 font-semibold">
                            Sans Modern
                        </button>
                    </div>
                </div>
            </div>
        </aside>

        <!-- Zona centrală a pânzei (Canvas de tip Canva) -->
        <main class="flex-1 bg-slate-900 flex flex-col p-6 justify-between items-center overflow-hidden">
            
            <!-- Controls superioare pentru Canvas (Zoom, Indicator) -->
            <div class="w-full max-w-4xl flex justify-between items-center text-xs text-slate-400 mb-2 px-2">
                <span id="slideIndicator" class="font-semibold tracking-wider text-slate-300">Slide 1 din 6</span>
                <div class="flex items-center space-x-3">
                    <button onclick="zoomCanvas(-10)" class="hover:text-slate-200 transition">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0zM13 10H7" /></svg>
                    </button>
                    <span id="zoomLabel" class="font-mono">100%</span>
                    <button onclick="zoomCanvas(10)" class="hover:text-slate-200 transition">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0zM10 7v6m3-3H7" /></svg>
                    </button>
                    <div class="h-3 w-px bg-slate-800"></div>
                    <button onclick="resetZoom()" class="hover:text-slate-200 transition text-[11px]">Resetează Zoom</button>
                </div>
            </div>

            <!-- Slide-ul propriu-zis (Format 16:9) -->
            <div class="flex-1 w-full flex items-center justify-center p-2 relative overflow-hidden">
                <div id="slideCanvas" class="aspect-[16/9] w-full max-w-4xl bg-[#FCF8F2] text-[#2D2A26] rounded-2xl shadow-2xl relative overflow-hidden transition-all duration-300 p-8 sm:p-12 flex flex-col justify-between border border-slate-800/20" style="transform: scale(1); transform-origin: center;">
                    <div id="canvasInner" class="h-full w-full flex flex-col justify-between">
                        <!-- Conținutul generat dinamic prin JavaScript -->
                    </div>
                </div>
            </div>

            <!-- Controlerele de navigare rapidă și Thumbnails (Jos) -->
            <div class="w-full max-w-4xl mt-4 bg-slate-950/80 backdrop-blur border border-slate-800 rounded-2xl p-3 flex items-center justify-between">
                <button onclick="prevSlide()" class="p-2.5 bg-slate-900 border border-slate-800 rounded-xl hover:bg-slate-800 text-slate-300 transition shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" /></svg>
                </button>

                <!-- Zona de previzualizare slide-uri mici -->
                <div id="thumbnailContainer" class="flex overflow-x-auto space-x-3 px-3 py-1 w-full mx-2 justify-center scroll-smooth">
                    <!-- Miniature generate dinamic -->
                </div>

                <button onclick="nextSlide()" class="p-2.5 bg-slate-900 border border-slate-800 rounded-xl hover:bg-slate-800 text-slate-300 transition shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" /></svg>
                </button>
            </div>
        </main>
    </div>

    <!-- Modul Prezentare Full-Screen -->
    <div id="presentationOverlay" class="fixed inset-0 bg-slate-950 z-50 hidden flex-col justify-center items-center">
        <!-- Ecran mare de prezentare -->
        <div class="w-full h-full max-w-7xl aspect-[16/9] max-h-screen p-8 flex items-center justify-center relative">
            <div id="presentationSlide" class="aspect-[16/9] w-full max-w-5xl bg-[#FCF8F2] text-[#2D2A26] rounded-2xl shadow-2xl relative overflow-hidden p-16 flex flex-col justify-between transition-all duration-300">
                <!-- Conținut sincronizat cu slide-ul activ -->
            </div>

            <!-- Butoane navigare stânga/dreapta în prezentare -->
            <button onclick="prevSlide()" class="absolute left-6 top-1/2 -translate-y-1/2 p-3 bg-white/10 hover:bg-white/20 text-white rounded-full transition-all focus:outline-none">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" /></svg>
            </button>
            <button onclick="nextSlide()" class="absolute right-6 top-1/2 -translate-y-1/2 p-3 bg-white/10 hover:bg-white/20 text-white rounded-full transition-all focus:outline-none">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" /></svg>
            </button>
        </div>

        <!-- Meniu flotant inferior -->
        <div class="absolute bottom-6 bg-slate-900/95 backdrop-blur border border-slate-800 text-white px-6 py-3 rounded-full flex items-center space-x-6 text-sm shadow-xl z-50">
            <span id="presIndicator" class="font-semibold text-purple-400">1 / 6</span>
            <div class="h-4 w-px bg-slate-700"></div>
            <button onclick="prevSlide()" class="hover:text-purple-400 transition">Precedent</button>
            <button onclick="nextSlide()" class="hover:text-purple-400 transition">Următorul</button>
            <div class="h-4 w-px bg-slate-700"></div>
            <button onclick="closePresentation()" class="bg-red-600 hover:bg-red-500 text-white font-semibold px-4 py-1.5 rounded-full transition text-xs">Închide Prezentarea (ESC)</button>
        </div>
    </div>

    <!-- Modalul de Exportare/Copiere Text -->
    <div id="summaryModal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-slate-900 border border-slate-800 rounded-2xl max-w-2xl w-full flex flex-col max-h-[85vh] shadow-2xl overflow-hidden animate-in fade-in zoom-in-95 duration-250">
            <div class="px-6 py-4 border-b border-slate-800 flex justify-between items-center">
                <h3 class="text-lg font-bold text-slate-100 flex items-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-purple-500 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" /></svg>
                    Conținut Proiect pentru Import în Canva
                </h3>
                <button onclick="toggleSummaryModal(false)" class="text-slate-400 hover:text-slate-200 transition">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
                </button>
            </div>
            <div class="p-6 overflow-y-auto space-y-4 text-sm text-slate-300 leading-relaxed" id="summaryModalContent">
                <!-- Raportul text generat automat -->
            </div>
            <div class="px-6 py-4 border-t border-slate-800 bg-slate-950 flex justify-between items-center">
                <span class="text-xs text-slate-500">Folosește acest document structurat ca suport de date.</span>
                <button onclick="copyToClipboard()" id="copyBtn" class="bg-purple-600 hover:bg-purple-500 text-white font-semibold text-xs px-4 py-2.5 rounded-xl shadow transition">
                    Copiază tot textul
                </button>
            </div>
        </div>
    </div>

    <!-- Logica Principală a Aplicației în JavaScript -->
    <script>
        // Structura și conținutul inițial al celor 6 slide-uri despre cărți
        const slides = [
            {
                id: 1,
                title: "Călătorie în Lumea Cărților",
                subtitle: "De la Pagină la Imaginație și Cunoaștere",
                layout: "cover",
                items: [
                    "Proiect de Cultură și Lectură Literară",
                    "Apasă pe oricare text în panoul stâng pentru a-l edita în timp real!"
                ]
            },
            {
                id: 2,
                title: "De Ce Citim? Beneficiile Lecturii",
                subtitle: "Impactul lecturii zilnice asupra corpului și minții noastre",
                layout: "benefits",
                items: [
                    "Stimulare Cerebrală: Lectura fortifică conexiunile neuronale și îmbunătățește considerabil memoria.",
                    "Reducerea Stresului: Doar 6 minute de lectură în fiecare zi pot reduce nivelul de stres cu 68%.",
                    "Empatie și Vocabular: Ne lărgește orizonturile lingvistice și ne ajută să înțelegem mai ușor oamenii."
                ]
            },
            {
                id: 3,
                title: "Genuri Literare Principale",
                subtitle: "Diversitatea scrierilor și importanța lor în lectură",
                layout: "genres",
                items: [
                    "Ficțiune: Fantasy, Sci-Fi, Romane Polițiste sau Istorice (Lumi create de imaginație).",
                    "Non-Ficțiune: Biografii, Istorie, Știință și Cărți de Dezvoltare Personală (Lumea reală).",
                    "Poezie și Dramă: Exprimarea directă a trăirilor profunde în versuri sau dialog teatral."
                ]
            },
            {
                id: 4,
                title: "Anatomia Fizică a unei Cărți",
                subtitle: "Elementele constructive pe care cititorul le atinge zilnic",
                layout: "anatomy",
                items: [
                    "Cotorul (Spine): Zona de legare care ține paginile la un loc, vizibilă pe raft.",
                    "Supracoperta (Dust Jacket): Învelitorul detașabil din hârtie lucioasă, destinat protecției coperților.",
                    "Marginea (Margin): Spațiul alb esențial din jurul textului pentru confort vizual."
                ]
            },
            {
                id: 5,
                title: "Cele Mai Vândute Cărți din Istorie",
                subtitle: "Topul lucrărilor cu cele mai de succes statistici de tipărire",
                layout: "topsellers",
                items: [
                    "Don Quijote (M. de Cervantes) — ~500 de milioane de copii vândute.",
                    "Poveste despre două orașe (C. Dickens) — ~200 de milioane de copii.",
                    "Stăpânul Inelelor (J.R.R. Tolkien) — ~150 de milioane de copii vândute."
                ]
            },
            {
                id: 6,
                title: "O cameră fără cărți este ca un corp fără suflet.",
                subtitle: "— Marcus Tullius Cicero",
                layout: "conclusion",
                items: [
                    "Proiect finalizat cu succes!",
                    "Tu ce carte plănuiești să citești săptămâna aceasta?"
                ]
            }
        ];

        // Stările globale
        let currentSlideIndex = 0;
        let activeFont = "playfair";
        let zoomLevel = 100;
        let isPresenting = false;

        // Palete de culori corespunzătoare temelor Canva
        const themePalettes = {
            "warm-cream": {
                bg: "#FCF8F2",
                titleColor: "#2D1E12",
                subtitleColor: "#6D533D",
                accentColor: "#A67B56",
                textColor: "#3D2B1F"
            },
            "emerald-green": {
                bg: "#0B2B26",
                titleColor: "#F4F9F4",
                subtitleColor: "#8DDF90",
                accentColor: "#D3B53D",
                textColor: "#C3E8CC"
            },
            "midnight-blue": {
                bg: "#0A1128",
                titleColor: "#FFFFFF",
                subtitleColor: "#61867D",
                accentColor: "#E0A96D",
                textColor: "#C0D6DF"
            },
            "minimalist-white": {
                bg: "#FFFFFF",
                titleColor: "#000000",
                subtitleColor: "#4B5563",
                accentColor: "#111827",
                textColor: "#374151"
            }
        };

        let activeThemeKey = "warm-cream";

        // Inițializare aplicație
        window.onload = function() {
            renderThumbnails();
            renderActiveSlide();
            populateEditorInputs();
            
            // Suport pentru taste în modul Prezentare
            document.addEventListener('keydown', function(e) {
                if (e.key === "ArrowRight" || e.key === " ") {
                    nextSlide();
                } else if (e.key === "ArrowLeft") {
                    prevSlide();
                } else if (e.key === "Escape" && isPresenting) {
                    closePresentation();
                }
            });

            // Suport touch gestures pe ecrane mobile
            let touchstartX = 0;
            let touchendX = 0;
            
            const pOverlay = document.getElementById('presentationOverlay');
            pOverlay.addEventListener('touchstart', e => {
                touchstartX = e.changedTouches[0].screenX;
            });
            pOverlay.addEventListener('touchend', e => {
                touchendX = e.changedTouches[0].screenX;
                handleGesture();
            });

            function handleGesture() {
                if (touchendX < touchstartX - 50) nextSlide();
                if (touchendX > touchstartX + 50) prevSlide();
            }
        };

        // Randarea slide-ului selectat în Canvas
        function renderActiveSlide() {
            const currentSlide = slides[currentSlideIndex];
            const palette = themePalettes[activeThemeKey];
            const canvas = document.getElementById("slideCanvas");
            const inner = document.getElementById("canvasInner");
            const ind = document.getElementById("slideIndicator");

            ind.innerText = `Slide ${currentSlideIndex + 1} din ${slides.length}`;
            canvas.style.backgroundColor = palette.bg;
            canvas.style.color = palette.textColor;

            // Alocă clasa corespunzătoare fontului activ
            canvas.className = `aspect-[16/9] w-full max-w-4xl rounded-2xl shadow-2xl relative overflow-hidden transition-all duration-300 p-8 sm:p-12 flex flex-col justify-between border border-slate-800/20 font-${activeFont}`;

            let htmlContent = "";

            // Generarea structurilor HTML pe baza tipului de slide
            if (currentSlide.layout === "cover") {
                htmlContent = `
                    <div class="flex-1 flex flex-col justify-center items-center text-center px-4">
                        <div class="mb-4 inline-block bg-opacity-20 bg-amber-500 text-amber-500 rounded-full px-4 py-1.5 text-xs font-semibold uppercase tracking-widest border border-amber-500/20" style="color: ${palette.accentColor}">
                            PROIECT DE LECTURĂ
                        </div>
                        <h2 class="text-3xl sm:text-5xl font-bold font-cinzel leading-tight tracking-wide mb-4" style="color: ${palette.titleColor}">
                            ${currentSlide.title}
                        </h2>
                        <div class="w-24 h-1 rounded-full mb-6 mx-auto" style="background-color: ${palette.accentColor}"></div>
                        <p class="text-sm sm:text-lg italic opacity-90 font-garamond" style="color: ${palette.subtitleColor}">
                            ${currentSlide.subtitle}
                        </p>
                    </div>
                    <div class="flex justify-between items-center text-[10px] sm:text-xs tracking-wider uppercase opacity-65 font-semibold" style="color: ${palette.subtitleColor}">
                        <span>${currentSlide.items[0]}</span>
                        <span>Creat pentru Canva</span>
                    </div>
                `;
            } else if (currentSlide.layout === "benefits") {
                htmlContent = `
                    <div class="flex-1 flex flex-col justify-center">
                        <div class="mb-4">
                            <span class="text-[10px] font-bold uppercase tracking-wider px-2.5 py-1 rounded" style="background: ${palette.accentColor}25; color: ${palette.accentColor}">STUDIRI ȘTIINȚIFICE</span>
                            <h2 class="text-2xl sm:text-3xl font-bold mt-2" style="color: ${palette.titleColor}">${currentSlide.title}</h2>
                            <p class="text-xs sm:text-sm mt-1" style="color: ${palette.subtitleColor}">${currentSlide.subtitle}</p>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-3 my-auto">
                            ${currentSlide.items.map((item, idx) => {
                                const parts = item.split(': ');
                                return `
                                    <div class="p-4 rounded-xl border border-black/5" style="background: ${palette.bg === '#FFFFFF' ? '#F9FAFB' : palette.titleColor + '08'}">
                                        <div class="w-8 h-8 rounded-full flex items-center justify-center font-bold text-xs mb-2" style="background: ${palette.accentColor}; color: ${palette.bg}">
                                            0${idx + 1}
                                        </div>
                                        <h4 class="font-bold text-xs sm:text-sm mb-1" style="color: ${palette.titleColor}">${parts[0]}</h4>
                                        <p class="text-xs opacity-85 leading-relaxed">${parts[1] || ''}</p>
                                    </div>
                                `;
                            }).join('')}
                        </div>
                    </div>
                `;
            } else if (currentSlide.layout === "genres") {
                htmlContent = `
                    <div class="flex-1 flex flex-col justify-center">
                        <div class="mb-4 flex justify-between items-end">
                            <div>
                                <h2 class="text-2xl sm:text-3xl font-bold" style="color: ${palette.titleColor}">${currentSlide.title}</h2>
                                <p class="text-xs sm:text-sm mt-1" style="color: ${palette.subtitleColor}">${currentSlide.subtitle}</p>
                            </div>
                            <span class="hidden sm:inline-block text-2xl">📖</span>
                        </div>
                        <div class="space-y-2.5 my-auto">
                            ${currentSlide.items.map((item, idx) => {
                                const parts = item.split(': ');
                                return `
                                    <div class="flex items-start p-3 rounded-lg border border-black/5" style="background: ${palette.titleColor + '05'}">
                                        <span class="text-[10px] font-bold uppercase px-2 py-1 rounded mr-3 shrink-0" style="background: ${palette.accentColor}30; color: ${palette.titleColor}">
                                            GEN ${idx + 1}
                                        </span>
                                        <div>
                                            <strong class="text-xs sm:text-sm font-bold block" style="color: ${palette.titleColor}">${parts[0]}</strong>
                                            <p class="text-xs opacity-85 leading-relaxed">${parts[1] || ''}</p>
                                        </div>
                                    </div>
                                `;
                            }).join('')}
                        </div>
                    </div>
                `;
            } else if (currentSlide.layout === "anatomy") {
                htmlContent = `
                    <div class="flex-1 flex flex-col justify-center">
                        <div class="mb-4 text-center">
                            <h2 class="text-2xl sm:text-3xl font-bold" style="color: ${palette.titleColor}">${currentSlide.title}</h2>
                            <p class="text-xs sm:text-sm" style="color: ${palette.subtitleColor}">${currentSlide.subtitle}</p>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 items-center my-auto">
                            <!-- Schiță grafică interactivă -->
                            <div class="flex justify-center">
                                <div class="relative w-36 h-40 border-2 rounded-r-lg shadow-lg flex items-center justify-center" style="border-color: ${palette.accentColor}; background: ${palette.bg}">
                                    <div class="absolute left-0 top-0 bottom-0 w-3 border-r-2" style="background: ${palette.accentColor}; border-color: ${palette.accentColor}"></div>
                                    <span class="text-[10px] font-cinzel font-bold text-center p-3 opacity-30">PAGINILE CĂRȚII</span>
                                    <div class="absolute -right-2 top-10 bg-rose-500 text-white text-[8px] font-bold px-1.5 py-0.5 rounded shadow">Copertă</div>
                                    <div class="absolute left-1/2 top-4 -translate-x-1/2 bg-indigo-500 text-white text-[8px] font-bold px-1.5 py-0.5 rounded shadow">Margine</div>
                                    <div class="absolute -left-12 bottom-10 bg-amber-500 text-white text-[8px] font-bold px-1.5 py-0.5 rounded shadow">Cotor</div>
                                </div>
                            </div>
                            <div class="space-y-3">
                                ${currentSlide.items.map((item, idx) => {
                                    const parts = item.split(': ');
                                    return `
                                        <div class="text-xs">
                                            <strong class="font-bold block" style="color: ${palette.titleColor}">${parts[0]}</strong>
                                            <span class="opacity-80">${parts[1] || ''}</span>
                                        </div>
                                    `;
                                }).join('')}
                            </div>
                        </div>
                    </div>
                `;
            } else if (currentSlide.layout === "topsellers") {
                htmlContent = `
                    <div class="flex-1 flex flex-col justify-center">
                        <div class="mb-4 text-center">
                            <h2 class="text-2xl sm:text-3xl font-bold" style="color: ${palette.titleColor}">${currentSlide.title}</h2>
                            <p class="text-xs sm:text-sm mt-1" style="color: ${palette.subtitleColor}">${currentSlide.subtitle}</p>
                        </div>
                        <div class="flex flex-col space-y-2.5 max-w-xl mx-auto w-full my-auto">
                            ${currentSlide.items.map((item, idx) => {
                                const parts = item.split(' — ');
                                return `
                                    <div class="flex items-center justify-between p-3 rounded-lg border border-black/5" style="background: ${palette.titleColor + '04'}">
                                        <div class="flex items-center space-x-3">
                                            <div class="w-7 h-7 rounded-full font-bold text-xs flex items-center justify-center shadow-sm" style="background: ${palette.accentColor}; color: ${palette.bg}">
                                                ${idx + 1}
                                            </div>
                                            <span class="text-xs sm:text-sm font-semibold" style="color: ${palette.titleColor}">${parts[0]}</span>
                                        </div>
                                        <span class="text-xs font-bold px-2.5 py-1 rounded shrink-0" style="background: ${palette.accentColor}18; color: ${palette.titleColor}">
                                            ${parts[1] || ''}
                                        </span>
                                    </div>
                                `;
                            }).join('')}
                        </div>
                    </div>
                `;
            } else if (currentSlide.layout === "conclusion") {
                htmlContent = `
                    <div class="flex-1 flex flex-col justify-center items-center text-center px-4">
                        <span class="text-3xl mb-3">⭐</span>
                        <h2 class="text-xl sm:text-2xl font-bold font-playfair italic max-w-2xl leading-normal mb-3" style="color: ${palette.titleColor}">
                            "${currentSlide.title}"
                        </h2>
                        <p class="text-xs font-semibold tracking-wider uppercase mb-6" style="color: ${palette.accentColor}">
                            ${currentSlide.subtitle}
                        </p>
                        <div class="h-px w-20 bg-slate-400/30 my-4 mx-auto"></div>
                        <div class="text-xs space-y-1" style="color: ${palette.subtitleColor}">
                            <p class="font-bold">${currentSlide.items[0]}</p>
                            <p class="opacity-80">${currentSlide.items[1]}</p>
                        </div>
                    </div>
                `;
            }

            inner.innerHTML = htmlContent;

            // Transmitere modificări către vizualizarea de prezentare (Fullscreen)
            if (isPresenting) {
                const presSlide = document.getElementById("presentationSlide");
                presSlide.style.backgroundColor = palette.bg;
                presSlide.style.color = palette.textColor;
                presSlide.className = `aspect-[16/9] w-full max-w-5xl rounded-2xl shadow-2xl relative overflow-hidden p-16 flex flex-col justify-between transition-all duration-300 font-${activeFont}`;
                presSlide.innerHTML = htmlContent;
                document.getElementById("presIndicator").innerText = `${currentSlideIndex + 1} / ${slides.length}`;
            }

            updateThumbnailHighlight();
        }

        // Generare câmpuri editor în panou stâng pe baza slide-ului curent
        function populateEditorInputs() {
            const currentSlide = slides[currentSlideIndex];
            document.getElementById("editorTitle").value = currentSlide.title;
            document.getElementById("editorSubtitle").value = currentSlide.subtitle;

            const inputsContainer = document.getElementById("editorInputs");
            inputsContainer.innerHTML = "";

            currentSlide.items.forEach((item, idx) => {
                const wrapper = document.createElement("div");
                wrapper.className = "flex flex-col space-y-1";
                
                const label = document.createElement("label");
                label.className = "text-[9px] text-slate-500 font-bold uppercase tracking-wider";
                label.innerText = `Subpunctul ${idx + 1}`;

                const input = document.createElement("textarea");
                input.className = "w-full bg-slate-900 border border-slate-800 rounded px-2.5 py-1.5 text-xs text-slate-200 focus:outline-none focus:ring-1 focus:ring-purple-500 resize-none";
                input.rows = 2;
                input.value = item;
                input.oninput = function() {
                    updateSlideItemText(idx, this.value);
                };

                wrapper.appendChild(label);
                wrapper.appendChild(input);
                inputsContainer.appendChild(wrapper);
            });
        }

        // Actualizare live a textelor prin evenimente
        function updateSlideText(key, val) {
            slides[currentSlideIndex][key] = val;
            renderActiveSlide();
            renderThumbnails();
        }

        function updateSlideItemText(idx, val) {
            slides[currentSlideIndex].items[idx] = val;
            renderActiveSlide();
            renderThumbnails();
        }

        // Modificare Font
        function changeFont(fontKey) {
            activeFont = fontKey;
            renderActiveSlide();
        }

        // Modificare Temă
        function changeTheme(themeKey) {
            activeThemeKey = themeKey;
            renderActiveSlide();
            renderThumbnails();
        }

        // Construire navigator cu miniaturi (thumbnails)
        function renderThumbnails() {
            const container = document.getElementById("thumbnailContainer");
            container.innerHTML = "";

            slides.forEach((slide, idx) => {
                const thumb = document.createElement("button");
                thumb.onclick = () => selectSlide(idx);
                thumb.id = `thumb-${idx}`;
                
                const isSelected = idx === currentSlideIndex;
                const palette = themePalettes[activeThemeKey];

                thumb.className = `w-28 aspect-[16/9] shrink-0 rounded-lg border text-left p-2 transition-all duration-200 flex flex-col justify-between overflow-hidden relative ${
                    isSelected ? 'ring-2 ring-purple-500 border-transparent scale-105 shadow-md' : 'border-slate-800 bg-slate-950 hover:border-slate-700'
                }`;

                thumb.style.backgroundColor = isSelected ? palette.bg : '#090d1a';
                thumb.style.color = isSelected ? palette.textColor : '#94a3b8';

                let titlePreview = slide.title.length > 20 ? slide.title.substring(0, 18) + "..." : slide.title;

                thumb.innerHTML = `
                    <span class="text-[8px] font-bold uppercase tracking-wider block opacity-70">${idx + 1}</span>
                    <span class="text-[9px] font-bold line-clamp-2 leading-tight block mt-1" style="color: ${isSelected ? palette.titleColor : '#cbd5e1'}">${titlePreview}</span>
                    <div class="mt-auto h-1 w-6 rounded-full" style="background-color: ${isSelected ? palette.accentColor : '#475569'}"></div>
                `;

                container.appendChild(thumb);
            });
        }

        function updateThumbnailHighlight() {
            slides.forEach((_, idx) => {
                const thumb = document.getElementById(`thumb-${idx}`);
                if (!thumb) return;
                const isSelected = idx === currentSlideIndex;
                const palette = themePalettes[activeThemeKey];

                if (isSelected) {
                    thumb.className = "w-28 aspect-[16/9] shrink-0 rounded-lg border text-left p-2 transition-all duration-200 flex flex-col justify-between overflow-hidden relative ring-2 ring-purple-500 border-transparent scale-105 shadow-md";
                    thumb.style.backgroundColor = palette.bg;
                    thumb.style.color = palette.textColor;
                } else {
                    thumb.className = "w-28 aspect-[16/9] shrink-0 rounded-lg border text-left p-2 transition-all duration-200 flex flex-col justify-between overflow-hidden relative border-slate-800 bg-slate-950 hover:border-slate-700";
                    thumb.style.backgroundColor = '#090d1a';
                    thumb.style.color = '#94a3b8';
                }
            });
        }

        function selectSlide(index) {
            currentSlideIndex = index;
            renderActiveSlide();
            populateEditorInputs();
        }

        function nextSlide() {
            if (currentSlideIndex < slides.length - 1) {
                currentSlideIndex++;
                selectSlide(currentSlideIndex);
            } else if (isPresenting) {
                closePresentation();
            }
        }

        function prevSlide() {
            if (currentSlideIndex > 0) {
                currentSlideIndex--;
                selectSlide(currentSlideIndex);
            }
        }

        // Zoom funcțional pe Canvas
        function zoomCanvas(amount) {
            zoomLevel += amount;
            if (zoomLevel < 60) zoomLevel = 60;
            if (zoomLevel > 140) zoomLevel = 140;
            document.getElementById("zoomLabel").innerText = `${zoomLevel}%`;
            document.getElementById("slideCanvas").style.transform = `scale(${zoomLevel / 100})`;
        }

        function resetZoom() {
            zoomLevel = 100;
            document.getElementById("zoomLabel").innerText = "100%";
            document.getElementById("slideCanvas").style.transform = "scale(1)";
        }

        // Mod Prezentare (Fullscreen)
        function openPresentation() {
            isPresenting = true;
            document.getElementById("presentationOverlay").classList.remove("hidden");
            document.getElementById("presentationOverlay").classList.add("flex");
            renderActiveSlide();
        }

        function closePresentation() {
            isPresenting = false;
            document.getElementById("presentationOverlay").classList.add("hidden");
            document.getElementById("presentationOverlay").classList.remove("flex");
        }

        // Modal de sinteză text
        function toggleSummaryModal(show) {
            const modal = document.getElementById("summaryModal");
            if (show) {
                modal.classList.remove("hidden");
                
                let summaryHTML = "";
                slides.forEach((slide) => {
                    summaryHTML += `
                        <div class="border-b border-slate-800 pb-3 mb-3">
                            <h4 class="font-bold text-purple-400 text-sm">Slide ${slide.id}: ${slide.title}</h4>
                            <p class="text-[11px] text-slate-400 italic mb-2">${slide.subtitle}</p>
                            <ul class="list-disc list-inside space-y-1 text-xs text-slate-300">
                                ${slide.items.map(i => `<li>${i}</li>`).join('')}
                            </ul>
                        </div>
                    `;
                });
                document.getElementById("summaryModalContent").innerHTML = summaryHTML;
            } else {
                modal.classList.add("hidden");
            }
        }

        // Copiere în clipboard utilizând metodă fallback pentru iframe-uri
        function copyToClipboard() {
            let textToCopy = "=== PROIECTUL MEU DESPRE CĂRȚI (PENTRU CANVA) ===\n\n";
            slides.forEach((slide) => {
                textToCopy += `SLIDE ${slide.id}: ${slide.title}\n`;
                textToCopy += `Subtitlu: ${slide.subtitle}\n`;
                textToCopy += `Conținut:\n`;
                slide.items.forEach(i => {
                    textToCopy += `- ${i}\n`;
                });
                textToCopy += "\n-------------------------------------\n\n";
            });

            const tempTextArea = document.createElement('textarea');
            tempTextArea.value = textToCopy;
            document.body.appendChild(tempTextArea);
            tempTextArea.select();
            document.execCommand('copy');
            document.body.removeChild(tempTextArea);

            const btn = document.getElementById("copyBtn");
            const originalText = btn.innerText;
            btn.innerText = "✓ Copiat cu succes!";
            btn.className = "bg-emerald-600 hover:bg-emerald-500 text-white font-semibold text-xs px-4 py-2.5 rounded-xl shadow transition";
            
            setTimeout(() => {
                btn.innerText = originalText;
                btn.className = "bg-purple-600 hover:bg-purple-500 text-white font-semibold text-xs px-4 py-2.5 rounded-xl shadow transition";
            }, 2000);
        }
    </script>
</body>
</html>

```
