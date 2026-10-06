<index. html.txt>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Excel Electricals - GST ERP & Billing Software</title>
    <style>
        :root {
            --primary: #1a73e8;
            --dark: #202124;
            --light: #f8f9fa;
            --border: #dadce0;
            --success: #137333;
        }
        body {
            font-family: Arial, sans-serif;
            margin: 0; padding: 0;
            background: #f0f2f5;
            color: var(--dark);
        }
        header {
            background: var(--dark);
            color: #fff;
            padding: 15px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        header h1 { margin: 0; font-size: 18px; }
        .nav-tabs {
            background: #fff;
            display: flex;
            border-bottom: 1px solid var(--border);
            padding: 0 20px;
            overflow-x: auto;
        }
        .tab-btn {
            background: none; border: none;
            padding: 15px 20px;
            font-size: 13px; font-weight: bold;
            cursor: pointer; color: #5f6368;
            border-bottom: 3px solid transparent;
        }
        .tab-btn.active {
            color: var(--primary);
            border-bottom-color: var(--primary);
        }
        .container {
            max-width: 1200px;
            margin: 20px auto;
            background: #fff;
            padding: 25px;
            border-radius: 8px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }
        .tab-content { display: none; }
        .tab-content.active { display: block; }
        
        /* Cards Dashboard */
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }
        .card {
            background: var(--light);
            border: 1px solid var(--border);
            padding: 20px;
            border-radius: 6px;
        }
        .card h3 { margin: 0 0 10px 0; font-size: 14px; color: #5f6368; }
        .card .value { font-size: 24px; font-weight: bold; color: var(--primary); }

        /* Tables & Forms */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
            margin-bottom: 15px;
        }
        th, td {
            border: 1px solid var(--border);
            padding: 10px;
            text-align: left;
            font-size: 12px;
        }
        th { background: var(--light); }
        .btn {
            background: var(--primary);
            color: #fff; border: none;
            padding: 8px 15px; border-radius: 4px;
            cursor: pointer; font-size: 12px;
        }
        .btn:hover { background: #1557b0; }
        .btn-danger { background: #d93025; }
        .btn-danger:hover { background: #b31412; }
        input, select {
            width: 100%; padding: 7px;
            border: 1px solid var(--border);
            border-radius: 4px; box-sizing: border-box;
            font-size: 12px;
        }
        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 15px;
        }
        .right { text-align: right; }
        .center { text-align: center; }
    </style>
</head>
<body>

<header>
    <h1>EXCEL ELECTRICALS — ERP & GST Billing Software</h1>
    <div>GSTIN: 32AAGPX3837Q1ZZ | Choondy, Aluva</div>
</header>

<div class="nav-tabs">
    <button class="tab-btn active" onclick="switchTab(event, 'dashboardTab')">Dashboard</button>
    <button class="tab-btn" onclick="switchTab(event, 'invoiceTab')">Create Invoice (Tally Style)</button>
    <button class="tab-btn" onclick="switchTab(event, 'customerTab')">Customer Master</button>
    <button class="tab-btn" onclick="switchTab(event, 'productTab')">Product & HSN Master</button>
    <button class="tab-btn" onclick="switchTab(event, 'reportsTab')">GST Returns (GSTR 1, 2, 3B)</button>
    <button class="tab-btn" onclick="switchTab(event, 'plTab')">Profit & Loss (P&L)</button>
</div>

<div class="container">

    <!-- 1. DASHBOARD -->
    <div id="dashboardTab" class="tab-content active">
        <h2>Business Overview</h2>
        <div class="dashboard-grid">
            <div class="card">
                <h3>Total Sales (Turnover)</h3>
                <div class="value" id="dashSales">₹0.00</div>
            </div>
            <div class="card">
                <h3>Total Tax Collected (GST)</h3>
                <div class="value" id="dashTax">₹0.00</div>
            </div>
            <div class="card">
                <h3>Registered Customers</h3>
                <div class="value" id="dashCustomers">0</div>
            </div>
            <div class="card">
                <h3>Estimated Net Profit</h3>
                <div class="value" id="dashProfit" style="color: var(--success);">₹0.00</div>
            </div>
        </div>
        <h3>Recent Invoices</h3>
        <table>
            <thead>
                <tr>
                    <th>Inv No</th>
                    <th>Date</th>
                    <th>Customer Name</th>
                    <th>Grand Total</th>
                    <th>GST Amount</th>
                </tr>
            </thead>
            <tbody id="dashRecentInvoices">
                <tr><td colspan="5" class="center">No invoices created yet.</td></tr>
            </tbody>
        </table>
    </div>

    <!-- 2. CREATE INVOICE -->
    <div id="invoiceTab" class="tab-content">
        <h2>New Tax Invoice Voucher</h2>
        <div class="form-row">
            <div>
                <label>Invoice Number</label>
                <input type="text" id="invNo" value="256">
            </div>
            <div>
                <label>Invoice Date</label>
                <input type="date" id="invDate">
            </div>
            <div>
                <label>Select Customer</label>
                <select id="selectedCustomer" onchange="populateCustomer()"></select>
            </div>
        </div>
        
        <div style="background: var(--light); padding: 15px; border-radius: 6px; margin-bottom: 15px;">
            <b>Buyer Details:</b> <span id="previewCustDetails">Select a customer above</span>
        </div>

        <h3>Itemized Entries</h3>
        <table>
            <thead>
                <tr>
                    <th style="width: 30%;">Product / Service</th>
                    <th>HSN/SAC</th>
                    <th>Qty</th>
                    <th>Rate (₹)</th>
                    <th>Per</th>
                    <th>Amount (₹)</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody id="invoiceItems">
                <tr>
                    <td>
                        <select class="item-select" onchange="productSelected(this)">
                            <option value="">-- Select Product --</option>
                        </select>
                    </td>
                    <td><input type="text" class="item-hsn" value=""></td>
                    <td><input type="number" class="item-qty" value="1" oninput="calcInvoice()"></td>
                    <td><input type="number" class="item-rate" value="0" oninput="calcInvoice()"></td>
                    <td class="center">NOS</td>
                    <td class="right item-amt">0.00</td>
                    <td class="center"><button class="btn btn-danger" onclick="removeRow(this)">X</button></td>
                </tr>
            </tbody>
        </table>
        <button class="btn" onclick="addInvoiceRow()">+ Add Item Row</button>

        <div style="margin-top: 20px; width: 350px; float: right;">
            <table>
                <tr><td><b>Subtotal:</b></td><td class="right" id="invSubtotal">0.00</td></tr>
                <tr><td><b>CGST (9%):</b></td><td class="right" id="invCgst">0.00</td></tr>
                <tr><td><b>SGST (9%):</b></td><td class="right" id="invSgst">0.00</td></tr>
                <tr><td><b>Grand Total:</b></td><td class="right" id="invTotal" style="font-weight:bold; font-size:14px;">0.00</td></tr>
            </table>
            <button class="btn" style="width: 100%; margin-top: 10px;" onclick="saveAndPrintInvoice()">Save & Print Invoice</button>
        </div>
        <div style="clear: both;"></div>
    </div>

    <!-- 3. CUSTOMER MASTER -->
    <div id="customerTab" class="tab-content">
        <h2>Customer Master Management</h2>
        <div class="form-row">
            <div><label>Customer Name / Company</label><input type="text" id="cName"></div>
            <div><label>GSTIN / UIN</label><input type="text" id="cGst"></div>
            <div><label>Address / Location</label><input type="text" id="cAddress"></div>
            <div style="display: flex; align-items: flex-end;"><button class="btn" onclick="addCustomer()">Save Customer</button></div>
        </div>
        <h3>Existing Customers</h3>
        <table>
            <thead><tr><th>Customer Name</th><th>GSTIN</th><th>Address</th><th>Action</th></tr></thead>
            <tbody id="customerTableBody"></tbody>
        </table>
    </div>

    <!-- 4. PRODUCT & HSN MASTER -->
    <div id="productTab" class="tab-content">
        <h2>Product & HSN/SAC Code Master</h2>
        <div class="form-row">
            <div><label>Product / Service Description</label><input type="text" id="pName"></div>
            <div><label>HSN / SAC Code</label><input type="text" id="pHsn"></div>
            <div><label>Default Rate (₹)</label><input type="number" id="pRate"></div>
            <div style="display: flex; align-items: flex-end;"><button class="btn" onclick="addProduct()">Save Product</button></div>
        </div>
        <h3>Saved Products & Rates</h3>
        <table>
            <thead><tr><th>Description</th><th>HSN/SAC</th><th>Default Rate (₹)</th><th>Action</th></tr></thead>
            <tbody id="productTableBody"></tbody>
        </table>
    </div>

    <!-- 5. GST RETURNS (GSTR 1, 2, 3B) -->
    <div id="reportsTab" class="tab-content">
        <h2>GST Return Reports (GSTR-1, GSTR-2, GSTR-3B)</h2>
        <h3>GSTR-1 (Outward Supplies / Sales Tax Summary)</h3>
        <table>
            <thead><tr><th>Total Invoices</th><th>Total Taxable Value (₹)</th><th>Total CGST (₹)</th><th>Total SGST (₹)</th><th>Total Tax Liability (₹)</th></tr></thead>
            <tbody id="gstr1Body"></tbody>
        </table>

        <h3>GSTR-2 (Inward Supplies / Purchase Input Tax Credit)</h3>
        <table>
            <thead><tr><th>Month / Period</th><th>Purchase Taxable Value</th><th>ITC Available CGST</th><th>ITC Available SGST</th></tr></thead>
            <tbody><tr><td>Current Period</td><td>₹0.00</td><td>₹0.00</td><td>₹0.00</td></tr></tbody>
        </table>

        <h3>GSTR-3B (Monthly Summary & Net Tax Payable)</h3>
        <table>
            <thead><tr><th>Tax Type</th><th>Output Tax Payable</th><th>Input Tax Credit (ITC)</th><th>Net Tax Payable</th></tr></thead>
            <tbody>
                <tr><td>CGST (9%)</td><td id="g3bOutCgst">₹0.00</td><td>₹0.00</td><td id="g3bNetCgst">₹0.00</td></tr>
                <tr><td>SGST (9%)</td><td id="g3bOutSgst">₹0.00</td><td>₹0.00</td><td id="g3bNetSgst">₹0.00</td></tr>
            </tbody>
        </table>
    </div>

    <!-- 6. PROFIT & LOSS -->
    <div id="plTab" class="tab-content">
        <h2>Profit & Loss (P&L) Statement</h2>
        <div class="dashboard-grid">
            <div class="card"><h3>Total Revenue (Sales)</h3><div class="value" id="plRevenue">₹0.00</div></div>
            <div class="card"><h3>Estimated Material/Cost (60%)</h3><div class="value" id="plCost">₹0.00</div></div>
            <div class="card"><h3>Net Operating Profit</h3><div class="value" id="plNetProfit" style="color:var(--success);">₹0.00</div></div>
        </div>
    </div>

</div>

<script>
    // Local Database State
    let customers = JSON.parse(localStorage.getItem('excel_customers')) || [
        {name: 'KANAKA POLYPACK PVT. LTD.', gstin: '32AAFCK1498J1ZD', address: 'ASOKAPURAM, ALUVA-683101'}
    ];
    let products = JSON.parse(localStorage.getItem('excel_products')) || [
        {name: 'Ceiling fan rewinding & bearing change', hsn: '8503', rate: 600},
        {name: 'Gear motor Bearing change', hsn: '8501', rate: 650}
    ];
    let invoices = JSON.parse(localStorage.getItem('excel_invoices')) || [];

    document.getElementById('invDate').valueAsDate = new Date();

    function switchTab(evt, tabName) {
        document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));
        document.getElementById(tabName).classList.add('active');
        evt.currentTarget.classList.add('active');
        refreshData();
    }

    // Customer Functions
    function addCustomer() {
        let name = document.getElementById('cName').value;
        let gstin = document.getElementById('cGst').value;
        let address = document.getElementById('cAddress').value;
        if(!name) return alert('Enter customer name');
        customers.push({name, gstin, address});
        localStorage.setItem('excel_customers', JSON.stringify(customers));
        document.getElementById('cName').value = ''; document.getElementById('cGst').value = ''; document.getElementById('cAddress').value = '';
        renderCustomers();
    }
    function renderCustomers() {
        let html = '';
        let selectHtml = '<option value="">-- Select Customer --</option>';
        customers.forEach((c, i) => {
            html += <tr><td>${c.name}</td><td>${c.gstin}</td><td>${c.address}</td><td><button class="btn btn-danger" onclick="delCustomer(${i})">Delete</button></td></tr>;
            selectHtml += <option value="${i}">${c.name}</option>;
        });
        document.getElementById('customerTableBody').innerHTML = html;
        document.getElementById('selectedCustomer').innerHTML = selectHtml;
    }
    function delCustomer(i) { customers.splice(i, 1); localStorage.setItem('excel_customers', JSON.stringify(customers)); renderCustomers(); }

    // Product Functions
    function addProduct() {
        let name = document.getElementById('pName').value;
        let hsn = document.getElementById('pHsn').value;
        let rate = parseFloat(document.getElementById('pRate').value) || 0;
        if(!name) return alert('Enter product name');
        products.push({name, hsn, rate});
        localStorage.setItem('excel_products', JSON.stringify(products));
        document.getElementById('pName').value = ''; document.getElementById('pHsn').value = ''; document.getElementById('pRate').value = '';
        renderProducts();
    }
    function renderProducts() {
        let html = '';
        let prodOptions = '<option value="">-- Select Product --</option>';
        products.forEach((p, i) => {
            html += <tr><td>${p.name}</td><td>${p.hsn}</td><td>${p.rate}</td><td><button class="btn btn-danger" onclick="delProduct(${i})">Delete</button></td></tr>;
            prodOptions += <option value="${i}" data-hsn="${p.hsn}" data-rate="${p.rate}">${p.name} (HSN: ${p.hsn})</option>;
        });
        document.getElementById('productTableBody').innerHTML = html;
        document.querySelectorAll('.item-select').forEach(sel => {
            let val = sel.value; sel.innerHTML = prodOptions; sel.value = val;
        });
    }
    function delProduct(i) { products.splice(i, 1); localStorage.setItem('excel_products', JSON.stringify(products)); renderProducts(); }

    // Invoice Handling
    function populateCustomer() {
        let idx = document.getElementById('selectedCustomer').value;
        if(idx === "") { document.getElementById('previewCustDetails').innerText = "Select a customer above"; return; }
        let c = customers[idx];
        document.getElementById('previewCustDetails').innerHTML = <b>${c.name}</b><br>GSTIN: ${c.gstin}<br>Address: ${c.address};
    }
    function addInvoiceRow() {
        let tbody = document.getElementById('invoiceItems');
        let prodOptions = '<option value="">-- Select Product --</option>';
        products.forEach((p, i) => {
            prodOptions += <option value="${i}" data-hsn="${p.hsn}" data-rate="${p.rate}">${p.name} (HSN: ${p.hsn})</option>;
        });
        let row = tbody.insertRow();
        row.innerHTML = `
            <td><select class="item-select" onchange="productSelected(this)">${prodOptions}</select></td>
            <td><input type="text" class="item-hsn" value=""></td>
            <td><input type="number" class="item-qty" value="1" oninput="calcInvoice()"></td>
            <td><input type="number" class="item-rate" value="0" oninput="calcInvoice()"></td>
            <td class="center">NOS</td>
            <td class="right item-amt">0.00</td>
            <td class="center"><button class="btn btn-danger" onclick="removeRow(this)">X</button></td>
        `;
    }
    function removeRow(btn) { btn.closest('tr').remove(); calcInvoice(); }
    function productSelected(sel) {
        let opt = sel.options[sel.selectedIndex];
        let row = sel.closest('tr');
        if(opt.dataset.hsn) {
            row.querySelector('.item-hsn').value = opt.dataset.hsn;
            row.querySelector('.item-rate').value = opt.dataset.rate;
            calcInvoice();
        }
    }
    function calcInvoice() {
        let subtotal = 0;
        document.querySelectorAll('#invoiceItems tr').forEach(row => {
            let qty = parseFloat(row.querySelector('.item-qty').value) || 0;
            let rate = parseFloat(row.querySelector('.item-rate').value) || 0;
            let amt = qty * rate;
            row.querySelector('.item-amt').innerText = amt.toFixed(2);
            subtotal += amt;
        });
        let cgst = subtotal * 0.09;
        let sgst = subtotal * 0.09;
        let total = subtotal + cgst + sgst;

        document.getElementById('invSubtotal').innerText = subtotal.toFixed(2);
        document.getElementById('invCgst').innerText = cgst.toFixed(2);
        document.getElementById('invSgst').innerText = sgst.toFixed(2);
        document.getElementById('invTotal').innerText = total.toFixed(2);
    }
    function saveAndPrintInvoice() {
        let custIdx = document.getElementById('selectedCustomer').value;
        if(custIdx === "") return alert('Please select a customer!');
        let invData = {
            no: document.getElementById('invNo').value,
            date: document.getElementById('invDate').value,
            customer: customers[custIdx].name,
            subtotal: document.getElementById('invSubtotal').innerText,
            cgst: document.getElementById('invCgst').innerText,
            sgst: document.getElementById('invSgst').innerText,
            total: document.getElementById('invTotal').innerText
        };
        invoices.push(invData);
        localStorage.setItem('excel_invoices', JSON.stringify(invoices));
        alert('Invoice Saved Successfully!');
        window.print();
    }

    // Reports & Dashboard Refresh
    function refreshData() {
        renderCustomers();
        renderProducts();
        
        let totalSales = invoices.reduce((sum, i) => sum + parseFloat(i.total), 0);
        let totalTax = invoices.reduce((sum, i) => sum + parseFloat(i.cgst) + parseFloat(i.sgst), 0);
        let taxableVal = invoices.reduce((sum, i) => sum + parseFloat(i.subtotal), 0);

        document.getElementById('dashSales').innerText = '₹' + totalSales.toFixed(2);
        document.getElementById('dashTax').innerText = '₹' + totalTax.toFixed(2);
        document.getElementById('dashCustomers').innerText = customers.length;
        
        let profit = totalSales * 0.40; // Estimated 40% margin model
        document.getElementById('dashProfit').innerText = '₹' + profit.toFixed(2);

        // Recent Invoices
        let recentHtml = '';
        if(invoices.length === 0) {
            recentHtml = '<tr><td colspan="5" class="center">No invoices created yet.</td></tr>';
        } else {
            invoices.slice(-5).reverse().forEach(inv => {
                let taxAmt = (parseFloat(inv.cgst) + parseFloat(inv.sgst)).toFixed(2);
                recentHtml += <tr><td>${inv.no}</td><td>${inv.date}</td><td>${inv.customer}</td><td>₹${inv.total}</td><td>₹${taxAmt}</td></tr>;
            });
        }
        document.getElementById('dashRecentInvoices').innerHTML = recentHtml;

        // GSTR-1 & 3B Summary
        let cgstTotal = invoices.reduce((sum, i) => sum + parseFloat(i.cgst), 0);
        let sgstTotal = invoices.reduce((sum, i) => sum + parseFloat(i.sgst), 0);
        document.getElementById('gstr1Body').innerHTML = <tr><td>${invoices.length}</td><td>₹${taxableVal.toFixed(2)}</td><td>₹${cgstTotal.toFixed(2)}</td><td>₹${sgstTotal.toFixed(2)}</td><td>₹${(cgstTotal+sgstTotal).toFixed(2)}</td></tr>;
        
        document.getElementById('g3bOutCgst').innerText = '₹' + cgstTotal.toFixed(2);
        document.getElementById('g3bNetCgst').innerText = '₹' + cgstTotal.toFixed(2);
        document.getElementById('g3bOutSgst').innerText = '₹' + sgstTotal.toFixed(2);
        document.getElementById('g3bNetSgst').innerText = '₹' + sgstTotal.toFixed(2);

        // P&L
        document.getElementById('plRevenue').innerText = '₹' + totalSales.toFixed(2);
        document.getElementById('plCost').innerText = '₹' + (totalSales * 0.60).toFixed(2);
        document.getElementById('plNetProfit').innerText = '₹' + profit.toFixed(2);
    }

    // Initial load
    refreshData();
    addInvoiceRow();
</script>

</body>
</html>
