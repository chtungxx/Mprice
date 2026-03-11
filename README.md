[MpriceV1.html](https://github.com/user-attachments/files/25897084/MpriceV1.html)
<!DOCTYPE html>
<html lang="zh-HK">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="M巾格價">
    <title>衛生巾格價神器</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --bg-color: #fdf2f8; }
        body { background-color: var(--bg-color); font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; -webkit-tap-highlight-color: transparent; }
        input[type=number]::-webkit-inner-spin-button, input[type=number]::-webkit-outer-spin-button { -webkit-appearance: none; margin: 0; }
        .modal-enter { animation: fadeIn 0.3s ease-out forwards; }
        .modal-exit { animation: fadeOut 0.3s ease-in forwards; }
        @keyframes fadeIn { from { opacity: 0; transform: scale(0.95); } to { opacity: 1; transform: scale(1); } }
        @keyframes fadeOut { from { opacity: 1; transform: scale(1); } to { opacity: 0; transform: scale(0.95); } }
    </style>
</head>
<body class="min-h-screen p-4 flex justify-center items-start pt-6 md:pt-12 pb-10">
    <div class="bg-white rounded-3xl shadow-xl w-full max-w-md overflow-hidden border border-pink-100 relative">
        <!-- 頂部標題列 -->
        <div class="bg-pink-500 text-white text-center py-5 px-4 shadow-sm relative">
            <h1 class="text-2xl font-bold tracking-wider"><i class="fa-solid fa-calculator mr-2"></i>M巾格價神器</h1>
            <p class="text-pink-100 text-sm mt-1">精打細算，唔做水魚！</p>
            <button id="open-db-btn" class="absolute top-4 right-4 bg-pink-600 hover:bg-pink-700 p-2 rounded-full transition-colors" title="管理底價資料庫">
                <i class="fa-solid fa-database text-white"></i>
            </button>
        </div>

        <!-- 主要表單內容 -->
        <div class="p-6 space-y-5">
            <div>
                <label class="block text-gray-700 font-bold mb-2 text-sm" for="size-select"><i class="fa-solid fa-ruler-combined text-pink-400 mr-2"></i>1. 選擇尺寸</label>
                <div class="relative">
                    <select id="size-select" class="block appearance-none w-full bg-pink-50 border border-pink-200 text-gray-700 py-3 px-4 pr-8 rounded-xl leading-tight focus:outline-none focus:bg-white focus:border-pink-500 transition-colors cursor-pointer text-lg">
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
                    <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-4 text-pink-500"><i class="fa-solid fa-chevron-down"></i></div>
                </div>
            </div>

            <div id="custom-size-container" class="hidden">
                <input type="text" id="custom-size-input" placeholder="請輸入尺寸 (例如: 19cm)" class="block w-full bg-gray-50 border border-gray-200 text-gray-700 py-3 px-4 rounded-xl leading-tight focus:outline-none focus:bg-white focus:border-pink-500 transition-colors">
            </div>

            <div class="flex space-x-4">
                <div class="flex-1">
                    <label class="block text-gray-700 font-bold mb-2 text-sm" for="price-input"><i class="fa-solid fa-dollar-sign text-pink-400 mr-2"></i>2. 總金額 ($)</label>
                    <input type="number" id="price-input" placeholder="例如: 35.9" step="0.1" min="0" class="block w-full bg-pink-50 border border-pink-200 text-gray-700 py-3 px-4 rounded-xl leading-tight focus:outline-none focus:bg-white focus:border-pink-500 transition-colors text-lg">
                </div>
                <div class="flex-1">
                    <label class="block text-gray-700 font-bold mb-2 text-sm" for="quantity-input"><i class="fa-solid fa-layer-group text-pink-400 mr-2"></i>3. 幾多塊？</label>
                    <input type="number" id="quantity-input" placeholder="例如: 36" step="1" min="1" class="block w-full bg-pink-50 border border-pink-200 text-gray-700 py-3 px-4 rounded-xl leading-tight focus:outline-none focus:bg-white focus:border-pink-500 transition-colors text-lg">
                </div>
            </div>

            <button id="calculate-btn" class="w-full bg-pink-500 hover:bg-pink-600 text-white font-bold py-4 px-4 rounded-xl shadow-md transition-all active:scale-95 text-lg mt-2 flex justify-center items-center">
                <i class="fa-solid fa-wand-magic-sparkles mr-2"></i> 即刻幫我算
            </button>
        </div>

        <!-- 結果顯示區 -->
        <div id="result-section" class="hidden bg-gray-50 border-t border-gray-100 p-6 text-center rounded-b-3xl">
            <h3 class="text-sm text-gray-500 font-bold uppercase tracking-wider mb-1">計算結果</h3>
            <div class="text-4xl font-extrabold text-gray-800 mb-2">
                $<span id="unit-price-display">0.00</span> <span class="text-lg text-gray-500 font-normal">/ 片</span>
            </div>
            
            <div id="verdict-box" class="mt-4 p-4 rounded-xl border-2 font-bold text-lg flex flex-col items-center justify-center">
                <div id="verdict-icon" class="text-3xl mb-2"></div>
                <div id="verdict-text"></div>
                <div id="reference-price-text" class="text-xs font-normal mt-2 opacity-80"></div>
                <div id="db-remarks-text" class="text-xs font-normal mt-1 opacity-70 italic hidden"></div>
            </div>

            <div id="update-db-container" class="mt-4 hidden">
                <div class="mb-2">
                    <input type="text" id="new-remark-input" placeholder="加入備註 (選填，例如: 屈臣氏買一送一)" class="block w-full bg-white border border-gray-300 text-gray-700 py-2 px-3 rounded-lg text-sm focus:outline-none focus:border-green-500">
                </div>
                <button id="update-db-btn" class="w-full bg-green-500 hover:bg-green-600 text-white font-bold py-3 px-4 rounded-xl shadow transition-all active:scale-95 text-sm flex justify-center items-center">
                    <i class="fa-solid fa-floppy-disk mr-2"></i> <span id="update-db-text">更新底價紀錄</span>
                </button>
            </div>
        </div>
    </div>

    <!-- 資料庫管理 Modal -->
    <div id="db-modal" class="fixed inset-0 bg-black bg-opacity-60 flex items-center justify-center hidden z-50 px-4">
        <div class="bg-white rounded-2xl shadow-2xl w-full max-w-md max-h-[85vh] flex flex-col overflow-hidden">
            <div class="bg-gray-100 py-4 px-6 border-b border-gray-200 flex justify-between items-center">
                <h2 class="text-lg font-bold text-gray-800"><i class="fa-solid fa-database text-pink-500 mr-2"></i>我的底價庫</h2>
                <button id="close-db-btn" class="text-gray-500 hover:text-gray-800 text-xl"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div class="p-4 overflow-y-auto flex-1 bg-gray-50">
                <p class="text-xs text-gray-500 mb-4 text-center">輸入總金額與數量，系統會自動幫你計算單價！</p>
                <div id="db-list" class="space-y-4"></div>
            </div>
            
            <div class="bg-white py-3 px-4 border-t border-gray-200 flex justify-end">
                <button id="reset-db-btn" class="text-xs text-red-500 hover:text-red-700 underline mr-auto self-center">重置回預設值</button>
                <button id="save-db-modal-btn" class="bg-pink-500 hover:bg-pink-600 text-white font-bold py-2 px-6 rounded-lg transition-colors">儲存修改</button>
            </div>
        </div>
    </div>

    <!-- 邏輯腳本 -->
    <script>
        // ==========================================
        // 💰 系統預設底價資料庫 (已加入總額與數量結構)
        // 結構: { "尺寸": { price: 單價, totalPrice: 總額, quantity: 數量, remarks: "備註" } }
        // ==========================================
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

        // 初始化：讀取資料庫，自動升級為 V3 版本 (包含總額和數量)
        function loadDatabase() {
            const savedData = localStorage.getItem('mPadTargetPricesV3');
            if (savedData) {
                try {
                    currentDB = JSON.parse(savedData);
                } catch (e) {
                    currentDB = JSON.parse(JSON.stringify(defaultDB));
                }
            } else {
                // 嘗試從舊版本 (V2) 升級
                const oldData = localStorage.getItem('mPadTargetPricesV2');
                if (oldData) {
                    try {
                        const oldDB = JSON.parse(oldData);
                        currentDB = {};
                        for (const key in oldDB) {
                            currentDB[key] = {
                                price: oldDB[key].price,
                                totalPrice: oldDB[key].totalPrice || oldDB[key].price, // 舊版無總額，預設為單價
                                quantity: oldDB[key].quantity || 1,                    // 舊版無數量，預設為 1
                                remarks: oldDB[key].remarks || ""
                            };
                        }
                    } catch (e) {
                         currentDB = JSON.parse(JSON.stringify(defaultDB));
                    }
                } else {
                     currentDB = JSON.parse(JSON.stringify(defaultDB));
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
        });

        let lastCalculatedSize = "";
        let lastCalculatedPrice = 0;
        let lastCalculatedTotalPrice = 0;
        let lastCalculatedQuantity = 0;

        calculateBtn.addEventListener('click', function() {
            let selectedSize = sizeSelect.value;
            if (selectedSize === 'other') {
                selectedSize = customSizeInput.value.trim();
            }
            const totalPrice = parseFloat(priceInput.value);
            const quantity = parseInt(quantityInput.value);

            if (!selectedSize) return alert('請選擇或輸入尺寸！');
            if (isNaN(totalPrice) || totalPrice <= 0) return alert('請輸入有效的總金額！');
            if (isNaN(quantity) || quantity <= 0) return alert('請輸入有效的片數！');

            const unitPrice = totalPrice / quantity;
            unitPriceDisplay.textContent = unitPrice.toFixed(2);
            
            lastCalculatedSize = selectedSize;
            lastCalculatedPrice = unitPrice;
            lastCalculatedTotalPrice = totalPrice;
            lastCalculatedQuantity = quantity;

            evaluatePrice(selectedSize, unitPrice);
            resultSection.classList.remove('hidden');
            resultSection.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
        });

        function evaluatePrice(size, calculatedUnitPrice) {
            verdictBox.className = 'mt-4 p-4 rounded-xl border-2 font-bold text-lg flex flex-col items-center justify-center transition-all duration-300';
            updateDbContainer.classList.add('hidden');
            dbRemarksText.classList.add('hidden');
            newRemarkInput.value = ""; 
            
            if (currentDB.hasOwnProperty(size)) {
                const targetData = currentDB[size];
                const targetPrice = targetData.price;
                
                if (targetData.remarks) {
                    dbRemarksText.textContent = `📝 紀錄備註: ${targetData.remarks}`;
                    dbRemarksText.classList.remove('hidden');
                }
                
                // 為了避免浮點數誤差，我們檢查差距是否小於 0.005
                if (calculatedUnitPrice < targetPrice - 0.005) {
                    verdictBox.classList.add('bg-yellow-50', 'border-yellow-400', 'text-yellow-700');
                    verdictIcon.innerHTML = '<i class="fa-solid fa-trophy text-yellow-500"></i>';
                    verdictText.textContent = '嘩！破底價！平過以前！';
                    referencePriceText.textContent = `(舊底價：$${targetPrice.toFixed(2)}/片)`;
                    
                    updateDbContainer.classList.remove('hidden');
                    updateDbText.textContent = `將 $${calculatedUnitPrice.toFixed(2)} 設為新底價`;
                    
                } else if (Math.abs(calculatedUnitPrice - targetPrice) <= 0.005) {
                    verdictBox.classList.add('bg-green-50', 'border-green-400', 'text-green-700');
                    verdictIcon.innerHTML = '<i class="fa-solid fa-face-grin-stars text-green-500"></i>';
                    verdictText.textContent = '抵買！去到你的入貨底線！';
                    referencePriceText.textContent = `(目標價：$${targetPrice.toFixed(2)}/片)`;
                } else {
                    verdictBox.classList.add('bg-red-50', 'border-red-400', 'text-red-700');
                    verdictIcon.innerHTML = '<i class="fa-solid fa-hand-holding-dollar text-red-500"></i>';
                    verdictText.textContent = '較平時貴，建議再格價！';
                    referencePriceText.textContent = `(你的入貨底線：$${targetPrice.toFixed(2)}/片)`;
                }
            } else {
                verdictBox.classList.add('bg-blue-50', 'border-blue-400', 'text-blue-700');
                verdictIcon.innerHTML = '<i class="fa-solid fa-circle-info text-blue-500"></i>';
                verdictText.textContent = '呢款尺寸暫時未有底價紀錄～';
                referencePriceText.textContent = '你可以儲存今次價錢作為未來參考！';
                
                updateDbContainer.classList.remove('hidden');
                updateDbText.textContent = `新增 $${calculatedUnitPrice.toFixed(2)} 為底價`;
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
            this.innerHTML = '<i class="fa-solid fa-check mr-2"></i> 已更新！';
            this.classList.replace('bg-green-500', 'bg-gray-400');
            this.classList.replace('hover:bg-green-600', 'hover:bg-gray-500');
            this.disabled = true;
            
            setTimeout(() => {
                evaluatePrice(lastCalculatedSize, lastCalculatedPrice);
                this.innerHTML = originalHTML;
                this.classList.replace('bg-gray-400', 'bg-green-500');
                this.classList.replace('hover:bg-gray-500', 'hover:bg-green-600');
                this.disabled = false;
            }, 1500);
        });

        // ==========================================
        // Modal 資料庫管理邏輯
        // ==========================================
        
        function renderDbList() {
            dbList.innerHTML = '';
            const sizes = Object.keys(currentDB);
            
            if (sizes.length === 0) {
                dbList.innerHTML = '<p class="text-center text-gray-400 py-4">暫無紀錄</p>';
                return;
            }

            sizes.sort((a, b) => {
                const numA = parseInt(a);
                const numB = parseInt(b);
                if (!isNaN(numA) && !isNaN(numB)) return numA - numB;
                return a.localeCompare(b);
            });

            sizes.forEach((size, index) => {
                const data = currentDB[size];
                const price = data.price.toFixed(2);
                const totalPrice = data.totalPrice !== undefined ? data.totalPrice : data.price;
                const quantity = data.quantity !== undefined ? data.quantity : 1;
                const remarks = data.remarks || '';
                
                const item = document.createElement('div');
                item.className = 'bg-white p-3.5 rounded-xl border border-pink-100 shadow-sm flex flex-col space-y-3';
                item.innerHTML = `
                    <!-- 頂部：尺寸與算好的單價 -->
                    <div class="flex items-center justify-between border-b border-gray-100 pb-2">
                        <div class="font-bold text-gray-800 text-lg">${size}</div>
                        <div class="text-pink-600 font-extrabold text-lg db-display-unit" id="unit-display-${index}">$${price}/片</div>
                    </div>
                    
                    <!-- 中間：總金額與數量輸入框 -->
                    <div class="flex items-center space-x-2 text-sm">
                        <span class="text-gray-500 font-bold">總額$</span>
                        <input type="number" step="0.1" min="0" data-size="${size}" data-index="${index}" value="${totalPrice}" class="db-edit-total flex-1 min-w-0 bg-gray-50 border border-gray-300 rounded-lg px-2 py-1.5 focus:outline-none focus:border-pink-500 focus:bg-white text-gray-700">
                        
                        <span class="text-gray-500 font-bold">/</span>
                        
                        <input type="number" step="1" min="1" data-size="${size}" data-index="${index}" value="${quantity}" class="db-edit-qty w-16 bg-gray-50 border border-gray-300 rounded-lg px-2 py-1.5 focus:outline-none focus:border-pink-500 focus:bg-white text-center text-gray-700">
                        <span class="text-gray-500 font-bold">塊</span>
                        
                        <button class="delete-db-btn text-gray-400 hover:text-red-500 ml-2 p-2 transition-colors" data-size="${size}" title="刪除此紀錄">
                            <i class="fa-solid fa-trash-can"></i>
                        </button>
                    </div>

                    <!-- 底部：備註 -->
                    <div>
                        <input type="text" data-size="${size}" value="${remarks}" placeholder="加入備註 (例如: 品牌/優惠)" class="db-edit-remark w-full text-sm bg-gray-50 border border-gray-200 rounded-lg px-3 py-2 text-gray-600 focus:outline-none focus:border-pink-400 focus:bg-white">
                    </div>
                `;
                
                // 動態綁定：輸入總額或數量時，即時更新上方的單價
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

            // 綁定刪除按鈕
            document.querySelectorAll('.delete-db-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const sizeToDelete = this.getAttribute('data-size');
                    if (confirm(`確定要刪除 ${sizeToDelete} 的紀錄嗎？`)) {
                        delete currentDB[sizeToDelete];
                        renderDbList(); // 重新渲染列表
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

        // 儲存 Modal 的修改
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
            
            // 如果背景正在顯示某個計算結果，重新評估它
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
