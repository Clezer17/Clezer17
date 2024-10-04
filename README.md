<!DOCTYPE html>
<html lang="pt-PT">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>InvestPlus</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background-color: #f0f2f5;
            color: #2c3e50;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
        }

        /* Navegação lateral */
        .sidebar {
            width: 250px;
            background: linear-gradient(135deg, #4b79a1, #283e51);
            color: #fff;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px 0;
            position: fixed;
            height: 100%;
            box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
            z-index: 100;
        }

        .sidebar img {
            width: 80px;
            margin-bottom: 20px;
        }

        .sidebar h1 {
            font-size: 1.8rem;
            margin-bottom: 30px;
            font-weight: 400;
        }

        .sidebar a {
            color: #fff;
            text-decoration: none;
            font-size: 1.1rem;
            margin: 15px 0;
            transition: color 0.3s;
        }

        .sidebar a:hover {
            color: #6dd5fa;
        }

        .container {
            margin-left: 250px;
            padding: 40px;
            transition: margin-left 0.3s ease;
        }

        h2, h3 {
            color: #34495e;
            margin-bottom: 20px;
            font-weight: 400;
        }

        input, select, button {
            width: calc(100% - 30px);
            padding: 14px;
            margin: 10px 0;
            border: 1px solid #dcdfe3;
            border-radius: 8px;
            font-size: 16px;
            transition: all 0.3s ease;
            outline: none;
        }

        input:focus, select:focus {
            border-color: #2980b9;
            box-shadow: 0 0 8px rgba(41, 128, 185, 0.2);
        }

        button {
            background-color: #2980b9;
            color: white;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.3s;
        }

        button:hover {
            background-color: #3498db;
            transform: translateY(-2px);
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        .balance {
            text-align: center;
            margin: 30px 0;
            font-size: 22px;
            color: #2c3e50;
        }

        .balance span {
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .balance img {
            width: 30px;
            margin-right: 10px;
        }

        .investment-options {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            margin-bottom: 30px;
            gap: 10px;
        }

        .investment-option {
            border: 1px solid #dcdfe3;
            padding: 20px;
            border-radius: 10px;
            background-color: #f9f9f9;
            margin-bottom: 20px;
            flex: 1 1 calc(32% - 10px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
            transition: transform 0.2s, box-shadow 0.2s;
            text-align: center;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            position: relative;
            overflow: hidden;
        }

        .investment-option img {
            width: 60px;
            margin-bottom: 15px;
            transition: transform 0.3s;
        }

        .investment-option:hover img {
            transform: scale(1.1);
        }

        .investment-option:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
        }

        .message {
            padding: 14px;
            margin: 15px 0;
            border-radius: 8px;
            display: none;
            transition: opacity 0.3s ease;
            font-weight: 500;
        }

        .success {
            background-color: #d4edda;
            color: #155724;
        }

        .error {
            background-color: #f8d7da;
            color: #721c24;
        }

        .transaction-history {
            margin: 30px 0;
        }

        .transaction-history table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }

        .transaction-history th, .transaction-history td {
            border: 1px solid #ddd;
            padding: 12px;
            text-align: left;
        }

        .transaction-history th {
            background-color: #e9ecef;
        }

        @media (max-width: 768px) {
            .sidebar {
                transform: translateX(-250px);
            }
            .container {
                margin-left: 0;
            }
        }
    </style>
</head>
<body>
    <div class="sidebar">
        <img src="https://img.icons8.com/ios-filled/100/ffffff/investment.png" alt="Logotipo de Investimento">
        <h1>InvestPlus</h1>
        <a href="#loginSection">Login</a>
        <a href="#investSection">Investimentos</a>
        <a href="#transactionHistory">Transações</a>
    </div>

    <div class="container">
        <div class="login" id="loginSection">
            <h2>Login</h2>
            <input type="text" id="phone" placeholder="Número de Telefone (moçambicano)" required>
            <input type="password" id="password" placeholder="Senha" required>
            <button onclick="login()">Entrar</button>
        </div>

        <div class="invest-section" id="investSection" style="display:none;">
            <h2>Área de investimento</h2>
            <div class="balance">
                <span>
                    <img src="https://img.icons8.com/ios-filled/50/000000/money-bag.png" alt="Saldo">
                    Saldo Atual: <span id="balance">0 MT</span> | Ganhos Diários: <span id="dailyEarnings">0 MT</span>
                </span>
            </div>
            <div class="investment-options">
                <div class="investment-option">
                    <img src="https://img.icons8.com/ios-filled/50/000000/investment-portfolio.png" alt="investimento">
                    <p>Investimento de 250 MT: Ganho de 15 MT por dia</p>
                    <button onclick="invest(250, 15)">Investir</button>
                </div>
                <div class="investment-option">
                    <img src="https://img.icons8.com/ios-filled/50/000000/investment-portfolio.png" alt="investimento">
                    <p>Investimento de 300 MT: Ganho de 25 MT por dia</p>
                    <button onclick="invest(300, 25)">Investir</button>
                </div>
                <div class="investment-option">
                    <img src="https://img.icons8.com/ios-filled/50/000000/investment-portfolio.png" alt="investimento">
                    <p>Investimento de 500 MT: Ganho de 50 MT por dia</p>
                    <button onclick="invest(500, 50)">Investir</button>
                </div>
                <div class="investment-option">
                    <img src="https://img.icons8.com/ios-filled/50/000000/investment-portfolio.png" alt="investimento">
                    <p>Investimento de 700 MT: Ganho de 70 MT por dia</p>
                    <button onclick="invest(700, 70)">Investir</button>
                </div>
                <div class="investment-option">
                    <img src="https://img.icons8.com/ios-filled/50/000000/investment-portfolio.png" alt="investimento">
                    <p>Investimento de 1000 MT: Ganho de 100 MT por dia</p>
                    <button onclick="invest(1000, 100)">Investir</button>
                </div>
                <div class="investment-option">
                    <img src="https://img.icons8.com/ios-filled/50/000000/investment-portfolio.png" alt="investimento">
                    <p>Investimento de 1500 MT: Ganho de 150 MT por dia</p>
                    <button onclick="invest(1500, 150)">Investir</button>
                </div>
                <div class="investment-option">
                    <img src="https://img.icons8.com/ios-filled/50/000000/investment-portfolio.png" alt="investimento">
                    <p>Investimento de 2000 MT: Ganho de 200 MT por dia</p>
                    <button onclick="invest(2000, 200)">Investir</button>
                </div>
                <div class="investment-option">
                    <img src="https://img.icons8.com/ios-filled/50/000000/investment-portfolio.png" alt="investimento">
                    <p>Investimento de 2500 MT: Ganho de 250 MT por dia</p>
                    <button onclick="invest(2500, 250)">Investir</button>
                </div>
                <div class="investment-option">
                    <img src="https://img.icons8.com/ios-filled/50/000000/investment-portfolio.png" alt="investimento">
                    <p>Investimento de 5000 MT: Ganho de 500 MT por dia</p>
                    <button onclick="invest(5000, 500)">Investir</button>
                </div>
            </div>

            <h3>Levantamento</h3>
            <input type="number" id="withdrawAmount" placeholder="Valor para Levantar">
            <button onclick="withdraw()">Levantar</button>

            <div class="deposit">
                <h3>Fazer Depósito</h3>
                <select id="operator">
                    <option value="emola">Emola</option>
                    <option value="mpesa">M-Pesa</option>
                </select>
                <input type="text" id="depositNumber" placeholder="Número de Telefone" required>
                <input type="number" id="depositAmount" placeholder="Valor do Depósito (mínimo 500 MT)" min="500" required>
                <button onclick="deposit()">Depositar</button>
            </div>

            <h3>Bônus de Referência</h3>
            <input type="text" id="referralCode" placeholder="Código de Referência">
            <button onclick="applyReferralBonus()">Aplicar Código</button>

            <div class="transaction-history">
                <h3>Histórico de Transações</h3>
                <table>
                    <thead>
                        <tr>
                            <th>Data</th>
                            <th>Tipo</th>
                            <th>Valor</th>
                        </tr>
                    </thead>
                    <tbody id="transactionHistory">
                        <!-- Histórico de transações será adicionado aqui -->
                    </tbody>
                </table>
            </div>

            <div class="message success" id="successMessage"></div>
            <div class="message error" id="errorMessage"></div>
        </div>
    </div>

    <script>
        let balance = 0;
        let dailyEarnings = 0;
        const transactionHistory = [];
        const usedReferralCodes = new Set();

        function isMozambicanNumber(phone) {
            const regex = /^8\d{8}$/;
            return regex.test(phone);
        }

        function login() {
            const phone = document.getElementById('phone').value;
            const password = document.getElementById('password').value;

            if (!isMozambicanNumber(phone)) {
                showMessage('Por favor, insira um número de telefone moçambicano válido.', 'error');
                return;
            }

            if (password.length < 4) {
                showMessage('A senha deve ter pelo menos 4 caracteres.', 'error');
                return;
            }

            // Simulação de login bem-sucedido
            document.getElementById('loginSection').style.display = 'none';
            document.getElementById('investSection').style.display = 'block';
            updateBalanceDisplay();
        }

        function invest(amount, dailyGain) {
            if (balance < amount) {
                showMessage('Saldo insuficiente para o investimento.', 'error');
                return;
            }

            balance -= amount;
            dailyEarnings += dailyGain;
            transactionHistory.push({ type: 'Investimento', amount, date: new Date().toLocaleString() });
            updateBalanceDisplay();
            updateTransactionHistory();
            showMessage(`Você investiu ${amount} MT! Lucro diário de ${dailyGain} MT.`, 'success');
        }

        function withdraw() {
            const amount = parseFloat(document.getElementById('withdrawAmount').value);
            if (amount > balance) {
                showMessage('Saldo insuficiente para o levantamento.', 'error');
                return;
            }

            balance -= amount;
            transactionHistory.push({ type: 'Levantamento', amount, date: new Date().toLocaleString() });
            updateBalanceDisplay();
            updateTransactionHistory();
            showMessage(`Você levantou ${amount} MT!`, 'success');
        }

        function deposit() {
            const amount = parseFloat(document.getElementById('depositAmount').value);
            if (amount < 500) {
                showMessage('O valor do depósito deve ser de no mínimo 500 MT.', 'error');
                return;
            }

            balance += amount;
            transactionHistory.push({ type: 'Depósito', amount, date: new Date().toLocaleString() });
            updateBalanceDisplay();
            updateTransactionHistory();
            showMessage(`Você depositou ${amount} MT!`, 'success');
        }

        function applyReferralBonus() {
            const referralCode = document.getElementById('referralCode').value;
            if (usedReferralCodes.has(referralCode)) {
                showMessage('Este código de referência já foi utilizado.', 'error');
                return;
            }

            const referralBonus = 25;
            balance += referralBonus;
            usedReferralCodes.add(referralCode);
            transactionHistory.push({ type: 'Bônus de Referência', amount: referralBonus, date: new Date().toLocaleString() });
            updateBalanceDisplay();
            updateTransactionHistory();
            showMessage(`Bônus de referência de ${referralBonus} MT aplicado!`, 'success');
        }

        function updateBalanceDisplay() {
            document.getElementById('balance').innerText = `${balance} MT`;
            document.getElementById('dailyEarnings').innerText = `${dailyEarnings} MT`;
        }

        function updateTransactionHistory() {
            const historyElement = document.getElementById('transactionHistory');
            historyElement.innerHTML = transactionHistory.map(transaction => `
                <tr>
                    <td>${transaction.date}</td>
                    <td>${transaction.type}</td>
                    <td>${transaction.amount} MT</td>
                </tr>
            `).join('');
        }

        function showMessage(message, type) {
            const messageElement = type === 'success' ? document.getElementById('successMessage') : document.getElementById('errorMessage');
            messageElement.innerText = message;
            messageElement.style.display = 'block';
            setTimeout(() => {
                messageElement.style.display = 'none';
            }, 3000);
        }
    </script>
</body>
</html>
```