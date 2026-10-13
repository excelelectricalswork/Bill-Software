<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Excel Electricals Billing Software</title>
style.css
</head>
<body>

<div class="invoice">

<div class="header">
<h1>EXCEL ELECTRICALS</h1>
<p>2/49 Aluva Munnar Road, Choondy, Edathala - 683112</p>
<p>GSTIN: 32AAGPX3837Q1ZZ</p>
<p>Mob: 7510144188 | 8590259451</p>
<p>Email: excelelectricalswork@gmail.com</p>
</div>

<div class="customer">
<input id="customer" placeholder="Customer Name">
<input id="invoiceNo" placeholder="Invoice Number">
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

<button onclick="addRow()">Add Item</button>
<button onclick="calculateTotal()">Calculate</button>

<h3>Subtotal ₹ <span id="subtotal">0</span></h3>
<h3>GST 18% ₹ <span id="gst">0</span></h3>
<h2>Total ₹ <span id="total">0</span></h2>

<div class="bank">
<h3>Bank Details</h3>
<p>EXCEL ELECTRICALS</p>
<p>A/C No: 43721477418</p>
<p>IFSC: SBIN0008596</p>
<p>State Bank of India, Asokapuram</p>
</div>

<button onclick="window.print()">Print Invoice</button>

</div>

<script src="appbody>
</html>
body{
font-family:Arial;
background:#f4f4f4;
margin:20px;
}

.invoice{
background:white;
padding:20px;
max-width:1000px;
margin:auto;
}

.header{
text-align:center;
}

table{
width:100%;
border-collapse:collapse;
margin-top:20px;
}

table,th,td{
border:1px solid #000;
}

th,td{
padding:8px;
}

input{
width:100%;
padding:8px;
margin:5px 0;
}

button{
padding:10px 15px;
margin:5px;
cursor:pointer;
}

.bank{
margin-top:20px;
}
