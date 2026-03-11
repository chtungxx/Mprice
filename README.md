[史迪仔幫你格價.html](https://github.com/user-attachments/files/25898078/default.html)
<!DOCTYPE html>
<html lang="zh-HK">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="M巾格價">
    <title>衛生巾格價神器 - 史迪仔版</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* 輕柔的字體與全局設定 */
        body { 
            /* 藍天白雲海邊的漸層背景 */
            background: linear-gradient(135deg, #e0f2fe 0%, #f0f9ff 50%, #cffafe 100%);
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; 
            -webkit-tap-highlight-color: transparent; 
            color: #334155;
        }
        /* 隱藏數字輸入框箭頭 */
        input[type=number]::-webkit-inner-spin-button, input[type=number]::-webkit-outer-spin-button { -webkit-appearance: none; margin: 0; }
        
        /* 動畫 */
        .modal-enter { animation: fadeIn 0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
        .modal-exit { animation: fadeOut 0.3s ease-in forwards; }
        .bounce-in { animation: bounceIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px) scale(0.98); } to { opacity: 1; transform: translateY(0) scale(1); } }
        @keyframes fadeOut { from { opacity: 1; transform: translateY(0) scale(1); } to { opacity: 0; transform: translateY(10px) scale(0.98); } }
        @keyframes bounceIn { 
            0% { transform: scale(0.8); opacity: 0; } 
            50% { transform: scale(1.05); opacity: 1; } 
            100% { transform: scale(1); opacity: 1; } 
        }
        
        /* 史迪仔浮動效果 */
        .float-anim { animation: float 3s ease-in-out infinite; }
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-5px); }
            100% { transform: translateY(0px); }
        }

        /* 語錄框的小尾巴 */
        .speech-bubble::after {
            content: '';
            position: absolute;
            left: -10px;
            top: 50%;
            transform: translateY(-50%);
            border-width: 10px 15px 10px 0;
            border-style: solid;
            border-color: transparent white transparent transparent;
        }

        /* 自訂滾動條 */
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #bae6fd; border-radius: 10px; }
        ::-webkit-scrollbar-thumb:hover { background: #7dd3fc; }
    </style>
</head>
<body class="min-h-screen p-4 flex justify-center items-start pt-4 md:pt-10 pb-10">
    
    <!-- 加上波浪裝飾的半透明主容器 (Glassmorphism) -->
    <div class="bg-white/80 backdrop-blur-md rounded-[2rem] shadow-[0_8px_30px_rgb(56,189,248,0.15)] w-full max-w-md overflow-hidden border border-white/60 relative mt-8">
        
        <!-- 頂部標題列 (Stitch 藍色調) -->
        <div class="bg-blue-500/90 text-white text-center py-5 px-4 shadow-sm relative border-b border-blue-400/50">
            <!-- 裝飾用小元素 -->
            <div class="absolute top-2 left-3 opacity-20 text-2xl">🌺</div>
            <div class="absolute bottom-1 right-12 opacity-20 text-3xl text-sky-200"><i class="fa-solid fa-water"></i></div>
            
            <h1 class="text-2xl font-extrabold tracking-wider flex items-center justify-center">
                <i class="fa-solid fa-paw mr-2 text-pink-300 text-xl"></i> M巾格價神器
            </h1>
            <p class="text-blue-100 text-sm mt-1 font-medium tracking-wide">精打細算 🌊 唔做水魚</p>
            
            <!-- 加入了 z-20 確保按鈕一定可以撳到 -->
            <button id="open-db-btn" class="absolute top-4 right-4 z-20 bg-white/20 hover:bg-white/30 backdrop-blur-sm p-2.5 rounded-2xl transition-all shadow-sm" title="我的底價庫">
                <i class="fa-solid fa-book-bookmark text-white"></i>
            </button>
        </div>

        <!-- 史迪仔小助手對話區塊 -->
        <div class="px-6 pt-5 pb-2 flex items-center">
            <!-- 史迪仔插圖 (加入防錯設計，如果圖片未準備好會顯示提示) -->
            <div class="w-24 h-24 mr-4 flex-shrink-0 float-anim relative overflow-hidden rounded-2xl shadow-md border-2 border-white bg-blue-50 flex flex-col justify-center items-center">
                <!-- 真正的圖片 (src 必須對應你放落 Koder 嘅檔案名) -->
                <img src="IMG_0351.jpeg" alt="史迪仔" class="w-full h-full object-cover object-center scale-110 absolute inset-0 z-10" onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';">
                
                <!-- 備用顯示 (當圖片找不到時顯示，方便你除錯) -->
                <div class="hidden flex-col items-center justify-center z-0 w-full h-full bg-sky-50">
                    <i class="fa-solid fa-image text-blue-300 text-2xl"></i>
                    <p class="text-[10px] text-blue-400 mt-1 leading-tight text-center font-bold">請將照片<br>放同一個Folder</p>
                </div>
            </div>
            
            <!-- 對話框 -->
            <div class="relative bg-white rounded-2xl p-3 shadow-md border border-sky-100 flex-1 speech-bubble">
                <p id="stitch-message" class="text-sm font-bold text-blue-800 m-0">史迪仔幫你計！Aloha！🌺</p>
            </div>
        </div>

        <!-- 主要表單內容 -->
        <div class="p-6 pt-2 space-y-4">
            <div>
                <label class="block text-slate-600 font-bold mb-2 text-sm ml-1" for="size-select">
                    <i class="fa-solid fa-ruler text-sky-400 mr-1.5"></i> 1. 選擇尺寸
                </label>
                <div class="relative">
                    <select id="size-select" class="block appearance-none w-full bg-sky-50/50 border border-sky-100 text-slate-700 py-3.5 px-4 pr-8 rounded-2xl leading-tight focus:outline-none focus:bg-white/90 focus:border-blue-400 focus:ring-2 focus:ring-blue-100 transition-all cursor-pointer text-lg font-medium shadow-sm">
                        <option value="" disabled selected>請選擇尺寸...</option>
                        <option value="25cm">25cm</option>
                        <option value="27cm (液態)">27cm (液態)</option>
                        <option value="28cm">28cm</option>
                        <option value="30cm (** best)">30cm (** best)</option>
                        <option value="35cm">35cm</option>
                        <option value="41cm">41cm</option>
                        <option value="安睡褲">安睡褲</option>
                        <option value="other">其他 (手動輸入)</option>
                    </select>
                    <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-4 text-sky-500"><i class="fa-solid fa-chevron-down"></i></div>
                </div>
            </div>

            <div id="custom-size-container" class="hidden">
                <input type="text" id="custom-size-input" placeholder="請輸入尺寸 (例如: 19cm)" class="block w-full bg-white/60 border border-sky-100 text-slate-700 py-3 px-4 rounded-2xl leading-tight focus:outline-none focus:bg-white focus:border-blue-400 focus:ring-2 focus:ring-blue-100 transition-all shadow-inner">
            </div>

            <div class="flex space-x-4">
                <div class="flex-1">
                    <label class="block text-slate-600 font-bold mb-2 text-sm ml-1" for="price-input">
                        <i class="fa-solid fa-sack-dollar text-sky-400 mr-1.5"></i> 2. 總金額 ($)
                    </label>
                    <input type="number" id="price-input" placeholder="例如: 35.9" step="0.1" min="0" class="block w-full bg-sky-50/50 border border-sky-100 text-slate-700 py-3.5 px-4 rounded-2xl leading-tight focus:outline-none focus:bg-white/90 focus:border-blue-400 focus:ring-2 focus:ring-blue-100 transition-all text-lg font-medium shadow-sm">
                </div>
                <div class="flex-1">
                    <label class="block text-slate-600 font-bold mb-2 text-sm ml-1" for="quantity-input">
                        <i class="fa-solid fa-layer-group text-sky-400 mr-1.5"></i> 3. 幾多塊？
                    </label>
                    <input type="number" id="quantity-input" placeholder="例如: 36" step="1" min="1" class="block w-full bg-sky-50/50 border border-sky-100 text-slate-700 py-3.5 px-4 rounded-2xl leading-tight focus:outline-none focus:bg-white/90 focus:border-blue-400 focus:ring-2 focus:ring-blue-100 transition-all text-lg font-medium shadow-sm">
                </div>
            </div>

            <button id="calculate-btn" class="w-full bg-blue-500 hover:bg-blue-600 text-white font-bold py-4 px-4 rounded-2xl shadow-[0_4px_15px_rgb(59,130,246,0.3)] transition-all active:scale-95 active:shadow-inner text-lg mt-2 flex justify-center items-center group">
                <i class="fa-solid fa-star text-pink-300 mr-2 group-hover:rotate-180 transition-transform duration-500"></i> 即刻幫我算！
            </button>
        </div>

        <!-- 結果顯示區 -->
        <div id="result-section" class="hidden bg-white/50 backdrop-blur-sm border-t border-sky-100/50 p-6 text-center rounded-b-[2rem]">
            <h3 class="text-sm text-sky-600 font-bold uppercase tracking-widest mb-1 flex items-center justify-center">
                <i class="fa-solid fa-water text-sky-300 mr-2"></i> 計算結果
            </h3>
            <div class="text-4xl font-extrabold text-blue-900 mb-2 drop-shadow-sm">
                $<span id="unit-price-display">0.00</span> <span class="text-lg text-slate-500 font-medium">/ 片</span>
            </div>
            
            <div id="verdict-box" class="mt-4 p-5 rounded-2xl border-2 font-bold text-lg flex flex-col items-center justify-center shadow-sm relative overflow-hidden">
                <div id="verdict-icon" class="text-4xl mb-2 z-10"></div>
                <div id="verdict-text" class="z-10"></div>
                <div id="reference-price-text" class="text-xs font-medium mt-2 opacity-80 z-10"></div>
                <div id="db-remarks-text" class="text-xs font-normal mt-1 opacity-70 italic hidden z-10"></div>
            </div>

            <div id="update-db-container" class="mt-5 hidden">
                <div class="mb-3">
                    <input type="text" id="new-remark-input" placeholder="🌺 紀錄備註 (例如: 買一送一)" class="block w-full bg-white/80 border border-sky-200 text-slate-700 py-2.5 px-4 rounded-xl text-sm focus:outline-none focus:border-blue-400 focus:ring-2 focus:ring-blue-100 shadow-inner">
                </div>
                <button id="update-db-btn" class="w-full bg-sky-500 hover:bg-sky-600 text-white font-bold py-3.5 px-4 rounded-xl shadow-md shadow-sky-200 transition-all active:scale-95 text-sm flex justify-center items-center">
                    <i class="fa-solid fa-box-archive mr-2"></i> <span id="update-db-text">更新底價紀錄</span>
                </button>
            </div>
        </div>
    </div>

    <!-- 資料庫管理 Modal -->
    <div id="db-modal" class="fixed inset-0 bg-slate-900/40 backdrop-blur-sm flex items-center justify-center hidden z-50 px-4">
        <div class="bg-white/95 rounded-[2rem] shadow-2xl w-full max-w-md max-h-[85vh] flex flex-col overflow-hidden border border-white">
            
            <div class="bg-gradient-to-r from-blue-50 to-sky-50 py-5 px-6 border-b border-sky-100 flex justify-between items-center relative">
                <h2 class="text-xl font-extrabold text-blue-900 flex items-center">
                    <i class="fa-solid fa-book-open text-blue-400 mr-2"></i> 我的底價庫
                </h2>
                <button id="close-db-btn" class="text-sky-400 hover:text-blue-600 bg-white rounded-full w-8 h-8 flex items-center justify-center shadow-sm transition-colors"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div class="p-4 overflow-y-auto flex-1 bg-slate-50/50">
                <p class="text-xs text-slate-500 mb-4 text-center font-medium bg-white/60 py-2 rounded-lg border border-sky-50">
                    <i class="fa-solid fa-lightbulb text-yellow-400 mr-1"></i> 輸入總額與數量，系統自動計單價！
                </p>
                <div id="db-list" class="space-y-4"></div>
            </div>
            
            <div class="bg-white/90 py-4 px-5 border-t border-sky-100 flex justify-between items-center">
                <button id="reset-db-btn" class="text-xs text-slate-400 hover:text-red-400 font-medium transition-colors"><i class="fa-solid fa-rotate-left mr-1"></i>重置</button>
                <button id="save-db-modal-btn" class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-2.5 px-6 rounded-xl shadow-md shadow-blue-200 transition-all active:scale-95 flex items-center">
                    <i class="fa-solid fa-check mr-2"></i> 儲存修改
                </button>
            </div>
        </div>
    </div>

    <!-- 邏輯腳本 -->
    <script>
        const defaultDB = {
            "25cm": { price: 35.9/36, totalPrice: 35.9, quantity: 36, remarks: "laurier 買一送一" },
            "27cm (液態)": { price: 12.9/6, totalPrice: 12.9, quantity: 6, remarks: "Whisper 試用裝" },
            "28cm": { price: 24.0/20, totalPrice: 24.0, quantity: 20, remarks: "kotex" },
            "30cm (** best)": { price: 31.9/28, totalPrice: 31.9, quantity: 28, remarks: "laurier" },
            "35cm": { price: 23.8/12, totalPrice: 23.8, quantity: 12, remarks: "lauria" },
            "41cm": { price: 36.0/16, totalPrice: 36.0, quantity: 16, remarks: "kotex 孖裝" },
            "安睡褲": { price: 19.0/4, totalPrice: 19.0, quantity: 4, remarks: "Whisper 四片裝" }
        };

        let currentDB = {};

        const sizeSelect = document.getElementById('size-select');
        const customSizeContainer = document.getElementById('custom-size-container');
        const customSizeInput = document.getElementById('custom-size-input');
        const priceInput = document.getElementById('price-input');
        const quantityInput = document.getElementById('quantity-input');
        const calculateBtn = document.getElementById('calculate-btn');
        const resultSection = document.getElementById('result-section');
        const unitPriceDisplay = document.getElementById('unit-price-display');
        
        const verdictBox = document.getElementById('verdict-box');
        const verdictIcon = document.getElementById('verdict-icon');
        const verdictText = document.getElementById('verdict-text');
        const referencePriceText = document.getElementById('reference-price-text');
        const dbRemarksText = document.getElementById('db-remarks-text');
        
        const updateDbContainer = document.getElementById('update-db-container');
        const updateDbBtn = document.getElementById('update-db-btn');
        const updateDbText = document.getElementById('update-db-text');
        const newRemarkInput = document.getElementById('new-remark-input');

        const dbModal = document.getElementById('db-modal');
        const openDbBtn = document.getElementById('open-db-btn');
        const closeDbBtn = document.getElementById('close-db-btn');
        const dbList = document.getElementById('db-list');
        const saveDbModalBtn = document.getElementById('save-db-modal-btn');
        const resetDbBtn = document.getElementById('reset-db-btn');
        
        const stitchMessage = document.getElementById('stitch-message');

        function loadDatabase() {
            try {
                const savedData = localStorage.getItem('mPadTargetPricesV3');
                if (savedData) {
                    currentDB = JSON.parse(savedData);
                } else {
                    const oldData = localStorage.getItem('mPadTargetPricesV2');
                    if (oldData) {
                        const oldDB = JSON.parse(oldData);
                        currentDB = {};
                        for (const key in oldDB) {
                            currentDB[key] = {
                                price: oldDB[key].price || 0,
                                totalPrice: oldDB[key].totalPrice || oldDB[key].price || 0,
                                quantity: oldDB[key].quantity || 1,
                                remarks: oldDB[key].remarks || ""
                            };
                        }
                    } else {
                        currentDB = JSON.parse(JSON.stringify(defaultDB));
                    }
                }
            } catch (e) {
                currentDB = JSON.parse(JSON.stringify(defaultDB));
            }

            // 【終極防錯機制】：確保所有讀出來嘅資料都係正確 Object 格式
            for (let key in currentDB) {
                if (typeof currentDB[key] !== 'object' || currentDB[key] === null) {
                    let val = parseFloat(currentDB[key]) || 0;
                    currentDB[key] = { price: val, totalPrice: val, quantity: 1, remarks: "" };
                }
            }
        }

        function saveDatabase() {
            localStorage.setItem('mPadTargetPricesV3', JSON.stringify(currentDB));
        }

        loadDatabase();

        sizeSelect.addEventListener('change', function() {
            if (this.value === 'other') {
                customSizeContainer.classList.remove('hidden');
                customSizeInput.focus();
            } else {
                customSizeContainer.classList.add('hidden');
            }
            resultSection.classList.add('hidden');
            
            stitchMessage.textContent = '史迪仔準備好啦！快啲入錢同數量！';
            stitchMessage.parentElement.classList.remove('bounce-in');
            void stitchMessage.parentElement.offsetWidth; 
            stitchMessage.parentElement.classList.add('bounce-in');
        });

        let lastCalculatedSize = "";
        let lastCalculatedPrice = 0;
        let lastCalculatedTotalPrice = 0;
        let lastCalculatedQuantity = 0;

        calculateBtn.addEventListener('click', function() {
            let selectedSize = sizeSelect.value;
            if (selectedSize === 'other') selectedSize = customSizeInput.value.trim();
            const totalPrice = parseFloat(priceInput.value);
            const quantity = parseInt(quantityInput.value);

            if (!selectedSize) {
                stitchMessage.textContent = '喂喂！你未揀尺寸喎！😤';
                return alert('請選擇或輸入尺寸！');
            }
            if (isNaN(totalPrice) || totalPrice <= 0) {
                stitchMessage.textContent = '金額要入數字呀！💸';
                return alert('請輸入有效的總金額！');
            }
            if (isNaN(quantity) || quantity <= 0) {
                stitchMessage.textContent = '到底有幾多塊呀？🤔';
                return alert('請輸入有效的片數！');
            }

            const unitPrice = totalPrice / quantity;
            unitPriceDisplay.textContent = unitPrice.toFixed(2);
            
            lastCalculatedSize = selectedSize;
            lastCalculatedPrice = unitPrice;
            lastCalculatedTotalPrice = totalPrice;
            lastCalculatedQuantity = quantity;

            evaluatePrice(selectedSize, unitPrice);
            resultSection.classList.remove('hidden');
            resultSection.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
            
            stitchMessage.parentElement.classList.remove('bounce-in');
            void stitchMessage.parentElement.offsetWidth;
            stitchMessage.parentElement.classList.add('bounce-in');
        });

        function evaluatePrice(size, calculatedUnitPrice) {
            verdictBox.className = 'mt-4 p-5 rounded-2xl border-2 font-bold text-lg flex flex-col items-center justify-center transition-all duration-300 relative overflow-hidden';
            updateDbContainer.classList.add('hidden');
            dbRemarksText.classList.add('hidden');
            newRemarkInput.value = ""; 
            
            if (currentDB.hasOwnProperty(size)) {
                const targetData = currentDB[size];
                const targetPrice = targetData.price || 0;
                
                if (targetData.remarks) {
                    dbRemarksText.textContent = `📝 紀錄備註: ${targetData.remarks}`;
                    dbRemarksText.classList.remove('hidden');
                }
                
                if (calculatedUnitPrice < targetPrice - 0.005) {
                    verdictBox.classList.add('bg-amber-50', 'border-amber-300', 'text-amber-700');
                    verdictIcon.innerHTML = '<i class="fa-solid fa-trophy text-amber-400"></i>';
                    verdictText.textContent = '嘩！破底價！平過以前！';
                    referencePriceText.textContent = `(舊底價：$${targetPrice.toFixed(2)}/片)`;
                    updateDbContainer.classList.remove('hidden');
                    updateDbText.textContent = `將 $${calculatedUnitPrice.toFixed(2)} 設為新底價`;
                    
                    stitchMessage.textContent = '嘩！平到笑！掃晒佢返屋企！😍🏄‍♂️';
                    stitchMessage.className = 'text-sm font-bold text-amber-600 m-0';
                    
                } else if (Math.abs(calculatedUnitPrice - targetPrice) <= 0.005) {
                    verdictBox.classList.add('bg-teal-50', 'border-teal-300', 'text-teal-700');
                    verdictIcon.innerHTML = '<i class="fa-solid fa-face-grin-stars text-teal-500"></i>';
                    verdictText.textContent = '抵買！去到你的入貨底線！';
                    referencePriceText.textContent = `(目標價：$${targetPrice.toFixed(2)}/片)`;
                    
                    stitchMessage.textContent = '抵呀！可以入貨啦！👍✨';
                    stitchMessage.className = 'text-sm font-bold text-teal-600 m-0';
                    
                } else {
                    verdictBox.classList.add('bg-rose-50', 'border-rose-300', 'text-rose-600');
                    verdictIcon.innerHTML = '<i class="fa-solid fa-hand-holding-dollar text-rose-400"></i>';
                    verdictText.textContent = '較平時貴，建議再格價！';
                    referencePriceText.textContent = `(你的入貨底線：$${targetPrice.toFixed(2)}/片)`;
                    
                    stitchMessage.textContent = '唔好買！貴到離譜！當你水魚咩！😤🐟';
                    stitchMessage.className = 'text-sm font-bold text-rose-600 m-0';
                }
            } else {
                verdictBox.classList.add('bg-sky-50', 'border-sky-300', 'text-sky-700');
                verdictIcon.innerHTML = '<i class="fa-solid fa-circle-info text-sky-400"></i>';
                verdictText.textContent = '呢款尺寸暫時未有底價紀錄～';
                referencePriceText.textContent = '你可以儲存今次價錢作為未來參考！';
                updateDbContainer.classList.remove('hidden');
                updateDbText.textContent = `新增 $${calculatedUnitPrice.toFixed(2)} 為底價`;
                
                stitchMessage.textContent = '咦？呢隻未見過喎？幫你記低佢先！👽📝';
                stitchMessage.className = 'text-sm font-bold text-blue-800 m-0';
            }
        }

        updateDbBtn.addEventListener('click', function() {
            const remark = newRemarkInput.value.trim();
            currentDB[lastCalculatedSize] = {
                price: lastCalculatedPrice,
                totalPrice: lastCalculatedTotalPrice,
                quantity: lastCalculatedQuantity,
                remarks: remark
            };
            saveDatabase();
            
            const originalHTML = this.innerHTML;
            this.innerHTML = '<i class="fa-solid fa-check mr-2"></i> 史迪仔幫你記低咗啦！';
            this.classList.replace('bg-sky-500', 'bg-slate-400');
            this.classList.replace('hover:bg-sky-600', 'hover:bg-slate-500');
            this.disabled = true;
            
            setTimeout(() => {
                evaluatePrice(lastCalculatedSize, lastCalculatedPrice);
                this.innerHTML = originalHTML;
                this.classList.replace('bg-slate-400', 'bg-sky-500');
                this.classList.replace('hover:bg-slate-500', 'hover:bg-sky-600');
                this.disabled = false;
            }, 1500);
        });

        // ==========================================
        // Modal 渲染 (加入防錯處理)
        // ==========================================
        function renderDbList() {
            dbList.innerHTML = '';
            const sizes = Object.keys(currentDB);
            
            if (sizes.length === 0) {
                dbList.innerHTML = '<p class="text-center text-slate-400 py-8"><i class="fa-solid fa-box-open text-2xl mb-2 block opacity-50"></i>暫無紀錄</p>';
                return;
            }

            sizes.sort((a, b) => {
                const numA = parseInt(a);
                const numB = parseInt(b);
                if (!isNaN(numA) && !isNaN(numB)) return numA - numB;
                return a.localeCompare(b);
            });

            sizes.forEach((size, index) => {
                let data = currentDB[size];
                
                // 再一次保護，防止因為舊資料導致畫面崩潰
                if (typeof data !== 'object' || data === null) {
                    let val = parseFloat(data) || 0;
                    data = { price: val, totalPrice: val, quantity: 1, remarks: "" };
                    currentDB[size] = data; // 修復
                }

                const price = (data.price || 0).toFixed(2);
                const totalPrice = data.totalPrice !== undefined ? data.totalPrice : (data.price || 0);
                const quantity = data.quantity !== undefined ? data.quantity : 1;
                const remarks = data.remarks || '';
                
                const item = document.createElement('div');
                item.className = 'bg-white p-4 rounded-2xl border border-sky-100 shadow-sm flex flex-col space-y-3 hover:shadow-md transition-shadow';
                item.innerHTML = `
                    <div class="flex items-center justify-between border-b border-slate-50 pb-2">
                        <div class="font-bold text-slate-700 text-lg flex items-center">
                            <span class="w-2 h-2 rounded-full bg-blue-400 mr-2"></span>${size}
                        </div>
                        <div class="text-blue-500 font-extrabold text-lg db-display-unit" id="unit-display-${index}">$${price}/片</div>
                    </div>
                    
                    <div class="flex items-center space-x-2 text-sm">
                        <span class="text-slate-500 font-medium">總額$</span>
                        <input type="number" step="0.1" min="0" data-size="${size}" data-index="${index}" value="${totalPrice}" class="db-edit-total flex-1 min-w-0 bg-slate-50 border border-slate-200 rounded-lg px-2 py-1.5 focus:outline-none focus:border-blue-400 focus:ring-1 focus:ring-blue-400 text-slate-700 transition-colors">
                        
                        <span class="text-slate-400">/</span>
                        
                        <input type="number" step="1" min="1" data-size="${size}" data-index="${index}" value="${quantity}" class="db-edit-qty w-16 bg-slate-50 border border-slate-200 rounded-lg px-2 py-1.5 focus:outline-none focus:border-blue-400 focus:ring-1 focus:ring-blue-400 text-center text-slate-700 transition-colors">
                        <span class="text-slate-500 font-medium">塊</span>
                        
                        <button class="delete-db-btn text-slate-300 hover:text-rose-500 ml-1 p-2 transition-colors rounded-lg hover:bg-rose-50" data-size="${size}" title="刪除此紀錄">
                            <i class="fa-solid fa-trash-can"></i>
                        </button>
                    </div>

                    <div>
                        <input type="text" data-size="${size}" value="${remarks}" placeholder="🌺 加入備註 (例如: 品牌/優惠)" class="db-edit-remark w-full text-sm bg-slate-50/50 border border-slate-200 rounded-lg px-3 py-2 text-slate-600 focus:outline-none focus:border-blue-400 focus:ring-1 focus:ring-blue-400 transition-colors">
                    </div>
                `;
                
                const totalInput = item.querySelector('.db-edit-total');
                const qtyInput = item.querySelector('.db-edit-qty');
                const unitDisplay = item.querySelector('.db-display-unit');
                
                const calculateLivePrice = () => {
                    const t = parseFloat(totalInput.value);
                    const q = parseInt(qtyInput.value);
                    if (!isNaN(t) && !isNaN(q) && q > 0) {
                        unitDisplay.textContent = `$${(t / q).toFixed(2)}/片`;
                    } else {
                        unitDisplay.textContent = '$-.--/片';
                    }
                };

                totalInput.addEventListener('input', calculateLivePrice);
                qtyInput.addEventListener('input', calculateLivePrice);

                dbList.appendChild(item);
            });

            document.querySelectorAll('.delete-db-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const sizeToDelete = this.getAttribute('data-size');
                    if (confirm(`確定要刪除 ${sizeToDelete} 的紀錄嗎？`)) {
                        delete currentDB[sizeToDelete];
                        saveDatabase(); // 立即儲存
                        renderDbList(); 
                    }
                });
            });
        }

        openDbBtn.addEventListener('click', () => {
            renderDbList();
            dbModal.classList.remove('hidden');
            dbModal.classList.remove('modal-exit');
            dbModal.classList.add('modal-enter');
        });

        closeDbBtn.addEventListener('click', () => {
            dbModal.classList.replace('modal-enter', 'modal-exit');
            setTimeout(() => dbModal.classList.add('hidden'), 300);
        });

        saveDbModalBtn.addEventListener('click', () => {
            const totalInputs = document.querySelectorAll('.db-edit-total');
            const qtyInputs = document.querySelectorAll('.db-edit-qty');
            const remarkInputs = document.querySelectorAll('.db-edit-remark');
            
            totalInputs.forEach((totalInput, i) => {
                const size = totalInput.getAttribute('data-size');
                const t = parseFloat(totalInput.value);
                const q = parseInt(qtyInputs[i].value);
                const remark = remarkInputs[i].value.trim();
                
                if (!isNaN(t) && !isNaN(q) && q > 0) {
                    currentDB[size] = {
                        price: t / q,
                        totalPrice: t,
                        quantity: q,
                        remarks: remark
                    };
                }
            });
            saveDatabase();
            
            if (!resultSection.classList.contains('hidden')) {
                evaluatePrice(lastCalculatedSize, lastCalculatedPrice);
            }

            dbModal.classList.replace('modal-enter', 'modal-exit');
            setTimeout(() => dbModal.classList.add('hidden'), 300);
        });

        resetDbBtn.addEventListener('click', () => {
            if(confirm('這將會清除你所有手動更新的價格和備註，回復到最初始的設定，確定嗎？')) {
                currentDB = JSON.parse(JSON.stringify(defaultDB));
                saveDatabase();
                renderDbList();
            }
        });

    </script>
</body>
</html>
