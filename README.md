<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Excel Electricals Billing Software</title>

<style>
body{
    font-family:Arial,sans-serif;
    background:#f2f4f7;
    margin:0;
    padding:20px;
}
.container{
    max-width:1200px;
    margin:auto;
    background:#fff;
    padding:20px;
    box-shadow:0 0 15px rgba(0,0,0,0.1);
}
.header{
    text-align:center;
    border-bottom:3px solid #0d6efd;
    padding-bottom:10px;
}
.header h1{
    margin:0;
    color:#0d6efd;
}
.row{
    display:flex;
    gap:10px;
    margin:10px 0;
}
input{
    flex:1;
    padding:10px;
}
table{
    width:100%;
    border-collapse:collapse;
    margin-top:15px;
}
table,th,td{
    border:1px solid #ccc;
}
th{
    background:#0d6efd;
    color:white;
}
th,td{
    padding:10px;
    text-align:center;
}
button{
    padding:10px 20px;
    background:#0d6efd;
    color:white;
    border:none;
    cursor:pointer;
    margin:5px;
}
button:hover{
    background:#084298;
}
.summary{
    text-align:right;
    margin-top:20px;
}
.bank{
    margin-top:30px;
    padding:10px;
    border:1px solid #ccc;
}
.signature{
    text-align:right;
    margin-top:40px;
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

<div class="container">

<div class="header">
<h1>EXCEL ELECTRICALS</h1>
<p>2/49 Aluva Munnar Road, Choondy, Edathala - 683112</p>
<p>GSTIN : 32AAGPX3837Q1ZZ</p>
<p>Mob : 7510144188 | 8590259451</p>
<p>Email : excelelectricalswork@gmail.com</p>
</div>

<div class="row">
<input type="text" id="invoiceNo" placeholder="Invoice Number">
<input type="date" id="invoiceDate">
</div>

<div class="row">
<input type="text" id="customer" placeholder="Customer Name">
<input type="text" id="place" placeholder="Place">
</div>

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

<button onclick="addItem()">Add Item</button>
<button onclick="calculateBill()">Calculate Bill</button>
<button onclick="window.print()">Print Invoice</button>

<div class="summary">
<h3>Subtotal : ₹ <span id="subtotal">0.00</span></h3>
<h3>GST (18%) : ₹ <span id="gst">0.00</span></h3>
<h2>Total : ₹ <span id="total">0.00</span></h2>
</div>

<div class="bank">
<h3>Bank Details</h3>
<p><b>EXCEL ELECTRICALS</b></p>
<p>Bank : State Bank Of India</p>
<p>Branch : Asokapuram</p>
<p>A/C No : 43721477418</p>
<p>IFSC : SBIN0008596</p>
</div>

<div class="signature">
<h4>For EXCEL ELECTRICALS</h4>
<br><br>
Authorized Signatory
</div>

</div>

<script>
function addItem(){
let row=`
<tr>
<td><input type="text" class="item"></td>
<td><input type="number" class="qty" value="1"></td>
<td><input type="number" class="rate" value="0"></td>
<td class="amount">0.00</td>
</tr>
`;
document.getElementById("items")
.insertAdjacentHTML("beforeend",row);
}

function calculateBill(){
let subtotal=0;

document.querySelectorAll("#items tr").forEach(row=>{

let qty=parseFloat(row.querySelector(".qty").value)||0;
let rate=parseFloat(row.querySelector(".rate").value)||0;

let amount=qty*rate;

row.querySelector(".amount").innerText=
amount.toFixed(2);

subtotal+=amount;
});

let gst=subtotal*0.18;
let total=subtotal+gst;

document.getElementById("subtotal").innerText=
subtotal.toFixed(2);

document.getElementById("gst").innerText=
gst.toFixed(2);

document.getElementById("total").innerText=
total.toFixed(2);
}

addItem();

document.getElementById("invoiceDate").value =
new Date().toISOString().split("T")[0];

document.getElementById("invoiceNo").value =
"INV-" + Date.now().toString().slice(-5);
</script>

</body>
</html>
