<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Toko Online Modern</title>
    <link rel="manifest" href="manifest.json">
    <style>
        :root {
            --bg: #f5f5f5;
            --bgCard: #fff;
            --text: #333;
            --main: #2c3e50;
            --mainLight: #ecf0f1;
            --danger: #e74c3c;
            --dangerHover: #c0392b;
            --success: #229954;
            --toast: #222d3d;
            --accent: #e67e22;
        }
        body.dark {
            --bg: #181c20;
            --bgCard: #23272e;
            --text: #eaeaea;
            --main: #8ab4f8;
            --mainLight: #31373e;
            --danger: #ff7070;
            --dangerHover: #d64b4b;
            --success: #4fd675;
            --toast: #eaeaea;
            --accent: #f39c12;
        }
        body {
            background-color: var(--bg);
            padding: 0;
            margin: 0;
            color: var(--text);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            transition: background 0.3s, color 0.3s;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 15px;
        }
        header {
            background-color: var(--bgCard);
            padding: 15px 0;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .logo {
            font-size: 1.8rem;
            font-weight: bold;
            color: var(--main);
        }
        .nav-icons {
            display: flex;
            gap: 15px;
            align-items: center;
        }
        .icon-btn {
            background: none;
            border: none;
            color: var(--text);
            font-size: 1.2rem;
            cursor: pointer;
            position: relative;
        }
        .cart-count {
            position: absolute;
            top: -8px;
            right: -8px;
            background: var(--danger);
            color: white;
            border-radius: 50%;
            width: 18px;
            height: 18px;
            font-size: 0.7rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .search-bar {
            display: flex;
            margin: 20px 0;
        }
        #search-input {
            flex: 1;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 4px 0 0 4px;
            font-size: 16px;
            background: var(--bg);
            color: var(--text);
        }
        #search-btn {
            padding: 12px 20px;
            background-color: var(--main);
            color: white;
            border: none;
            border-radius: 0 4px 4px 0;
            cursor: pointer;
        }
        .categories {
            display: flex;
            gap: 10px;
            margin: 20px 0;
            overflow-x: auto;
            padding-bottom: 10px;
        }
        .category-btn {
            padding: 8px 15px;
            background-color: var(--mainLight);
            border: none;
            border-radius: 20px;
            cursor: pointer;
            white-space: nowrap;
            color: var(--text);
        }
        .category-btn.active {
            background-color: var(--main);
            color: white;
        }
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }
        .product-card {
            background-color: var(--bgCard);
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            transition: transform 0.3s;
        }
        .product-card:hover {
            transform: translateY(-5px);
        }
        .product-image {
            width: 100%;
            height: 180px;
            object-fit: cover;
            background-color: #f0f0f0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            color: #666;
        }
        .product-info {
            padding: 15px;
        }
        .product-title {
            font-weight: bold;
            margin-bottom: 5px;
            font-size: 1.1rem;
        }
        .product-price {
            color: var(--accent);
            font-weight: bold;
            font-size: 1.2rem;
            margin: 10px 0;
        }
        .product-rating {
            color: #f1c40f;
            margin-bottom: 10px;
        }
        .add-to-cart-btn {
            width: 100%;
            padding: 10px;
            background-color: var(--main);
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
        }
        .cart-sidebar {
            position: fixed;
            top: 0;
            right: -400px;
            width: 100%;
            max-width: 400px;
            height: 100vh;
            background-color: var(--bgCard);
            box-shadow: -2px 0 10px rgba(0,0,0,0.1);
            transition: right 0.3s;
            z-index: 1000;
            display: flex;
            flex-direction: column;
        }
        .cart-sidebar.open {
            right: 0;
        }
        .cart-header {
            padding: 20px;
            border-bottom: 1px solid #eee;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .cart-title {
            font-size: 1.3rem;
            font-weight: bold;
        }
        .close-cart {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--text);
        }
        .cart-items {
            flex: 1;
            overflow-y: auto;
            padding: 15px;
        }
        .cart-item {
            display: flex;
            margin-bottom: 15px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        .cart-item-image {
            width: 80px;
            height: 80px;
            object-fit: cover;
            border-radius: 4px;
            background-color: #f0f0f0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            color: #666;
        }
        .cart-item-details {
            flex: 1;
            padding: 0 15px;
        }
        .cart-item-title {
            font-weight: bold;
            margin-bottom: 5px;
        }
        .cart-item-price {
            color: var(--accent);
            font-weight: bold;
        }
        .cart-item-quantity {
            display: flex;
            align-items: center;
            margin-top: 5px;
        }
        .quantity-btn {
            width: 25px;
            height: 25px;
            background: var(--mainLight);
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .quantity-input {
            width: 40px;
            text-align: center;
            margin: 0 5px;
            border: 1px solid #ddd;
            border-radius: 4px;
            padding: 2px;
        }
        .remove-item {
            background: none;
            border: none;
            color: var(--danger);
            cursor: pointer;
            font-size: 1.2rem;
        }
        .cart-footer {
            padding: 20px;
            border-top: 1px solid #eee;
        }
        .cart-total {
            display: flex;
            justify-content: space-between;
            font-size: 1.2rem;
            font-weight: bold;
            margin-bottom: 15px;
        }
        .checkout-btn {
            width: 100%;
            padding: 12px;
            background-color: var(--success);
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: bold;
        }
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 999;
            display: none;
        }
        .overlay.active {
            display: block;
        }
        .toast {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: var(--toast);
            color: #fff;
            padding: 12px 26px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.11);
            opacity: 0;
            z-index: 999;
            font-size: 1rem;
            pointer-events: none;
            transition: opacity 0.4s, bottom 0.4s;
        }
        .toast.show {
            opacity: 1;
            pointer-events: auto;
            bottom: 50px;
        }
        footer {
            background-color: var(--bgCard);
            padding: 30px 0;
            margin-top: 40px;
            text-align: center;
            border-top: 1px solid #eee;
        }
        @media (max-width: 768px) {
            .products-grid {
                grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            }
            .cart-sidebar {
                max-width: 100%;
            }
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(12px);}
            to { opacity: 1; transform: none;}
        }
    </style>
</head>
<body>
    <div class="overlay" id="overlay"></div>
    
    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo">TokoKu</div>
                <div class="nav-icons">
                    <button class="icon-btn" id="toggle-dark-btn" title="Dark/Light mode">🌙</button>
                    <button class="icon-btn" id="cart-btn" title="Keranjang">
                        🛒
                        <span class="cart-count" id="cart-count">0</span>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <main class="container">
        <div class="search-bar">
            <input type="text" id="search-input" placeholder="Cari produk...">
            <button id="search-btn">Cari</button>
        </div>

        <div class="categories">
            <button class="category-btn active" data-category="all">Semua</button>
            <button class="category-btn" data-category="elektronik">Elektronik</button>
            <button class="category-btn" data-category="fashion">Fashion</button>
            <button class="category-btn" data-category="makanan">Makanan</button>
            <button class="category-btn" data-category="rumah-tangga">Rumah Tangga</button>
            <button class="category-btn" data-category="olahraga">Olahraga</button>
        </div>

        <div class="products-grid" id="products-grid">
            <!-- Produk akan diisi oleh JavaScript -->
        </div>
    </main>

    <div class="cart-sidebar" id="cart-sidebar">
        <div class="cart-header">
            <div class="cart-title">Keranjang Belanja</div>
            <button class="close-cart" id="close-cart">×</button>
        </div>
        <div class="cart-items" id="cart-items">
            <!-- Item keranjang akan diisi oleh JavaScript -->
        </div>
        <div class="cart-footer">
            <div class="cart-total">
                <span>Total:</span>
                <span id="cart-total">Rp 0</span>
            </div>
            <button class="checkout-btn" id="checkout-btn">Checkout</button>
        </div>
    </div>

    <footer>
        <div class="container">
            <p>&copy; 2023 TokoKu - Toko Online Modern. All rights reserved.</p>
        </div>
    </footer>

    <div class="toast" id="toast"></div>

    <script>
        // Fungsi untuk menghasilkan gambar placeholder SVG berdasarkan nama produk
        function generateProductImage(name, category) {
            // Warna latar belakang berdasarkan kategori
            const colors = {
                elektronik: '#e3f2fd',
                fashion: '#fce4ec',
                makanan: '#fff3e0',
                'rumah-tangga': '#e8f5e9',
                olahraga: '#e0f2f1'
            };
            
            const bgColor = colors[category] || '#f5f5f5';
            const textColor = '#666';
            
            // Buat SVG inline sebagai gambar placeholder
            const svg = `
                <svg xmlns="http://www.w3.org/2000/svg" width="300" height="200" viewBox="0 0 300 200">
                    <rect width="300" height="200" fill="${bgColor}"/>
                    <text x="150" y="100" text-anchor="middle" dy=".3em" font-family="Arial, sans-serif" font-size="16" fill="${textColor}">
                        ${name}
                    </text>
                    <text x="150" y="130" text-anchor="middle" dy=".3em" font-family="Arial, sans-serif" font-size="12" fill="${textColor}">
                        ${category}
                    </text>
                </svg>
            `;
            
            // Konversi SVG ke data URL
            return 'data:image/svg+xml;base64,' + btoa(svg);
        }

        // Data produk dengan gambar SVG inline
        const products = [
            {
                id: 1,
                name: "Smartphone X",
                price: 2999000,
                category: "elektronik",
                image: generateProductImage("Smartphone X", "elektronik"),
                rating: 4.5,
                description: "Smartphone canggih dengan kamera terbaru"
            },
            {
                id: 2,
                name: "Laptop Pro",
                price: 8999000,
                category: "elektronik",
                image: generateProductImage("Laptop Pro", "elektronik"),
                rating: 4.8,
                description: "Laptop untuk produktivitas tinggi"
            },
            {
                id: 3,
                name: "Kaos Polos",
                price: 89900,
                category: "fashion",
                image: generateProductImage("Kaos Polos", "fashion"),
                rating: 4.2,
                description: "Kaos polos nyaman untuk sehari-hari"
            },
            {
                id: 4,
                name: "Sepatu Running",
                price: 499000,
                category: "olahraga",
                image: generateProductImage("Sepatu Running", "olahraga"),
                rating: 4.6,
                description: "Sepatu lari dengan teknologi terbaru"
            },
            {
                id: 5,
                name: "Blender Multifungsi",
                price: 350000,
                category: "rumah-tangga",
                image: generateProductImage("Blender Multifungsi", "rumah-tangga"),
                rating: 4.3,
                description: "Blender untuk berbagai keperluan dapur"
            },
            {
                id: 6,
                name: "Snack Box",
                price: 75000,
                category: "makanan",
                image: generateProductImage("Snack Box", "makanan"),
                rating: 4.7,
                description: "Kumpulan snack pilihan dalam satu box"
            },
            {
                id: 7,
                name: "Headphone Wireless",
                price: 450000,
                category: "elektronik",
                image: generateProductImage("Headphone Wireless", "elektronik"),
                rating: 4.4,
                description: "Headphone nirkabel dengan kualitas suara tinggi"
            },
            {
                id: 8,
                name: "Jaket Hoodie",
                price: 199000,
                category: "fashion",
                image: generateProductImage("Jaket Hoodie", "fashion"),
                rating: 4.1,
                description: "Jaket hoodie nyaman untuk cuaca dingin"
            }
        ];

        // State aplikasi
        let cart = JSON.parse(localStorage.getItem('cart')) || [];
        let currentCategory = 'all';
        let searchTerm = '';

        // DOM Elements
        const productsGrid = document.getElementById('products-grid');
        const cartSidebar = document.getElementById('cart-sidebar');
        const cartItems = document.getElementById('cart-items');
        const cartCount = document.getElementById('cart-count');
        const cartTotal = document.getElementById('cart-total');
        const cartBtn = document.getElementById('cart-btn');
        const closeCart = document.getElementById('close-cart');
        const overlay = document.getElementById('overlay');
        const categoryBtns = document.querySelectorAll('.category-btn');
        const searchInput = document.getElementById('search-input');
        const searchBtn = document.getElementById('search-btn');
        const checkoutBtn = document.getElementById('checkout-btn');
        const toggleDarkBtn = document.getElementById('toggle-dark-btn');
        const toast = document.getElementById('toast');

        // Fungsi untuk menampilkan produk
        function renderProducts() {
            productsGrid.innerHTML = '';
            
            const filteredProducts = products.filter(product => {
                const matchesCategory = currentCategory === 'all' || product.category === currentCategory;
                const matchesSearch = product.name.toLowerCase().includes(searchTerm.toLowerCase()) || 
                                     product.description.toLowerCase().includes(searchTerm.toLowerCase());
                return matchesCategory && matchesSearch;
            });

            if (filteredProducts.length === 0) {
                productsGrid.innerHTML = '<p style="grid-column: 1/-1; text-align: center; padding: 40px;">Tidak ada produk yang ditemukan.</p>';
                return;
            }

            filteredProducts.forEach(product => {
                const productCard = document.createElement('div');
                productCard.className = 'product-card';
                productCard.innerHTML = `
                    <div class="product-image">
                        <img src="${product.image}" alt="${product.name}" style="width: 100%; height: 100%; object-fit: cover;" onerror="this.src='${generateProductImage(product.name, product.category)}'">
                    </div>
                    <div class="product-info">
                        <div class="product-title">${product.name}</div>
                        <div class="product-rating">${'★'.repeat(Math.floor(product.rating))}${'☆'.repeat(5-Math.floor(product.rating))} ${product.rating}</div>
                        <div class="product-price">Rp ${product.price.toLocaleString('id-ID')}</div>
                        <button class="add-to-cart-btn" data-id="${product.id}">Tambah ke Keranjang</button>
                    </div>
                `;
                productsGrid.appendChild(productCard);
            });

            // Tambah event listener untuk tombol tambah ke keranjang
            document.querySelectorAll('.add-to-cart-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.dataset.id);
                    addToCart(productId);
                });
            });
        }

        // Fungsi untuk menambah produk ke keranjang
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const existingItem = cart.find(item => item.id === productId);
            
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({
                    id: product.id,
                    name: product.name,
                    price: product.price,
                    image: product.image,
                    quantity: 1
                });
            }
            
            updateCart();
            showToast(`${product.name} ditambahkan ke keranjang`);
        }

        // Fungsi untuk memperbarui tampilan keranjang
        function updateCart() {
            // Simpan ke localStorage
            localStorage.setItem('cart', JSON.stringify(cart));
            
            // Perbarui jumlah item di ikon keranjang
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            cartCount.textContent = totalItems;
            
            // Perbarui daftar item di sidebar keranjang
            cartItems.innerHTML = '';
            
            if (cart.length === 0) {
                cartItems.innerHTML = '<p style="text-align: center; padding: 20px;">Keranjang belanja kosong</p>';
                cartTotal.textContent = 'Rp 0';
                return;
            }
            
            let totalPrice = 0;
            
            cart.forEach(item => {
                const itemTotal = item.price * item.quantity;
                totalPrice += itemTotal;
                
                const cartItem = document.createElement('div');
                cartItem.className = 'cart-item';
                cartItem.innerHTML = `
                    <div class="cart-item-image">
                        <img src="${item.image}" alt="${item.name}" style="width: 100%; height: 100%; object-fit: cover;" onerror="this.src='${generateProductImage(item.name, 'produk')}'">
                    </div>
                    <div class="cart-item-details">
                        <div class="cart-item-title">${item.name}</div>
                        <div class="cart-item-price">Rp ${item.price.toLocaleString('id-ID')}</div>
                        <div class="cart-item-quantity">
                            <button class="quantity-btn minus" data-id="${item.id}">-</button>
                            <input type="number" class="quantity-input" value="${item.quantity}" min="1" data-id="${item.id}">
                            <button class="quantity-btn plus" data-id="${item.id}">+</button>
                        </div>
                    </div>
                    <button class="remove-item" data-id="${item.id}">×</button>
                `;
                cartItems.appendChild(cartItem);
            });
            
            cartTotal.textContent = `Rp ${totalPrice.toLocaleString('id-ID')}`;
            
            // Tambah event listener untuk tombol di keranjang
            document.querySelectorAll('.quantity-btn.plus').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.dataset.id);
                    updateQuantity(productId, 1);
                });
            });
            
            document.querySelectorAll('.quantity-btn.minus').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.dataset.id);
                    updateQuantity(productId, -1);
                });
            });
            
            document.querySelectorAll('.quantity-input').forEach(input => {
                input.addEventListener('change', (e) => {
                    const productId = parseInt(e.target.dataset.id);
                    const newQuantity = parseInt(e.target.value);
                    if (newQuantity > 0) {
                        setQuantity(productId, newQuantity);
                    } else {
                        e.target.value = 1;
                    }
                });
            });
            
            document.querySelectorAll('.remove-item').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.dataset.id);
                    removeFromCart(productId);
                });
            });
        }

        // Fungsi untuk mengupdate jumlah item
        function updateQuantity(productId, change) {
            const item = cart.find(item => item.id === productId);
            if (item) {
                item.quantity += change;
                if (item.quantity < 1) item.quantity = 1;
                updateCart();
            }
        }

        // Fungsi untuk mengatur jumlah item
        function setQuantity(productId, quantity) {
            const item = cart.find(item => item.id === productId);
            if (item) {
                item.quantity = quantity;
                updateCart();
            }
        }

        // Fungsi untuk menghapus item dari keranjang
        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCart();
            showToast('Produk dihapus dari keranjang');
        }

        // Fungsi untuk menampilkan/sembunyikan keranjang
        function toggleCart() {
            cartSidebar.classList.toggle('open');
            overlay.classList.toggle('active');
        }

        // Fungsi untuk checkout
        function checkout() {
            if (cart.length === 0) {
                showToast('Keranjang belanja kosong');
                return;
            }
            
            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            alert(`Terima kasih! Total pembelian: Rp ${total.toLocaleString('id-ID')}\n\nFitur checkout lengkap akan diimplementasikan lebih lanjut.`);
            
            // Reset keranjang setelah checkout
            cart = [];
            updateCart();
            toggleCart();
        }

        // Fungsi untuk menampilkan toast notifikasi
        function showToast(message) {
            toast.textContent = message;
            toast.classList.add('show');
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        // Fungsi untuk dark mode
        function setDarkMode(on) {
            document.body.classList.toggle('dark', on);
            toggleDarkBtn.textContent = on ? "☀️" : "🌙";
            localStorage.setItem('darkMode', on ? '1' : '0');
        }

        // Event Listeners
        cartBtn.addEventListener('click', toggleCart);
        closeCart.addEventListener('click', toggleCart);
        overlay.addEventListener('click', toggleCart);

        categoryBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                categoryBtns.forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                currentCategory = btn.dataset.category;
                renderProducts();
            });
        });

        searchBtn.addEventListener('click', () => {
            searchTerm = searchInput.value;
            renderProducts();
        });

        searchInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                searchTerm = searchInput.value;
                renderProducts();
            }
        });

        checkoutBtn.addEventListener('click', checkout);

        toggleDarkBtn.addEventListener('click', () => {
            setDarkMode(!document.body.classList.contains('dark'));
        });

        // Inisialisasi
        setDarkMode(localStorage.getItem('darkMode') === '1');
        renderProducts();
        updateCart();

        // Service Worker untuk PWA
        if ('serviceWorker' in navigator) {
            window.addEventListener('load', () => {
                navigator.serviceWorker.register('/sw.js')
                    .then((registration) => {
                        console.log('SW registered: ', registration);
                    })
                    .catch((registrationError) => {
                        console.log('SW registration failed: ', registrationError);
                    });
            });
        }
    </script>
</body>
</html>
