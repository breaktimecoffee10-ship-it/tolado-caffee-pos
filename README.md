
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Tolado Caffee POS</title>
    <script src="https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            margin: 0;
            background: #050505;
            color: #f5d27a;
            font-family: 'Poppins', sans-serif;
            text-align: center;
            min-height: 100vh;
            padding: 20px;
        }
        button {
            background: linear-gradient(45deg, #c58a28, #f5d27a);
            border: none;
            padding: 12px 20px;
            border-radius: 12px;
            font-weight: 600;
            color: #050505;
            cursor: pointer;
            margin: 10px 0;
            width: 80%;
            max-width: 300px;
            transition: transform 0.2s;
        }
        button:hover {
            transform: scale(1.05);
        }
        input, select {
            padding: 12px;
            border-radius: 12px;
            border: 2px solid #c58a28;
            margin: 10px 0;
            width: 80%;
            max-width: 300px;
            background: #111;
            color: #f5d27a;
            font-family: 'Poppins', sans-serif;
        }
        .card {
            background: #111;
            border-radius: 18px;
            margin: 20px auto;
            padding: 25px;
            box-shadow: 0 0 25px rgba(245, 210, 122, .15);
            max-width: 400px;
            width: 90%;
        }
        #splash {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: black;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 9999;
            flex-direction: column;
        }
        #splash img {
            width: 200px;
            height: 200px;
            background: #f5d27a;
            border-radius: 50%;
            padding: 20px;
            margin-bottom: 20px;
        }
        #splash .loading {
            color: #f5d27a;
            font-size: 18px;
            margin-top: 20px;
        }
        #struk {
            background: white;
            color: black;
            width: 280px;
            padding: 15px;
            border-radius: 10px;
            margin: 20px auto;
            font-family: 'Courier New', monospace;
            display: none;
            border: 2px solid #c58a28;
        }
        .hidden {
            display: none !important;
        }
        h1 {
            margin: 20px 0;
            color: #f5d27a;
            text-shadow: 0 0 10px rgba(245, 210, 122, 0.5);
        }
        h3 {
            margin-bottom: 20px;
            color: #f5d27a;
        }
        #hasil {
            margin-top: 20px;
        }
        .logo-placeholder {
            width: 150px;
            height: 150px;
            background: linear-gradient(45deg, #c58a28, #f5d27a);
            border-radius: 50%;
            margin: 0 auto 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
            font-weight: bold;
            color: #050505;
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        hr {
            border: none;
            height: 1px;
            background: linear-gradient(to right, transparent, #c58a28, transparent);
            margin: 15px 0;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        .footer {
            margin-top: 30px;
            color: #666;
            font-size: 14px;
        }
        @media (max-width: 768px) {
            .card {
                padding: 15px;
                margin: 10px auto;
            }
            button, input, select {
                width: 90%;
            }
            .logo-placeholder {
                width: 120px;
                height: 120px;
                font-size: 24px;
            }
        }
    </style>
</head>
<body>
    <div id="splash">
        <div class="logo-placeholder">TC</div>
        <div class="loading">Loading Tolado Caffee POS...</div>
    </div>
    
    <div class="container">
        <h1>☕ TOLADO CAFFEE</h1>
        <p style="color: #aaa; margin-bottom: 30px;">Point of Sale System</p>
        
        <div id="login" class="card">
            <h3>LOGIN KASIR</h3>
            <select id="user">
                <option value="">Pilih Kasir</option>
                <option value="faishal">Faishal</option>
                <option value="ziyan">Ziyan</option>
            </select>
            <input id="pass" type="password" placeholder="Password" autocomplete="off">
            <button onclick="login()">MASUK</button>
            <p style="font-size: 12px; color: #888; margin-top: 15px;">
                Demo: Pilih Faishal → Password: 780709
            </p>
        </div>
        
        <div id="kasir" class="hidden">
            <div class="card">
                <h3>PESANAN</h3>
                <select id="menu">
                    <option value="">Pilih Menu</option>
                    <option value="12000">Kopi Susu Gula Aren - Rp 12.000</option>
                    <option value="10000">Americano - Rp 10.000</option>
                    <option value="15000">Butter Scoot - Rp 15.000</option>
                    <option value="8000">Es Teh - Rp 8.000</option>
                    <option value="18000">Cappuccino - Rp 18.000</option>
                    <option value="22000">Latte Special - Rp 22.000</option>
                </select>
                <input id="bayar" type="number" placeholder="Uang Pembayaran (Rp)" min="0">
                <button onclick="proses()">PROSES PEMBAYARAN</button>
                <button onclick="logout()" style="background: #555; margin-top: 10px;">LOGOUT</button>
            </div>
            
            <div id="hasil" class="card hidden">
                <h3>💰 Kembalian: Rp <span id="kembali">0</span></h3>
                <button onclick="cetak()">🖨️ CETAK STRUK PNG</button>
                <button onclick="resetTransaksi()" style="background: #c58a28; margin-top: 10px;">🔄 TRANSAKSI BARU</button>
            </div>
            
            <div id="struk">
                <center>
                    <b style="font-size: 18px;">TOLADO CAFFEE</b><br>
                    <small>tolado.caffee.id</small><br>
                    <hr>
                </center>
                <div style="text-align: left;">
                    Tanggal: <span id="stanggal"></span><br>
                    Waktu: <span id="swaktu"></span><br>
                    Kasir: <span id="skasir"></span><br>
                    <hr>
                    <b>PESANAN:</b><br>
                    <span id="smenu"></span><br>
                    Harga: Rp <span id="sharga"></span><br>
                    Bayar: Rp <span id="sbayar"></span><br>
                    <b>Kembali: Rp <span id="skembali"></span></b><br>
                    <hr>
                    <center><b>Terima kasih atas kunjungannya!</b></center>
                    <center>♥</center>
                </div>
            </div>
        </div>
        
        <div class="footer">
            <p>Tolado Caffee POS System v1.0</p>
            <p>© 2024 - Dibuat dengan ❤️ untuk Tolado Caffee</p>
        </div>
    </div>

    <script>
        // Splash screen
        document.addEventListener('DOMContentLoaded', function() {
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
            }, 2000);
        });

        // Login function
        function login() {
            const user = document.getElementById('user').value;
            const pass = document.getElementById('pass').value;
            
            if (!user) {
                alert('Silakan pilih kasir!');
                return;
            }
            
            // Password untuk masing-masing kasir
            const passwords = {
                'faishal': '780709',
                'ziyan': '900098'
            };
            
            if (passwords[user] === pass) {
                document.getElementById('login').classList.add('hidden');
                document.getElementById('kasir').classList.remove('hidden');
                document.getElementById('skasir').innerText = user === 'faishal' ? 'Faishal' : 'Ziyan';
                
                // Reset form
                document.getElementById('menu').selectedIndex = 0;
                document.getElementById('bayar').value = '';
                document.getElementById('hasil').classList.add('hidden');
                document.getElementById('struk').style.display = 'none';
            } else {
                alert('Password salah!');
                document.getElementById('pass').value = '';
                document.getElementById('pass').focus();
            }
        }

        // Proses pembayaran
        function proses() {
            const menuSelect = document.getElementById('menu');
            const harga = parseInt(menuSelect.value);
            const bayar = parseInt(document.getElementById('bayar').value);
            
            if (!menuSelect.value) {
                alert('Silakan pilih menu terlebih dahulu!');
                return;
            }
            
            if (!bayar || isNaN(bayar)) {
                alert('Masukkan jumlah uang pembayaran!');
                return;
            }
            
            if (bayar < harga) {
                alert(`Uang kurang! Harga: Rp ${harga.toLocaleString('id-ID')}`);
                return;
            }
            
            const kembali = bayar - harga;
            
            // Update tampilan
            document.getElementById('kembali').innerText = kembali.toLocaleString('id-ID');
            document.getElementById('hasil').classList.remove('hidden');
            
            // Update struk
            const now = new Date();
            document.getElementById('stanggal').innerText = now.toLocaleDateString('id-ID', {
                weekday: 'long',
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            });
            document.getElementById('swaktu').innerText = now.toLocaleTimeString('id-ID');
            document.getElementById('smenu').innerText = menuSelect.options[menuSelect.selectedIndex].text;
            document.getElementById('sharga').innerText = harga.toLocaleString('id-ID');
            document.getElementById('sbayar').innerText = bayar.toLocaleString('id-ID');
            document.getElementById('skembali').innerText = kembali.toLocaleString('id-ID');
            
            // Scroll ke hasil
            document.getElementById('hasil').scrollIntoView({ behavior: 'smooth' });
        }

        // Cetak struk
        function cetak() {
            const strukElement = document.getElementById('struk');
            strukElement.style.display = 'block';
            
            html2canvas(strukElement, {
                scale: 2,
                backgroundColor: '#ffffff'
            }).then(canvas => {
                const link = document.createElement('a');
                const timestamp = new Date().getTime();
                link.download = `struk_tolado_${timestamp}.png`;
                link.href = canvas.toDataURL('image/png');
                link.click();
                
                // Reset tampilan struk
                setTimeout(() => {
                    strukElement.style.display = 'none';
                }, 100);
            });
        }

        // Reset transaksi
        function resetTransaksi() {
            document.getElementById('menu').selectedIndex = 0;
            document.getElementById('bayar').value = '';
            document.getElementById('hasil').classList.add('hidden');
            document.getElementById('struk').style.display = 'none';
            
            // Focus ke select menu
            document.getElementById('menu').focus();
        }

        // Logout
        function logout() {
            document.getElementById('kasir').classList.add('hidden');
            document.getElementById('login').classList.remove('hidden');
            document.getElementById('pass').value = '';
            document.getElementById('user').selectedIndex = 0;
            document.getElementById('user').focus();
        }

        // Event listener untuk Enter key
        document.addEventListener('keypress', function(event) {
            if (event.key === 'Enter') {
                if (!document.getElementById('login').classList.contains('hidden')) {
                    login();
                } else if (!document.getElementById('hasil').classList.contains('hidden')) {
                    cetak();
                } else {
                    proses();
                }
            }
        });

        // Auto focus
        document.getElementById('user').focus();
    </script>
</body>
</html>
