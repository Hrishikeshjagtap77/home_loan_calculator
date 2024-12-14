<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Home Loan EMI Calculator</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.0.1/chart.min.css">
    <style>
        table tbody td {
            padding: 15px;
            /* Add padding for better spacing in cells */
            text-align: left;
            /* Align text for readability */
        }

        table tbody tr {
            margin-bottom: 10px;
            /* Increase space between table rows */
        }

        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            padding: 0;
            background: url('bg.jpg') no-repeat center center fixed;
            background-size: cover;
            color: #333;
        }

        .container {
            max-width: 900px;
            margin: 20px auto;
            padding: 30px;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 10px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
        }

        h1 {
            text-align: center;
            color: #0077b6;
            margin-bottom: 30px;
        }

        .form-group {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
        }

        .form-group label {
            flex: 1;
            margin-right: 10px;
            font-weight: bold;
            color: #555;
        }

        .form-group input {
            flex: 2;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 1rem;
        }

        button {
            padding: 10px 20px;
            margin: 10px 0;
            border: none;
            border-radius: 5px;
            font-size: 1rem;
            cursor: pointer;
            background-color: #0077b6;
            color: #ffffff;
            transition: background-color 0.3s, transform 0.2s;
        }

        button:hover {
            background-color: #005f8a;
            transform: scale(1.05);
        }

        .results {
            margin-top: 30px;
        }

        .chart-container {
            margin: 20px 0;
            text-align: center;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        table,
        th,
        td {
            border: 1px solid #ddd;
        }

        th,
        td {
            padding: 12px;
            text-align: center;
            font-size: 0.9rem;
        }

        th {
            background-color: #0077b6;
            color: #ffffff;
        }

        tr:nth-child(even) {
            background-color: #f9f9f9;
        }

        .extra-repayment-container {
            margin-top: 20px;
        }

        .panel {
            padding: 0 15px;
            display: none;
            overflow: hidden;
            background-color: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin: 10px 69px 20px 20px;
        }

        .panel label {
            display: block;
            margin: 5px 0;
        }

        .totals {
            margin-top: 20px;
            padding: 15px;
            background-color: #f9f9f9;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            font-size: 1.1rem;
            color: #333;
        }

        .totals h3 {
            color: #0077b6;
            margin-bottom: 10px;
        }

        @media screen and (max-width: 768px) {
            .form-group {
                flex-direction: column;
                align-items: flex-start;
            }

            .form-group label {
                margin-bottom: 5px;
            }

            .form-group input {
                width: 100%;
            }

            button {
                width: 100%;
            }
        }

        .funbtn {
            background-color: red !important;
            margin-right: 20px;
        }

        .panel {
            display: none;
            overflow: hidden;
            background-color: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-bottom: 15px;
            /* Increased spacing between panels */
            padding: 15px;
            /* Added more padding inside panels */
        }

        .panel .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            /* Increased space between grid items */
        }

        .panel label {
            display: flex;
            flex-direction: column;
            align-items: start;
            margin-bottom: 10px;
            /* Added margin between labels */
        }

        .panel .grid label {
            margin-bottom: 15px;
            /* Increased space between input rows */
        }

        .grid input {
            margin-top: 5px;
            /* Added margin above input for better spacing */
            padding: 8px;
        }

        .accordion {
            background-color: #0077b6;
            color: white;
            cursor: pointer;
            padding: 13px;
            margin: 15px 10px;
            border: none;
            outline: none;
            text-align: left;
            font-size: 1.0rem;
            transition: 0.4s;
            border-radius: 5px;
        }

        .accordion.active {
            background-color: #005f8a;
        }
    </style>
</head>

<body>
    <div class="container">
        <h1>Home Loan EMI Calculator</h1>

        <div class="form-group">
            <label for="loanAmount">Loan Amount (₹):</label>
            <input type="number" id="loanAmount" value="4000000">
        </div>

        <div class="form-group">
            <label for="interestRate">Interest Rate (%):</label>
            <input type="number" id="interestRate" value="9">
        </div>

        <div class="form-group">
            <label for="loanTenure">Loan Tenure (Years):</label>
            <input type="number" id="loanTenure" value="20">
        </div>

        <div class="form-group">
            <label for="startDate">Start Date:</label>
            <input type="month" id="startDate" value="2024-01">
        </div>

        <div class="extra-repayment-container" id="extraRepaymentContainer">
            <h3>Custom Extra Repayments (₹ per month):</h3>
        </div>
        
        <button class="funbtn" onclick="generateRepaymentInputs()">Generate Repayment Inputs</button>
        <button class="funbtn" onclick="calculateEMI()">Calculate EMI</button>
        <button type="reset" class="funbtn" onclick="resetToDefault()">Reset</button>

        <div class="totals">
            <h3>Total Summary</h3>
            <p><b>Principal Amount Paid:</b> ₹<span id="totalPrincipal">0</span></p>
            <p><b>Interest Paid:</b> ₹<span id="totalInterest">0</span></p>
            <p><b>Total Amount Paid:</b> ₹<span id="totalPaid">0</span></p>
        </div>


        <div class="results">
            <h2>Monthly EMI: ₹<span id="monthlyEMI">0</span></h2>
            <table>
                <thead>
                    <tr>
                        <th>Month</th>
                        <th>Principal Paid (₹)</th>
                        <th>Interest Paid (₹)</th>
                        <th>Extra Repayment (₹)</th>
                        <th>Total Payment (₹)</th>
                        <th>Remaining Balance (₹)</th>
                    </tr>
                </thead>
                <tbody id="paymentSchedule">
                    <!-- Dynamic rows will be inserted here -->
                </tbody>
            </table>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.0.1/chart.min.js"></script>
    <script>
        function generateRepaymentInputs() {
            const loanTenureYears = parseInt(document.getElementById('loanTenure').value);
            const months = loanTenureYears * 12;
            const container = document.getElementById('extraRepaymentContainer');
            const startDate = new Date(document.getElementById('startDate').value);

            container.innerHTML = '<h3>Custom Extra Repayments (₹ per month):</h3>';

            const yearGroups = {};

            for (let i = 0; i < months; i++) {
                const currentMonth = new Date(startDate);
                currentMonth.setMonth(startDate.getMonth() + i);
                const monthName = currentMonth.toLocaleString('default', { month: 'long' });
                const year = currentMonth.getFullYear();

                if (!yearGroups[year]) {
                    yearGroups[year] = [];
                }

                yearGroups[year].push({
                    monthName,
                    inputId: `extraRepayment${i + 1}`
                });
            }

            for (const [year, months] of Object.entries(yearGroups)) {
                const accordion = document.createElement('button');
                accordion.className = 'accordion';
                accordion.textContent = `Year ${year}`;

                const panel = document.createElement('div');
                panel.className = 'panel';

                const grid = document.createElement('div');
                grid.className = 'grid';

                months.forEach(({ monthName, inputId }) => {
                    const label = document.createElement('label');
                    label.innerHTML = `
                <span>${monthName}</span>
                <input type="number" id="${inputId}" value="0">
            `;
                    grid.appendChild(label);
                });

                panel.appendChild(grid);
                container.appendChild(accordion);
                container.appendChild(panel);

                accordion.addEventListener('click', function () {
                    this.classList.toggle('active');
                    const panel = this.nextElementSibling;
                    panel.style.display = panel.style.display === 'block' ? 'none' : 'block';
                });
            }
        }


        function calculateEMI() {
            const loanAmount = parseFloat(document.getElementById('loanAmount').value);
            const interestRate = parseFloat(document.getElementById('interestRate').value) / 12 / 100;
            const loanTenure = parseInt(document.getElementById('loanTenure').value) * 12;
            const startDate = new Date(document.getElementById('startDate').value);

            const emi = (loanAmount * interestRate * Math.pow(1 + interestRate, loanTenure)) /
                (Math.pow(1 + interestRate, loanTenure) - 1);
            document.getElementById('monthlyEMI').innerText = emi.toFixed(2);

            generatePaymentSchedule(loanAmount, interestRate, loanTenure, emi, startDate);
        }

        function resetToDefault() {
            document.getElementById('loanAmount').value = 4000000; // Default Loan Amount
            document.getElementById('interestRate').value = 9; // Default Interest Rate
            document.getElementById('loanTenure').value = 20; // Default Loan Tenure
            document.getElementById('startDate').value = "2024-01"; // Default Start Date

            // Clear the extra repayment inputs
            const extraRepaymentContainer = document.getElementById('extraRepaymentContainer');
            extraRepaymentContainer.innerHTML = '<h3>Custom Extra Repayments (₹ per month):</h3>';

            // Reset Results
            document.getElementById('monthlyEMI').innerText = "0";
            document.getElementById('totalPrincipal').innerText = "0";
            document.getElementById('totalInterest').innerText = "0";
            document.getElementById('totalPaid').innerText = "0";

            const paymentSchedule = document.getElementById('paymentSchedule');
            paymentSchedule.innerHTML = ''; // Clear the payment schedule table

            // Optionally, clear any charts (if applicable)
            const emiChartCanvas = document.getElementById('emiChart');
            if (emiChartCanvas && emiChartCanvas.parentElement) {
                emiChartCanvas.parentElement.innerHTML = '<canvas id="emiChart"></canvas>';
            }
        }


        function generatePaymentSchedule(loanAmount, interestRate, loanTenure, emi, startDate) {
            let balance = loanAmount;
            const paymentSchedule = document.getElementById('paymentSchedule');
            paymentSchedule.innerHTML = '';

            const principalData = [];
            const interestData = [];
            let totalPrincipalPaid = 0;
            let totalInterestPaid = 0;

            for (let month = 0; month < loanTenure; month++) {
                const extraRepayment = parseFloat(document.getElementById(`extraRepayment${month + 1}`).value) || 0;

                const interest = balance * interestRate;
                const principal = emi - interest;
                const totalPrincipal = principal + extraRepayment;
                balance -= totalPrincipal;

                if (balance < 0) {
                    balance = 0;
                }

                // Accumulate totals
                totalPrincipalPaid += totalPrincipal;
                totalInterestPaid += interest;

                principalData.push(totalPrincipal);
                interestData.push(interest);

                const paymentDate = new Date(startDate);
                paymentDate.setMonth(startDate.getMonth() + month);

                const monthName = paymentDate.toLocaleString('default', { month: 'long' });
                const year = paymentDate.getFullYear();

                paymentSchedule.innerHTML += `
                    <tr>
                        <td>${monthName} ${year}</td>
                        <td>${principal.toFixed(2)}</td>
                        <td>${interest.toFixed(2)}</td>
                        <td>${extraRepayment.toFixed(2)}</td>
                        <td>${(emi + extraRepayment).toFixed(2)}</td>
                        <td>${balance.toFixed(2)}</td>
                    </tr>`;

                if (balance === 0) break;
            }

            // Update total summary
            document.getElementById('totalPrincipal').innerText = totalPrincipalPaid.toFixed(2);
            document.getElementById('totalInterest').innerText = totalInterestPaid.toFixed(2);
            document.getElementById('totalPaid').innerText = (totalPrincipalPaid + totalInterestPaid).toFixed(2);

            updateChart(principalData, interestData);
        }

        function updateChart(principalData, interestData) {
            const ctx = document.getElementById('emiChart').getContext('2d');
            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: principalData.map((_, i) => `Month ${i + 1}`),
                    datasets: [
                        {
                            label: 'Principal Paid (with Extra)',
                            data: principalData,
                            borderColor: 'rgba(75, 192, 192, 1)',
                            fill: false,
                        },
                        {
                            label: 'Interest Paid',
                            data: interestData,
                            borderColor: 'rgba(255, 99, 132, 1)',
                            fill: false,
                        }
                    ]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'top',
                        },
                    },
                },
            });
        }
    </script>
</body>

</html>
