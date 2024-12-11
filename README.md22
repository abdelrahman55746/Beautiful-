<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beautiful Store - متجر الهودي والتيشيرت</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        .container {
            width: 80%;
            margin: 20px auto;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .product {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 10px;
            margin: 10px 0;
            background-color: #fff;
            border: 1px solid #ddd;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        .product img {
            width: 100px;
            height: 100px;
            object-fit: cover;
            border-radius: 8px;
        }
        .product-details {
            flex-grow: 1;
            margin-left: 10px;
        }
        .product-details h3 {
            margin: 0;
            color: #333;
        }
        .product-details p {
            margin: 5px 0;
        }
        .form-container {
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            margin-top: 20px;
        }
        form {
            display: flex;
            flex-direction: column;
        }
        form label {
            margin: 10px 0 5px;
        }
        form input,
        form select,
        form button {
            padding: 10px;
            margin: 5px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
        }
        form button {
            background-color: #007bff;
            color: #fff;
            cursor: pointer;
        }
        form button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Beautiful Store - متجر الهودي والتيشيرت</h1>

        <!-- عرض المنتجات -->
        <div id="products">
            <div class="product">
                <img src="hoodie.jpg" alt="هودي">
                <div class="product-details">
                    <h3>هودي</h3>
                    <p>السعر: 350 جنيه</p>
                    <p>الكمية المتوفرة: 50 قطعة</p>
                </div>
            </div>

            <div class="product">
                <img src="tshirt.jpg" alt="تيشيرت">
                <div class="product-details">
                    <h3>تيشيرت</h3>
                    <p>السعر: 200 جنيه</p>
                    <p>الكمية المتوفرة: 50 قطعة</p>
                </div>
            </div>
        </div>

        <!-- نموذج الدفع -->
        <div class="form-container">
            <h2>نموذج الدفع</h2>
            <form action="process_payment.php" method="POST">
                <label for="name">الاسم الكامل:</label>
                <input type="text" id="name" name="name" placeholder="أدخل اسمك" required>

                <label for="email">البريد الإلكتروني:</label>
                <input type="email" id="email" name="email" placeholder="أدخل بريدك الإلكتروني" required>

                <label for="card">رقم البطاقة:</label>
                <input type="text" id="card" name="card" placeholder="أدخل رقم البطاقة" required>

                <label for="expiry">تاريخ انتهاء الصلاحية:</label>
                <input type="text" id="expiry" name="expiry" placeholder="MM/YY" required>

                <label for="cvv">CVV:</label>
                <input type="text" id="cvv" name="cvv" placeholder="أدخل الرقم السري" required>

                <button type="submit">إتمام الدفع</button>
            </form>
        </div>

        <!-- نموذج إضافة المنتجات -->
        <div class="form-container">
            <h2>إضافة منتج جديد</h2>
            <form action="add_product.php" method="POST" enctype="multipart/form-data">
                <label for="product_name">اسم المنتج:</label>
                <input type="text" id="product_name" name="product_name" placeholder="اسم المنتج" required>

                <label for="description">وصف المنتج:</label>
                <input type="text" id="description" name="description" placeholder="وصف المنتج" required>

                <label for="price">السعر:</label>
                <input type="number" id="price" name="price" step="0.01" placeholder="السعر" required>

                <label for="category">الفئة:</label>
                <input type="text" id="category" name="category" placeholder="فئة المنتج" required>

                <label for="stock">الكمية:</label>
                <input type="number" id="stock" name="stock" placeholder="الكمية المتوفرة" required>

                <label for="image">صورة المنتج:</label>
                <input type="file" id="image" name="image" accept="image/*" required>

                <button type="submit">إضافة المنتج</button>
            </form>
        </div>

        <!-- نموذج الشحن -->
        <div class="form-container">
            <h2>تفاصيل الشحن</h2>
            <form action="process_shipping.php" method="POST">
                <label for="address">عنوان الشحن:</label>
                <input type="text" id="address" name="address" placeholder="أدخل عنوان الشحن" required>

                <label for="city">المدينة:</label>
                <input type="text" id="city" name="city" placeholder="أدخل المدينة" required>

                <label for="phone">رقم الهاتف:</label>
                <input type="text" id="phone" name="phone" placeholder="أدخل رقم الهاتف" required>

                <button type="submit">إتمام الشحن</button>
            </form>
        </div>
    </div>
</body>
</html>
