 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Serene | Currency Automation</title>
    <style>
        :root {
            --serene-green: #4a7c59;
            --serene-light: #f8faf9;
            --serene-accent: #8fc0a9;
            --text-dark: #2f3e46;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--serene-light);
            color: var(--text-dark);
            display: flex;
            justify-content: center;
            padding: 40px 20px;
            margin: 0;
        }

        .container {
            background: white;
            padding: 3rem;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.05);
            max-width: 600px;
            width: 100%;
            border-top: 8px solid var(--serene-green);
        }

        .header {
            text-align: center;
            margin-bottom: 2rem;
        }

        .header h1 {
            margin: 0;
            font-size: 2.5rem;
            letter-spacing: 2px;
            color: var(--serene-green);
            text-transform: uppercase;
        }

        .header p {
            margin: 5px 0 0;
            color: #888;
            font-style: italic;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th {
            text-align: left;
            text-transform: uppercase;
            font-size: 0.8rem;
            letter-spacing: 1px;
            color: #999;
            padding: 10px;
            border-bottom: 1px solid #eee;
        }

        td {
            padding: 15px 10px;
            border-bottom: 1px solid #f9f9f9;
        }

        .denom-label {
            font-weight: 600;
            color: var(--text-dark);
        }

        input {
            width: 100px;
            padding: 10px;
            border: 2px solid #eee;
            border-radius: 8px;
            font-size: 1.1rem;
            text-align: center;
            transition: all 0.3s ease;
        }

        input:focus {
            outline: none;
            border-color: var(--serene-accent);
            background-color: #fff;
        }

        /* Removes arrows from number input */
        input::-webkit-outer-spin-button,
        input::-webkit-inner-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }

        .total-cell {
            font-weight: 700;
            color: var(--serene-green);
            text-align: right;
            font-size: 1.1rem;
        }

        .grand-total-section {
            margin-top: 30px;
            padding: 25px;
            background-color: var(--serene-light);
            border-radius: 12px;
            text-align: center;
        }

        .grand-total-label {
            display: block;
            font-size: 0.9rem;
            color: #666;
            text-transform: uppercase;
            margin-bottom: 5px;
        }

        #grand-total {
            font-size: 3rem;
            font-weight: 800;
            color: var(--serene-green);
        }

        .footer {
            text-align: center;
            margin-top: 20px;
            font-size: 0.8rem;
            color: #ccc;
        }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <h1>Serene</h1>
        <p>Currency Management Solutions</p>
    </div>
    
    <table>
        <thead>
            <tr>
                <th>Denomination</th>
                <th>Quantity</th>
                <th style="text-align: right;">Subtotal</th>
            </tr>
        </thead>
        <tbody id="currency-rows">
            </tbody>
    </table>

    <div class="grand-total-section">
        <span class="grand-total-label">Grand Total Balance</span>
        <span id="grand-total">$0.00</span>
    </div>

    <div class="footer">
        &copy; 2026 Serene Systems. Prepared for Christian Martinez.
    </div>
</div>

<script>
    const denominations = [
        { label: '$100 Bills', value: 100 },
        { label: '$50 Bills', value: 50 },
        { label: '$20 Bills', value: 20 },
        { label: '$10 Bills', value: 10 },
        { label: '$5 Bills', value: 5 },
        { label: '$1 Bills', value: 1 },
        { label: 'Quarters', value: 0.25 },
        { label: 'Dimes', value: 0.10 },
        { label: 'Nickels', value: 0.05 },
        { label: 'Pennies', value: 0.01 }
    ];

    const tableBody = document.getElementById('currency-rows');

    denominations.forEach((denom, index) => {
        const row = document.createElement('tr');
        row.innerHTML = `
            <td class="denom-label">${denom.label}</td>
            <td>
                <input type="number" 
                       id="qty-${index}" 
                       min="0" 
                       placeholder="0" 
                       oninput="calculate()">
            </td>
            <td class="total-cell">$<span id="total-${index}">0.00</span></td>
        `;
        tableBody.appendChild(row);
    });

    function calculate() {
        let grandTotal = 0;

        denominations.forEach((denom, index) => {
            const qtyInput = document.getElementById(`qty-${index}`);
            const qty = parseFloat(qtyInput.value) || 0;
            const rowTotal = qty * denom.value;
            
            document.getElementById(`total-${index}`).innerText = rowTotal.toLocaleString(undefined, {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2
            });

            grandTotal += rowTotal;
        });

        document.getElementById('grand-total').innerText = '$' + grandTotal.toLocaleString(undefined, {
            minimumFractionDigits: 2,
            maximumFractionDigits: 2
        });
    }
</script>

</body>
</html>