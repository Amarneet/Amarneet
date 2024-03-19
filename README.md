- 👋 Hi, I’m @Amarneet 210997029
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Amarneet/Amarneet is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shopping Site</title>
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Architects+Daughter&family=Quintessential&family=Supermercado+One&display=swap" rel="stylesheet">
   
</head>
<body>
    <h1>Shopping Site</h1>
    
    <div id="Shopping"> 
    </div> 
    <table class="chair"> 
        <thead id="thead" class="change">
            <tr><th>Name</th><th>Image</th><th>Quantity</th><th>Price</th>
                <th>Remove</th></tr>
        </thead>
        <tbody id="tbody"> </tbody>
        <tfoot id="tfoot"></tfoot>
        <hr>
    </table>
    </div>  
    <script src="index.js"></script>
</body>
</html>


/* for style */
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Quintessential', 'cursive';
    font-size: 25px;
    font-weight: bold;
}
h1{
    text-align: center;
    font-size: 45px;
    padding: 10px;
    color: teal;
}
.btn
{
   
    background-color: coral;
    padding: 10px;
    font-size: 20px;
    border: none;
    cursor: pointer;
    text-align: center;
     
}
.btn:hover
{
    color:white;
    padding: 15px;
    font-weight: bold;
    background-color: cornflowerblue;
} 
div{
    display: inline-block;
    line-height: 30px;

}
#Shopping
    {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-evenly;
        border-bottom: 4px solid maroon;
    }
    .Child {
        padding: 10px;
        width:350px;
        text-align: center;
        font-size: 20px;
        
        
    }
    .Child img 
    {
        height:250px;
        width: 100%;
        object-fit: cover;
    }
    .Child img:hover
    {
        padding: 10px;
        object-fit: cover;
    }
.change{
    display: none;
    width: 100%;;
}
.chair
{
    width: 100%;
}
 /* for js */
 var product = [
    {
        id: 1,
        name: "T-Shirt",
        price: 400,
        image: "images/t-shirt.jpeg",
        quantity: 1
    },
    {
        id: 2,
        name: "T-Shirt",
        price: 650,
        image: "images/t-shirt2.jpeg",
        quantity: 1
    },
    {
        id: 3,
        name: "shirt",
        price: 300,
        image: "images/shirt.jpeg",
        quantity: 1
    },
    {
        id: 4,
        name: "shirt",
        price: 500,
        image: "images/shirt2.jpeg",
        quantity: 1
    },
    {
        id: 5,
        name: "Jeans",
        price: 800,
        image: "images/jeans.jpeg",
        quantity: 1
    },
    {
        id: 6,
        name: "Jeans",
        price: 1400,
        image: "images/jeans2.jpeg",
        quantity: 1
    },
    {
        id: 7,
        name: "jacket",
        price: 2400,
        image: "images/jacket.jpeg",
        quantity: 1
    },
    {
        id: 8,
        name: "jacket",
        price: 4500,
        image: "images/jacket2.jpeg",
        quantity: 1
    },
]


let total = 0;
// var i = 0;
var CartData = [];
var cartItem = document.getElementById('Shopping');
for (var i in product) {
    var pro = document.createElement("div");
    tbl = `<div class="Child"><h3>${product[i].name}</h3>
    <img src="${product[i].image}">
    <p> ${"Price:$" + product[i].price}</p>
    <button class= "btn"onclick="AddToCart(${product[i].id})">ADD To Cart</button>
    </div>`;
    pro.innerHTML = tbl;
    cartItem.appendChild(pro);
}


function showData(pro) {
    var thead = document.getElementById('thead');
    thead.classList.remove("change");
    var tbody = document.getElementById("tbody");
    const row = document.createElement('tr');
    row.id = "row" + pro.id;

    var showrow = "";
    var deleteRow = "";

    showrow = `<td>${pro.name}</td>
     <td> <img src="${pro.image}" width="200px" height="150px"></td>
     <td><input type="number" min="0" oninput="this.value=Math.abs(this.value) "value="${pro.quantity}" id="Cart${pro.id}" onchange ="PriceShow(${pro.id},${pro.price})"></td>
     <td>${"Price:$" + pro.price}</td>
     <td id="pro${pro.id}" class = " totalPrice change" onchange = "totalPrice(${pro.id})">${pro.price}</td>
     <td><i class="fa fa-trash-o" onclick="RemoveItem(${pro.id})"style="font-size:48px;color:red"></i></td>`;

    row.innerHTML = showrow;
    tbody.appendChild(row);

    tfoot = document.getElementById("tfoot");
    tfoot.classList.remove("change");

    deleteRow = `<br><tr><td rowspan="2">Total Price:$<span id="total"></span></td>
      <td><input type="button" id="del" value="PurChase" class="btn" onclick="payNow()"></td></tr>`;
    tfoot.innerHTML = deleteRow;
    totalPrice();
}
function AddToCart(id) {

    let pro = product.find(e => {
        return e.id == id;
    });
    if (!CartData.includes(pro)) {
        CartData.push(pro);

    }
    else {
        var quan = document.getElementById("Cart"+pro.id);
        // console.log(quan)
        quan.value = Number(quan.value)+1;
        PriceShow(pro.id, pro.price);
        return;
    }
    showData(pro);
}

function RemoveItem(id) {
    CartData = CartData.filter(e => {
        return e.id != id;
    });
    if (CartData.length == 0) 
    {
        document.getElementById('row' + id).remove();
        document.getElementById("thead").classList.add("change");
        document.getElementById("tfoot").classList.add("change");
    }
    else 
    {
        document.getElementById("row" + id).remove();
       
    }
    totalPrice();

}
function PriceShow(id, price) {
    let qp = document.getElementById(`Cart${id}`);
    qp = Math.abs(qp.value);
    document.getElementById(`pro${id}`).innerHTML = qp * price;
    totalPrice();
}

function totalPrice() {
    let price = document.getElementsByClassName('totalPrice');
    total = 0;
    for (let j = 0; j < price.length; j++) {
        total += +price[j].innerHTML;
    }
    document.getElementById('total').innerHTML = total;
}
function payNow() {
    alert("Thanks to Purchase!");
    location.reload();
}
