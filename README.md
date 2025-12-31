<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>USD Currency Counter</title>
    <style>
        :root {
            --primary-green: #2e7d32;
            --bg-color: #f4f7f6;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg-color);
            display: flex;
            justify-content: center;
            padding: 20px;
        }

        .container {
            background: white;
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
            max-width: 500px;
            width: 100%;
        }

        h1 {
            color: var(--primary-green);
            text-align: center;
            margin-bottom: 1.5rem;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th {
            text-align: left;
            border-bottom: 2px solid #eee;
            padding: 10px;
        }

        td {
            padding: 12px 10px;
            border-bottom: 1px solid #eee;
        }

        input {
            width: 80px;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 1rem;
            text-align: center;
        }

        input:focus {
            outline: none;
            border-color: var(--primary-green);
            box-shadow: 0 0 5px rgba(46, 125, 50, 0.3);
        }

        .total-cell {
            font-weight: bold;
            color: #444;
            text-align: right;
        }

        .grand-total-section {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 3px double #eee;
            text-align: right;
        }

        #grand-total {
            font-size: 2rem;
            color: var(--primary-green);
            display: block;
        }

        .label {
            font-size: 0.9rem;
            color: #666;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Money Counter</h1>
    
    <table>
        <thead>
            <tr>
                <th>Denomination</th>
                <th>Quantity</th>
                <th style="text-align: right;">Total</th>
            </tr>
        </thead>
        <tbody id="currency-rows">
            </tbody>
    </table>

    <div class="grand-total-section">
        <span class="label">Total Amount</span>
        <span id="grand-total">$0.00</span>
    </div>
</div>

<script>
    // List of USD denominations
    const denominations = [
        { label: '$100 Bills', value: 100 },
        { label: '$50 Bills', value: 50 },
        { label: '$20 Bills', value: 20 },
        { label: '$10 Bills', value: 10 },
        { label: '$5 Bills', value: 5 },
        { label: '$2 Bills', value: 2 },
        { label: '$1 Bills', value: 1 },
        { label: 'Quarters (25¢)', value: 0.25 },
        { label: 'Dimes (10¢)', value: 0.10 },
        { label: 'Nickels (5¢)', value: 0.05 },
        { label: 'Pennies (1¢)', value: 0.01 }
    ];

    const tableBody = document.getElementById('currency-rows');

    // Create the table rows dynamically
    denominations.forEach((denom, index) => {
        const row = document.createElement('tr');
        row.innerHTML = `
            <td>${denom.label}</td>
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
            
            // Update the specific row total display
            document.getElementById(`total-${index}`).innerText = rowTotal.toLocaleString(undefined, {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2
            });

            grandTotal += rowTotal;
        });

        // Update the big grand total at the bottom
        document.getElementById('grand-total').innerText = '$' + grandTotal.toLocaleString(undefined, {
            minimumFractionDigits: 2,
            maximumFractionDigits: 2
        });
    }
</script>

</body>
</html>