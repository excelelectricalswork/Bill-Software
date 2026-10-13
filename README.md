<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Excel Electricals ERP</title>

style.css
</head>

<body>

<div class="sidebar">
<h2>EXCEL ELECTRICALS</h2>

index.htmlDashboard</a>
invoice.htmlGST Invoice</a>
customers.htmlCustomers</a>
products.htmlProducts</a>
reports.htmlReports</a>
</div>

<div class="content">

<h1>Dashboard</h1>

<div class="cards">

<div class="card">
<h3>Total Sales</h3>
<h2 id="sales">₹0</h2>
</div>

<div class="card">
<h3>Customers</h3>
<h2 id="customers">0</h2>
</div>

<div class="card">
<h3>Products</h3>
<h2 id="products">0</h2>
</div>

</div>

</div>

app.jsscript>

</body>
</html>
body{
margin:0;
font-family:Segoe UI,sans-serif;
background:#f5f7fa;
}

.sidebar{
width:250px;
height:100vh;
position:fixed;
background:#003366;
padding:20px;
}

.sidebar h2{
color:white;
}

.sidebar a{
display:block;
color:white;
text-decoration:none;
padding:10px;
margin-bottom:5px;
background:#004c99;
border-radius:4px;
}

.content{
margin-left:270px;
padding:20px;
}

.cards{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:20px;
}

.card{
background:white;
padding:20px;
border-radius:10px;
box-shadow:0 2px 10px rgba(0,0,0,.1);
}

table{
width:100%;
border-collapse:collapse;
}

table th,table td{
border:1px solid #ddd;
padding:10px;
}

button{
background:#0066cc;
color:white;
padding:10px 20px;
border:none;
cursor:pointer;
}

input{
padding:10px;
width:100%;
margin:5px 0;
}
``
function getData(key){
return JSON.parse(localStorage.getItem(key)) || [];
}

function saveData(key,data){
localStorage.setItem(key,JSON.stringify(data));
}

function createInvoiceNumber(){
return "INV-"+Date.now();
}

console.log(createInvoiceNumber());
<!DOCTYPE html>
<html>
<head>
style.css
</head>

<body>

<div class="content">

<h2>Customer Master</h2>

<input id="name" placeholder="Customer Name">

<button onclick="saveCustomer()">
Save Customer
</button>

<ul id="list"></ul>

</div>

<script>

function saveCustomer(){

let customers=
JSON.parse(localStorage.getItem("customers"))
||[];

customers.push({
name:document.getElementById("name").value
});

localStorage.setItem(
"customers",
JSON.stringify(customers)
);

location.reload();
}

let list=document.getElementById("list");

(JSON.parse(localStorage.getItem("customers"))||[])
.forEach(c=>{

list.innerHTML+=`<li>${c.name}</li>`;

});

</script>

</body>
</html>
<!DOCTYPE html>
<html>
<head>
style.css
</head>

<body>

<div class="content">

<h2>Product Master</h2>

<input id="product" placeholder="Product">

<input id="rate" placeholder="Rate">

<button onclick="saveProduct()">
Save Product
</button>

</div>

<script>

function saveProduct(){

let products=
JSON.parse(localStorage.getItem("products"))
||[];

products.push({
name:product.value,
rate:rate.value
});

localStorage.setItem(
"products",
JSON.stringify(products)
);

alert("Saved");
}

</script>

</body>
</html>
<!DOCTYPE html>
<html>
<head>
style.css
</head>

<body>

<div class="content">

<h1>Tax Invoice</h1>

<input id="customer"
placeholder="Customer Name">

<table>

<tr>
<th>Product</th>
<th>Qty</th>
<th>Rate</th>
<th>Amount</th>
</tr>

<tr>
<td><input id="p"></td>
<td><input id="q"></td>
<td><input id="r"></td>
<td id="amt">0</td>
</tr>

</table>

<button onclick="calc()">
Calculate
</button>

<h3>Total : ₹ <span id="total">0</span></h3>

<button onclick="window.print()">
Print Invoice
</button>

</div>

<script>

function calc(){

let q=
Number(document.getElementById("q").value);

let r=
Number(document.getElementById("r").value);

let a=q*r;

let gst=a*0.18;

document.getElementById("amt")
.innerHTML=a.toFixed(2);

document.getElementById("total")
.innerHTML=(a+gst).toFixed(2);

}

</script>

</body>
</html>
{
  "name":"Excel Electricals Billing",
  "short_name":"Billing",
  "start_url":"./",
  "display":"standalone",
  "background_color":"#ffffff",
  "theme_color":"#003366"
}
self.addEventListener("install",e=>{
console.log("installed");
});
``
git add .
git commit -m "Tally Prime Billing Software"
git push origin 
