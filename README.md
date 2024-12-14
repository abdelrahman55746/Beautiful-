<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>السلة - Beautiful Store</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
    <style>
        /* نفس التنسيق السابق مع إضافة التعديلات المطلوبة */
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
            margin: 0;
            padding: 0;
        }

        .top-bar {
            background-color: #0056b3;
            color: #fff;
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .top-bar .logo {
            font-size: 24px;
            font-weight: bold;
        }

        .top-bar .cart {
            position: relative;
            font-size: 20px;
            cursor: pointer;
        }

        .top-bar .cart i {
            color: #fff;
        }

        .top-bar .cart .cart-count {
            position: absolute;
            top: -5px;
            right: -10px;
            background-color: #ff5733;
            color: #fff;
            font-size: 12px;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            display: flex;
            flex-direction: row;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .sidebar {
            width: 20%;
            background: #003d80;
            color: #fff;
            padding: 20px;
            height: 100vh;
        }

        .sidebar a {
            color: #fff;
            text-decoration: none;
            display: block;
            margin: 10px 0;
            font-size: 18px;
            transition: transform 0.3s ease, background-color 0.3s ease;
        }

        .sidebar a:hover {
            background: #002a5c;
            padding: 5px;
            transform: scale(1.05);
        }

        .main-content {
            width: 80%;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .product {
            display: flex;
            justify-content: space-between;
            margin: 10px 0;
            padding: 10px;
            background: #f9f9f9;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .product img {
            width: 150px;
            height: auto;
            border-radius: 8px;
        }

        .product button {
            background-color: #0056b3;
            color: white;
            padding: 10px 20px;
            font-size: 16px;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }

        .product button:hover {
            background-color: #003d80;
        }

        .featured-products {
            margin-top: 20px;
        }

        .featured-products h2 {
            color: #0056b3;
            font-size: 24px;
        }

        .featured-products .product {
            flex-direction: column;
            align-items: center;
        }

        .featured-products img {
            width: 120px;
            margin-bottom: 10px;
        }

        .cart-modal {
            position: fixed;
            top: 0;
            right: 0;
            width: 300px;
            height: 100%;
            background-color: white;
            box-shadow: -4px 0 8px rgba(0, 0, 0, 0.1);
            transform: translateX(100%);
            transition: transform 0.3s ease-in-out;
            padding: 20px;
            z-index: 999;
        }

        .cart-modal.show {
            transform: translateX(0);
        }

        .cart-modal ul {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .cart-modal li {
            margin: 10px 0;
            color: #333;
        }

        .cart-modal .remove-btn {
            color: #ff0000;
            cursor: pointer;
            font-size: 14px;
        }

        .cart-modal .remove-btn:hover {
            text-decoration: underline;
        }

        .reviews-section {
            margin-top: 20px;
            padding: 20px;
            background-color: #f4f4f4;
            border-radius: 8px;
        }

        .reviews-section h2 {
            font-size: 20px;
            color: #0056b3;
        }

        .add-review {
            margin-top: 10px;
        }

        .add-review .rating span {
            font-size: 24px;
            cursor: pointer;
            transition: transform 0.3s ease, color 0.3s ease;
        }

        .add-review .rating span.active {
            color: #ffcc00;
        }

        .rating span:hover {
            transform: scale(1.2); /* تكبير النجم عند التفاعل */
            color: #ffcc00; /* تغيير اللون عند المرور فوق النجمة */
        }

        .review-item {
            margin-top: 10px;
            padding: 10px;
            background-color: #fff;
            border-radius: 5px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .review-item .stars {
            color: #ffcc00;
        }

        /* تأثير إضافة إلى السلة */
        @keyframes add-to-cart-animation {
            0% {
                transform: scale(1);
                opacity: 1;
            }
            50% {
                transform: scale(1.2);
                opacity: 0.8;
            }
            100% {
                transform: scale(1);
                opacity: 1;
            }
        }

        .cart .added {
            animation: add-to-cart-animation 0.5s ease-out;
        }

        /* تأثير عند إرسال المراجعة */
        .review-submitted {
            background-color: #4CAF50;
            color: white;
            padding: 10px;
            border-radius: 5px;
            margin-top: 20px;
            animation: submit-review 0.5s ease-out;
        }

        @keyframes submit-review {
            0% {
                opacity: 0;
                transform: translateY(-20px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }
    </style>
</head>
<body>
    <div class="top-bar">
        <div class="logo">Beautiful Store</div>
        <div class="cart" onclick="toggleCartModal()">
            <i class="fas fa-shopping-cart"></i>
            <span class="cart-count" id="cartCount">0</span>
        </div>
    </div>

    <div class="container">
        <div class="sidebar">
            <a href="#">الرئيسية</a>
            <a href="hoodie-real-madrid.html">تيشرت الأهلي</a>
            <a href="hoodie-barcelona.html">تيشرت النصر السعودي</a>
            <a href="#">الدفع</a>
            <a href="login.html">تسجيل الدخول/التسجيل</a>
        </div>

        <div class="main-content">
            <h1>أهلاً بكم في Beautiful Store</h1>

            <!-- المنتجات الرئيسية -->
            <div class="product">
                <img src="hoodie-real-madrid.jpg" alt="تيشرت الأهلي">
                <div>
                    <h3>تيشرت الأهلي</h3>
                    <p>400 جنيه</p>
                    <button onclick="addToCart('تيشرت الأهلي', 400)">إضافة إلى السلة</button>
                    <select>
                        <option value="M">ميديم</option>
                        <option value="L">لارج</option>
                        <option value="XL">اكس لارج</option>
                    </select>
                </div>
            </div>

            <div class="product">
                <img src="hoodie-barcelona.jpg" alt="تيشرت النصر السعودي">
                <div>
                    <h3>تيشرت النصر السعودي</h3>
                    <p>500 جنيه</p>
                    <button onclick="addToCart('تيشرت النصر السعودي', 500)">إضافة إلى السلة</button>
                    <select>
                        <option value="M">ميديم</option>
                        <option value="L">لارج</option>
                        <option value="XL">اكس لارج</option>
                    </select>
                </div>
            </div>

            <!-- قسم المراجعات لتيشرت الأهلي -->
            <div class="reviews-section" data-product-id="t-shirt-ahly">
                <h2>آراء العملاء - تيشرت الأهلي</h2>

                <div id="reviewsContainer-t-shirt-ahly">
                    <p>لم يتم إضافة مراجعات بعد.</p>
                </div>

                <div class="add-review">
                    <h3>إضافة مراجعة</h3>
                    <div class="rating">
                        <span data-value="5" onclick="setRating(5)">&#9733;</span>
                        <span data-value="4" onclick="setRating(4)">&#9733;</span>
                        <span data-value="3" onclick="setRating(3)">&#9733;</span>
                        <span data-value="2" onclick="setRating(2)">&#9733;</span>
                        <span data-value="1" onclick="setRating(1)">&#9733;</span>
                    </div>
                    <textarea id="reviewText-t-shirt-ahly" placeholder="اكتب رأيك هنا..." rows="4"></textarea>
                    <button onclick="submitReview('t-shirt-ahly')">إرسال</button>
                </div>
            </div>

            <!-- قسم المراجعات لتيشرت النصر السعودي -->
            <div class="reviews-section" data-product-id="t-shirt-nassr">
                <h2>آراء العملاء - تيشرت النصر السعودي</h2>

                <div id="reviewsContainer-t-shirt-nassr">
                    <p>لم يتم إضافة مراجعات بعد.</p>
                </div>

                <div class="add-review">
                    <h3>إضافة مراجعة</h3>
                    <div class="rating">
                        <span data-value="5" onclick="setRating(5)">&#9733;</span>
                        <span data-value="4" onclick="setRating(4)">&#9733;</span>
                        <span data-value="3" onclick="setRating(3)">&#9733;</span>
                        <span data-value="2" onclick="setRating(2)">&#9733;</span>
                        <span data-value="1" onclick="setRating(1)">&#9733;</span>
                    </div>
                    <textarea id="reviewText-t-shirt-nassr" placeholder="اكتب رأيك هنا..." rows="4"></textarea>
                    <button onclick="submitReview('t-shirt-nassr')">إرسال</button>
                </div>
            </div>
        </div>
    </div>

    <!-- السلة المنبثقة -->
    <div class="cart-modal" id="cartModal">
        <h3>السلة</h3>
        <ul id="cartList"></ul>
        <button onclick="toggleCartModal()">إغلاق</button>
    </div>

    <script>
        // JavaScript code for the cart and reviews functionality
        let cartItems = [];

        // إضافة المنتج إلى السلة
        function addToCart(item, price) {
            cartItems.push({ item, price });
            document.getElementById("cartCount").innerText = cartItems.length;
            updateCart();

            // إضافة تأثير عند إضافة المنتج إلى السلة
            const cartIcon = document.querySelector(".cart i");
            cartIcon.classList.add("added");

            // إزالة التأثير بعد الإنتهاء
            setTimeout(() => {
                cartIcon.classList.remove("added");
            }, 500);
        }

        // تحديث قائمة السلة
        function updateCart() {
            const cartList = document.getElementById("cartList");
            cartList.innerHTML = '';
            cartItems.forEach(item => {
                const li = document.createElement("li");
                li.innerHTML = `${item.item} - ${item.price} جنيه <span class="remove-btn" onclick="removeFromCart('${item.item}')">حذف</span>`;
                cartList.appendChild(li);
            });
        }

        // إزالة منتج من السلة
        function removeFromCart(item) {
            cartItems = cartItems.filter(cartItem => cartItem.item !== item);
            document.getElementById("cartCount").innerText = cartItems.length;
            updateCart();
        }

        // فتح وإغلاق السلة
        function toggleCartModal() {
            const cartModal = document.getElementById("cartModal");
            cartModal.classList.toggle('show');
        }

        // نظام التقييم
        let currentRating = 0;

        function setRating(value) {
            currentRating = value;
            const stars = document.querySelectorAll('.rating span');
            
            stars.forEach(star => {
                if (star.dataset.value <= value) {
                    star.classList.add('active');
                } else {
                    star.classList.remove('active');
                }
            });
        }

        // حفظ المراجعة
        function saveReview(productId, review) {
            localStorage.setItem(productId, JSON.stringify(review));
        }

        // عرض المراجعات
        function displayReviews(productId) {
            const reviewsContainer = document.getElementById(`reviewsContainer-${productId}`);
            const savedReview = JSON.parse(localStorage.getItem(productId));
            if (savedReview) {
                reviewsContainer.innerHTML = `
                    <div class="review-item">
                        <div class="stars">${'★'.repeat(savedReview.rating)}</div>
                        <p>${savedReview.text}</p>
                    </div>
                `;
            }
        }

        // إرسال المراجعة
        function submitReview(productId) {
            const reviewText = document.getElementById(`reviewText-${productId}`).value;
            if (!currentRating || !reviewText.trim()) {
                alert('يرجى إضافة تقييم وكتابة مراجعة.');
                return;
            }

            const review = {
                rating: currentRating,
                text: reviewText.trim(),
                date: new Date().toLocaleDateString(),
            };

            saveReview(productId, review);
            displayReviews(productId);
            resetReviewForm(productId);

            // إضافة تأثير بعد إرسال المراجعة
            const reviewSection = document.querySelector('.add-review');
            const reviewMessage = document.createElement('div');
            reviewMessage.classList.add('review-submitted');
            reviewMessage.textContent = 'تم إرسال المراجعة بنجاح!';
            reviewSection.appendChild(reviewMessage);

            // إزالة الرسالة بعد 3 ثواني
            setTimeout(() => {
                reviewMessage.remove();
            }, 3000);
        }

        // إعادة ضبط النموذج بعد إرسال المراجعة
        function resetReviewForm(productId) {
            document.getElementById(`reviewText-${productId}`).value = '';
            currentRating = 0;
            const stars = document.querySelectorAll('.rating span');
            stars.forEach(star => {
                star.classList.remove('active');
            });
        }
        
        // عرض المراجعات عند تحميل الصفحة
        document.addEventListener('DOMContentLoaded', function () {
            displayReviews('t-shirt-ahly');
            displayReviews('t-shirt-nassr');
        });
    </script>
</body>
</html>
