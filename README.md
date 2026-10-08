<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Excel Electricals - ERP & Billing</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: Arial, sans-serif; }
        body { background: #f1f5f9; color: #1e293b; padding-bottom: 40px; }
        header { background: #0f172a; color: white; padding: 15px 20px; position: sticky; top: 0; z-index: 100; box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
        .header-container { max-width: 1000px; margin: 0 auto; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 10px; }
        .header-title h1 { font-size: 18px; font-weight: bold; }
        .header-title p { font-size: 12px; color: #94a3b8; }
        .nav-buttons { display: flex; gap: 8px; flex-wrap: wrap; }
        .nav-btn { background: #334155; color: white; border: none; padding: 8px 14px; border-radius: 4px; font-size: 13px; cursor: pointer; font-weight: bold; transition: background 0.2s; }
        .nav-btn.active { background: #2563eb; }
        .nav-btn:hover { background: #475569; }
        
        main { max-width: 950px; margin: 25px auto; padding: 0 15px; }
        .tab-content { display: none; background: white; padding: 25px; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); border: 1px solid #e2e8f0; }
        .tab-content.active { display: block; }

        /* Invoice Layout */
        .inv-header { display: flex; justify-content: space-between; border-bottom: 2px solid #e2e8f0; padding-bottom: 15px; margin-bottom: 20px; flex-wrap: wrap; gap: 15px; }
        .shop-info h2 { color: #1d4ed8; font-size: 22px; margin-bottom: 4px; }
        .shop-info p { font-size: 12px; color: #475569; line-height: 1.4; }
        .inv-meta { text-align: right; }
        .inv-meta h3 { font-size: 18px; color: #1e293b; margin-bottom: 8px; }
        .inv-meta label { font-size: 12px; color: #64748b; display: inline-block; width: 80px; text-align: left; }
        .inv-meta input { padding: 5px; font-size: 13px; border: 1px solid #cbd5e1; border-radius: 4px; width: 130px; text-align: right; }

        .customer-box { background: #f8fafc; padding: 12px; border: 1px solid #e2e8f0; border-radius: 6px; margin-bottom: 20px; display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        @media(max-width: 700px) { .customer-box { grid-template-columns: 1fr; } }
        .customer-box label { font-size: 12px; font-weight: bold; color: #475569; display: block; margin-bottom: 4px; }
        .customer-box select, .customer-box textarea { width: 100%; padding: 8px; font-size: 13px; border: 1px solid #cbd5e1; border-radius: 4px; background: white; }

        table { width: 100%; border-collapse: collapse; margin-bottom: 15px; font-size: 13px; }
        th, td { border: 1px solid #cbd5e1; padding: 8px; text-align: left; }
        th { background: #e2e8f0; color: #334155; font-weight: bold; }
        .text-center { text-align: center; }
        .text-right { text-align: right; }
        
        table input, table select { width: 100%; padding: 5px; border: 1px solid #cbd5e1; border-radius: 3px; font-size: 13px; }
        .add-row-btn { background: #0f172a; color: white; border: none; padding: 8px 14px; border-radius: 4px; font-size: 12px; cursor: pointer; font-weight: bold; }
        .add-row-btn:hover { background: #1e293b; }

        .totals-section { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; border-top: 2px solid #e2e8f0; padding-top: 15px; font-size: 13px; }
        @media(max-width: 700px) { .totals-section { grid-template-columns: 1fr; } }
        .bank-details p { font-size: 12px; color: #475569; line-height: 1.5; }
        .declaration { margin-top: 10px; background: #f8fafc; padding: 8px; border: 1px solid #e2e8f0; border-radius: 4px; font-size: 11px; color: #64748b; }
        
        .calculation-box { background: #f8fafc; padding: 12px; border: 1px solid #e2e8f0; border-radius: 6px; display: flex; flex-direction: column; gap: 6px; }
        .calc-row { display: flex; justify-content: space-between; color: #475569; }
        .calc-row.grand { font-size: 15px; font-weight: bold; color: #0f172a; border-bottom: 1px solid #cbd5e1; padding-bottom: 6px; }
        .calc-row.tax-total { font-weight: bold; color: #1e293b; border-top: 1px solid #cbd5e1; padding-top: 6px; }

        .action-buttons { margin-top: 25px; display: flex; justify-content: flex-end; gap: 10px; flex-wrap: wrap; border-top: 1px solid #e2e8f0; padding-top: 15px; }
        .btn { padding: 10px 18px; border: none; border-radius: 4px; font-size: 13px; font-weight: bold; cursor: pointer; color: white; }
        .btn-save { background: #059669; }
        .btn-save:hover { background: #047857; }
        .btn-json { background: #d97706; }
        .btn-json:hover { background: #b45309; }
        .btn-print { background: #2563eb; }
        .btn-print:hover { background: #1d4ed8; }

        .form-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 12px; background: #f8fafc; padding: 15px; border: 1px solid #e2e8f0; border-radius: 6px; margin-bottom: 20px; }
        .form-grid input { padding: 8px; font-size: 13px; border: 1px solid #cbd5e1; border-radius: 4px; }
        .form-grid button { grid-column: 1 / -1; background: #2563eb; color: white; border: none; padding: 10px; border-radius: 4px; font-weight: bold; cursor: pointer; }

        h2.section-title { font-size: 16px; font-weight: bold; margin-bottom: 15px; color: #1e293b; border-bottom: 1px solid #e2e8f0; padding-bottom: 8px; }

        @media print {
            header, .no-print, .action-buttons, .add-row-btn { display: none !important; }
            body { background: white; padding: 0; }
            .tab-content { border: none; box-shadow: none; padding: 0; }
        }
    </style>
</head>
<body>

    <header>
        <div class="header-container">
            <div class="header-title">
                <h1>Excel Electricals - ERP & Billing</h1>
                <p>GSTIN: 32AAGPX3837Q1ZZ | Choondy, Aluva, Kerala</p>
            </div>
            <div class="nav-buttons no-print">
                <button onclick="switchTab('billing')" id="btn-billing" class="nav-btn active">New Invoice</button>
                <button onclick="switchTab('customers')" id="btn-customers" class="nav-btn">Customers</button>
                <button onclick="switchTab('products')" id="btn-products" class="nav-btn">Products/Services</button>
                <button onclick="switchTab('gstr')" id="btn-gstr" class="nav-btn">GSTR Reports</button>
            </div>
        </div>
    </header>

    <main>
        <!-- TAB 1: BILLING -->
        <div id="tab-billing" class="tab-content active">
            <div class="inv-header">
                <div class="shop-info">
                    <h2>EXCEL ELECTRICALS</h2>
                    <p>2/49, Aluva Munnar Road, Opp. Nest Building</p>
                    <p>Choondy, Edathala - 683112, Ernakulam, Kerala</p>
                    <p>Phone: 751014418, 8590259451</p>
                    <p style="font-weight: bold; margin-top: 4px;">GSTIN/UIN: 32AAGPX3837Q1ZZ</p>
                </div>
                <div class="inv-meta">
                    <h3>TAX INVOICE</h3>
                    <div style="margin-bottom: 6px;">
                        <label>Invoice No:</label>
                        <input type="text" id="invNo" value="EE/2026-27/01">
                    </div>
                    <div>
                        <label>Date:</label>
                        <input type="date" id="invDate">
                    </div>
                </div>
            </div>

            <div class="customer-box">
                <div>
                    <label>Select Registered Customer:</label>
                    <select id="selectCustomer" onchange="fillCustomer()">
                        <option value="">-- Choose Customer --</option>
                    </select>
                </div>
                <div>
                    <label>Buyer Details (Bill To):</label>
                    <textarea id="buyerDetails" rows="2" placeholder="Customer Name, Address & GSTIN"></textarea>
                </div>
            </div>

            <div style="overflow-x: auto;">
                <table>
                    <thead>
                        <tr>
                            <th style="width: 40px;" class="text-center">SI</th>
                            <th>Description of Goods / Service</th>
                            <th style="width: 90px;">HSN/SAC</th>
                            <th style="width: 60px;" class="text-center">Qnty</th>
                            <th style="width: 90px;" class="text-right">Rate (₹)</th>
                            <th style="width: 75px;" class="text-center">Tax %</th>
                            <th style="width: 100px;" class="text-right">Amount (₹)</th>
                            <th style="width: 40px;" class="text-center no-print">✕</th>
                        </tr>
                    </thead>
                    <tbody id="invoiceItems"></tbody>
                </table>
                <button onclick="addInvoiceRow()" class="add-row-btn no-print">+ Add Line Item</button>
            </div>

            <div class="totals-section">
                <div class="bank-details">
                    <p style="font-weight: bold; margin-bottom: 4px;">Bank Details:</p>
                    <p><b>Bank Name:</b> STATE BANK OF INDIA, ASOKAPURAM</p>
                    <p><b>A/C NO:</b> 43721477418</p>
                    <p><b>IFSC CODE:</b> SBIN0008596</p>
                    <div class="declaration">
                        <b>Declaration:</b> We declare that this invoice shows the actual price of the goods described and that all particulars are true and correct.
                    </div>
                </div>
                <div class="calculation-box">
                    <div class="calc-row grand">
                        <span>Total Invoice Value:</span>
                        <span id="grandTotalDisplay">₹0.00</span>
                    </div>
                    <div class="calc-row">
                        <span>Taxable Value:</span>
                        <span id="subTotalDisplay">₹0.00</span>
                    </div>
                    <div class="calc-row">
                        <span>Central Tax (CGST):</span>
                        <span id="cgstDisplay">₹0.00</span>
                    </div>
                    <div class="calc-row">
                        <span>State Tax (SGST):</span>
                        <span id="sgstDisplay">₹0.00</span>
                    </div>
                    <div class="calc-row tax-total">
                        <span>Total Tax Amount:</span>
                        <span id="totalTaxDisplay">₹0.00</span>
                    </div>
                </div>
            </div>

            <div class="action-buttons no-print">
                <button onclick="saveAndRecordInvoice()" class="btn btn-save">Save Invoice to GSTR Logs</button>
                <button onclick="generateEWayBillJSON()" class="btn btn-json">Generate E-Way Bill JSON</button>
                <button onclick="window.print()" class="btn btn-print">Print / Save PDF</button>
            </div>
        </div>

        <!-- TAB 2: CUSTOMERS -->
        <div id="tab-customers" class="tab-content">
            <h2 class="section-title">Customer Directory</h2>
            <div class="form-grid">
                <input type="text" id="newCustName" placeholder="Customer / Business Name">
                <input type="text" id="newCustGst" placeholder="GSTIN (e.g. 32AACCA6248B1Z9)">
                <input type="text" id="newCustAddress" placeholder="Address & City">
                <button onclick="addCustomer()">Add Customer to Database</button>
            </div>
            <div style="overflow-x: auto;">
                <table>
                    <thead>
                        <tr>
                            <th>Customer Name</th>
                            <th>GSTIN</th>
                            <th>Address</th>
                        </tr>
                    </thead>
                    <tbody id="customerTableBody"></tbody>
                </table>
            </div>
        </div>

        <!-- TAB 3: PRODUCTS -->
        <div id="tab-products" class="tab-content">
            <h2 class="section-title">Product & Service Master</h2>
            <div class="form-grid">
                <input type="text" id="prodDesc" placeholder="Item Description (e.g., Ceiling Fan Rewinding)" style="grid-column: span 2;">
                <input type="text" id="prodHsn" placeholder="HSN/SAC Code (e.g. 995469)">
                <input type="number" id="prodRate" placeholder="Standard Rate (₹)">
                <button onclick="addProduct()">Save Product / Service</button>
            </div>
            <div style="overflow-x: auto;">
                <table>
                    <thead>
                        <tr>
                            <th>Description</th>
                            <th>HSN/SAC</th>
                            <th>Default Rate (₹)</th>
                        </tr>
                    </thead>
                    <tbody id="productTableBody"></tbody>
                </table>
            </div>
        </div>

        <!-- TAB 4: GSTR REPORTS -->
        <div id="tab-gstr" class="tab-content">
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px;">
                <h2 class="section-title" style="border:none; margin:0;">GST Return Filing Summaries</h2>
                <button onclick="loadGSTRData()" class="add-row-btn">Refresh Reports</button>
            </div>
            <div style="background: #f8fafc; border: 1px solid #e2e8f0; padding: 15px; border-radius: 6px; margin-bottom: 15px;">
                <h3 style="font-size: 14px; font-weight: bold; color: #2563eb; margin-bottom: 8px;">GSTR-1 Summary (Outward Supplies)</h3>
                <div id="gstr1-content" style="font-size: 13px; color: #475569;">Loading summary...</div>
            </div>
            <div style="background: #f8fafc; border: 1px solid #e2e8f0; padding: 15px; border-radius: 6px;">
                <h3 style="font-size: 14px; font-weight: bold; color: #2563eb; margin-bottom: 8px;">GSTR-3B Monthly Tax Liability Summary</h3>
                <div id="gstr3b-content" style="font-size: 13px; color: #475569;">Loading liability...</div>
            </div>
        </div>
    </main>

    <script>
        // Setup initial local storage defaults if empty
        if (!localStorage.getItem('ee_customers')) {
            localStorage.setItem('ee_customers', JSON.stringify([
                { name: "ALAMPALLY BROTHERS LTD", gstin: "32AACCA6248B1Z9", address: "Manalimukku, Naval Armament Depot P.O, Aluva-683563" }
            ]));
        }
        if (!localStorage.getItem('ee_products')) {
            localStorage.setItem('ee_products', JSON.stringify([
                { desc: "Ceiling fan rewinding & bearing change", hsn: "995469", rate: 600 },
                { desc: "Copper wire 22 SWG (per kg)", hsn: "8544", rate: 850 },
                { desc: "Ball Bearing 6202 ZZ", hsn: "8482", rate: 150 }
            ]));
        }
        if (!localStorage.getItem('ee_invoices')) {
            localStorage.setItem('ee_invoices', JSON.stringify([]));
        }

        // Initialize App on Load
        window.addEventListener('DOMContentLoaded', () => {
            const dateInput = document.getElementById('invDate');
            if(dateInput) dateInput.valueAsDate = new Date();
            initApp();
        });

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(el => el.classList.remove('active'));
            
            const targetTab = document.getElementById('tab-' + tabId);
            const targetBtn = document.getElementById('btn-' + tabId);
            
            if(targetTab) targetTab.classList.add('active');
            if(targetBtn) targetBtn.classList.add('active');

            if(tabId === 'customers') renderCustomers();
            if(tabId === 'products') renderProducts();
            if(tabId === 'gstr') loadGSTRData();
        }

        function initApp() {
            const customers = JSON.parse(localStorage.getItem('ee_customers') || '[]');
            const select = document.getElementById('selectCustomer');
            if(select) {
                select.innerHTML = '<option value="">-- Choose Customer --</option>';
                customers.forEach((c, idx) => {
                    select.innerHTML += <option value="${idx}">${c.name} (${c.gstin})</option>;
                });
            }
            const tbody = document.getElementById('invoiceItems');
            if(tbody && tbody.rows.length === 0) {
                addInvoiceRow('Ceiling fan rewinding & bearing change', '995469', 1, 600, 18);
            }
        }

        function fillCustomer() {
            const idx = document.getElementById('selectCustomer').value;
            if(idx === "") return;
            const customers = JSON.parse(localStorage.getItem('ee_customers') || '[]');
            const c = customers[idx];
            if(c) {
                document.getElementById('buyerDetails').value = ${c.name}\n${c.address}\nGSTIN/UIN: ${c.gstin}\nState Name: Kerala, Code: 32;
            }
        }

        function addInvoiceRow(desc='', hsn='995469', qty=1, rate=0, tax=18) {
            const tbody = document.getElementById('invoiceItems');
            if(!tbody) return;
            const rowCount = tbody.rows.length + 1;
            const row = document.createElement('tr');
            row.innerHTML = `
                <td class="text-center">${rowCount}</td>
                <td><input type="text" value="${desc}" class="item-desc"></td>
                <td><input type="text" value="${hsn}" class="item-hsn"></td>
                <td class="text-center"><input type="number" value="${qty}" min="1" oninput="calculateTotals()" class="item-qty text-center"></td>
                <td class="text-right"><input type="number" value="${rate}" step="0.01" oninput="calculateTotals()" class="item-rate text-right"></td>
                <td class="text-center">
                    <select onchange="calculateTotals()" class="item-tax">
                        <option value="18" ${tax==18?'selected':''}>18%</option>
                        <option value="12" ${tax==12?'selected':''}>12%</option>
                        <option value="5" ${tax==5?'selected':''}>5%</option>
                        <option value="0" ${tax==0?'selected':''}>0%</option>
                    </select>
                </td>
                <td class="text-right item-amount" style="font-weight: bold;">₹0.00</td>
                <td class="text-center no-print"><button onclick="this.closest('tr').remove(); calculateTotals();" style="background:none; border:none; color:#dc2626; font-weight:bold; cursor:pointer;">✕</button></td>
            `;
            tbody.appendChild(row);
            calculateTotals();
        }

        function calculateTotals() {
            let subtotal = 0;
            let totalTax = 0;
            const rows = document.querySelectorAll('#invoiceItems tr');
            
            rows.forEach(row => {
                const qty = parseFloat(row.querySelector('.item-qty').value) || 0;
                const rate = parseFloat(row.querySelector('.item-rate').value) || 0;
                const taxRate = parseFloat(row.querySelector('.item-tax').value) || 0;
                
                const amount = qty * rate;
                const taxAmt = (amount * taxRate) / 100;
                
                row.querySelector('.item-amount').innerText = ₹${amount.toFixed(2)};
                subtotal += amount;
                totalTax += taxAmt;
            });

            const grandTotal = subtotal + totalTax;
            const cgst = totalTax / 2;
            const sgst = totalTax / 2;

            if(document.getElementById('subTotalDisplay')) document.getElementById('subTotalDisplay').innerText = ₹${subtotal.toFixed(2)};
            if(document.getElementById('cgstDisplay')) document.getElementById('cgstDisplay').innerText = ₹${cgst.toFixed(2)};
            if(document.getElementById('sgstDisplay')) document.getElementById('sgstDisplay').innerText = ₹${sgst.toFixed(2)};
            if(document.getElementById('totalTaxDisplay')) document.getElementById('totalTaxDisplay').innerText = ₹${totalTax.toFixed(2)};
            if(document.getElementById('grandTotalDisplay')) document.getElementById('grandTotalDisplay').innerText = ₹${grandTotal.toFixed(2)};
        }

        function addCustomer() {
            const name = document.getElementById('newCustName').value.trim();
            const gstin = document.getElementById('newCustGst').value.trim();
            const address = document.getElementById('newCustAddress').value.trim();
            if(!name) return alert('Please enter customer name');
            
            let customers = JSON.parse(localStorage.getItem('ee_customers') || '[]');
            customers.push({ name, gstin, address });
            localStorage.setItem('ee_customers', JSON.stringify(customers));
            
            document.getElementById('newCustName').value = '';
            document.getElementById('newCustGst').value = '';
            document.getElementById('newCustAddress').value = '';
            
            renderCustomers();
            initApp();
            alert('Customer added successfully!');
        }

        function renderCustomers() {
            const customers = JSON.parse(localStorage.getItem('ee_customers') || '[]');
            const tbody = document.getElementById('customerTableBody');
            if(!tbody) return;
            tbody.innerHTML = '';
            if(customers.length === 0) {
                tbody.innerHTML = <tr><td colspan="3" class="text-center">No customers found.</td></tr>;
                return;
            }
            customers.forEach(c => {
                tbody.innerHTML += <tr><td style="font-weight:500">${c.name}</td><td>${c.gstin || '-'}</td><td>${c.address || '-'}</td></tr>;
            });
        }

        function addProduct() {
            const desc = document.getElementById('prodDesc').value.trim();
            const hsn = document.getElementById('prodHsn').value.trim();
            const rate = parseFloat(document.getElementById('prodRate').value) || 0;
            if(!desc) return alert('Please enter item description');

            let products = JSON.parse(localStorage.getItem('ee_products') || '[]');
            products.push({ desc, hsn, rate });
            localStorage.setItem('ee_products', JSON.stringify(products));
            
            document.getElementById('prodDesc').value = '';
            document.getElementById('prodHsn').value = '';
            document.getElementById('prodRate').value = '';
            
            renderProducts();
            alert('Product saved successfully!');
        }

        function renderProducts() {
            const products = JSON.parse(localStorage.getItem('ee_products') || '[]');
            const tbody = document.getElementById('productTableBody');
            if(!tbody) return;
            tbody.innerHTML = '';
            if(products.length === 0) {
                tbody.innerHTML = <tr><td colspan="3" class="text-center">No products found.</td></tr>;
                return;
            }
            products.forEach(p => {
                tbody.innerHTML += <tr><td style="font-weight:500">${p.desc}</td><td>${p.hsn || '-'}</td><td>₹${p.rate.toFixed(2)}</td></tr>;
            });
        }

        function saveAndRecordInvoice() {
            const invNo = document.getElementById('invNo').value.trim();
            const date = document.getElementById('invDate').value;
            const buyer = document.getElementById('buyerDetails').value.trim();
            const grandTotal = document.getElementById('grandTotalDisplay').innerText;
            const taxable = document.getElementById('subTotalDisplay').innerText;
            const tax = document.getElementById('totalTaxDisplay').innerText;

            if(!invNo) return alert('Please enter Invoice Number');

            let invoices = JSON.parse(localStorage.getItem('ee_invoices') || '[]');
            invoices.push({ invNo, date, buyer, taxable, tax, grandTotal });
            localStorage.setItem('ee_invoices', JSON.stringify(invoices));
            
            alert('Invoice #' + invNo + ' successfully saved into GSTR Logs!');
        }

        function generateEWayBillJSON() {
            const invNo = document.getElementById('invNo').value.trim();
            const rawDate = document.getElementById('invDate').value;
            if(!invNo || !rawDate) return alert('Please check Invoice No and Date before generating E-Way Bill JSON.');
            
            const invDate = rawDate.split('-').reverse().join('/');
            const grandTotalVal = parseFloat(document.getElementById('grandTotalDisplay').innerText.replace('₹','')) || 0;

            const ewayData = {
                supplyType: "O",
                subSupplyType: "1",
                docType: "INV",
                docNo: invNo,
                docDate: invDate,
                fromGstin: "32AAGPX3837Q1ZZ",
                fromTrdName: "EXCEL ELECTRICALS",
                fromAddr1: "2/49, Aluva Munnar Road, Choondy",
                fromPlace: "Aluva",
                fromPincode: 683112,
                fromStateCode: 32,
                totInvValue: grandTotalVal,
                transMode: "1",
                transDistance: 25,
                vehicleNo: "KL07XX0000"
            };

            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(ewayData, null, 4));
            const dlAnchor = document.createElement('a');
            dlAnchor.setAttribute("href", dataStr);
            dlAnchor.setAttribute("download", EWayBill_${invNo}.json);
            document.body.appendChild(dlAnchor);
            dlAnchor.click();
            dlAnchor.remove();
        }

        function loadGSTRData() {
            const invoices = JSON.parse(localStorage.getItem('ee_invoices') || '[]');
            const gstr1El = document.getElementById('gstr1-content');
            const gstr3bEl = document.getElementById('gstr3b-content');
            
            if(invoices.length === 0) {
                if(gstr1El) gstr1El.innerHTML = "No saved invoices found in logs yet. Click 'Save Invoice to GSTR Logs' from the New Invoice tab.";
                if(gstr3bEl) gstr3bEl.innerHTML = "No liability recorded yet.";
                return;
            }

            let totalTaxableVal = 0;
            let totalTaxVal = 0;
            let rowsHtml = <div style="overflow-x:auto;"><table style="margin-top:8px;"><tr><th>Inv No</th><th>Date</th><th>Taxable Value</th><th>Tax Amount</th></tr>;
            
            invoices.forEach(inv => {
                totalTaxableVal += parseFloat((inv.taxable || '0').replace('₹','')) || 0;
                totalTaxVal += parseFloat((inv.tax || '0').replace('₹','')) || 0;
                rowsHtml += <tr><td>${inv.invNo}</td><td>${inv.date}</td><td>${inv.taxable}</td><td>${inv.tax}</td></tr>;
            });
            rowsHtml += </table></div>;

            if(gstr1El) gstr1El.innerHTML = <p style="margin-bottom: 4px; font-weight:bold;">Total Outward Invoices Logged: ${invoices.length}</p> + rowsHtml;
            if(gstr3bEl) gstr3bEl.innerHTML = `
                <div style="display: flex; gap: 20px; flex-wrap: wrap;">
                    <div>Total Taxable Outward Supplies: <b>₹${totalTaxableVal.toFixed(2)}</b></div>
                    <div>Total Tax Payable: <b>₹${totalTaxVal.toFixed(2)}</b> (CGST: ₹${(totalTaxVal/2).toFixed(2)} | SGST: ₹${(totalTaxVal/2).toFixed(2)})</div>
                </div>
            `;
        }
    </script>
</body>
</html>
