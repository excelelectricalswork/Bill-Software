<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Excel Electricals - Secure Workshop ERP & Billing</title>
    <style>
        :root {
            --primary: #1e3a8a;
            --primary-light: #3b82f6;
            --accent: #059669;
            --warning: #d97706;
            --danger: #dc2626;
            --bg-main: #f1f5f9;
            --card-bg: #ffffff;
            --text-main: #1e293b;
            --text-muted: #64748b;
            --border: #cbd5e1;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background: var(--bg-main); color: var(--text-main); padding-bottom: 50px; }

       

        /* Header & Navigation */
        header { background: var(--primary); color: white; padding: 15px 25px; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .brand h2 { font-size: 18px; letter-spacing: 0.5px; color: #60a5fa; }
        .brand p { font-size: 11px; color: #9ca3af; }
        .user-badge { font-size: 12px; background: rgba(255,255,255,0.15); color: white; padding: 6px 12px; border-radius: 20px; font-weight: bold; display: flex; align-items: center; gap: 8px; }

        .nav-tabs { background: #1e293b; display: flex; padding: 0 15px; gap: 4px; overflow-x: auto; box-shadow: inset 0 -2px 5px rgba(0,0,0,0.2); }
        .nav-tab { padding: 12px 14px; color: #94a3b8; cursor: pointer; font-size: 12px; font-weight: 600; border-bottom: 3px solid transparent; white-space: nowrap; transition: all 0.2s; }
        .nav-tab:hover { color: white; background: rgba(255,255,255,0.05); }
        .nav-tab.active { color: white; border-bottom-color: #60a5fa; background: rgba(255,255,255,0.08); }

        .container { max-width: 1100px; margin: 25px auto; padding: 0 15px; }
        .panel { display: none; }
        .panel.active { display: block; animation: fadeIn 0.2s ease; }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(4px); } to { opacity: 1; transform: translateY(0); } }

        /* Cards & Grids */
        .card { background: var(--card-bg); border-radius: 8px; border: 1px solid var(--border); padding: 25px; margin-bottom: 20px; box-shadow: 0 1px 3px rgba(0,0,0,0.05); }
        .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
        .grid-4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 15px; }

        @media (max-width: 768px) {
            .grid-2, .grid-4 { grid-template-columns: 1fr; }
            header { flex-direction: column; align-items: flex-start; gap: 10px; }
        }

        /* Forms & Tables */
        label { display: block; font-size: 11px; font-weight: bold; color: var(--text-muted); margin-bottom: 5px; text-transform: uppercase; }
        input, select, textarea { width: 100%; padding: 8px 12px; border: 1px solid var(--border); border-radius: 6px; font-size: 13px; background: #f8fafc; margin-bottom: 12px; }
        input:focus, select:focus, textarea:focus { outline: none; border-color: var(--primary-light); background: white; box-shadow: 0 0 0 3px rgba(59,130,246,0.15); }

        table { width: 100%; border-collapse: collapse; margin-top: 10px; margin-bottom: 15px; background: white; }
        th, td { border: 1px solid var(--border); padding: 10px; text-align: left; font-size: 13px; }
        th { background: #f1f5f9; color: var(--text-main); font-weight: 600; }

        /* Buttons */
        .btn { padding: 9px 16px; border: none; border-radius: 6px; cursor: pointer; font-weight: 600; font-size: 13px; display: inline-flex; align-items: center; gap: 6px; transition: opacity 0.2s; }
        .btn:hover { opacity: 0.9; }
        .btn-primary { background: var(--primary-light); color: white; }
        .btn-success { background: var(--accent); color: white; }
        .btn-warning { background: var(--warning); color: white; }
        .btn-danger { background: var(--danger); color: white; }
        .btn-sm { padding: 5px 10px; font-size: 11px; }

        /* Metrics */
        .metric-card { background: white; border-left: 4px solid var(--primary-light); padding: 20px; border-radius: 6px; border: 1px solid var(--border); }
        .metric-card h3 { font-size: 11px; color: var(--text-muted); text-transform: uppercase; }
        .metric-card .val { font-size: 22px; font-weight: bold; color: var(--primary); margin-top: 5px; }

        .invoice-box { background: white; padding: 35px; border: 1px solid var(--border); border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); }

        .hsn-suggestions { position: absolute; background: white; border: 1px solid var(--border); max-height: 150px; overflow-y: auto; width: 100%; z-index: 50; box-shadow: 0 4px 6px rgba(0,0,0,0.1); border-radius: 0 0 6px 6px; display: none; }
        .hsn-suggestion-item { padding: 8px 12px; font-size: 12px; cursor: pointer; border-bottom: 1px solid #f1f5f9; }
        .hsn-suggestion-item:hover { background: #f8fafc; color: var(--primary); font-weight: bold; }

        @media print {
            header, .nav-tabs, .no-print, #loginOverlay { display: none !important; }
            body { background: white; padding: 0; }
            .container { max-width: 100%; margin: 0; padding: 0; }
            .invoice-box { border: none; padding: 0; box-shadow: none; }
        }
    </style>
</head>
<body>

    

    <header>
        <div class="brand">
            <h2>EXCEL ELECTRICALS</h2>
            <p>Choondy, Edathala, Aluva, Ernakulam, Kerala</p>
        </div>
        <div style="display: flex; gap: 10px; align-items: center;">
            <div class="user-badge">GSTIN: 32AAGPX3837Q1ZZ</div>
            <button class="btn btn-sm btn-danger no-print" onclick="lockApp()">🔒 Lock</button>
        </div>
    </header>

    <div class="nav-tabs">
        <div class="nav-tab active" onclick="switchTab('dash', this)">📊 Dashboard</div>
        <div class="nav-tab" onclick="switchTab('invoice', this)">📝 New Invoice</div>
        <div class="nav-tab" onclick="switchTab('gstr1', this)">📁 GSTR-1 (Sales)</div>
        <div class="nav-tab" onclick="switchTab('gstr2', this)">📥 GSTR-2 (Purchases)</div>
        <div class="nav-tab" onclick="switchTab('gstr3b', this)">📑 GSTR-3B Return</div>
        <div class="nav-tab" onclick="switchTab('inventory', this)">⚙️ Goods & Services</div>
        <div class="nav-tab" onclick="switchTab('customers', this)">👥 Customers</div>
        <div class="nav-tab" onclick="switchTab('accounts', this)">💰 Accounts</div>
        <div class="nav-tab" onclick="switchTab('pl', this)">📈 Profit & Loss</div>
        <div class="nav-tab" onclick="switchTab('eway', this)">🚚 E-Way Bill Hub</div>
    </div>

    <div class="container">

        <!-- 1. DASHBOARD -->
        <div id="panel-dash" class="panel active">
            <div class="grid-4" style="margin-bottom: 25px;">
                <div class="metric-card">
                    <h3>Total Invoices</h3>
                    <div class="val" id="dashCount">0</div>
                </div>
                <div class="metric-card" style="border-left-color: var(--accent);">
                    <h3>Total Revenue</h3>
                    <div class="val" id="dashRevenue">₹0.00</div>
                </div>
                <div class="metric-card" style="border-left-color: var(--warning);">
                    <h3>Collected Payments</h3>
                    <div class="val" id="dashCollected">₹0.00</div>
                </div>
                <div class="metric-card" style="border-left-color: var(--danger);">
                    <h3>Pending Dues</h3>
                    <div class="val" id="dashPending">₹0.00</div>
                </div>
            </div>

            <div class="card">
                <h3>Quick Actions</h3>
                <p style="font-size: 13px; color: var(--text-muted); margin-bottom: 20px;">Manage motor winding jobs, generate GST invoices, and file GSTR-1, GSTR-2 & GSTR-3B.</p>
                <div style="display: flex; gap: 10px; flex-wrap: wrap;">
                    <button class="btn btn-primary" onclick="switchTab('invoice', document.querySelectorAll('.nav-tab')[1])">➕ Create Tax Invoice</button>
                    <button class="btn btn-success" onclick="switchTab('inventory', document.querySelectorAll('.nav-tab')[5])">⚙️ Manage Goods & Services</button>
                    <button class="btn btn-warning" onclick="switchTab('gstr3b', document.querySelectorAll('.nav-tab')[4])">📑 File GSTR-3B Summary</button>
                </div>
            </div>
        </div>

        <!-- 2. NEW INVOICE / BILLING -->
        <div id="panel-invoice" class="panel">
            <div class="invoice-box">
                <div style="display: flex; justify-content: space-between; border-bottom: 2px solid var(--primary); padding-bottom: 20px; margin-bottom: 25px; flex-wrap: wrap; gap: 15px;">
                    <div>
                        <h2 style="color: var(--primary); font-size: 20px;">EXCEL ELECTRICALS</h2>
                        <p style="font-size: 11px; color: var(--text-muted);">Electric Motor Winding & Workshop Services</p>
                        <p style="font-size: 11px; color: var(--text-muted);">Choondy, Edathala, Aluva, Ernakulam, Kerala</p>
                        <p style="font-size: 11px; color: var(--text-muted);">GSTIN: 32AAGPX3837Q1ZZ</p>
                    </div>
                    <div style="text-align: right;">
                        <h3 style="color: var(--text-main); font-size: 16px;">TAX INVOICE</h3>
                        <div style="margin-top: 5px;">
                            <label style="text-align: right;">Invoice No:</label>
                            <input type="text" id="invNumber" value="EE/2026-27/001" style="width: 150px; text-align: right;">
                        </div>
                        <div>
                            <label style="text-align: right;">Date:</label>
                            <input type="date" id="invDate" style="width: 150px; text-align: right;">
                        </div>
                    </div>
                </div>

                <div class="grid-2" style="margin-bottom: 20px;">
                    <div>
                        <label>Select Customer:</label>
                        <select id="invCustomerSelect" onchange="fillCustomerDetails()">
                            <option value="">-- Choose Customer --</option>
                        </select>
                        <textarea id="custDetails" rows="2" placeholder="Client Name, Phone & Address"></textarea>
                    </div>
                    <div>
                        <label>Customer GSTIN:</label>
                        <input type="text" id="custGstin" placeholder="22AAAAA0000A1Z5">
                        <label>Job / Motor Reference:</label>
                        <input type="text" id="jobRef" placeholder="e.g. Crompton 3HP Motor Rewinding">
                    </div>
                </div>

                <div style="overflow-x: auto;">
                    <table id="invoiceTable">
                        <thead>
                            <tr>
                                <th>Description of Goods / Service (Auto HSN)</th>
                                <th style="width: 110px;">HSN/SAC</th>
                                <th style="width: 70px;">Qty</th>
                                <th style="width: 110px;">Rate (₹)</th>
                                <th style="width: 110px;">Total (₹)</th>
                                <th style="width: 45px;" class="no-print">Act</th>
                            </tr>
                        </thead>
                        <tbody id="invoiceItemsBody">
                            <tr>
                                <td style="position: relative;">
                                    <input type="text" class="item-desc" value="Electric Motor Rewinding (3HP)" oninput="searchHsn(this)" placeholder="Type item or service...">
                                    <div class="hsn-suggestions"></div>
                                </td>
                                <td><input type="text" class="item-hsn" value="995469"></td>
                                <td><input type="number" class="item-qty" value="1" oninput="calculateInvoice()"></td>
                                <td style="position: relative;"><input type="number" class="item-rate" value="2500" oninput="calculateInvoice()"></td>
                                <td class="item-total" style="font-weight: bold; text-align: right; padding-top: 14px;">2,500.00</td>
                                <td class="no-print"><button class="btn btn-danger btn-sm" onclick="removeRow(this)">X</button></td>
                            </tr>
                        </tbody>
                    </table>
                </div>

                <button class="btn btn-success btn-sm no-print" onclick="addRow()" style="margin-bottom: 20px;">➕ Add Item Row</button>

                <div style="display: flex; justify-content: flex-end;">
                    <div style="width: 300px; background: #f8fafc; padding: 15px; border-radius: 6px; border: 1px solid var(--border);">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 8px; font-size: 13px;">
                            <span>Taxable Amount:</span>
                            <span id="lblTaxable" style="font-weight: bold;">₹2,500.00</span>
                        </div>
                        <div style="display: flex; justify-content: space-between; margin-bottom: 8px; font-size: 13px;">
                            <span>CGST (9%) + SGST (9%):</span>
                            <span id="lblTax" style="font-weight: bold;">₹450.00</span>
                        </div>
                        <div style="display: flex; justify-content: space-between; border-top: 1px solid var(--border); padding-top: 10px; font-size: 15px; font-weight: bold; color: var(--primary);">
                            <span>Grand Total:</span>
                            <span id="lblGrand">₹2,950.00</span>
                        </div>
                    </div>
                </div>

                <div class="no-print" style="margin-top: 25px; display: flex; gap: 10px; justify-content: flex-end; flex-wrap: wrap;">
                    <button class="btn btn-success" onclick="saveAndLogInvoice()">💾 Save & Register Invoice</button>
                    <button class="btn btn-primary" onclick="window.print()">🖨️ Print / Preview Tax Invoice (PDF)</button>
                </div>
            </div>
        </div>

        <!-- 3. GSTR-1 (SALES) -->
        <div id="panel-gstr1" class="panel">
            <div class="card">
                <h3>GSTR-1 Outward Supplies (Sales Register)</h3>
                <p style="font-size: 13px; color: var(--text-muted); margin-bottom: 15px;">Detailed breakdown of all B2B and B2C invoices issued for GST filing.</p>
                <div style="overflow-x: auto;">
                    <table>
                        <thead>
                            <tr>
                                <th>Invoice No</th>
                                <th>Date</th>
                                <th>Customer / GSTIN</th>
                                <th>Taxable Value</th>
                                <th>GST (18%)</th>
                                <th>Grand Total</th>
                                <th class="no-print">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="gstr1TableBody">
                            <tr><td colspan="7" style="text-align: center; color: var(--text-muted);">No sales recorded yet.</td></tr>
                        </tbody>
                    </table>
                </div>
                <div style="display: flex; gap: 10px; margin-top: 15px;" class="no-print">
                    <button class="btn btn-warning" onclick="downloadGstr1Json()">📥 Download GSTR-1 JSON</button>
                    <button class="btn btn-danger btn-sm" onclick="clearLedger()">Clear Register</button>
                </div>
            </div>
        </div>

        <!-- 4. GSTR-2 (PURCHASES) -->
        <div id="panel-gstr2" class="panel">
            <div class="grid-2">
                <div class="card">
                    <h3>Add Purchase / Inward Bill</h3>
                    <p style="font-size: 13px; color: var(--text-muted); margin-bottom: 15px;">Log copper wire, bearings, varnish & spare part purchases for ITC claim.</p>
                    <label>Supplier Name:</label>
                    <input type="text" id="purSupplier" placeholder="e.g. Kerala Electrical Spares">
                    <label>Supplier GSTIN:</label>
                    <input type="text" id="purGstin" placeholder="32BBBBB0000B1Z2">
                    <label>Bill No & Date:</label>
                    <div class="grid-2" style="margin-bottom:0;">
                        <input type="text" id="purNo" placeholder="Bill #">
                        <input type="date" id="purDate">
                    </div>
                    <label>Taxable Amount (₹):</label>
                    <input type="number" id="purTaxable" placeholder="5000">
                    <label>GST Amount (18%):</label>
                    <input type="number" id="purGst" placeholder="900">
                    <button class="btn btn-success" onclick="savePurchaseBill()">💾 Save Purchase Bill</button>
                </div>
                <div class="card">
                    <h3>GSTR-2 Purchase Register (ITC)</h3>
                    <div style="max-height: 380px; overflow-y: auto;">
                        <table>
                            <thead>
                                <tr>
                                    <th>Supplier</th>
                                    <th>Taxable</th>
                                    <th>ITC (GST)</th>
                                    <th class="no-print">Act</th>
                                </tr>
                            </thead>
                            <tbody id="gstr2TableBody">
                                <tr><td colspan="4" style="text-align: center;">No purchase bills logged.</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- 5. GSTR-3B RETURN -->
        <div id="panel-gstr3b" class="panel">
            <div class="card" style="max-width: 750px; margin: 0 auto;">
                <h3 style="border-bottom: 2px solid var(--primary); padding-bottom: 10px; margin-bottom: 20px;">GSTR-3B Monthly Return Summary</h3>
                <div style="display: flex; justify-content: space-between; padding: 12px 0; border-bottom: 1px solid var(--border);">
                    <span>Total Outward Taxable Supplies (Sales):</span>
                    <span id="g3bSalesTaxable" style="font-weight: bold; color: var(--primary);">₹0.00</span>
                </div>
                <div style="display: flex; justify-content: space-between; padding: 12px 0; border-bottom: 1px solid var(--border);">
                    <span>Total Output Tax Payable (GST on Sales):</span>
                    <span id="g3bOutputTax" style="font-weight: bold; color: var(--danger);">₹0.00</span>
                </div>
                <div style="display: flex; justify-content: space-between; padding: 12px 0; border-bottom: 1px solid var(--border);">
                    <span>Eligible Input Tax Credit (ITC on Purchases):</span>
                    <span id="g3bItc" style="font-weight: bold; color: var(--accent);">₹0.00</span>
                </div>
                <div style="display: flex; justify-content: space-between; padding: 15px 0; font-size: 16px; font-weight: bold; background: #f8fafc; margin-top: 15px; padding-left: 10px; padding-right: 10px; border-radius: 6px;">
                    <span>Net Tax Payable in Cash:</span>
                    <span id="g3bNetPayable" style="color: var(--warning);">₹0.00</span>
                </div>
                <div style="margin-top: 20px; display: flex; gap: 10px;" class="no-print">
                    <button class="btn btn-primary" onclick="window.print()">🖨️ Print GSTR-3B Summary</button>
                </div>
            </div>
        </div>

        <!-- 6. GOODS & SERVICES CATALOG -->
        <div id="panel-inventory" class="panel">
            <div class="grid-2">
                <div class="card">
                    <h3 id="catFormTitle">Add Service or Spare Part</h3>
                    <p style="font-size: 13px; color: var(--text-muted); margin-bottom: 15px;">Configure workshop catalog items with auto HSN lookup.</p>
                    <input type="hidden" id="editItemIndex" value="-1">
                    <label>Description (Auto HSN):</label>
                    <div style="position: relative;">
                        <input type="text" id="itemCatName" oninput="searchCatalogHsn(this)" placeholder="e.g. Monoblock Pump Rewinding">
                        <div class="hsn-suggestions" id="catHsnSuggestions"></div>
                    </div>
                    <label>HSN / SAC Code:</label>
                    <input type="text" id="itemCatHsn" value="995469">
                    <label>Standard Rate (₹):</label>
                    <input type="number" id="itemCatRate" placeholder="1500">
                    <div style="display: flex; gap: 10px;">
                        <button class="btn btn-success" onclick="saveCatalogItem()">💾 Save Item</button>
                        <button class="btn btn-warning" onclick="resetCatalogForm()" id="cancelCatBtn" style="display:none;">Cancel</button>
                    </div>
                </div>
                <div class="card">
                    <h3>Workshop Rate Matrix</h3>
                    <div style="max-height: 380px; overflow-y: auto;">
                        <table>
                            <thead>
                                <tr>
                                    <th>Description</th>
                                    <th>HSN</th>
                                    <th>Rate</th>
                                    <th class="no-print">Action</th>
                                </tr>
                            </thead>
                            <tbody id="catalogTableBody"></tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- 7. CUSTOMER DIRECTORY -->
        <div id="panel-customers" class="panel">
            <div class="grid-2">
                <div class="card">
                    <h3 id="custFormTitle">Add New Customer</h3>
                    <p style="font-size: 13px; color: var(--text-muted); margin-bottom: 15px;">Add or edit client details.</p>
                    <input type="hidden" id="editCustIndex" value="-1">
                    <label>Customer / Business Name:</label>
                    <input type="text" id="newCustName" placeholder="e.g. Acme Industries">
                    <label>Phone Number:</label>
                    <input type="text" id="newCustPhone" placeholder="9847000000">
                    <label>Address:</label>
                    <textarea id="newCustAddress" rows="2" placeholder="Choondy, Aluva"></textarea>
                    <label>GSTIN (Optional):</label>
                    <input type="text" id="newCustGstin" placeholder="32AAAAA0000A1Z5">
                    <div style="display: flex; gap: 10px;">
                        <button class="btn btn-success" onclick="saveCustomer()">💾 Save Customer</button>
                        <button class="btn btn-warning" onclick="resetCustomerForm()" id="cancelCustBtn" style="display:none;">Cancel</button>
                    </div>
                </div>
                <div class="card">
                    <h3>Customer Directory</h3>
                    <div style="max-height: 380px; overflow-y: auto;">
                        <table>
                            <thead>
                                <tr>
                                    <th>Name & Phone</th>
                                    <th>GSTIN</th>
                                    <th class="no-print">Action</th>
                                </tr>
                            </thead>
                            <tbody id="customerTableBody">
                                <tr><td colspan="3" style="text-align: center;">No customers added yet.</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- 8. ACCOUNTS & PAYMENTS -->
        <div id="panel-accounts" class="panel">
            <div class="card">
                <h3>Accounts & Payment Collection</h3>
                <p style="font-size: 13px; color: var(--text-muted); margin-bottom: 15px;">Record collected payments and track pending balances.</p>
                <div style="overflow-x: auto;">
                    <table>
                        <thead>
                            <tr>
                                <th>Invoice No</th>
                                <th>Customer</th>
                                <th>Grand Total</th>
                                <th>Amount Paid (₹)</th>
                                <th>Balance Due</th>
                                <th>Status</th>
                                <th class="no-print">Action</th>
                            </tr>
                        </thead>
                        <tbody id="accountsTableBody">
                            <tr><td colspan="7" style="text-align: center;">No invoices found.</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- 9. PROFIT & LOSS -->
        <div id="panel-pl" class="panel">
            <div class="card" style="max-width: 650px; margin: 0 auto;">
                <h3 style="border-bottom: 2px solid var(--primary); padding-bottom: 10px; margin-bottom: 20px;">Excel Electricals - Profit & Loss Statement</h3>
                <div style="display: flex; justify-content: space-between; padding: 12px 0; border-bottom: 1px solid var(--border);">
                    <span>Total Billed Revenue:</span>
                    <span id="plTotalRevenue" style="font-weight: bold; color: var(--primary);">₹0.00</span>
                </div>
                <div style="display: flex; justify-content: space-between; padding: 12px 0; border-bottom: 1px solid var(--border);">
                    <span>Estimated Material & Winding Costs (~40%):</span>
                    <span id="plTotalCosts" style="font-weight: bold; color: var(--danger);">₹0.00</span>
                </div>
                <div style="display: flex; justify-content: space-between; padding: 15px 0; font-size: 16px; font-weight: bold; background: #f8fafc; margin-top: 15px; padding-left: 10px; padding-right: 10px; border-radius: 6px;">
                    <span>Net Operating Profit:</span>
                    <span id="plNetProfit" style="color: var(--accent);">₹0.00</span>
                </div>
                <button class="btn btn-primary no-print" onclick="window.print()" style="margin-top: 20px;">🖨️ Print P&L Statement (PDF)</button>
            </div>
        </div>

        <!-- 10. E-WAY BILL HUB -->
        <div id="panel-eway" class="panel">
            <div class="card" style="max-width: 650px; margin: 0 auto;">
                <h3>E-Way Bill Hub & PDF Preview</h3>
                <p style="font-size: 13px; color: var(--text-muted); margin-bottom: 15px;">Generate official E-Way JSON and preview delivery challans.</p>
                <label>Select Invoice:</label>
                <select id="ewayInvSelect" onchange="loadEwayDetails()"></select>
                <label>Transport Distance (KM):</label>
                <input type="number" id="ewayDist" value="30">
                <label>Vehicle Number:</label>
                <input type="text" id="ewayVehicle" value="KL07AB1234">
                
                <div style="display: flex; gap: 10px; margin-top: 15px; flex-wrap: wrap;">
                    <button class="btn btn-warning" onclick="generateEwayJson()">📥 Download E-Way JSON</button>
                    <button class="btn btn-primary" onclick="previewEwayChallan()">👁️ Preview E-Way Challan / PDF</button>
                </div>
            </div>
        </div>

    </div>

    <!-- E-WAY CHALLAN MODAL -->
    <div id="ewayModal" style="display:none; position: fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.6); z-index:10000; justify-content:center; align-items:center;">
        <div style="background:white; width:90%; max-width:650px; padding:25px; border-radius:8px; max-height:90vh; overflow-y:auto; position:relative;">
            <button onclick="document.getElementById('ewayModal').style.display='none'" style="position:absolute; top:15px; right:15px; background:none; border:none; font-size:18px; cursor:pointer;">✕</button>
            <div id="ewayChallanContent"></div>
            <div style="margin-top:20px; text-align:right;" class="no-print">
                <button class="btn btn-primary" onclick="window.print()">🖨️ Print Challan / PDF</button>
            </div>
        </div>
    </div>

    <script>
        // Security PIN Verification
        function verifyPin() {
            let pin = document.getElementById('loginPin').value;
            if(pin === '1234') {
                document.getElementById('loginOverlay').style.display = 'none';
            } else {
                alert('Incorrect Security PIN! Default is 1234');
            }
        }
        function lockApp() {
            document.getElementById('loginPin').value = '';
            document.getElementById('loginOverlay').style.display = 'flex';
        }

        // HSN/SAC Database
        const hsnDatabase = [
            { keyword: "rewind", hsn: "995469", desc: "Electric Motor Rewinding & Repair Services" },
            { keyword: "motor", hsn: "8501", desc: "Electric Motors and Generators (AC/DC)" },
            { keyword: "pump", hsn: "8413", desc: "Monoblock & Water Pumps" },
            { keyword: "fan", hsn: "8414", desc: "Ceiling / Exhaust / Cabin Fans" },
            { keyword: "bearing", hsn: "8482", desc: "Ball or Roller Bearings" },
            { keyword: "capacitor", hsn: "8532", desc: "Electrical Capacitors (Run/Start)" },
            { keyword: "copper", hsn: "7408", desc: "Super Enamelled Copper Winding Wire" },
            { keyword: "varnish", hsn: "3208", desc: "Insulating Electrical Varnish / Enamel" },
            { keyword: "starter", hsn: "8536", desc: "Motor Starters, Relays & Contactors" },
            { keyword: "switch", hsn: "8536", desc: "Electrical Switches & Control Gear" },
            { keyword: "cable", hsn: "8544", desc: "Insulated Wires, Cables & Flexibles" },
            { keyword: "service", hsn: "995469", desc: "General Maintenance & Electrical Servicing" }
        ];

        function searchHsn(inputElem) {
            let query = inputElem.value.toLowerCase();
            let suggestionsDiv = inputElem.nextElementSibling;
            if(query.length < 2) { suggestionsDiv.style.display = 'none'; return; }
            let matches = hsnDatabase.filter(item => item.keyword.includes(query) || item.desc.toLowerCase().includes(query));
            if(matches.length === 0) { suggestionsDiv.style.display = 'none'; return; }
            let html = '';
            matches.forEach(m => {
                html += <div class="hsn-suggestion-item" onclick="selectHsnSuggestion(this, '${m.hsn}', '${m.desc}')"><b>${m.hsn}</b> - ${m.desc}</div>;
            });
            suggestionsDiv.innerHTML = html;
            suggestionsDiv.style.display = 'block';
        }

        function selectHsnSuggestion(elem, hsn, desc) {
            let row = elem.closest('tr');
            row.querySelector('.item-desc').value = desc;
            row.querySelector('.item-hsn').value = hsn;
            elem.parentElement.style.display = 'none';
        }

        function searchCatalogHsn(inputElem) {
            let query = inputElem.value.toLowerCase();
            let suggestionsDiv = document.getElementById('catHsnSuggestions');
            if(query.length < 2) { suggestionsDiv.style.display = 'none'; return; }
            let matches = hsnDatabase.filter(item => item.keyword.includes(query) || item.desc.toLowerCase().includes(query));
            if(matches.length === 0) { suggestionsDiv.style.display = 'none'; return; }
            let html = '';
            matches.forEach(m => {
                html += <div class="hsn-suggestion-item" onclick="selectCatalogHsnSuggestion('${m.hsn}', '${m.desc}')"><b>${m.hsn}</b> - ${m.desc}</div>;
            });
            suggestionsDiv.innerHTML = html;
            suggestionsDiv.style.display = 'block';
        }

        function selectCatalogHsnSuggestion(hsn, desc) {
            document.getElementById('itemCatName').value = desc;
            document.getElementById('itemCatHsn').value = hsn;
            document.getElementById('catHsnSuggestions').style.display = 'none';
        }

        // Local Storage Initialization
        if(!localStorage.getItem('ee_customers')) {
            localStorage.setItem('ee_customers', JSON.stringify([
                { name: 'Walk-in Customer', phone: '9847000000', address: 'Aluva, Kerala', gstin: '' },
                { name: 'KSEB Substation Aluva', phone: '04842622000', address: 'Aluva, Ernakulam', gstin: '32AABCD1234E1Z5' }
            ]));
        }

        if(!localStorage.getItem('ee_catalog')) {
            localStorage.setItem('ee_catalog', JSON.stringify([
                { desc: 'Ceiling Fan Rewinding', hsn: '995469', rate: 600 },
                { desc: '1 HP Monoblock Pump Rewinding', hsn: '995469', rate: 1500 },
                { desc: '3 HP Three Phase Motor Rewinding', hsn: '995469', rate: 3500 },
                { desc: 'Bearing Replacement Service', hsn: '8482', rate: 350 }
            ]));
        }

        document.getElementById('invDate').valueAsDate = new Date();
        if(document.getElementById('purDate')) document.getElementById('purDate').valueAsDate = new Date();

        function switchTab(panelId, element) {
            document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
            document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
            document.getElementById('panel-' + panelId).classList.add('active');
            if(element) element.classList.add('active');

            if(panelId === 'gstr1') loadGstr1();
            if(panelId === 'gstr2') loadGstr2();
            if(panelId === 'gstr3b') calculateGstr3b();
            if(panelId === 'customers') loadCustomers();
            if(panelId === 'inventory') loadCatalog();
            if(panelId === 'accounts') loadAccounts();
            if(panelId === 'pl') calculatePL();
            if(panelId === 'eway') populateEwayDropdown();
        }

        function loadInvoiceDropdowns() {
            let custs = JSON.parse(localStorage.getItem('ee_customers') || '[]');
            let select = document.getElementById('invCustomerSelect');
            select.innerHTML = '<option value="">-- Choose Customer --</option>';
            custs.forEach((c, idx) => {
                select.innerHTML += <option value="${idx}">${c.name} (${c.phone})</option>;
            });
        }

        function fillCustomerDetails() {
            let idx = document.getElementById('invCustomerSelect').value;
            if(idx === '') return;
            let custs = JSON.parse(localStorage.getItem('ee_customers') || '[]');
            let c = custs[idx];
            document.getElementById('custDetails').value = ${c.name}\nPhone: ${c.phone}\nAddress: ${c.address};
            document.getElementById('custGstin').value = c.gstin || '';
        }

        function addRow() {
            let tbody = document.getElementById('invoiceItemsBody');
            let tr = document.createElement('tr');
            tr.innerHTML = `
                <td style="position: relative;">
                    <input type="text" class="item-desc" value="Rewinding service / Spare" oninput="searchHsn(this)" placeholder="Type item or service...">
                    <div class="hsn-suggestions"></div>
                </td>
                <td><input type="text" class="item-hsn" value="995469"></td>
                <td><input type="number" class="item-qty" value="1" oninput="calculateInvoice()"></td>
                <td><input type="number" class="item-rate" value="500" oninput="calculateInvoice()"></td>
                <td class="item-total" style="font-weight: bold; text-align: right; padding-top: 14px;">500.00</td>
                <td class="no-print"><button class="btn btn-danger btn-sm" onclick="removeRow(this)">X</button></td>
            `;
            tbody.appendChild(tr);
            calculateInvoice();
        }

        function removeRow(btn) {
            let row = btn.closest('tr');
            if(document.querySelectorAll('#invoiceItemsBody tr').length > 1) {
                row.remove();
                calculateInvoice();
            } else {
                alert('Invoice must contain at least one item.');
            }
        }

        function calculateInvoice() {
            let rows = document.querySelectorAll('#invoiceItemsBody tr');
            let totalTaxable = 0;
            rows.forEach(row => {
                let qty = parseFloat(row.querySelector('.item-qty').value) || 0;
                let rate = parseFloat(row.querySelector('.item-rate').value) || 0;
                let lineTotal = qty * rate;
                row.querySelector('.item-total').innerText = lineTotal.toFixed(2);
                totalTaxable += lineTotal;
            });
            let gstAmount = totalTaxable * 0.18;
            let grandTotal = totalTaxable + gstAmount;

            document.getElementById('lblTaxable').innerText = '₹' + totalTaxable.toFixed(2);
            document.getElementById('lblTax').innerText = '₹' + gstAmount.toFixed(2);
            document.getElementById('lblGrand').innerText = '₹' + grandTotal.toFixed(2);
        }

        function saveAndLogInvoice() {
            let invNo = document.getElementById('invNumber').value;
            let date = document.getElementById('invDate').value;
            let customer = document.getElementById('custDetails').value || 'Walk-in Customer';
            let gstin = document.getElementById('custGstin').value || '';
            let taxableStr = document.getElementById('lblTaxable').innerText;
            let taxStr = document.getElementById('lblTax').innerText;
            let grand = document.getElementById('lblGrand').innerText;
            let numericGrand = parseFloat(grand.replace('₹', '').replace(/,/g, '')) || 0;
            let numericTaxable = parseFloat(taxableStr.replace('₹', '').replace(/,/g, '')) || 0;
            let numericTax = parseFloat(taxStr.replace('₹', '').replace(/,/g, '')) || 0;

            if(!invNo) { alert('Please enter an invoice number.'); return; }

            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            ledger.push({ invNo, date, customer, gstin, taxable: numericTaxable, tax: numericTax, grand, paid: 0, balance: numericGrand, status: 'Unpaid' });
            localStorage.setItem('ee_erp_ledger', JSON.stringify(ledger));

            updateDashboardMetrics();
            alert('Invoice ' + invNo + ' successfully saved!');
            switchTab('gstr1', document.querySelectorAll('.nav-tab')[2]);
        }

        // GSTR-1
        function loadGstr1() {
            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            let tbody = document.getElementById('gstr1TableBody');
            tbody.innerHTML = '';
            if(ledger.length === 0) {
                tbody.innerHTML = '<tr><td colspan="7" style="text-align: center; color: var(--text-muted);">No sales recorded yet.</td></tr>';
                return;
            }
            ledger.forEach((item, index) => {
                tbody.innerHTML += `<tr>
                    <td>${item.invNo}</td>
                    <td>${item.date}</td>
                    <td>${item.customer.split('\n')[0]}<br><span style="font-size:11px; color:#64748b;">GSTIN: ${item.gstin || 'Unregistered'}</span></td>
                    <td>₹${(item.taxable || 0).toFixed(2)}</td>
                    <td>₹${(item.tax || 0).toFixed(2)}</td>
                    <td><b>${item.grand}</b></td>
                    <td class="no-print"><button class="btn btn-danger btn-sm" onclick="deleteLedgerItem(${index})">Delete</button></td>
                </tr>`;
            });
            updateDashboardMetrics();
        }

        function downloadGstr1Json() {
            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            if(ledger.length === 0) { alert('No sales data to export.'); return; }
            let blob = new Blob([JSON.stringify(ledger, null, 4)], {type: "application/json"});
            let url = URL.createObjectURL(blob);
            let a = document.createElement('a');
            a.href = url;
            a.download = "GSTR1_ExcelElectricals.json";
            a.click();
        }

        function clearLedger() {
            if(confirm('Are you sure you want to clear all invoice logs?')) {
                localStorage.removeItem('ee_erp_ledger');
                loadGstr1();
            }
        }

        // GSTR-2 (Purchases)
        function savePurchaseBill() {
            let supplier = document.getElementById('purSupplier').value;
            let gstin = document.getElementById('purGstin').value;
            let billNo = document.getElementById('purNo').value;
            let date = document.getElementById('purDate').value;
            let taxable = parseFloat(document.getElementById('purTaxable').value) || 0;
            let gst = parseFloat(document.getElementById('purGst').value) || 0;

            if(!supplier || !billNo) { alert('Please enter Supplier Name and Bill No.'); return; }

            let purchases = JSON.parse(localStorage.getItem('ee_erp_purchases') || '[]');
            purchases.push({ supplier, gstin, billNo, date, taxable, gst });
            localStorage.setItem('ee_erp_purchases', JSON.stringify(purchases));

            document.getElementById('purSupplier').value = '';
            document.getElementById('purGstin').value = '';
            document.getElementById('purNo').value = '';
            document.getElementById('purTaxable').value = '';
            document.getElementById('purGst').value = '';
            loadGstr2();
        }

        function loadGstr2() {
            let purchases = JSON.parse(localStorage.getItem('ee_erp_purchases') || '[]');
            let tbody = document.getElementById('gstr2TableBody');
            tbody.innerHTML = '';
            if(purchases.length === 0) {
                tbody.innerHTML = '<tr><td colspan="4" style="text-align: center;">No purchase bills logged.</td></tr>';
                return;
            }
            purchases.forEach((p, idx) => {
                tbody.innerHTML += `<tr>
                    <td><b>${p.supplier}</b><br><span style="font-size:11px; color:#64748b;">Bill: ${p.billNo} | GSTIN: ${p.gstin || '-'}</span></td>
                    <td>₹${p.taxable.toFixed(2)}</td>
                    <td style="color: var(--accent); font-weight:bold;">₹${p.gst.toFixed(2)}</td>
                    <td class="no-print"><button class="btn btn-danger btn-sm" onclick="deletePurchase(${idx})">Del</button></td>
                </tr>`;
            });
        }

        function deletePurchase(idx) {
            let purchases = JSON.parse(localStorage.getItem('ee_erp_purchases') || '[]');
            purchases.splice(idx, 1);
            localStorage.setItem('ee_erp_purchases', JSON.stringify(purchases));
            loadGstr2();
        }

        // GSTR-3B Summary
        function calculateGstr3b() {
            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            let purchases = JSON.parse(localStorage.getItem('ee_erp_purchases') || '[]');

            let totalTaxableSales = ledger.reduce((sum, item) => sum + (item.taxable || 0), 0);
            let totalOutputTax = ledger.reduce((sum, item) => sum + (item.tax || 0), 0);
            let totalItc = purchases.reduce((sum, p) => sum + (p.gst || 0), 0);
            let netPayable = Math.max(0, totalOutputTax - totalItc);

            document.getElementById('g3bSalesTaxable').innerText = '₹' + totalTaxableSales.toLocaleString('en-IN', {minimumFractionDigits: 2});
            document.getElementById('g3bOutputTax').innerText = '₹' + totalOutputTax.toLocaleString('en-IN', {minimumFractionDigits: 2});
            document.getElementById('g3bItc').innerText = '₹' + totalItc.toLocaleString('en-IN', {minimumFractionDigits: 2});
            document.getElementById('g3bNetPayable').innerText = '₹' + netPayable.toLocaleString('en-IN', {minimumFractionDigits: 2});
        }

        // Customer CRUD
        function saveCustomer() {
            let name = document.getElementById('newCustName').value;
            let phone = document.getElementById('newCustPhone').value;
            let address = document.getElementById('newCustAddress').value;
            let gstin = document.getElementById('newCustGstin').value;
            let editIdx = parseInt(document.getElementById('editCustIndex').value);

            if(!name) { alert('Please enter customer name.'); return; }

            let custs = JSON.parse(localStorage.getItem('ee_customers') || '[]');
            if(editIdx >= 0) { custs[editIdx] = { name, phone, address, gstin }; }
            else { custs.push({ name, phone, address, gstin }); }
            localStorage.setItem('ee_customers', JSON.stringify(custs));
            resetCustomerForm();
            loadCustomers();
        }

        function loadCustomers() {
            let custs = JSON.parse(localStorage.getItem('ee_customers') || '[]');
            let tbody = document.getElementById('customerTableBody');
            tbody.innerHTML = '';
            if(custs.length === 0) {
                tbody.innerHTML = '<tr><td colspan="3" style="text-align: center;">No customers added yet.</td></tr>';
                return;
            }
            custs.forEach((c, idx) => {
                tbody.innerHTML += `<tr>
                    <td><b>${c.name}</b><br><span style="font-size:11px; color:#64748b;">${c.phone} | ${c.address}</span></td>
                    <td>${c.gstin || '-'}</td>
                    <td class="no-print">
                        <button class="btn btn-primary btn-sm" onclick="editCustomer(${idx})">Edit</button>
                        <button class="btn btn-danger btn-sm" onclick="deleteCustomer(${idx})">Del</button>
                    </td>
                </tr>`;
            });
            loadInvoiceDropdowns();
        }

        function editCustomer(idx) {
            let custs = JSON.parse(localStorage.getItem('ee_customers') || '[]');
            let c = custs[idx];
            document.getElementById('newCustName').value = c.name;
            document.getElementById('newCustPhone').value = c.phone;
            document.getElementById('newCustAddress').value = c.address;
            document.getElementById('newCustGstin').value = c.gstin;
            document.getElementById('editCustIndex').value = idx;
            document.getElementById('custFormTitle').innerText = 'Edit Customer';
            document.getElementById('cancelCustBtn').style.display = 'inline-block';
        }

        function resetCustomerForm() {
            document.getElementById('newCustName').value = '';
            document.getElementById('newCustPhone').value = '';
            document.getElementById('newCustAddress').value = '';
            document.getElementById('newCustGstin').value = '';
            document.getElementById('editCustIndex').value = '-1';
            document.getElementById('custFormTitle').innerText = 'Add New Customer';
            document.getElementById('cancelCustBtn').style.display = 'none';
        }

        function deleteCustomer(idx) {
            let custs = JSON.parse(localStorage.getItem('ee_customers') || '[]');
            custs.splice(idx, 1);
            localStorage.setItem('ee_customers', JSON.stringify(custs));
            loadCustomers();
        }

        // Goods & Services Catalog CRUD
        function saveCatalogItem() {
            let desc = document.getElementById('itemCatName').value;
            let hsn = document.getElementById('itemCatHsn').value;
            let rate = parseFloat(document.getElementById('itemCatRate').value) || 0;
            let editIdx = parseInt(document.getElementById('editItemIndex').value);

            if(!desc) { alert('Please enter item description.'); return; }

            let catalog = JSON.parse(localStorage.getItem('ee_catalog') || '[]');
            if(editIdx >= 0) {
                catalog[editIdx] = { desc, hsn, rate };
            } else {
                catalog.push({ desc, hsn, rate });
            }
            localStorage.setItem('ee_catalog', JSON.stringify(catalog));
            resetCatalogForm();
            loadCatalog();
        }

        function loadCatalog() {
            let catalog = JSON.parse(localStorage.getItem('ee_catalog') || '[]');
            let tbody = document.getElementById('catalogTableBody');
            tbody.innerHTML = '';
            if(catalog.length === 0) {
                tbody.innerHTML = '<tr><td colspan="4" style="text-align: center;">No catalog items.</td></tr>';
                return;
            }
            catalog.forEach((item, idx) => {
                tbody.innerHTML += `<tr>
                    <td><b>${item.desc}</b></td>
                    <td>${item.hsn}</td>
                    <td>₹${item.rate.toFixed(2)}</td>
                    <td class="no-print">
                        <button class="btn btn-primary btn-sm" onclick="editCatalog(${idx})">Edit</button>
                        <button class="btn btn-danger btn-sm" onclick="deleteCatalog(${idx})">Del</button>
                    </td>
                </tr>`;
            });
        }

        function editCatalog(idx) {
            let catalog = JSON.parse(localStorage.getItem('ee_catalog') || '[]');
            let item = catalog[idx];
            document.getElementById('itemCatName').value = item.desc;
            document.getElementById('itemCatHsn').value = item.hsn;
            document.getElementById('itemCatRate').value = item.rate;
            document.getElementById('editItemIndex').value = idx;
            document.getElementById('catFormTitle').innerText = 'Edit Service / Spare';
            document.getElementById('cancelCatBtn').style.display = 'inline-block';
        }

        function resetCatalogForm() {
            document.getElementById('itemCatName').value = '';
            document.getElementById('itemCatHsn').value = '995469';
            document.getElementById('itemCatRate').value = '';
            document.getElementById('editItemIndex').value = '-1';
            document.getElementById('catFormTitle').innerText = 'Add Service or Spare Part';
            document.getElementById('cancelCatBtn').style.display = 'none';
        }

        function deleteCatalog(idx) {
            let catalog = JSON.parse(localStorage.getItem('ee_catalog') || '[]');
            catalog.splice(idx, 1);
            localStorage.setItem('ee_catalog', JSON.stringify(catalog));
            loadCatalog();
        }

        // Accounts & Payments
        function loadAccounts() {
            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            let tbody = document.getElementById('accountsTableBody');
            tbody.innerHTML = '';
            if(ledger.length === 0) {
                tbody.innerHTML = '<tr><td colspan="7" style="text-align: center;">No invoices found.</td></tr>';
                return;
            }
            ledger.forEach((item, index) => {
                let numericGrand = parseFloat(item.grand.replace('₹', '').replace(/,/g, '')) || 0;
                let paid = item.paid || 0;
                let balance = numericGrand - paid;
                tbody.innerHTML += `<tr>
                    <td>${item.invNo}</td>
                    <td>${item.customer.split('\n')[0]}</td>
                    <td>${item.grand}</td>
                    <td>₹<input type="number" id="pay_${index}" value="${paid}" style="width: 90px; display:inline-block;" oninput="updatePayment(${index})"></td>
                    <td style="font-weight:bold; color:var(--danger);">₹${balance.toFixed(2)}</td>
                    <td><span style="color: ${item.status==='Paid'?'var(--accent)':'var(--danger)'}; font-weight:bold;">${item.status}</span></td>
                    <td class="no-print"><button class="btn btn-success btn-sm" onclick="markPaid(${index})">Mark Paid</button></td>
                </tr>`;
            });
        }

        function updatePayment(index) {
            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            let numericGrand = parseFloat(ledger[index].grand.replace('₹', '').replace(/,/g, '')) || 0;
            let paid = parseFloat(document.getElementById('pay_' + index).value) || 0;
            ledger[index].paid = paid;
            ledger[index].balance = numericGrand - paid;
            ledger[index].status = paid >= numericGrand ? 'Paid' : (paid > 0 ? 'Partial' : 'Unpaid');
            localStorage.setItem('ee_erp_ledger', JSON.stringify(ledger));
            loadAccounts();
            updateDashboardMetrics();
        }

        function markPaid(index) {
            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            let numericGrand = parseFloat(ledger[index].grand.replace('₹', '').replace(/,/g, '')) || 0;
            document.getElementById('pay_' + index).value = numericGrand;
            updatePayment(index);
        }

        // P&L
        function calculatePL() {
            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            let totalRev = ledger.reduce((sum, item) => sum + (parseFloat(item.grand.replace('₹', '').replace(/,/g, '')) || 0), 0);
            let totalCosts = totalRev * 0.40;
            let netProfit = totalRev - totalCosts;

            document.getElementById('plTotalRevenue').innerText = '₹' + totalRev.toLocaleString('en-IN', {minimumFractionDigits: 2});
            document.getElementById('plTotalCosts').innerText = '₹' + totalCosts.toLocaleString('en-IN', {minimumFractionDigits: 2});
            document.getElementById('plNetProfit').innerText = '₹' + netProfit.toLocaleString('en-IN', {minimumFractionDigits: 2});
        }

        // Dashboard Metrics
        function updateDashboardMetrics() {
            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            document.getElementById('dashCount').innerText = ledger.length;
            let totalRev = ledger.reduce((sum, item) => sum + (parseFloat(item.grand.replace('₹', '').replace(/,/g, '')) || 0), 0);
            let totalCollected = ledger.reduce((sum, item) => sum + (item.paid || 0), 0);
            let totalPending = totalRev - totalCollected;

            document.getElementById('dashRevenue').innerText = '₹' + totalRev.toLocaleString('en-IN', {minimumFractionDigits: 2});
            document.getElementById('dashCollected').innerText = '₹' + totalCollected.toLocaleString('en-IN', {minimumFractionDigits: 2});
            document.getElementById('dashPending').innerText = '₹' + totalPending.toLocaleString('en-IN', {minimumFractionDigits: 2});
        }

        // E-Way Bill Hub
        function populateEwayDropdown() {
            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            let select = document.getElementById('ewayInvSelect');
            select.innerHTML = '';
            if(ledger.length === 0) {
                select.innerHTML = '<option value="">No invoices available</option>';
                return;
            }
            ledger.forEach((item, idx) => {
                select.innerHTML += <option value="${idx}">Invoice ${item.invNo} - ${item.customer.split('\n')[0]} (${item.grand})</option>;
            });
        }

        function generateEwayJson() {
            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            let idx = document.getElementById('ewayInvSelect').value;
            if(idx === '' || ledger.length === 0) { alert('Please select a valid invoice.'); return; }
            let inv = ledger[idx];
            let dist = document.getElementById('ewayDist').value;
            let vehicle = document.getElementById('ewayVehicle').value;

            let payload = {
                version: "1.0.35",
                userGstin: "32AAGPX3837Q1ZZ",
                supplyType: "O",
                docNo: inv.invNo,
                totInvValue: parseFloat(inv.grand.replace('₹', '').replace(/,/g, '')),
                transDistance: parseInt(dist),
                vehicleNo: vehicle
            };

            let blob = new Blob([JSON.stringify(payload, null, 4)], {type: "application/json"});
            let url = URL.createObjectURL(blob);
            let a = document.createElement('a');
            a.href = url;
            a.download = "EWayBill_" + inv.invNo.replace(/[/\\?%*:|"<>]/g, '-') + ".json";
            a.click();
        }

        function previewEwayChallan() {
            let ledger = JSON.parse(localStorage.getItem('ee_erp_ledger') || '[]');
            let idx = document.getElementById('ewayInvSelect').value;
            if(idx === '' || ledger.length === 0) { alert('Please select a valid invoice.'); return; }
            let inv = ledger[idx];
            let dist = document.getElementById('ewayDist').value;
            let vehicle = document.getElementById('ewayVehicle').value;

            let html = `
                <div style="border-bottom: 2px solid #1e3a8a; padding-bottom: 12px; margin-bottom: 15px;">
                    <h2>EXCEL ELECTRICALS - E-WAY CHALLAN</h2>
                    <p style="font-size: 11px; color: #64748b;">Choondy, Edathala, Aluva | GSTIN: 32AAGPX3837Q1ZZ</p>
                </div>
                <div style="display:grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 20px; font-size: 12px;">
                    <div><b>Invoice Number:</b> ${inv.invNo}</div>
                    <div><b>Date:</b> ${inv.date}</div>
                    <div><b>Customer:</b><br>${inv.customer.replace(/\n/g, '<br>')}</div>
                    <div><b>Transport:</b><br>Vehicle No: <b>${vehicle}</b><br>Distance: <b>${dist} KM</b></div>
                </div>
                <div style="background:#f8fafc; padding:12px; border-radius:6px; font-size:14px; font-weight:bold; display:flex; justify-content:space-between;">
                    <span>Total Consignment Value:</span>
                    <span>${inv.grand}</span>
                </div>
            `;
            document.getElementById('ewayChallanContent').innerHTML = html;
            document.getElementById('ewayModal').style.display = 'flex';
        }

        loadInvoiceDropdowns();
        updateDashboardMetrics();
    </script>
</body>
</html>
