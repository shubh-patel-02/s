<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Campus Dining | Premium Experience</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap');
        :root { --accent: #ef4444; --bg: #020617; --glass: rgba(15, 23, 42, 0.8); }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: var(--bg); color: #f8fafc; overflow-x: hidden; user-select: none; }
        @keyframes liquid { 0% { border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%; } 50% { border-radius: 30% 60% 70% 40% / 50% 60% 30% 60%; } 100% { border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%; } }
        @keyframes scaleUp { from { transform: scale(0.8); opacity: 0; } to { transform: scale(1); opacity: 1; } }
        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
        @keyframes pulse-glow { 0% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0.4); } 70% { box-shadow: 0 0 0 15px rgba(239, 68, 68, 0); } 100% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0); } }
        @keyframes checkmark { 0% { width: 0; height: 0; opacity: 0; } 50% { width: 20px; height: 0; opacity: 1; } 100% { width: 20px; height: 40px; opacity: 1; } }
        .animate-pop { animation: scaleUp 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards; }
        .animate-slide { animation: slideUp 0.5s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
        .liquid-shape { animation: liquid 8s ease-in-out infinite; }
        .payment-pulse { animation: pulse-glow 1.5s infinite; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .glass { background: var(--glass); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.05); }
        .red-gradient { background: linear-gradient(135deg, #ef4444 0%, #7f1d1d 100%); }
        .gold-gradient { background: linear-gradient(135deg, #fbbf24 0%, #b45309 100%); }
        .nav-active { color: var(--accent); border-bottom: 3px solid var(--accent); text-shadow: 0 0 10px rgba(239, 68, 68, 0.5); }
        .check-container { width: 80px; height: 80px; border-radius: 50%; border: 4px solid #22c55e; position: relative; margin: 0 auto 20px; }
        .check-container::after { content: ''; position: absolute; top: 40px; left: 15px; border-right: 4px solid #22c55e; border-top: 4px solid #22c55e; transform: scaleX(-1) rotate(135deg); transform-origin: left top; animation: checkmark 0.5s ease forwards 0.2s; opacity: 0; }
    </style>
</head>
<body class="p-0 m-0">

    <div id="app" class="max-w-md mx-auto min-h-screen relative pb-28">
        
        <div id="auth-overlay" class="fixed inset-0 z-[1000] bg-slate-950 flex flex-col items-center justify-center p-8 transition-all duration-700">
            <div class="liquid-shape w-24 h-24 bg-red-600 flex items-center justify-center text-white text-4xl mb-12 shadow-[0_0_40px_rgba(239,68,68,0.3)]">
                <i class="fa-solid fa-fire-burner"></i>
            </div>
            <div class="w-full glass p-10 rounded-[3rem] text-center border-t border-white/10 animate-pop">
                <h2 id="auth-title" class="text-3xl font-black italic tracking-tighter uppercase mb-2">Campus Dining</h2>
                <p id="auth-sub" class="text-slate-500 text-[10px] font-bold uppercase tracking-widest mb-8 italic">Premium Student Access</p>
                <div class="space-y-4">
                    <input id="email-field" type="email" placeholder="Email Address" class="w-full p-4 bg-slate-900 rounded-2xl border border-white/5 outline-none focus:border-red-500 font-bold text-sm transition-all">
                    <input id="pass-field" type="password" placeholder="Password" class="w-full p-4 bg-slate-900 rounded-2xl border border-white/5 outline-none focus:border-red-500 font-bold text-sm transition-all">
                    <div id="signup-box" class="hidden">
                        <select id="role-field" class="w-full p-4 bg-slate-900 rounded-2xl border border-white/10 outline-none font-bold text-sm text-slate-400 mt-2">
                            <option value="dayScholar">Day Scholar</option>
                            <option value="hosteller">Hostel Resident</option>
                        </select>
                    </div>
                    <button onclick="processAuth()" class="w-full red-gradient p-5 rounded-2xl font-black text-white uppercase tracking-widest mt-4 shadow-xl active:scale-95 transition-all">Continue</button>
                    <button onclick="toggleAuth()" id="toggle-btn" class="w-full text-[10px] font-black uppercase text-slate-500 mt-4 text-center tracking-widest">New Student? Sign Up</button>
                </div>
            </div>
        </div>

        <header class="p-6 flex justify-between items-center sticky top-0 z-50 bg-slate-950/80 backdrop-blur-xl border-b border-white/5">
            <div>
                <p class="text-[9px] font-black text-red-500 tracking-[0.4em] uppercase leading-none italic mb-1">Elite</p>
                <p class="text-xl font-black tracking-tighter uppercase">Campus Dining</p>
            </div>
            <div class="flex items-center gap-3">
                <div onclick="openVault()" class="glass px-4 py-2 rounded-xl flex items-center gap-2 cursor-pointer border-white/10 hover:border-red-500/30 transition-all">
                    <i class="fa-solid fa-bolt-lightning text-yellow-400 text-[10px]"></i>
                    <span id="header-bal" class="font-black text-sm">₹0</span>
                </div>
                <button onclick="toggleProfile()" class="w-12 h-12 glass rounded-2xl flex items-center justify-center text-slate-400 hover:text-white transition-all"><i class="fa-solid fa-fingerprint text-xl"></i></button>
            </div>
        </header>

        <section id="hostel-hub" class="hidden px-6 mt-6 animate-pop">
            <div class="glass p-6 rounded-[2.5rem] border-red-500/20 bg-gradient-to-br from-red-600/5 to-transparent relative overflow-hidden">
                <h3 class="font-black text-lg italic uppercase text-red-500">Residential Meal Pass</h3>
                <p id="sub-status-text" class="text-[9px] font-bold text-slate-500 uppercase mb-4 tracking-widest">Unlimited Access</p>
                <div class="grid grid-cols-2 gap-3 relative z-10">
                    <button onclick="buySub(6000, 'Monthly')" class="bg-white/5 border border-white/10 p-4 rounded-3xl font-black text-[10px] uppercase hover:bg-red-600 transition-all">Monthly<br><span class="text-lg">₹6k</span></button>
                    <button onclick="buySub(60000, 'Yearly')" class="gold-gradient text-black p-4 rounded-3xl font-black text-[10px] uppercase shadow-lg shadow-yellow-500/20">Yearly<br><span class="text-lg">₹60k</span></button>
                </div>
                <i class="fa-solid fa-crown absolute -right-6 -bottom-6 text-white/5 text-9xl"></i>
            </div>
        </section>

        <nav class="flex justify-around items-center px-10 py-8">
            <button onclick="setTab('mess', this)" class="nav-item nav-active font-black uppercase text-[10px] tracking-[0.2em]">Mess</button>
            <button onclick="setTab('cafe', this)" class="nav-item font-black uppercase text-[10px] tracking-[0.2em]">Café</button>
            <button onclick="setTab('tickets', this)" class="nav-item font-black uppercase text-[10px] tracking-[0.2em]">Tickets</button>
        </nav>

        <div id="slot-nav" class="px-6 mb-8 flex gap-3 overflow-x-auto no-scrollbar"></div>
        <main id="food-grid" class="px-6 space-y-6 pb-10"></main>

        <div id="profile-drawer" class="fixed inset-y-0 right-0 w-full z-[1100] bg-slate-950 translate-x-full transition-transform duration-500 flex flex-col border-l border-white/5">
            <div class="p-10 red-gradient text-white rounded-bl-[4rem] relative">
                <button onclick="toggleProfile()" class="absolute top-10 right-10 text-2xl opacity-40"><i class="fa-solid fa-xmark"></i></button>
                <div class="w-20 h-20 bg-white/10 backdrop-blur-md rounded-[2rem] flex items-center justify-center text-4xl mb-6 border border-white/20 italic font-black" id="prof-init">S</div>
                <h3 class="text-xl font-black uppercase tracking-tighter" id="prof-email"></h3>
                <div class="flex flex-col gap-2 mt-2">
                    <div class="flex gap-2">
                        <span id="badge-role" class="text-[8px] bg-white/20 px-3 py-1 rounded-full font-black uppercase tracking-widest">Day Scholar</span>
                        <span id="badge-sub" class="hidden text-[8px] bg-yellow-400 text-black px-3 py-1 rounded-full font-black uppercase">PRO MEMBER</span>
                    </div>
                    <p id="prof-expiry" class="text-[10px] font-bold text-yellow-200 uppercase tracking-tighter hidden italic"></p>
                </div>
            </div>
            <div class="p-8 flex-1 overflow-y-auto no-scrollbar">
                <div class="grid grid-cols-2 gap-4 mb-10 text-center">
                    <div class="glass p-4 rounded-3xl border-white/5">
                        <p class="text-[8px] font-black text-slate-500 uppercase mb-1">Balance</p>
                        <p class="text-xl font-black text-white" id="prof-bal">₹0</p>
                    </div>
                    <div class="glass p-4 rounded-3xl border-white/5">
                        <p class="text-[8px] font-black text-slate-500 uppercase mb-1">Credits</p>
                        <p class="text-xl font-black text-yellow-500" id="prof-pts">0</p>
                    </div>
                </div>
                <p class="text-[10px] font-black text-slate-500 uppercase tracking-widest mb-6">Activity Ledger</p>
                <div id="history-box" class="space-y-4"></div>
            </div>
            <div class="p-8 border-t border-white/5"><button onclick="location.reload()" class="w-full p-5 rounded-2xl bg-white/5 border border-white/10 font-black uppercase text-xs tracking-widest text-red-500 active:bg-red-500 active:text-white transition-all italic">Terminate Session</button></div>
        </div>

        <div id="vault-modal" class="hidden fixed inset-0 z-[1200] bg-black/90 backdrop-blur-2xl flex items-end justify-center">
            <div class="w-full glass rounded-t-[4rem] p-10 border-t border-white/10 animate-slide">
                <div class="w-12 h-1 bg-white/10 rounded-full mx-auto mb-10"></div>
                <h2 class="text-3xl font-black italic text-red-600 mb-8 uppercase tracking-tighter text-center">Add Amount</h2>
                <input id="vault-input" type="number" placeholder="Enter the Amount" class="w-full p-6 bg-slate-900 rounded-[2rem] text-4xl font-black outline-none border border-white/5 focus:border-red-500 text-center mb-8">
                <div class="grid grid-cols-2 gap-4 mb-8">
                    <button onclick="selectUPI('GPay', this)" class="upi-opt p-6 glass rounded-3xl flex flex-col items-center gap-3 border-white/5 hover:border-red-500 transition-all"><img src="https://www.vectorlogo.zone/logos/google_pay/google_pay-icon.svg" class="w-10"><span class="text-[8px] font-black uppercase text-slate-400">Google Pay</span></button>
                    <button onclick="selectUPI('PhonePe', this)" class="upi-opt p-6 glass rounded-3xl flex flex-col items-center gap-3 border-white/5 hover:border-red-500 transition-all"><img src="https://www.vectorlogo.zone/logos/phonepe/phonepe-icon.svg" class="w-10"><span class="text-[8px] font-black uppercase text-slate-400">PhonePe</span></button>
                </div>
                <button onclick="executeRecharge()" id="recharge-btn" class="w-full red-gradient p-6 rounded-3xl font-black text-xl shadow-2xl uppercase tracking-tighter">Authorize Refill</button>
                <button onclick="closeVault()" class="w-full mt-6 text-[10px] font-black text-slate-500 uppercase tracking-widest text-center italic">Dismiss</button>
            </div>
        </div>

        <div id="status-modal" class="hidden fixed inset-0 z-[1300] bg-slate-950/95 flex items-center justify-center p-8 text-center">
            <div class="w-full glass p-12 rounded-[4rem] animate-pop border-red-500/20">
                <div id="status-icon"></div>
                <h3 id="status-title" class="text-2xl font-black italic uppercase text-red-500 mb-2"></h3>
                <p id="status-sub" class="text-[10px] font-bold text-slate-500 uppercase tracking-widest mb-8"></p>
                <div id="qr-area" class="hidden flex flex-col items-center mb-8">
                    <div class="p-4 bg-white rounded-3xl mb-4"><i class="fa-solid fa-qrcode text-8xl text-black"></i></div>
                    <p class="text-[8px] font-black text-slate-400 uppercase italic">Show this at counter to redeem</p>
                </div>
                <button onclick="closeStatus()" class="w-full red-gradient p-5 rounded-2xl font-black uppercase tracking-widest shadow-lg">Confirm</button>
            </div>
        </div>

    </div>

    <script>
        // ADDED: Expiry tracking in state
        let state = { bal: 500, pts: 0, role: 'dayScholar', isSub: false, subExpiry: null, email: '', tickets: [], history: [], view: 'mess', slot: 'Breakfast', isLogin: true };
        let qtys = {}; let upi = "";

        const menuData = {
            mess: {
                Breakfast: [
                    {id:1, name:'Poha', price:40, img:'https://images.unsplash.com/photo-1626132646529-500637532537?w=500'},
                    {id:2, name:'Upma', price:40, img:'https://images.unsplash.com/photo-1589301760014-d929f3979dbc?w=500'},
                    {id:3, name:'Tea', price:10, img:'https://uzhavarbumi.com/recipes/caramel-tea'},
                    {id:4, name:'Coffee', price:15, img:'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500'},
                    {id:26, name:'Bread Butter', price:20, img:'https://hotelkunal.com/product/bread-butter/'}
                ], 	
                Lunch: [{id:5, name:'Maharaja Thali', price:100, img:'https://images.unsplash.com/photo-1546833999-b9f581a1996d?w=500'}],
                'High Tea': [
                    {id:6, name:'Samosa Platter', price:45, img:'https://images.unsplash.com/photo-1601050644117-3aff98844805?w=500'},
                    {id:7, name:'Idli Sambar', price:45, img:'https://www.chitrasfoodbook.com/tomato-brinjal-sambhar-for-idly-dosa/'},
                    {id:8, name:'Cold Coffee', price:30, img:'https://www.vegrecipesofindia.com/cold-coffee-recipe-coffee-milkshake/'},
                    {id:9, name:'Pani Poori', price:45, img:'https://images.unsplash.com/photo-1601050644117-3aff98844805?w=500'}
                ],	
                Dinner: [{id:10, name:'Executive Meal', price:120, img:'https://images.unsplash.com/photo-1546833999-b9f581a1996d?w=500'}]
            },
            cafe: {
                'Quick Snacks': [
                    {id: 12, name: 'Cheese Burger', price: 85, img: 'https://images.unsplash.com/photo-1571091718767-18b5b1457add?w=500'},
                    {id: 13, name: 'French Fries', price: 60, img: 'https://images.unsplash.com/photo-1573080496219-bb080dd4f877?w=500'},
                    {id: 14, name: 'Veg Sandwich', price: 50, img: 'https://images.unsplash.com/photo-1528735602780-2552fd46c7af?w=500'},
                    {id: 15, name: 'Vada Pav', price: 30, img: 'https://images.unsplash.com/photo-1606491956391-70868b5d0f47?w=500'},
                    {id: 16, name: 'Maggi Special', price: 45, img: 'https://images.unsplash.com/photo-1612927621604-c282371b4a92?w=500'},
                    {id: 17, name: 'Samosa (2pc)', price: 30, img: 'https://images.unsplash.com/photo-1601050644117-3aff98844805?w=500'}
                ],
                'Full Meals': [
                    {id: 18, name: 'Paneer Tikka', price: 180, img: 'https://images.unsplash.com/photo-1631452180519-c014fe946bc7?w=500'},
                    {id: 19, name: 'White Sauce Pasta', price: 140, img: 'https://images.unsplash.com/photo-1645112481338-35623979ea0e?w=500'},
                    {id: 20, name: 'Veg Biryani', price: 160, img: 'https://images.unsplash.com/photo-1563379091339-03b21bc4a4f8?w=500'},
                    {id: 21, name: 'Veg Manchurian', price: 120, img: 'https://images.unsplash.com/photo-1512058560550-42749d9a4077?w=500'},
                    {id: 22, name: 'Chole Bhature', price: 95, img: 'https://images.unsplash.com/photo-1589301760014-d929f3979dbc?w=500'}
                ],
                'Beverages': [
                    {id: 23, name: 'Oreo Shake', price: 95, img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500'},
                    {id: 24, name: 'Virgin Mojito', price: 80, img: 'https://images.unsplash.com/photo-1546173159-315724a31696?w=500'},
                    {id: 25, name: 'Cold Coffee', price: 70, img: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500'}
                ]
            }
        };

        function checkExpiry() {
            if (state.subExpiry && new Date().getTime() > state.subExpiry) {
                state.isSub = false;
                state.subExpiry = null;
                updateUI();
            }
        }

        function processAuth() {
            const e = document.getElementById('email-field').value;
            const p = document.getElementById('pass-field').value;
            if(!e.includes('@') || p.length < 4) return alert("Security Breach: Invalid Credentials");
            state.email = e;
            state.role = document.getElementById('role-field').value;
            document.getElementById('auth-overlay').style.transform = 'translateY(-100%)';
            if(state.role === 'hosteller') document.getElementById('hostel-hub').classList.remove('hidden');
            setTab('mess', document.querySelector('.nav-item'));
            updateUI();
        }

        function isWindowOpen() {
            const now = new Date();
            const mins = now.getHours() * 60 + now.getMinutes();
            return mins >= (8 * 60) && mins <= (10 * 60 + 30);
        }

        function handleOrder(id, name, p, isMess) {
            checkExpiry();
            const qty = qtys[id] || 1;
            const isFree = isMess && state.role === 'hosteller' && state.isSub;
            const total = isFree ? 0 : p * qty;

            if(state.bal < total) return openVault();

            const btn = event.currentTarget;
            btn.innerHTML = "<i class='fa-solid fa-spinner fa-spin'></i>";
            btn.classList.add('payment-pulse');

            setTimeout(() => {
                state.bal -= total; state.pts += Math.floor(total * 0.1);
                const tId = Math.floor(1000 + Math.random()*9000);
                state.tickets.unshift({ id: tId, name, qty, time: new Date().toLocaleTimeString() });
                state.history.unshift({ title: `${qty}x ${name}`, amt: total, type: 'debit' });
                updateUI();
                showStatus(isFree ? 'Redeemed' : 'Order Success', `Transaction ID: #CAM-${tId}`, true, name);
                renderGrid();
            }, 1200);
        }

        function executeRecharge() {
            const a = parseInt(document.getElementById('vault-input').value);
            if(!a || !upi) return alert("Identify App & Amount");
            const btn = document.getElementById('recharge-btn');
            btn.innerHTML = "<i class='fa-solid fa-circle-notch fa-spin'></i> Linking to " + upi;
            setTimeout(() => {
                state.bal += a;
                state.history.unshift({ title: `Vault Refill (${upi})`, amt: a, type: 'credit' });
                updateUI(); closeVault();
                showStatus('Capital Added', `₹${a} injected via Secure UPI`, false);
                btn.innerHTML = "Authorize Refill";
            }, 1800);
        }

        function buySub(cost, type) {
            // Check if already active and not expired
            if (state.isSub && state.subExpiry && new Date().getTime() < state.subExpiry) {
                return alert("You already have an active plan!");
            }
            if(state.bal < cost) return openVault();
            
            state.bal -= cost; 
            state.isSub = true;
            
            // Set Expiry Date
            let expiryDate = new Date();
            if(type === 'Monthly') expiryDate.setMonth(expiryDate.getMonth() + 1);
            else expiryDate.setFullYear(expiryDate.getFullYear() + 1);
            
            state.subExpiry = expiryDate.getTime();
            
            state.history.unshift({ title: `${type} Resident Plan`, amt: cost, type: 'debit' });
            updateUI(); 
            showStatus('Pro Active', `Unlimited Mess Unlocked until ${expiryDate.toLocaleDateString()}`, false);
        }

        function updateUI() {
            checkExpiry();
            document.getElementById('header-bal').innerText = `₹${state.bal}`;
            document.getElementById('prof-bal').innerText = `₹${state.bal}`;
            document.getElementById('prof-pts').innerText = state.pts;
            document.getElementById('prof-email').innerText = state.email;
            document.getElementById('prof-init').innerText = state.email ? state.email.charAt(0).toUpperCase() : 'S';
            document.getElementById('badge-role').innerText = state.role === 'dayScholar' ? 'DAY SCHOLAR' : 'RESIDENT';
            
            const badgeSub = document.getElementById('badge-sub');
            const profExpiry = document.getElementById('prof-expiry');
            const subStatusText = document.getElementById('sub-status-text');

            if(state.isSub) {
                badgeSub.classList.remove('hidden');
                profExpiry.classList.remove('hidden');
                const expiryObj = new Date(state.subExpiry);
                profExpiry.innerText = `Expires: ${expiryObj.toLocaleDateString()} ${expiryObj.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})}`;
                subStatusText.innerText = `PRO ACTIVE UNTIL ${expiryObj.toLocaleDateString()}`;
                subStatusText.classList.add('text-yellow-400');
            } else {
                badgeSub.classList.add('hidden');
                profExpiry.classList.add('hidden');
                subStatusText.innerText = `Unlimited Access`;
                subStatusText.classList.remove('text-yellow-400');
            }

            document.getElementById('history-box').innerHTML = state.history.map(h => `<div class="flex justify-between p-4 glass rounded-2xl border-white/5 animate-pop"><p class="text-[9px] font-black uppercase text-slate-400">${h.title}</p><p class="font-black ${h.type==='debit'?'text-red-500':'text-green-500'} text-xs">₹${h.amt}</p></div>`).join('');
        }

        function setTab(v, btn) {
            state.view = v;
            document.querySelectorAll('.nav-item').forEach(b => b.classList.remove('nav-active'));
            if(btn) btn.classList.add('nav-active');
            const slotNav = document.getElementById('slot-nav');
            if(v === 'tickets') { slotNav.innerHTML = ''; renderTickets(); return; }
            const slots = v === 'mess' ? ['Breakfast', 'Lunch', 'High Tea', 'Dinner'] : ['Quick Snacks', 'Full Meals', 'Beverages'];
            slotNav.innerHTML = slots.map((s, i) => `<button onclick="setSlot('${s}', this)" class="s-btn px-6 py-2.5 rounded-2xl text-[9px] font-black uppercase border border-white/5 ${i===0?'bg-red-600 border-red-600 shadow-[0_0_20px_rgba(239,68,68,0.3)]':''} transition-all whitespace-nowrap">${s}</button>`).join('');
            setSlot(slots[0], slotNav.querySelector('button'));
        }

        function setSlot(s, btn) {
            state.slot = s;
            document.querySelectorAll('.s-btn').forEach(b => { b.classList.remove('bg-red-600', 'border-red-600','shadow-[0_0_20px_rgba(239,68,68,0.3)]'); });
            btn.classList.add('bg-red-600', 'border-red-600','shadow-[0_0_20px_rgba(239,68,68,0.3)]');
            renderGrid();
        }

        function renderGrid() {
            const grid = document.getElementById('food-grid');
            if(state.view === 'mess' && (state.slot === 'Lunch' || state.slot === 'Dinner') && !isWindowOpen()) {
                grid.innerHTML = `<div class="p-20 text-center opacity-30 animate-pop"><i class="fa-solid fa-lock text-5xl mb-4"></i><p class="font-black uppercase text-[10px] tracking-widest">Window Closed (10:30 AM)</p></div>`;
                return;
            }
            grid.innerHTML = (menuData[state.view][state.slot] || []).map(item => {
                qtys[item.id] = 1;
                const isFree = state.view === 'mess' && state.role === 'hosteller' && state.isSub;
                return `<div class="glass p-2 rounded-[3rem] overflow-hidden animate-pop"><img src="${item.img}" class="w-full h-44 object-cover rounded-[2.5rem] opacity-70"><div class="p-6"><h4 class="font-black text-xl uppercase tracking-tighter italic">${item.name}</h4><div class="flex items-center justify-between mt-4"><div class="flex items-center glass p-1.5 rounded-2xl gap-4"><button onclick="changeQty(${item.id},-1)" class="w-8 h-8 rounded-lg bg-white/5 flex items-center justify-center">-</button><span id="qty-${item.id}" class="font-black text-lg">1</span><button onclick="changeQty(${item.id},1)" class="w-8 h-8 rounded-lg bg-red-600 flex items-center justify-center shadow-lg shadow-red-500/20">+</button></div><button onclick="handleOrder(${item.id},'${item.name}',${item.price}, ${state.view==='mess'})" class="red-gradient px-8 py-4 rounded-3xl font-black text-[10px] uppercase shadow-2xl">${isFree ? 'REDEEM' : '₹'+item.price}</button></div></div></div>`;
            }).join('');
        }

        function renderTickets() {
            document.getElementById('food-grid').innerHTML = state.tickets.map(t => `<div class="glass p-6 border-dashed border-red-500/30 flex justify-between items-center animate-slide"><div class="flex items-center gap-5"><div class="w-14 h-14 bg-white/5 rounded-2xl flex items-center justify-center text-red-500 text-2xl"><i class="fa-solid fa-qrcode"></i></div><div><p class="font-black text-xs uppercase">${t.name} (x${t.qty})</p><p class="text-[9px] font-bold text-slate-500 tracking-tighter mt-1">REF: #CAMP-${t.id}</p></div></div><button onclick="redeem(${t.id})" class="text-[9px] font-black uppercase text-red-500 bg-red-500/10 px-4 py-2 rounded-xl transition-all active:bg-red-500 active:text-white">Redeem</button></div>`).join('') || `<p class="text-center py-20 font-black text-slate-700 uppercase italic text-[10px]">No active tokens</p>`;
        }

        function showStatus(title, sub, qr, name = "") { document.getElementById('status-title').innerText = title; document.getElementById('status-sub').innerText = sub; document.getElementById('status-icon').innerHTML = '<div class="check-container"></div>'; document.getElementById('qr-area').style.display = qr ? 'flex' : 'none'; document.getElementById('status-modal').classList.remove('hidden'); }
        function closeStatus() { document.getElementById('status-modal').classList.add('hidden'); }
        function toggleProfile() { document.getElementById('profile-drawer').classList.toggle('translate-x-full'); }
        function openVault() { document.getElementById('vault-modal').classList.remove('hidden'); }
        function closeVault() { document.getElementById('vault-modal').classList.add('hidden'); }
        function changeQty(id, d) { qtys[id] = Math.max(1, (qtys[id] || 1) + d); document.getElementById(`qty-${id}`).innerText = qtys[id]; }
        function redeem(id) { state.tickets = state.tickets.filter(t => t.id !== id); renderTickets(); }
        function toggleAuth() { state.isLogin = !state.isLogin; document.getElementById('signup-box').classList.toggle('hidden'); document.getElementById('toggle-btn').innerText = state.isLogin ? 'New? Sign Up' : 'Back to Login'; }
        function selectUPI(id, btn) { upi = id; document.querySelectorAll('.upi-opt').forEach(b => b.classList.remove('border-red-500','bg-white/5')); btn.classList.add('border-red-500','bg-white/5'); }
    </script>
</body>
</html>
