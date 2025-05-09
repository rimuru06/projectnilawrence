<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Drink Store</title>
    <style>
        body { font-family: Arial, sans-serif; padding: 20px; }
        h1 { text-align: center; }
        .product {
            border: 1px solid #ccc;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 10px;
            text-align: center;
        }
        img { width: 100px; height: auto; }
        .order-btn { padding: 10px; background: green; color: white; border: none; cursor: pointer; border-radius: 5px; }
        input[type='number'] { width: 50px; }
        .container { display: flex; justify-content: space-around; flex-wrap: wrap; }
    </style>
</head>
<body>
    <h1>Welcome to Our Drink Store!</h1>

    <div class="container" id="product-list"></div>

    <script>
        let products = [
            {
                name: "Coke 1.5L",
                price: 65,
                stock: 10,
                image: "https://upload.wikimedia.org/wikipedia/commons/9/94/Coca-Cola_Bottle.jpg"
            },
            {
                name: "Sprite 1.5L",
                price: 60,
                stock: 8,
                image: "https://upload.wikimedia.org/wikipedia/commons/0/0c/Sprite_2L.jpg"
            },
            {
                name: "Royal 1.5L",
                price: 60,
                stock: 5,
                image: "https://upload.wikimedia.org/wikipedia/commons/4/47/Royal_Tru-Orange.jpg"
            }
        ];

        function renderProducts() {
            const list = document.getElementById("product-list");
            list.innerHTML = "";
            products.forEach((product, index) => {
                list.innerHTML += `
                    <div class="product">
                        <h3>${product.name}</h3>
                        <img src="${product.image}" alt="${product.name}">
                        <p>Price: ₱${product.price}</p>
                        <p>Stock: <span id="stock-${index}">${product.stock}</span></p>
                        <label>Qty: <input type="number" min="1" max="${product.stock}" id="qty-${index}" value="1"></label>
                        <button class="order-btn" onclick="order(${index})">Order</button>
                    </div>
                `;
            });
        }

        function order(index) {
            let qty = parseInt(document.getElementById(`qty-${index}`).value);
            if (qty > 0 && qty <= products[index].stock) {
                products[index].stock -= qty;
                alert(`You ordered ${qty} of ${products[index].name}.`);
                renderProducts();
            } else {
                alert("Invalid quantity.");
            }
        }

        renderProducts();
    </script>
</body>
</html>
