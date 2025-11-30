<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ujian PJOK - MTS Assalam</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        .fade-in {
            animation: fadeIn 0.5s ease-in;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 via-green-50 to-cyan-50 min-h-screen">
    
    <!-- Login Page -->
    <div id="loginPage" class="p-4 fade-in">
        <div class="max-w-2xl mx-auto pt-8">
            <div class="bg-white rounded-lg shadow-xl p-8">
                <div class="text-center mb-8">
                    <svg class="w-16 h-16 mx-auto text-blue-600 mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path>
                    </svg>
                    <h1 class="text-3xl font-bold text-gray-800 mb-2">MTS Assalam</h1>
                    <h2 class="text-xl text-gray-600 mb-1">Ujian Semester PJOK</h2>
                    <p class="text-sm text-gray-500">Tahun Ajaran 2024/2025</p>
                </div>

                <div class="space-y-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Nama Lengkap</label>
                        <input type="text" id="studentName" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Masukkan nama lengkap">
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Kelas</label>
                        <select id="studentClass" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            <option value="">Pilih Kelas</option>
                            <option value="7A">7A</option>
                            <option value="7B">7B</option>
                            <option value="7C">7C</option>
                            <option value="8A">8A</option>
                            <option value="8B">8B</option>
                            <option value="8C">8C</option>
                            <option value="9A">9A</option>
                            <option value="9B">9B</option>
                            <option value="9C">9C</option>
                        </select>
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">NIS (Nomor Induk Siswa)</label>
                        <input type="text" id="studentNIS" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Masukkan NIS">
                    </div>

                    <div class="bg-blue-50 border border-blue-200 rounded-lg p-4 mt-6">
                        <h3 class="font-semibold text-blue-900 mb-2">📋 Informasi Ujian:</h3>
                        <ul class="text-sm text-blue-800 space-y-1">
                            <li>• Soal Pilihan Ganda: 30 soal (90 poin)</li>
                            <li>• Soal Isian: 5 soal (10 poin)</li>
                            <li>• Total Nilai: 100 poin</li>
                            <li>• Waktu: 90 menit</li>
                            <li>• 🔀 Soal DIACAK UNIK untuk setiap siswa</li>
                            <li>• Hasil akan dikirim ke email guru</li>
                        </ul>
                    </div>

                    <div class="bg-yellow-50 border border-yellow-300 rounded-lg p-4">
                        <p class="text-sm text-yellow-800">
                            <strong>⚠️ PERHATIAN:</strong> Setiap siswa akan mendapat urutan soal dan opsi jawaban yang BERBEDA. Tidak ada gunanya mencontek!
                        </p>
                    </div>

                    <button onclick="startExam()" class="w-full bg-blue-600 text-white py-3 rounded-lg font-semibold hover:bg-blue-700 transition-colors">
                        🔀 Mulai Ujian PJOK
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Exam Page -->
    <div id="examPage" class="hidden p-4">
        <div class="max-w-4xl mx-auto pt-4">
            <!-- Header Sticky -->
            <div class="bg-white rounded-lg shadow-xl p-6 mb-4 sticky top-4 z-10">
                <div class="flex justify-between items-center">
                    <div>
                        <h2 class="text-xl font-bold text-gray-800" id="examStudentName"></h2>
                        <p class="text-gray-600" id="examStudentInfo"></p>
                        <p class="text-xs text-gray-500 mt-1">Kode Soal: <span id="examCode" class="font-mono font-bold"></span></p>
                    </div>
                    <div class="flex items-center gap-2 bg-red-100 px-4 py-2 rounded-lg">
                        <svg class="w-5 h-5 text-red-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                        </svg>
                        <span class="text-xl font-bold text-red-600" id="timer">90:00</span>
                    </div>
                </div>
            </div>

            <!-- Multiple Choice Section -->
            <div class="bg-white rounded-lg shadow-xl p-8 mb-6">
                <div class="flex items-center gap-3 mb-6">
                    <svg class="w-8 h-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"></path>
                    </svg>
                    <h3 class="text-2xl font-bold text-gray-800">Bagian A: Pilihan Ganda (30 Soal)</h3>
                </div>
                <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-3 mb-4 text-sm text-yellow-800">
                    <strong>🔀 Soal Anda UNIK!</strong> Setiap siswa mendapat urutan soal dan pilihan jawaban yang berbeda
                </div>
                <div id="mcQuestions" class="space-y-6"></div>
            </div>

            <!-- Essay Section -->
            <div class="bg-white rounded-lg shadow-xl p-8">
                <div class="flex items-center gap-3 mb-6">
                    <svg class="w-8 h-8 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path>
                    </svg>
                    <h3 class="text-2xl font-bold text-gray-800">Bagian B: Soal Isian (5 Soal)</h3>
                </div>
                <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-3 mb-4 text-sm text-yellow-800">
                    <strong>🔀 Soal Anda UNIK!</strong> Urutan soal isian juga berbeda untuk setiap siswa
                </div>
                <div id="essayQuestions" class="space-y-6"></div>

                <div class="mt-8 pt-6 border-t border-gray-200 flex justify-between items-center">
                    <div class="text-sm text-gray-600">
                        <p>Pilihan Ganda: <span id="mcProgress">0/30</span></p>
                        <p>Isian: <span id="essayProgress">0/5</span></p>
                    </div>
                    <button onclick="submitExam()" class="bg-blue-600 text-white px-8 py-3 rounded-lg font-semibold hover:bg-blue-700 transition-colors">
                        ✉️ Kirim Jawaban
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Result Page -->
    <div id="resultPage" class="hidden p-4 fade-in">
        <div class="max-w-2xl mx-auto pt-8">
            <div class="bg-white rounded-lg shadow-xl p-8 text-center">
                <svg class="w-20 h-20 mx-auto text-green-600 mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                </svg>
                <h2 class="text-3xl font-bold text-gray-800 mb-4">Ujian Selesai!</h2>
                
                <div class="bg-gradient-to-br from-blue-50 to-green-50 rounded-lg p-6 mb-6">
                    <p class="text-gray-600 mb-2">Nilai Anda:</p>
                    <p class="text-5xl font-bold text-blue-600 mb-4" id="finalScore">0</p>
                    <div class="grid grid-cols-2 gap-4 text-sm">
                        <div class="bg-white rounded p-3">
                            <p class="text-gray-600">Pilihan Ganda</p>
                            <p class="font-bold text-blue-600" id="mcResult">0/30</p>
                        </div>
                        <div class="bg-white rounded p-3">
                            <p class="text-gray-600">Soal Isian</p>
                            <p class="font-bold text-blue-600" id="essayResult">0/5</p>
                        </div>
                    </div>
                    <p class="text-xs text-gray-500 mt-3">Kode Soal: <span id="resultExamCode" class="font-mono font-bold"></span></p>
                </div>

                <div class="text-left bg-green-50 border border-green-200 rounded-lg p-4 mb-6">
                    <p class="text-sm text-green-800">
                        <strong>✉️ Email Terkirim!</strong><br/>
                        Hasil ujian Anda telah dibuka di aplikasi email dan siap dikirim ke:<br/>
                        <strong>olengkluyarkluyur@gmail.com</strong>
                    </p>
                    <p class="text-xs text-green-700 mt-2">
                        Silakan klik "Send" di aplikasi email Anda untuk mengirim hasil.
                    </p>
                </div>

                <button onclick="location.reload()" class="bg-blue-600 text-white px-8 py-3 rounded-lg font-semibold hover:bg-blue-700 transition-colors">
                    Kembali ke Halaman Awal
                </button>
            </div>
        </div>
    </div>

    <script>
        // Data Soal Master
        const masterMCQuestions = [
            { id: 1, question: 'Permainan bola voli dimainkan oleh berapa orang dalam satu tim di lapangan?', options: ['5 orang', '6 orang', '7 orang', '8 orang'], correct: '6 orang' },
            { id: 2, question: 'Tinggi net bola voli putra adalah...', options: ['2,24 meter', '2,43 meter', '2,34 meter', '2,54 meter'], correct: '2,43 meter' },
            { id: 3, question: 'Dalam permainan sepak bola, posisi pemain yang bertugas menjaga gawang disebut...', options: ['Striker', 'Defender', 'Goalkeeper', 'Midfielder'], correct: 'Goalkeeper' },
            { id: 4, question: 'Jumlah pemain dalam satu tim sepak bola adalah...', options: ['9 orang', '10 orang', '11 orang', '12 orang'], correct: '11 orang' },
            { id: 5, question: 'Lama waktu permainan sepak bola dalam satu pertandingan adalah...', options: ['2 x 35 menit', '2 x 40 menit', '2 x 45 menit', '2 x 50 menit'], correct: '2 x 45 menit' },
            { id: 6, question: 'Dalam permainan bola basket, berapa poin yang didapat jika memasukkan bola dari luar garis three point?', options: ['1 poin', '2 poin', '3 poin', '4 poin'], correct: '3 poin' },
            { id: 7, question: 'Jumlah pemain bola basket dalam satu tim di lapangan adalah...', options: ['4 orang', '5 orang', '6 orang', '7 orang'], correct: '5 orang' },
            { id: 8, question: 'Teknik dasar dalam permainan bola basket yang dilakukan dengan memantulkan bola ke lantai disebut...', options: ['Passing', 'Shooting', 'Dribbling', 'Pivot'], correct: 'Dribbling' },
            { id: 9, question: 'Induk organisasi bola voli Indonesia adalah...', options: ['PSSI', 'PBVSI', 'PERBASI', 'PBSI'], correct: 'PBVSI' },
            { id: 10, question: 'Servis dalam permainan bola voli yang dilakukan dengan cara memukul bola sambil melompat disebut...', options: ['Servis bawah', 'Servis atas', 'Servis mengapung', 'Jump service'], correct: 'Jump service' },
            { id: 11, question: 'Teknik dasar lari jarak pendek yang benar saat start adalah...', options: ['Start melayang', 'Start jongkok', 'Start berdiri', 'Start duduk'], correct: 'Start jongkok' },
            { id: 12, question: 'Jarak lari sprint adalah...', options: ['100-400 meter', '800-1500 meter', '3000-5000 meter', '10.000 meter'], correct: '100-400 meter' },
            { id: 13, question: 'Dalam lompat jauh, papan tolakan berjarak dari tempat pendaratan sejauh...', options: ['1 meter', '2 meter', '3 meter', '4 meter'], correct: '1 meter' },
            { id: 14, question: 'Gaya lompat jauh yang paling sederhana adalah...', options: ['Gaya jongkok', 'Gaya menggantung', 'Gaya berjalan di udara', 'Gaya melenting'], correct: 'Gaya jongkok' },
            { id: 15, question: 'Nomor lari estafet yang diperlombakan dalam atletik adalah...', options: ['4 x 50 meter', '4 x 100 meter', '4 x 200 meter', '4 x 500 meter'], correct: '4 x 100 meter' },
            { id: 16, question: 'Organisasi bulu tangkis Indonesia adalah...', options: ['PSSI', 'PBSI', 'PERBASI', 'PBVSI'], correct: 'PBSI' },
            { id: 17, question: 'Dalam permainan bulu tangkis, jika skor 20-20, maka permainan akan berakhir saat salah satu pemain unggul...', options: ['1 poin', '2 poin', '3 poin', '5 poin'], correct: '2 poin' },
            { id: 18, question: 'Pukulan permulaan dalam permainan bulu tangkis disebut...', options: ['Smash', 'Service', 'Dropshot', 'Lob'], correct: 'Service' },
            { id: 19, question: 'Senam lantai yang dilakukan dengan gerakan berguling ke depan disebut...', options: ['Roll depan', 'Roll belakang', 'Headstand', 'Handstand'], correct: 'Roll depan' },
            { id: 20, question: 'Sikap permulaan saat melakukan roll depan adalah...', options: ['Berdiri tegak', 'Jongkok', 'Tidur telentang', 'Tidur telungkup'], correct: 'Jongkok' },
            { id: 21, question: 'Gerakan senam yang dilakukan dengan bertumpu pada kedua tangan dan kaki lurus ke atas disebut...', options: ['Roll depan', 'Headstand', 'Handstand', 'Kayang'], correct: 'Handstand' },
            { id: 22, question: 'Renang gaya dada disebut juga dengan gaya...', options: ['Kupu-kupu', 'Bebas', 'Katak', 'Punggung'], correct: 'Katak' },
            { id: 23, question: 'Posisi badan saat melakukan renang gaya bebas adalah...', options: ['Telentang', 'Telungkup', 'Miring', 'Tegak'], correct: 'Telungkup' },
            { id: 24, question: 'Gerakan kaki renang gaya bebas adalah...', options: ['Naik turun bergantian', 'Melingkar', 'Menggunting', 'Diam'], correct: 'Naik turun bergantian' },
            { id: 25, question: 'Dalam permainan tenis meja, raket terbuat dari bahan...', options: ['Kayu dan karet', 'Plastik', 'Alumunium', 'Besi'], correct: 'Kayu dan karet' },
            { id: 26, question: 'Panjang meja tenis meja adalah...', options: ['2,54 meter', '2,64 meter', '2,74 meter', '2,84 meter'], correct: '2,74 meter' },
            { id: 27, question: 'Gerakan pemanasan sebelum olahraga berguna untuk...', options: ['Menambah berat badan', 'Mencegah cedera', 'Menurunkan stamina', 'Memperlemah otot'], correct: 'Mencegah cedera' },
            { id: 28, question: 'Latihan untuk meningkatkan daya tahan tubuh adalah...', options: ['Lari sprint', 'Lari jarak jauh', 'Angkat beban', 'Senam lantai'], correct: 'Lari jarak jauh' },
            { id: 29, question: 'Push up adalah latihan untuk melatih kekuatan otot...', options: ['Kaki', 'Lengan dan dada', 'Perut', 'Punggung'], correct: 'Lengan dan dada' },
            { id: 30, question: 'Sikap awal dalam melakukan push up adalah...', options: ['Berdiri', 'Duduk', 'Telungkup', 'Telentang'], correct: 'Telungkup' }
        ];

        const masterEssayQuestions = [
            { id: 'essay1', question: 'Sebutkan 3 manfaat melakukan olahraga secara teratur!' },
            { id: 'essay2', question: 'Jelaskan teknik dasar passing bawah dalam permainan bola voli!' },
            { id: 'essay3', question: 'Sebutkan 4 jenis gaya renang yang diperlombakan!' },
            { id: 'essay4', question: 'Apa yang dimaksud dengan fair play dalam olahraga?' },
            { id: 'essay5', question: 'Sebutkan 3 peralatan yang dibutuhkan dalam permainan bola basket!' }
        ];

        let studentData = {};
        let mcAnswers = {};
        let essayAnswers = {};
        let timeLeft = 5400; // 90 menit
        let timerInterval;
        let shuffledMCQuestions = [];
        let shuffledEssayQuestions = [];
        let examCode = '';

        // Fungsi untuk generate kode ujian unik berdasarkan NIS dan waktu
        function generateExamCode(nis) {
            const timestamp = Date.now();
            const combined = nis + timestamp.toString();
            let hash = 0;
            for (let i = 0; i < combined.length; i++) {
                hash = ((hash << 5) - hash) + combined.charCodeAt(i);
                hash = hash & hash;
            }
            return Math.abs(hash).toString(36).toUpperCase().substring(0, 8);
        }

        // Fungsi untuk shuffle array berdasarkan seed unik (NIS + waktu)
        function uniqueShuffle(array, seed) {
            let shuffled = [...array];
            
            // Generate random seed dari string
            let randomSeed = 0;
            for (let i = 0; i < seed.length; i++) {
                randomSeed = randomSeed * 31 + seed.charCodeAt(i);
            }
            
            const seededRandom = () => {
                randomSeed = (randomSeed * 9301 + 49297) % 233280;
                return randomSeed / 233280;
            };
            
            // Fisher-Yates shuffle
            for (let i = shuffled.length - 1; i > 0; i--) {
                const j = Math.floor(seededRandom() * (i + 1));
                [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
            }
            
            return shuffled;
        }

        // Fungsi untuk shuffle opsi jawaban
        function shuffleOptions(options, seed) {
            let shuffled = [...options];
            let randomSeed = seed;
            
            const seededRandom = () => {
                randomSeed = (randomSeed * 9301 + 49297) % 233280;
                return randomSeed / 233280;
            };
            
            for (let i = shuffled.length - 1; i > 0; i--) {
                const j = Math.floor(seededRandom() * (i + 1));
                [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
            }
            
            return shuffled;
        }

        function startExam() {
            const name = document.getElementById('studentName').value.trim();
            const cls = document.getElementById('studentClass').value;
            const nis = document.getElementById('studentNIS').value.trim();

            if (!name || !cls || !nis) {
                alert('Mohon lengkapi semua data!');
                return;
            }

            studentData = { name, class: cls, nis };
            
            // Generate kode ujian unik untuk setiap siswa
            examCode = generateExamCode(nis);
            const uniqueSeed = nis + examCode;

            // Acak soal berdasarkan 
