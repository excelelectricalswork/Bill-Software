<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Excel Electricals - Advanced Billing & GST Software</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @media print {
            .no-print { display: none !important; }
            body { background: white; padding: 0; }
            .invoice-box { box-shadow: none; border: none; padding: 0; }
        }
    </style>
</head>
<body class="bg-slate-100 text-slate-800 font-sans pb-12">

    <!-- Top Navigation Bar -->
    <header class="bg-slate-900 text-white shadow-md no-print">
        <div class="max-w-6xl mx-auto px-4 py-3 flex flex-wrap justify-between items-center">
            <div>
                <h1 class="text-lg font-bold">Excel Electricals - ERP & Billing</h1>
                <p class="text-xs text-slate-400">GSTIN: 32AAGPX3837Q1ZZ | Choondy, Aluva</p>
            </div>
            <div class="space-x-2 mt-2 sm:mt-0">
                <button onclick="switchTab('billing')" id="btn-billing" class="px-3 py-1.5 text-sm bg-blue-600 rounded font-medium">New Invoice</button>
                <button onclick="switchTab('customers')" id="btn-customers" class="px-3 py-1.5 text-sm bg-slate-700 rounded font-medium hover:bg-slate-600">Customers</button>
                <button onclick="switchTab('products')" id="btn-products" class="px-3 py-1.5 text-sm bg-slate-700 rounded font-medium hover:bg-slate-600">Products/Services</button>
                <button onclick="switchTab('gstr')" id="btn-gstr" class="px-3 py-1.5 text-sm bg-slate-700 rounded font-medium hover:bg-slate-600">GSTR Reports</button>
            </div>
        </div>
    </header>

    <main class="max-w-5xl mx-auto mt-6 px-4">

        <!-- TAB 1: BILLING & INVOICE CREATION -->
        <div id="tab-billing" class="tab-content">
            <div class="bg-white rounded-lg shadow-lg p-6 md:p-8 invoice-box border border-slate-200">
                
                <!-- Header Info -->
                <div class="border-b pb-4 mb-4 flex justify-between items-start">
                    <div>
                        <h2 class="text-xl font-bold text-blue-700">EXCEL ELECTRICALS</h2>
                        <p class="text-xs text-slate-600">2/49, Aluva Munnar Road, Opp. Nest Building</p>
                        <p class="text-xs text-slate-600">Choondy, Edathala - 683112, Ernakulam, Kerala</p>
                        <p class="text-xs text-slate-600">Phone: 751014418, 8590259451</p>
                        <p class="text-xs font-semibold text-slate-700 mt-1">GSTIN/UIN: 32AAGPX3837Q1ZZ</p>
                    </div>
                    <div class="text-right">
                        <h3 class="text-lg font-bold text-slate-800">TAX INVOICE</h3>
                        <div class="mt-2 text-xs">
                            <span class="text-slate-500">Invoice No:</span>
                            <input type="text" id="invNo" value="EE/2026-27/328" class="border px-2 py-1 rounded w-32 text-right font-medium">
                        </div>
                        <div class="mt-1 text-xs">
                            <span class="text-slate-500">Date:</span>
                            <input type="date" id="invDate" class="border px-2 py-1 rounded w-32 text-right">
                        </div>
                    </div>
                </div>

                <!-- Customer Selection Section -->
                <div class="mb-4 bg-slate-50 p-3 rounded border text-xs grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                        <label class="block font-bold text-slate-600 mb-1">Select / Search Customer:</label>
                        <select id="selectCustomer" onchange="fillCustomer()" class="w-full border p-1.5 rounded bg-white font-medium">
                            <option value="">-- Select Registered Customer --</option>
                        </select>
                    </div>
                    <div>
                        <label class="block font-bold text-slate-600 mb-1">Buyer Details (Bill To):</label>
                        <textarea id="buyerDetails" rows="2" class="w-full border p-1 rounded bg-white" placeholder="Customer Name, Address & GSTIN"></textarea>
                    </div>
                </div>

                <!-- Items Table matching official layout -->
                <div class="overflow-x-auto mb-4">
                    <table class="w-full text-left border-collapse text-xs">
                        <thead>
                            <tr class="bg-slate-200 text-slate-700">
                                <th class="p-2 border w-10 text-center">SI</th>
                                <th class="p-2 border">Description of Goods / Service</th>
                                <th class="p-2 border w-24">HSN/SAC</th>
                                <th class="p-2 border w-16 text-center">Qnty</th>
                                <th class="p-2 border w-24 text-right">Rate (₹)</th>
                                <th class="p-2 border w-20 text-center">Tax %</th>
                                <th class="p-2 border w-28 text-right">Amount (₹)</th>
                                <th class="p-2 border w-10 text-center no-print">✕</th>
                            </tr>
                        </thead>
                        <tbody id="invoiceItems">
                            <!-- Dynamic Rows -->
                        </tbody>
                    </table>
                    <button onclick="addInvoiceRow()" class="mt-2 no-print bg-slate-800 text-white px-3 py-1.5 rounded text-xs hover:bg-slate-700">+ Add Line Item</button>
                </div>

                <!-- Totals & Tax Breakdowns -->
                <div class="border-t pt-4 grid grid-cols-1 md:grid-cols-2 gap-4 text-xs">
                    <div>
                        <p class="font-bold text-slate-700">Bank Details:</p>
                        <p>Bank Name: STATE BANK OF INDIA, ASOKAPURAM</p>
                        <p>A/C NO: 43721477418</p>
                        <p>IFSC CODE: SBIN0008596</p>
                        <div class="mt-4 border p-2 bg-slate-50 rounded">
                            <p class="font-bold">Declaration:</p>
                            <p class="text-[10px] text-slate-600">We declare that this invoice shows the actual price of the goods described and that all particulars are true and correct.</p>
                        </div>
                    </div>
                    <div class="space-y-1.5 bg-slate-50 p-3 rounded border">
                        <div class="flex justify-between font-bold text-sm border-b pb-1">
                            <span>Total Invoice Value:</span>
                            <span id="grandTotalDisplay">₹0.00</span>
                        </div>
                        <div class="flex justify-between text-slate-600">
                            <span>Taxable Value:</span>
                            <span id="subTotalDisplay">₹0.00</span>
                        </div>
                        <div class="flex justify-between text-slate-600">
                            <span>Central Tax (CGST 9%):</span>
                            <span id="cgstDisplay">₹0.00</span>
                        </div>
                        <div class="flex justify-between text-slate-600">
                            <span>State Tax (SGST 9%):</span>
                            <span id="sgstDisplay">₹0.00</span>
                        </div>
                        <div class="flex justify-between font-semibold text-slate-800 border-t pt-1">
                            <span>Total Tax Amount:</span>
                            <span id="totalTaxDisplay">₹0.00</span>
                        </div>
                    </div>
                </div>

                <!-- Action Buttons -->
                <div class="mt-6 flex flex-wrap justify-end gap-3 no-print border-t pt-4">
                    <button onclick="saveAndRecordInvoice()" class="bg-emerald-600 text-white px-4 py-2 rounded text-xs font-bold hover:bg-emerald-700">Save Invoice to GSTR Logs</button>
                    <button onclick="generateEWayBillJSON()" class="bg-amber-600 text-white px-4 py-2 rounded text-xs font-bold hover:bg-amber-700">Generate E-Way Bill JSON</button>
                    <button onclick="window.print()" class="bg-blue-600 text-white px-5 py-2 rounded text-xs font-bold hover:bg-blue-700">Print / Save PDF</button>
                </div>
            </div>
        </div>

        <!-- TAB 2: CUSTOMER DIRECTORY -->
        <div id="tab-customers" class="tab-content hidden">
            <div class="bg-white rounded-lg shadow p-6">
                <h2 class="text-lg font-bold mb-4">Customer Directory</h2>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-4 bg-slate-50 p-4 rounded border">
                    <input type="text" id="newCustName" placeholder="Customer / Business Name" class="border p-2 rounded text-xs">
                    <input type="text" id="newCustGst" placeholder="GSTIN (e.g. 32AACCA6248B1Z9)" class="border p-2 rounded text-xs uppercase">
                    <input type="text" id="newCustAddress" placeholder="Address & City" class="border p-2 rounded text-xs">
                    <button onclick="addCustomer()" class="col-span-full bg-blue-600 text-white py-2 rounded text-xs font-bold">Add Customer to Database</button>
                </div>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse text-xs">
                        <thead>
                            <tr class="bg-slate-200">
                                <th class="p-2 border">Customer Name</th>
                                <th class="p-2 border">GSTIN</th>
                                <th class="p-2 border">Address</th>
                            </tr>
                        </thead>
                        <tbody id="customerTableBody"></tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- TAB 3: PRODUCT & SERVICE MASTER -->
        <div id="tab-products" class="tab-content hidden">
            <div class="bg-white rounded-lg shadow p-6">
                <h2 class="text-lg font-bold mb-4">Product & Service Master (Rewinding/Spares)</h2>
                <div class="grid grid-cols-1 md:grid-cols-4 gap-4 mb-4 bg-slate-50 p-4 rounded border">
                    <input type="text" id="prodDesc" placeholder="Item Description (e.g., Ceiling Fan Rewinding)" class="border p-2 rounded text-xs md:col-span-2">
                    <input type="text" id="prodHsn" placeholder="HSN/SAC Code (e.g. 995469)" class="border p-2 rounded text-xs">
                    <input type="number" id="prodRate" placeholder="Standard Rate (₹)" class="border p-2 rounded text-xs">
                    <button onclick="addProduct()" class="col-span-full bg-blue-600 text-white py-2 rounded text-xs font-bold">Save Product / Service</button>
                </div>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse text-xs">
                        <thead>
                            <tr class="bg-slate-200">
                                <th class="p-2 border">Description</th>
                                <th class="p-2 border">HSN/SAC</th>
                                <th class="p-2 border">Default Rate (₹)</th>
                            </tr>
                        </thead>
                        <tbody id="productTableBody"></tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- TAB 4: GSTR REPORTS (1, 2, 3B, 4) -->
        <div id="tab-gstr" class="tab-content hidden">
            <div class="bg-white rounded-lg shadow p-6 space-y-6">
                <div class="flex justify-between items-center border-b pb-3">
                    <h2 class="text-lg font-bold text-slate-800">GST Return Filing Summaries</h2>
                    <button onclick="loadGSTRData()" class="bg-slate-800 text-white px-3 py-1.5 rounded text-xs">Refresh Calculations</button>
                </div>

                <!-- GSTR-1 Summary -->
                <div class="border rounded p-4 bg-slate-50">
                    <h3 class="font-bold text-blue-700 text-sm mb-2">GSTR-1 Summary (Outward Supplies to Registered & Consumers)</h3>
                    <div id="gstr1-content" class="text-xs text-slate-700">No saved invoices found for reporting period.</div>
                </div>

                <!-- GSTR-3B Summary -->
                <div class="border rounded p-4 bg-slate-50">
                    <h3 class="font-bold text-blue-700 text-sm mb-2">GSTR-3B Monthly Tax Liability Summary</h3>
                    <div id="gstr3b-content" class="text-xs text-slate-700">No liability recorded yet.</div>
                </div>

                <!-- GSTR-2 & GSTR-4 Info -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="border rounded p-4 bg-slate-50 text-xs">
                        <h4 class="font-bold text-slate-700 mb-1">GSTR-2 (Inward Supplies / Purchase Credit)</h4>
                        <p class="text-slate-500">Tracks component purchases (copper wire, bearings) for Input Tax Credit (ITC) reconciliation.</p>
                    </div>
                    <div class="border rounded p-4 bg-slate-50 text-xs">
                        <h4 class="font-bold text-slate-700 mb-1">GSTR-4 (Composition / Annual Details)</h4>
                        <p class="text-slate-500">Applicable if registered under composite schemes; regular returns use GSTR-1 & 3B logs above.</p>
                    </div>
                </div>
            </div>
        </div>

    </main>

    <script>
        // Initial Mock Data setup if empty
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

        document.getElementById('invDate').valueAsDate = new Date();

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('header button').forEach(el => {
                el.classList.remove('bg-blue-600');
                el.classList.add('bg-slate-700');
            });
            document.getElementById('tab-' + tabId).classList.remove('hidden');
            document.getElementById('btn-' + tabId).classList.remove('bg-slate-700');
            document.getElementById('btn-' + tabId).classList.add('bg-blue-600');

            if(tabId === 'customers') renderCustomers();
            if(tabId === 'products') renderProducts();
            if(tabId === 'gstr') loadGSTRData();
        }

        // Populate dropdowns
        function initApp() {
            const customers = JSON.parse(localStorage.getItem('ee_customers'));
            const select = document.getElementById('selectCustomer');
            select.innerHTML = '<option value="">-- Select Registered Customer --</option>';
            customers.forEach((c, idx) => {
                select.innerHTML += <option value="${idx}">${c.name} (${c.gstin})</option>;
            });
            addInvoiceRow('Ceiling fan rewinding & bearing change', '995469', 3, 600, 18);
        }

        function fillCustomer() {
            const idx = document.getElementById('selectCustomer').value;
            if(idx === "") return;
            const customers = JSON.parse(localStorage.getItem('ee_customers'));
            const c = customers[idx];
            document.getElementById('buyerDetails').value = ${c.name}\n${c.address}\nGSTIN/UIN: ${c.gstin}\nState Name: Kerala, Code: 32;
        }

        function addInvoiceRow(desc='', hsn='995469', qty=1, rate=0, tax=18) {
            const tbody = document.getElementById('invoiceItems');
            const rowCount = tbody.rows.length + 1;
            const row = document.createElement('tr');
            row.innerHTML = `
                <td class="p-2 border text-center">${rowCount}</td>
                <td class="p-2 border"><input type="text" value="${desc}" class="w-full border p-1 rounded item-desc"></td>
                <td class="p-2 border"><input type="text" value="${hsn}" class="w-full border p-1 rounded item-hsn"></td>
                <td class="p-2 border"><input type="number" value="${qty}" min="1" oninput="calculateTotals()" class="w-full border p-1 rounded item-qty text-center"></td>
                <td class="p-2 border"><input type="number" value="${rate}" step="0.01" oninput="calculateTotals()" class="w-full border p-1 rounded item-rate text-right"></td>
                <td class="p-2 border text-center">
                    <select onchange="calculateTotals()" class="border p-1 rounded item-tax text-xs">
                        <option value="18" ${tax==18?'selected':''}>18%</option>
                        <option value="12" ${tax==12?'selected':''}>12%</option>
                        <option value="5" ${tax==5?'selected':''}>5%</option>
                        <option value="0" ${tax==0?'selected':''}>0%</option>
                    </select>
                </td>
                <td class="p-2 border text-right font-semibold item-amount">₹0.00</td>
                <td class="p-2 border text-center no-print"><button onclick="this.closest('tr').remove(); calculateTotals();" class="text-red-600 font-bold">✕</button></td>
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

            document.getElementById('subTotalDisplay').innerText = ₹${subtotal.toFixed(2)};
            document.getElementById('cgstDisplay').innerText = ₹${cgst.toFixed(2)};
            document.getElementById('sgstDisplay').innerText = ₹${sgst.toFixed(2)};
            document.getElementById('totalTaxDisplay').innerText = ₹${totalTax.toFixed(2)};
            document.getElementById('grandTotalDisplay').innerText = ₹${grandTotal.toFixed(2)};
        }

        // Customer management
        function addCustomer() {
            const name = document.getElementById('newCustName').value.trim();
            const gstin = document.getElementById('newCustGst').value.trim();
            const address = document.getElementById('newCustAddress').value.trim();
            if(!name) return alert('Enter customer name');
            
            let customers = JSON.parse(localStorage.getItem('ee_customers'));
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
            const customers = JSON.parse(localStorage.getItem('ee_customers'));
            const tbody = document.getElementById('customerTableBody');
            tbody.innerHTML = '';
            customers.forEach(c => {
                tbody.innerHTML += <tr><td class="p-2 border font-medium">${c.name}</td><td class="p-2 border">${c.gstin}</td><td class="p-2 border">${c.address}</td></tr>;
            });
        }

        // Product management
        function addProduct() {
            const desc = document.getElementById('prodDesc').value.trim();
            const hsn = document.getElementById('prodHsn').value.trim();
            const rate = parseFloat(document.getElementById('prodRate').value) || 0;
            if(!desc) return alert('Enter description');

            let products = JSON.parse(localStorage.getItem('ee_products'));
            products.push({ desc, hsn, rate });
            localStorage.setItem('ee_products', JSON.stringify(products));
            document.getElementById('prodDesc').value = '';
            document.getElementById('prodHsn').value = '';
            document.getElementById('prodRate').value = '';
            renderProducts();
            alert('Product saved successfully!');
        }

        function renderProducts() {
            const products = JSON.parse(localStorage.getItem('ee_products'));
            const tbody = document.getElementById('productTableBody');
            tbody.innerHTML = '';
            products.forEach(p => {
                tbody.innerHTML += <tr><td class="p-2 border font-medium">${p.desc}</td><td class="p-2 border">${p.hsn}</td><td class="p-2 border">₹${p.rate}</td></tr>;
            });
        }

        // Save Invoice for GSTR Records
        function saveAndRecordInvoice() {
            const invNo = document.getElementById('invNo').value;
            const date = document.getElementById('invDate').value;
            const buyer = document.getElementById('buyerDetails').value;
            const grandTotal = document.getElementById('grandTotalDisplay').innerText;
            const taxable = document.getElementById('subTotalDisplay').innerText;
            const tax = document.getElementById('totalTaxDisplay').innerText;

            let invoices = JSON.parse(localStorage.getItem('ee_invoices'));
            invoices.push({ invNo, date, buyer, taxable, tax, grandTotal });
            localStorage.setItem('ee_invoices', JSON.stringify(invoices));
            alert('Invoice successfully recorded into GSTR summary database!');
        }

        // E-Way Bill JSON Generation
        function generateEWayBillJSON() {
            const invNo = document.getElementById('invNo').value;
            const invDate = document.getElementById('invDate').value.split('-').reverse().join('/');
            
            const ewayData = {
                supplyType: "O",
                subSupplyType: "1",
                docType: "INV",
                docNo: invNo,
                docDate: invDate,
                fromGstin: "32AAGPX3837Q1ZZ",
                fromTrdName: "EXCEL ELECTRICALS",
                fromAddr1: "2/49, Aluva Munnar Road",
                fromPlace: "Aluva",
                fromPincode: 683112,
                fromStateCode: 32,
                toGstin: "32AACCA6248B1Z9",
                toTrdName: "Customer / Recipient",
                toAddr1: "Ernakulam",
                toPlace: "Ernakulam",
                toPincode: 683101,
                toStateCode: 32,
                totInvValue: parseFloat(document.getElementById('grandTotalDisplay').innerText.replace('₹','')) || 0,
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

        // GSTR Reports loader
        function loadGSTRData() {
            const invoices = JSON.parse(localStorage.getItem('ee_invoices'));
            if(invoices.length === 0) return;

            let totalTaxableVal = 0;
            let totalTaxVal = 0;
            let rowsHtml = <table class="w-full border mt-2"><tr class="bg-slate-200"><th class="p-1 border">Inv No</th><th class="p-1 border">Date</th><th class="p-1 border">Taxable</th><th class="p-1 border">Tax</th></tr>;
            
            invoices.forEach(inv => {
                totalTaxableVal += parseFloat(inv.taxable.replace('₹','')) || 0;
                totalTaxVal += parseFloat(inv.tax.replace('₹','')) || 0;
                rowsHtml += <tr><td class="p-1 border">${inv.invNo}</td><td class="p-1 border">${inv.date}</td><td class="p-1 border">${inv.taxable}</td><td class="p-1 border">${inv.tax}</td></tr>;
            });
            rowsHtml += </table>;

            document.getElementById('gstr1-content').innerHTML = <p class="mb-2 font-semibold">Total Outward B2B / B2CS Invoices logged: ${invoices.length}</p> + rowsHtml;
            document.getElementById('gstr3b-content').innerHTML = `
                <div class="grid grid-cols-2 gap-2">
                    <div>Total Taxable Outward Supplies: <b>₹${totalTaxableVal.toFixed(2)}</b></div>
                    <div>Total Integrated / Central / State Tax Payable: <b>₹${totalTaxVal.toFixed(2)}</b> (CGST: ₹${(totalTaxVal/2).toFixed(2)} | SGST: ₹${(totalTaxVal/2).toFixed(2)})</div>
                </div>
            `;
        }

        initApp();
    </script>
</body>
</html>
