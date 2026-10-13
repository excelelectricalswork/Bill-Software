<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">

<title>Excel Electricals Billing Software</title>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Segoe UI,sans-serif;
}

body{
background:#f2f5f9;
}

.header{
background:#0b3d91;
color:white;
padding:20px;
text-align:center;
}

.container{
max-width:1200px;
margin:auto;
padding:15px;
}

.card{
background:white;
padding:15px;
margin-bottom:15px;
border-radius:10px;
box-shadow:0 2px 10px rgba(0,0,0,.1);
}

.row{
display:flex;
gap:10px;
flex-wrap:wrap;
}

input{
padding:10px;
flex:1;
min-width:150px;
}

button{
padding:10px 20px;
border:none;
background:#0b3d91;
color:white;
cursor:pointer;
border-radius:5px;
}

table{
width:100%;
border-collapse:collapse;
margin-top:10px;
}

table th{
background:#0b3d91;
color:white;
}

table th,
table td{
border:1px solid #ddd;
padding:8px;
text-align:center;
}

.summary{
text-align:right;
margin-top:20px;
}

.bank{
margin-top:20px;
line-height:28px;
}

.signature{
text-align:right;
margin-top:50px;
}

@media print{
button{
display:none;
}
body{
background:white;
}
}
</style>

</head>
<body>

<div class="header">

<h1>EXCEL ELECTRICALS</h1>

<p>
2/49 Aluva Munnar Road,
Choondy, Edathala - 683112
</p>

<p>GSTIN : 32AAGPX3837Q1ZZ</p>

<p>Mob : 7510144188, 8590259451</p>

<p>Email : excelelectricalswork@gmail.com</p>

</div>

<div class="container">

<div class="card">

<div class="row">

<input id="invoice"
readonly>

<input id="date"
type="date">

</div>

<br>

<div class="row">

<input id="customer"
placeholder="Customer Name">

<input id="phone"
placeholder="Mobile">

</div>

</div>

<div class="card">

<h2>Invoice Items</h2>

<table>

<thead>
<tr>
<th>Item</th>
<th>Qty</th>
<th>Rate</th>
<th>Amount</th>
</tr>
</thead>

<tbody id="items"></tbody>

</table>

<br>

<button onclick="addRow()">
Add Item
</button>

<button onclick="calculateBill()">
Calculate
</button>

<button onclick="window.print()">
Print Bill
</button>

</div>

<div class="card summary">

<h3>Subtotal : ₹ <span id="subtotal">0.00</span></h3>

<h3>CGST 9% : ₹ <span id="cgst">0.00</span></h3>

<h3>SGST 9% : ₹ <span id="sgst">0.00</span></h3>

<h1>Total : ₹ <span id="grand">0.00</span></h1>

</div>

<div class="card bank">

<h3>Bank Details</h3>

<p><b>EXCEL ELECTRICALS</b></p>

<p>Bank : State Bank of India</p>

<p>Branch : Asokapuram</p>

<p>A/C No : 43721477418</p>

<p>IFSC : SBIN0008596</p>

</div>

<div class="card">

<h3>Declaration</h3>

<p>
We declare that this invoice shows the
actual value of goods/services supplied.
</p>

<div class="signature">

<h3>For EXCEL ELECTRICALS</h3>

<br><br>

Authorized Signatory

</div>

</div>

</div>

<script>

document.getElementById("invoice").value =
"INV-" +
Math.floor(Math.random()*90000+10000);

document.getElementById("date").value =
new Date().toISOString().split("T")[0];

function addRow(){

let html = `
<tr>

<td>
<input class="item">
</td>

<td>
<input class="qty"
type="number"
value="1">
</td>

<td>
<input class="rate"
type="number"
value="0">
</td>

<td class="amount">
0.00
</td>

</tr>
`;

document
.getElementById("items")
.insertAdjacentHTML(
"beforeend",
html
);

}

function calculateBill(){

let subtotal=0;

document
.querySelectorAll("#items tr")
.forEach(row=>{

let qty=parseFloat(
row.querySelector(".qty").value
)||0;

let rate=parseFloat(
row.querySelector(".rate").value
)||0;

let amt=qty*rate;

row.querySelector(".amount")
.innerHTML=
amt.toFixed(2);

subtotal+=amt;

});

let cgst=subtotal*0.09;

let sgst=subtotal*0.09;

let total=
subtotal+cgst+sgst;

document.getElementById(
"subtotal"
).innerHTML=
subtotal.toFixed(2);

document.getElementById(
"cgst"
).innerHTML=
cgst.toFixed(2);

document.getElementById(
"sgst"
).innerHTML=
sgst.toFixed(2);

document.getElementById(
"grand"
).innerHTML=
total.toFixed(2);

}

addRow();

</script>

</body>
</html>
