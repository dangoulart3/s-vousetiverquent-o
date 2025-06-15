<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SÓ VOU SE TIVER QUENTÃO!</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Google Fonts: Lobster -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Lobster&family=Roboto:wght@400;700&display=swap" rel="stylesheet">

    <style>
        /* Estilo customizado para aplicar a fonte Lobster e um visual retrô */
        body {
            background-color: #FDF4E3; /* Um bege claro que lembra festa junina */
            font-family: 'Roboto', sans-serif;
            color: #4A2E2A; /* Marrom escuro para o texto */
        }
        .font-lobster {
            font-family: 'Lobster', cursive;
        }
        .title-shadow {
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }
        .form-container {
            background-color: rgba(255, 255, 255, 0.7);
            backdrop-filter: blur(5px);
        }
        /* Efeito sutil de bandeirinha */
        .bandeirinha {
            clip-path: polygon(0 0, 100% 0, 100% 100%, 50% 85%, 0 100%);
        }
        /* Estilizando o radio button */
        input[type="radio"]:checked + label {
            transform: scale(1.05);
            box-shadow: 0 0 0 3px #FBBF24; /* Amarelo ao selecionar */
        }
        /* Animação para o botão de loading */
        .animate-spin {
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            from {
                transform: rotate(0deg);
            }
            to {
                transform: rotate(360deg);
            }
        }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center p-4 bg-cover bg-center" style="background-image: url('https://www.transparenttextures.com/patterns/straw-netting.png');">

    <div id="app" class="w-full max-w-2xl mx-auto">

        <!-- Cabeçalho -->
        <header class="text-center p-6 rounded-t-xl bg-amber-500">
            <h1 class="font-lobster text-5xl md:text-6xl text-yellow-300 title-shadow">SÓ VOU SE TIVER QUENTÃO!</h1>
        </header>

        <main class="form-container p-6 md:p-8 rounded-b-xl shadow-2xl">
            <!-- Visão do Convidado (padrão) -->
            <div id="guestView">
                <!-- Descrição do Evento -->
                <div class="text-center mb-8 border-b-2 border-dashed border-amber-700 pb-6">
                    <p class="mb-4 text-lg">Vai ter festa. Vai ter música. Vai ter quentão. Mas pra isso acontecer sem virar bagunça (mentira, vai virar), você precisa preencher esse formulário aqui.</p>
                    <p class="font-bold text-xl text-brown-800">🗓️ 11 de Julho, às 20h</p>
                    <button onclick="openMap()" class="mt-4 inline-flex items-center bg-green-600 text-white font-bold py-2 px-4 rounded-lg shadow-md hover:bg-green-700 transition-transform transform hover:scale-105">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M5.05 4.05a7 7 0 119.9 9.9L10 18.9l-4.95-4.95a7 7 0 010-9.9zM10 11a2 2 0 100-4 2 2 0 000 4z" clip-rule="evenodd" /></svg>
                        Ver Endereço no Mapa
                    </button>
                </div>

                <!-- Formulário de Confirmação -->
                <form id="partyForm">
                    <!-- Campos do formulário... -->
                    <div class="mb-6">
                        <label for="guestName" class="block text-xl font-bold mb-2">Quem é você no arraiá?</label>
                        <p class="text-sm mb-2 opacity-80">Seu nome completo, apelido, nome de casal, nome artístico, tanto faz. Só pra sabermos quem confirmar na porta com a prancheta imaginária.</p>
                        <input type="text" id="guestName" name="guestName" class="w-full p-3 border-2 border-amber-700 rounded-lg focus:outline-none focus:ring-2 focus:ring-amber-500" required>
                    </div>
                    <div class="mb-6">
                        <h3 class="text-xl font-bold mb-2">O que cê vai trazer pra forrar o bucho da galera?</h3>
                        <p class="text-sm mb-4 opacity-80">Aqui a tradição é clara: cada um traz um prato típico. Se vier em dupla romântica ou parceria de crime, um prato já tá ótimo pros dois.</p>
                        <div id="foodList" class="grid grid-cols-2 md:grid-cols-3 gap-3"></div>
                         <p id="foodError" class="text-red-500 text-sm mt-2 hidden">Opa, escolha uma comida pra levar!</p>
                    </div>
                     <div class="mb-8">
                        <label for="musicSuggestion" class="block text-xl font-bold mb-2">Que sons você quer ouvir?</label>
                        <p class="text-sm mb-2 opacity-80">Escolhe uns 3 sons... Forró emo, funk gospel, tudo vale...</p>
                        <input type="text" id="musicSuggestion" name="musicSuggestion" class="w-full p-3 border-2 border-amber-700 rounded-lg focus:outline-none focus:ring-2 focus:ring-amber-500">
                    </div>
                    <p id="formError" class="text-red-600 text-center font-bold my-4 hidden"></p>
                    <button type="submit" class="w-full bg-orange-500 text-white font-bold text-xl py-4 rounded-lg shadow-lg hover:bg-orange-600 transition-all duration-300 flex items-center justify-center disabled:bg-gray-400">
                        <span id="buttonText">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 inline-block mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
                            Confirmar Presença
                        </span>
                    </button>
                </form>

                <!-- Lista de Confirmados -->
                <section id="confirmedGuestsSection" class="mt-12 pt-8 border-t-2 border-dashed border-amber-700">
                    <h2 class="text-2xl font-bold text-center mb-6">Galera que já confirmou!</h2>
                    <div id="confirmedGuestsList" class="space-y-3"></div>
                </section>
            </div>
            
            <!-- Visão do Administrador (inicialmente oculta) -->
            <div id="adminView" class="hidden">
                 <h2 class="text-2xl font-bold text-center mb-6">Gerenciamento de Convidados</h2>
                 <div id="adminGuestList" class="space-y-2">
                     <!-- Lista de administradores será preenchida aqui -->
                 </div>
                 <button id="backToGuestView" class="mt-6 w-full bg-gray-500 text-white font-bold py-2 px-4 rounded-lg hover:bg-gray-600">Voltar para a visão de convidado</button>
            </div>

            <!-- Rodapé com acesso do admin -->
            <footer class="text-center mt-8 pt-4 border-t border-amber-700/50">
                <a href="#" id="adminLoginLink" class="text-sm text-gray-500 hover:underline">Acesso do Organizador</a>
            </footer>
        </main>
    </div>
    
    <!-- Modal de Sucesso -->
    <div id="successModal" class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center hidden z-50 p-4">
        <div class="bg-white rounded-lg p-8 text-center shadow-2xl max-w-sm transform transition-all scale-95 opacity-0" id="modalContent">
            <h2 class="text-2xl font-bold text-green-600 mb-2">Confirmado com Sucesso!</h2>
            <p class="mb-6">Sua presença foi registrada! 🎉</p>
            <a id="whatsappLink" href="#" target="_blank" class="w-full inline-flex items-center justify-center bg-green-500 text-white font-bold py-3 px-4 rounded-lg hover:bg-green-600 transition-colors mb-3">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
                Enviar Confirmação no WhatsApp
            </a>
            <button id="closeModalBtn" class="w-full bg-gray-500 text-white font-bold py-2 px-4 rounded-lg hover:bg-gray-600 transition-colors">Fechar</button>
        </div>
    </div>


    <!-- Firebase -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getFirestore, collection, onSnapshot, addDoc, serverTimestamp, deleteDoc, doc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signInWithCustomToken } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        
        // --- Variáveis Globais ---
        let db; // Instância do Firestore
        const WHATSAPP_NUMBER = "5511964492986";
        const ADMIN_PASSWORD = "quentao2024";
        const foodOptions = [
            'Milho Cozido', 'Canjica', 'Arroz-doce', 'Cuscuz', 'Pamonha', 'Cachorro-quente', 
            'Pastel', 'Caldo Verde', 'Bolo de Fubá', 'Bolo de Milho', 'Paçoca', 
            'Pé de Moleque', 'Maçã do Amor', 'Curau', 'Bolinho Caipira'
        ];

        // --- Funções de Renderização ---
        const renderFoodList = (confirmations = []) => {
            const foodListContainer = document.getElementById('foodList');
            if (!foodListContainer) return;
            foodListContainer.innerHTML = ''; 
            const takenFoods = confirmations.map(c => c.food);

            foodOptions.forEach(food => {
                const isTaken = takenFoods.includes(food);
                const guestWhoTook = isTaken ? confirmations.find(c => c.food === food)?.name : '';
                const foodId = `food-${food.replace(/\s+/g, '-')}`;

                const itemHTML = isTaken ? `
                    <div class="relative p-3 text-center bg-gray-300 text-gray-500 rounded-lg shadow-inner cursor-not-allowed bandeirinha">
                        <p class="font-bold line-through">${food}</p>
                        <p class="text-xs font-semibold">Trazido por:</p>
                        <p class="text-xs font-bold">${guestWhoTook || '...'}</p>
                    </div>
                ` : `
                    <div class="relative">
                        <input type="radio" name="foodChoice" value="${food}" id="${foodId}" class="sr-only peer">
                        <label for="${foodId}" class="block p-4 text-center bg-yellow-200 text-amber-900 font-bold rounded-lg cursor-pointer transition-transform duration-200 hover:bg-yellow-300 peer-checked:bg-amber-500 peer-checked:text-white bandeirinha">
                            ${food}
                        </label>
                    </div>
                `;
                foodListContainer.innerHTML += itemHTML;
            });
        };

        const renderConfirmedGuests = (confirmations = []) => {
            const guestListContainer = document.getElementById('confirmedGuestsList');
            if (!guestListContainer) return;
            if (confirmations.length === 0) {
                guestListContainer.innerHTML = '<p class="text-center opacity-70">Ninguém confirmou ainda. Seja o primeiro!</p>';
                return;
            }
            guestListContainer.innerHTML = '';
            const sortedConfirmations = [...confirmations].sort((a, b) => (b.timestamp?.seconds || 0) - (a.timestamp?.seconds || 0));

            sortedConfirmations.forEach(guest => {
                guestListContainer.innerHTML += `
                    <div class="flex items-center bg-white/60 p-3 rounded-lg shadow">
                        <div class="flex-shrink-0 h-10 w-10 rounded-full bg-orange-400 flex items-center justify-center text-white font-bold text-xl">
                            ${guest.name.charAt(0).toUpperCase()}
                        </div>
                        <div class="ml-4">
                            <p class="font-bold text-lg">${guest.name}</p>
                            <p class="text-sm opacity-80">Vai levar: <strong>${guest.food}</strong></p>
                        </div>
                    </div>
                `;
            });
        };

        const renderAdminList = (confirmations = []) => {
            const adminListContainer = document.getElementById('adminGuestList');
            if (!adminListContainer) return;
            if (confirmations.length === 0) {
                adminListContainer.innerHTML = '<p class="text-center opacity-70">Nenhum convidado confirmado.</p>';
                return;
            }
            adminListContainer.innerHTML = '';
            const sortedConfirmations = [...confirmations].sort((a, b) => (b.timestamp?.seconds || 0) - (a.timestamp?.seconds || 0));

            sortedConfirmations.forEach(guest => {
                adminListContainer.innerHTML += `
                    <div class="flex items-center justify-between bg-white p-3 rounded-lg shadow">
                        <div>
                            <p class="font-bold text-lg">${guest.name}</p>
                            <p class="text-sm">Comida: <strong>${guest.food}</strong></p>
                            <p class="text-xs text-gray-500">Música: ${guest.music || 'N/A'}</p>
                        </div>
                        <button class="delete-btn text-red-500 hover:text-red-700 p-2" data-id="${guest.id}">
                             <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="3 6 5 6 21 6"></polyline><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path><line x1="10" y1="11" x2="10" y2="17"></line><line x1="14" y1="11" x2="14" y2="17"></line></svg>
                        </button>
                    </div>
                `;
            });
        };


        // --- Funções Principais ---
        function setupEventListeners() {
            // Formulário principal
            const partyForm = document.getElementById('partyForm');
            if(partyForm) partyForm.addEventListener('submit', handleFormSubmit);

            // Modal
            const closeModalBtn = document.getElementById('closeModalBtn');
            if(closeModalBtn) closeModalBtn.addEventListener('click', closeModal);

            // Links de Admin
            const adminLoginLink = document.getElementById('adminLoginLink');
            if(adminLoginLink) adminLoginLink.addEventListener('click', showAdminLogin);
            
            const backToGuestView = document.getElementById('backToGuestView');
            if(backToGuestView) backToGuestView.addEventListener('click', () => toggleAdminView(false));
            
            // Delegação de eventos para botões de deletar
            const adminGuestList = document.getElementById('adminGuestList');
            if(adminGuestList) adminGuestList.addEventListener('click', handleDeleteClick);
        }

        async function handleFormSubmit(e) {
            e.preventDefault();
            const submitButton = e.target.querySelector('button[type="submit"]');
            const buttonText = document.getElementById('buttonText');
            const formErrorEl = document.getElementById('formError');
            
            const name = document.getElementById('guestName').value.trim();
            const foodChoice = document.querySelector('input[name="foodChoice"]:checked');
            const music = document.getElementById('musicSuggestion').value.trim();

            formErrorEl.classList.add('hidden');
            if (!name) { alert('Por favor, digite seu nome!'); return; }
            if (!foodChoice) {
                document.getElementById('foodError').classList.remove('hidden');
                setTimeout(() => document.getElementById('foodError').classList.add('hidden'), 3000);
                return;
            }

            submitButton.disabled = true;
            const originalButtonHTML = buttonText.innerHTML;
            buttonText.innerHTML = `<svg class="animate-spin h-5 w-5 -ml-1 mr-3 inline-block" ...></svg>Confirmando...`;

            try {
                const canvasAppId = typeof __app_id !== 'undefined' ? __app_id : 'arraia-form-v2';
                const confirmationsCollection = collection(db, `artifacts/${canvasAppId}/public/data/confirmations`);
                await addDoc(confirmationsCollection, { name, food: foodChoice.value, music, timestamp: serverTimestamp() });
                
                e.target.reset();
                showSuccessModal(name, foodChoice.value);
            } catch (error) {
                console.error("Erro ao confirmar presença: ", error);
                formErrorEl.textContent = 'Ops! Não foi possível salvar. Verifique sua conexão e tente novamente.';
                formErrorEl.classList.remove('hidden');
            } finally {
                submitButton.disabled = false;
                buttonText.innerHTML = originalButtonHTML;
            }
        }
        
        async function handleDeleteClick(e) {
            const deleteButton = e.target.closest('.delete-btn');
            if (!deleteButton) return;

            const docId = deleteButton.dataset.id;
            if (confirm(`Tem certeza que quer remover esta confirmação?`)) {
                try {
                    const canvasAppId = typeof __app_id !== 'undefined' ? __app_id : 'arraia-form-v2';
                    const docRef = doc(db, `artifacts/${canvasAppId}/public/data/confirmations`, docId);
                    await deleteDoc(docRef);
                    console.log("Confirmação removida com sucesso");
                } catch (error) {
                    console.error("Erro ao remover confirmação: ", error);
                    alert("Não foi possível remover a confirmação.");
                }
            }
        }

        function showSuccessModal(name, food) {
            const whatsappLink = document.getElementById('whatsappLink');
            const message = `Opa! Confirmei minha presença no arraiá "Só vou se tiver quentão!".\n\n- Nome: ${name}\n- Vou levar: ${food}\n\nAté lá! 🎉`;
            whatsappLink.href = `https://wa.me/${WHATSAPP_NUMBER}?text=${encodeURIComponent(message)}`;
            
            const successModal = document.getElementById('successModal');
            const modalContent = document.getElementById('modalContent');
            successModal.classList.remove('hidden');
            setTimeout(() => {
                modalContent.classList.remove('scale-95', 'opacity-0');
            }, 10);
        }
        
        function closeModal() {
            const successModal = document.getElementById('successModal');
            const modalContent = document.getElementById('modalContent');
            modalContent.classList.add('scale-95', 'opacity-0');
            setTimeout(() => {
                successModal.classList.add('hidden');
            }, 200);
        }

        function showAdminLogin(e) {
            e.preventDefault();
            const password = prompt("Digite a senha de organizador:");
            if (password === ADMIN_PASSWORD) {
                toggleAdminView(true);
            } else if (password) {
                alert("Senha incorreta!");
            }
        }

        function toggleAdminView(showAdmin) {
            document.getElementById('guestView').classList.toggle('hidden', showAdmin);
            document.getElementById('adminView').classList.toggle('hidden', !showAdmin);
        }
        
        async function initializeAppFlow() {
            renderFoodList();
            renderConfirmedGuests();
            setupEventListeners();

            try {
                const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
                const app = initializeApp(firebaseConfig);
                db = getFirestore(app);
                const auth = getAuth(app);

                onAuthStateChanged(auth, (user) => {
                    if (user) {
                        const canvasAppId = typeof __app_id !== 'undefined' ? __app_id : 'arraia-form-v2';
                        const confirmationsCollection = collection(db, `artifacts/${canvasAppId}/public/data/confirmations`);
                        onSnapshot(confirmationsCollection, (snapshot) => {
                            const confirmations = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                            renderFoodList(confirmations);
                            renderConfirmedGuests(confirmations);
                            renderAdminList(confirmations);
                        });
                    }
                });
                
                const token = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;
                if (token) {
                    await signInWithCustomToken(auth, token);
                } else {
                    await signInAnonymously(auth);
                }
            } catch (error) {
                console.error("Erro Crítico no Firebase:", error);
                document.getElementById('foodList').innerHTML = '<p class="col-span-full text-red-600 font-bold text-center">Erro de conexão.</p>';
            }
        }
        
        window.openMap = () => {
            const address = "Rua Belém do Pará, 367, Recreio Estoril, Atibaia, SP";
            window.open(`https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(address)}`, '_blank');
        };

        initializeAppFlow();

    </script>
</body>
</html>
