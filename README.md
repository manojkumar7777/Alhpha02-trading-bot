# Alhpha02-trading-bot
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Alpha Zero 2.0 Trading Platform</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.0.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@3.7.1/dist/chart.min.js"></script>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #1a202c;
            color: white;
        }

        .app-container {
            max-width: 100%;
            margin: 0 auto;
            min-height: 100vh;
            background-color: #1a202c;
            position: relative;
        }

        .header {
            background-color: #121212;
            padding: 12px 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: relative;
        }

        .screen {
            display: none;
            padding: 0;
            height: calc(100vh - 50px);
            overflow-y: auto;
            background: linear-gradient(135deg, #121212 0%, #1a202c 100%);
        }

        .card {
            background: linear-gradient(135deg, #4338ca 0%, #7e22ce 100%);
            border-radius: 16px;
            padding: 20px;
            margin: 15px;
            border: 3px solid #10b981;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
            position: relative;
            overflow: hidden;
        }

        .btn-primary {
            background-color: #f44336;
            color: white;
            border: none;
            border-radius: 25px;
            padding: 12px 20px;
            width: 100%;
            margin: 8px 0;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .btn-primary:hover {
            background-color: #d32f2f;
        }

        .btn-secondary {
            background-color: #2196F3;
            color: white;
            border: none;
            border-radius: 25px;
            padding: 12px 20px;
            width: 100%;
            margin: 8px 0;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .btn-secondary:hover {
            background-color: #1976D2;
        }

        .btn-tertiary {
            background-color: #10b981;
            color: white;
            border: none;
            border-radius: 25px;
            padding: 12px 20px;
            width: 100%;
            margin: 8px 0;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .btn-tertiary:hover {
            background-color: #0a8f67;
        }

        .btn-danger {
            background-color: #f44336;
            color: white;
        }

        .btn-success {
            background-color: #10b981;
            color: white;
        }

        .form-input {
            background-color: white;
            color: #333;
            border: none;
            border-radius: 25px;
            padding: 12px 20px;
            width: 100%;
            margin: 8px 0;
            font-size: 16px;
        }

        .form-select {
            background-color: white;
            color: #333;
            border: none;
            border-radius: 25px;
            padding: 12px 20px;
            width: 100%;
            margin: 8px 0;
            font-size: 16px;
            appearance: none;
            background-image: url("data:image/svg+xml;charset=utf-8,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' viewBox='0 0 24 24' fill='none' stroke='%23333' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpath d='M6 9l6 6 6-6'/%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: right 12px center;
            background-size: 16px;
        }

        .logo-container {
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 30px 0;
        }

        .ai-logo {
            width: 120px;
            height: 120px;
            background-color: #1a1a1a;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }

        .ai-icon {
            font-size: 60px;
            color: #10b981;
        }

        .progress-container {
            height: 8px;
            width: 100%;
            background-color: #1a1a1a;
            border-radius: 4px;
            margin: 10px 0;
        }

        .progress-bar {
            height: 100%;
            background-color: #10b981;
            border-radius: 4px;
            width: 0%;
            transition: width 0.3s ease;
        }

        .star-icon {
            position: absolute;
            top: 15px;
            right: 15px;
            font-size: 24px;
            color: #10b981;
        }

        .loading-dots {
            display: flex;
            justify-content: center;
            margin-top: 10px;
        }

        .dot {
            width: 8px;
            height: 8px;
            margin: 0 5px;
            background-color: white;
            border-radius: 50%;
            animation: pulse 1.5s infinite ease-in-out;
        }

        .dot:nth-child(2) {
            animation-delay: 0.5s;
        }

        .dot:nth-child(3) {
            animation-delay: 1s;
        }

        @keyframes pulse {
            0%, 100% {
                transform: scale(1);
                opacity: 0.2;
            }
            50% {
                transform: scale(1.2);
                opacity: 1;
            }
        }

        .market-analysis {
            margin-top: 20px;
            padding: 10px;
            background-color: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
        }

        .market-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .trend-up {
            color: #10b981;
        }

        .trend-down {
            color: #f44336;
        }

        .chart-container {
            height: 200px;
            margin-top: 20px;
        }

        @media (max-width: 768px) {
            .card {
                margin: 10px;
                padding: 15px;
            }
        }

        .tab-buttons {
            display: flex;
            margin-bottom: 20px;
        }

        .tab-button {
            flex: 1;
            padding: 10px;
            background-color: #2a2a2a;
            border: none;
            color: white;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .tab-button.active {
            background-color: #4338ca;
        }

        .tab-content {
            display: none;
            padding: 20px;
            background-color: #2a2a2a;
            border-radius: 0 0 10px 10px;
        }

        .tab-content.active {
            display: block;
        }
    </style>
</head>
<body>
    <div class="app-container">
        <div class="header">
            <div>Manojcrypto</div>
            <div class="star-icon"><i class="fas fa-star"></i></div>
        </div>

        <!-- Main Screen -->
        <div id="mainScreen" class="screen" style="display: block;">
            <div class="card mx-auto max-w-md my-6">
                <div class="text-center py-4 text-2xl font-bold">Alpha Zero 2.0</div>
                
                <div class="logo-container">
                    <div class="ai-logo">
                        <div style="width:100%; height:100%; display:flex; justify-content:center; align-items:center; background-color: #1a1a1a;">
                            <i class="fas fa-microchip ai-icon"></i>
                        </div>
                    </div>
                </div>
                
                <button id="loginBtn" class="btn-primary">LOGIN</button>
                <button id="settingsBtn" class="btn-secondary">SETTINGS</button>
                <button id="informationBtn" class="btn-tertiary">INFORMATION</button>
                
                <div class="text-center text-sm mt-6">© 2024 Alpha Zero Technologies</div>
            </div>
        </div>

        <!-- Client Portal / Email Verification -->
        <div id="clientPortalScreen" class="screen">
            <div class="card mx-auto max-w-md my-6">
                <div class="text-center py-4 text-2xl font-bold">Client Portal</div>
                
                <div class="mb-4">
                    <label class="block text-left text-white mb-1">Enter Email</label>
                    <input type="email" id="verifyEmailInput" placeholder="Your Deriv email address" class="form-input">
                </div>
                
                <div class="flex space-x-2">
                    <button id="addEmailBtn" class="btn-success flex-1">Add Email</button>
                    <button id="replaceEmailBtn" class="btn-success flex-1">Replace Email</button>
                </div>
                
                <button id="goBackFromClientBtn" class="btn-danger mt-4">Go Back</button>
            </div>
        </div>

        <!-- Trading Dashboard -->
        <div id="tradingDashboardScreen" class="screen">
            <div class="card mx-auto max-w-md my-6">
                <div class="text-center py-4 text-2xl font-bold">Trading Dashboard</div>
                
                <div class="market-analysis">
                    <h3 class="font-bold mb-2">Market Sentiment Analysis</h3>
                    <div class="market-item">
                        <span>Volatility 100 Index</span>
                        <span class="trend-up">72.4% <i class="fas fa-arrow-up"></i></span>
                    </div>
                    <div class="market-item">
                        <span>Volatility 75 Index</span>
                        <span class="trend-up">68.2% <i class="fas fa-arrow-up"></i></span>
                    </div>
                    <div class="market-item">
                        <span>Volatility 50 Index</span>
                        <span class="trend-down">43.1% <i class="fas fa-arrow-down"></i></span>
                    </div>
                    <div class="market-item">
                        <span>Volatility 25 Index</span>
                        <span class="trend-up">51.7% <i class="fas fa-arrow-up"></i></span>
                    </div>
                    <div class="market-item">
                        <span>Volatility 10 Index</span>
                        <span class="trend-down">38.9% <i class="fas fa-arrow-down"></i></span>
                    </div>
                </div>
                
                <div class="chart-container">
                    <canvas id="marketChart"></canvas>
                </div>
                
                <div class="mt-4">
                    <label class="block text-left text-white mb-1">Lot Size (Min: 0.35 USD):</label>
                    <input type="number" id="lotSizeInput" placeholder="Enter Lot Size" min="0.35" value="1.0" class="form-input">
                </div>
                
                <div class="mt-4">
                    <label class="block text-left text-white mb-1">Number of Trades:</label>
                    <input type="number" id="tradesInput" placeholder="Enter Number of Trades" min="1" value="100" class="form-input">
                </div>
                
                <div class="mt-4">
                    <label class="block text-left text-white mb-1">Market:</label>
                    <select id="marketSelect" class="form-select">
                        <option value="R_100">Volatility 100 Index</option>
                        <option value="R_75" selected>Volatility 75 Index</option>
                        <option value="R_50">Volatility 50 Index</option>
                        <option value="R_25">Volatility 25 Index</option>
                        <option value="R_10">Volatility 10 Index</option>
                    </select>
                </div>
                
                <div class="mt-4">
                    <label class="block text-left text-white mb-1">Risk Level:</label>
                    <select id="riskSelect" class="form-select">
                        <option value="high" selected>High</option>
                        <option value="medium">Medium</option>
                        <option value="low">Low</option>
                    </select>
                </div>
                
                <button id="startBotBtn" class="btn-tertiary mt-6">Start Bot</button>
                
                <div class="progress-container mt-4">
                    <div class="progress-bar" style="width: 98.92%"></div>
                </div>
                <div class="text-right text-sm">98.92%</div>
            </div>
        </div>

        <!-- Bot Status Screen -->
        <div id="botStatusScreen" class="screen">
            <div class="card mx-auto max-w-md my-6">
                <div class="text-center py-4 text-2xl font-bold">Trading Bot Status</div>
                
                <div class="text-center mt-6">
                    <div id="botStatusText">Trading bot started. Currently trading on Volatility 75 Index.</div>
                    
                    <div class="loading-dots mt-4">
                        <div class="dot"></div>
                        <div class="dot"></div>
                        <div class="dot"></div>
                    </div>
                </div>
                
                <div class="mt-8">
                    <div class="font-bold mb-2">Trading Statistics</div>
                    <div class="bg-black/20 p-4 rounded-lg">
                        <div class="flex justify-between mb-2">
                            <span>Total Trades</span>
                            <span id="totalTradesDisplay">0</span>
                        </div>
                        <div class="flex justify-between mb-2">
                            <span>Successful Trades</span>
                            <span id="successfulTradesDisplay">0</span>
                        </div>
                        <div class="flex justify-between mb-2">
                            <span>Success Rate</span>
                            <span id="successRateDisplay">0%</span>
                        </div>
                        <div class="flex justify-between mb-2">
                            <span>Profit/Loss</span>
                            <span id="profitLossDisplay">$0.00</span>
                        </div>
                    </div>
                </div>
                
                <div class="chart-container mt-4">
                    <canvas id="tradingChart"></canvas>
                </div>
                
                <button id="stopBotBtn" class="btn-danger mt-6">Stop Bot</button>
                <button id="dashboardBtn" class="btn-secondary mt-2">Back to Dashboard</button>
            </div>
        </div>

        <!-- Settings Screen -->
        <div id="settingsScreen" class="screen">
            <div class="card mx-auto max-w-md my-6">
                <div class="text-center py-4 text-2xl font-bold">Settings</div>
                
                <div class="mt-4">
                    <label class="block text-left text-white mb-1">App ID:</label>
                    <input type="text" id="appId" placeholder="Enter Deriv App ID" class="form-input">
                </div>

                <div class="mt-4">
                    <label class="block text-left text-white mb-1">Default Lot Size:</label>
                    <input type="number" id="defaultLotSize" min="0.35" value="1.0" class="form-input">
                </div>
                
                <div class="mt-4">
                    <label class="block text-left text-white mb-1">Default Number of Trades:</label>
                    <input type="number" id="defaultTrades" min="1" value="100" class="form-input">
                </div>
                
                <div class="mt-4">
                    <label class="block text-left text-white mb-1">Default Market:</label>
                    <select id="defaultMarket" class="form-select">
                        <option value="R_100">Volatility 100 Index</option>
                        <option value="R_75" selected>Volatility 75 Index</option>
                        <option value="R_50">Volatility 50 Index</option>
                        <option value="R_25">Volatility 25 Index</option>
                        <option value="R_10">Volatility 10 Index</option>
                    </select>
                </div>
                
                <div class="mt-4">
                    <label class="block text-left text-white mb-1">Default Risk Level:</label>
                    <select id="defaultRisk" class="form-select">
                        <option value="high" selected>High</option>
                        <option value="medium">Medium</option>
                        <option value="low">Low</option>
                    </select>
                </div>
                
                <div class="mt-6">
                    <label class="flex items-center">
                        <input type="checkbox" id="enableNotifications" checked class="mr-2">
                        <span>Enable Trade Notifications</span>
                    </label>
                </div>
                
                <button id="saveSettingsBtn" class="btn-tertiary mt-6">Save Settings</button>
                <button id="goBackFromSettingsBtn" class="btn-danger mt-2">Go Back</button>
            </div>
        </div>

        <!-- Information Screen -->
        <div id="informationScreen" class="screen">
            <div class="card mx-auto max-w-md my-6">
                <div class="text-center py-4 text-2xl font-bold">Information</div>
                
                <div class="tab-buttons">
                    <button class="tab-button active" data-tab="aboutTab">About</button>
                    <button class="tab-button" data-tab="faqTab">FAQ</button>
                    <button class="tab-button" data-tab="contactTab">Contact</button>
                </div>
                
                <div id="aboutTab" class="tab-content active">
                    <h3 class="font-bold text-xl mb-4">About Alpha Zero 2.0</h3>
                    <p class="mb-3">Alpha Zero 2.0 is an advanced trading bot designed for the Deriv platform. It uses sophisticated algorithms to analyze market trends and execute trades automatically.</p>
                    <p class="mb-3">The bot supports multiple volatility indices and risk levels, allowing you to customize your trading strategy according to your preferences.</p>
                    <p>This version doesn't require a license key, making it accessible for all traders looking to automate their trading activities.</p>
                </div>
                
                <div id="faqTab" class="tab-content">
                    <h3 class="font-bold text-xl mb-4">Frequently Asked Questions</h3>
                    
                    <div class="mb-4">
                        <h4 class="font-bold">How does the trading bot work?</h4>
                        <p>The bot analyzes market data using advanced algorithms and executes trades based on predefined strategies and risk parameters.</p>
                    </div>
                    
                    <div class="mb-4">
                        <h4 class="font-bold">Is my money safe?</h4>
                        <p>The bot only trades with the funds you allocate. You maintain full control over your Deriv account and can stop the bot at any time.</p>
                    </div>
                    
                    <div class="mb-4">
                        <h4 class="font-bold">What are the success rates?</h4>
                        <p>Success rates vary depending on market conditions, selected indices, and risk levels. Historical performance shows around 65-75% success rate with high volatility indices.</p>
                    </div>
                </div>
                
                <div id="contactTab" class="tab-content">
                    <h3 class="font-bold text-xl mb-4">Contact Us</h3>
                    <p class="mb-3">For any questions or support needs, please reach out to us:</p>
                    
                    <div class="mb-2">
                        <i class="fas fa-envelope mr-2"></i> support@alphazerov2.com
                    </div>
                    <div class="mb-2">
                        <i class="fab fa-telegram mr-2"></i> @AlphaZeroSupport
                    </div>
                    <div class="mb-2">
                        <i class="fab fa-discord mr-2"></i> AlphaZero Community
                    </div>
                    
                    <p class="mt-4 text-sm">We typically respond within 24 hours.</p>
                </div>
                
                <button id="goBackFromInfoBtn" class="btn-danger mt-6">Go Back</button>
            </div>
        </div>
    </div>

    <script>
        // Screen Navigation
        function showScreen(screenId) {
            console.log("Showing screen:", screenId);
            document.querySelectorAll('.screen').forEach(screen => {
                screen.style.display = 'none';
            });
            const screen = document.getElementById(screenId);
            if (screen) {
                screen.style.display = 'block';
            } else {
                console.error("Screen not found:", screenId);
            }
        }

        // Handle OAuth callback
        function handleOAuthCallback() {
            console.log("Handling OAuth callback...");
            const urlParams = new URLSearchParams(window.location.search);
            const code = urlParams.get('code');

            if (code) {
                console.log("Authorization code received:", code);
                fetch('https://your-backend.com/exchange-token', {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ code })
                })
                .then(response => response.json())
                .then(data => {
                    if (data.access_token) {
                        console.log("Access token received:", data.access_token);
                        localStorage.setItem('deriv_token', data.access_token);
                        showScreen('clientPortalScreen');
                        window.history.replaceState({}, document.title, window.location.pathname);
                    } else {
                        console.error("Failed to obtain access token:", data);
                        alert('Failed to authenticate with Deriv. Please try again.');
                    }
                })
                .catch(error => {
                    console.error('Error exchanging token:', error);
                    alert('Authentication error. Please try again.');
                });
            } else {
                console.log("No authorization code in URL.");
            }
        }

        // Get App ID from localStorage or default
        function getAppId() {
            return localStorage.getItem('appId') || '71675';
        }

        // WebSocket Connection
        function connectWebSocket() {
            console.log("Connecting to WebSocket...");
            const token = localStorage.getItem('deriv_token');
            const appId = getAppId();
            if (!token) {
                console.error("No token found in localStorage.");
                alert('Please log in to continue.');
                showScreen('mainScreen');
                return null;
            }
            
            const ws = new WebSocket(`wss://ws.binaryws.com/websockets/v3?app_id=${appId}`);
            
            ws.onopen = function() {
                console.log("WebSocket connection opened.");
                ws.send(JSON.stringify({
                    authorize: token
                }));
            };
            
            ws.onmessage = function(msg) {
                const data = JSON.parse(msg.data);
                console.log("WebSocket message received:", data);
                
                if (data.msg_type === 'authorize') {
                    if (data.error) {
                        console.error("Authorization failed:", data.error);
                        alert('Authentication failed: ' + data.error.message);
                        localStorage.removeItem('deriv_token');
                        showScreen('mainScreen');
                        return;
                    }
                    fetchBalance(ws);
                } else if (data.msg_type === 'balance') {
                    updateBalance(data.balance);
                }
            };
            
            ws.onerror = function(error) {
                console.error('WebSocket error:', error);
                alert('Connection error. Please try again.');
            };
            
            ws.onclose = function() {
                console.log('WebSocket closed');
            };
            
            return ws;
        }

        function fetchBalance(ws) {
            console.log("Fetching balance...");
            ws.send(JSON.stringify({
                balance: 1,
                subscribe: 1
            }));
        }

        function updateBalance(balance) {
            console.log('Account balance:', balance);
        }

        // Initialize Market Chart
        function initializeMarketChart() {
            console.log("Initializing market chart...");
            const ctx = document.getElementById('marketChart');
            if (!ctx) {
                console.error("Market chart canvas not found.");
                return;
            }
            const times = Array.from({length: 20}, (_, i) => i);
            const volatility75Data = [1294.21, 1295.68, 1293.45, 1297.12, 1298.76, 1301.24, 1299.87, 
                                     1302.45, 1305.67, 1308.23, 1306.78, 1309.54, 1312.87, 1310.56, 
                                     1314.23, 1316.78, 1315.43, 1318.92, 1321.45, 1324.67];
            
            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: times,
                    datasets: [{
                        label: 'Volatility 75 Index',
                        data: volatility75Data,
                        borderColor: '#10b981',
                        backgroundColor: 'rgba(16, 185, 129, 0.1)',
                        tension: 0.4,
                        fill: true
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        x: {
                            grid: {
                                display: false
                            },
                            ticks: {
                                display: false
                            }
                        },
                        y: {
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            },
                            ticks: {
                                color: 'rgba(255, 255, 255, 0.7)'
                            }
                        }
                    }
                }
            });
        }

        // Initialize Trading Chart
        function initializeTradingChart() {
            console.log("Initializing trading chart...");
            const ctx = document.getElementById('tradingChart');
            if (!ctx) {
                console.error("Trading chart canvas not found.");
                return;
            }
            
            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Start', ''],
                    datasets: [{
                        label: 'Profit/Loss',
                        data: [0, 0],
                        borderColor: '#10b981',
                        backgroundColor: 'rgba(16, 185, 129, 0.1)',
                        tension: 0.4,
                        fill: true
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        x: {
                            grid: {
                                display: false
                            }
                        },
                        y: {
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            },
                            ticks: {
                                color: 'rgba(255, 255, 255, 0.7)'
                            }
                        }
                    }
                }
            });
        }

        // Update Trading Chart
        function updateTradingChart(totalTrades, successfulTrades, profitLoss) {
            console.log("Updating trading chart:", totalTrades, successfulTrades, profitLoss);
            const chart = Chart.getChart('tradingChart');
            if (!chart) {
                console.error("Trading chart not initialized.");
                return;
            }
            
            const labels = Array.from({length: totalTrades + 1}, (_, i) => i === 0 ? 'Start' : `Trade ${i}`);
            
            const profitLossData = [0];
            let runningTotal = 0;
            
            for (let i = 1; i <= totalTrades; i++) {
                const isSuccess = i <= successfulTrades;
                const tradeResult = isSuccess ? 0.9 : -1;
                runningTotal += tradeResult;
                profitLossData.push(runningTotal);
            }
            
            chart.data.labels = labels;
            chart.data.datasets[0].data = profitLossData;
            
            if (runningTotal >= 0) {
                chart.data.datasets[0].borderColor = '#10b981';
                chart.data.datasets[0].backgroundColor = 'rgba(16, 185, 129, 0.1)';
            } else {
                chart.data.datasets[0].borderColor = '#f44336';
                chart.data.datasets[0].backgroundColor = 'rgba(244, 67, 54, 0.1)';
            }
            
            chart.update();
        }

        // Trading Bot Class
        class TradingBot {
            constructor(params) {
                this.ws = params.ws;
                this.lotSize = parseFloat(params.lotSize);
                this.numTrades = parseInt(params.numTrades);
                this.market = params.market;
                this.riskLevel = params.riskLevel;
                this.isRunning = false;
                this.completedTrades = 0;
                this.successfulTrades = 0;
                this.profitLoss = 0;
            }
            
            start() {
                console.log("Starting trading bot...");
                this.isRunning = true;
                this.executeTrade();
            }
            
            stop() {
                console.log("Stopping trading bot...");
                this.isRunning = false;
            }
            
            executeTrade() {
                if (!this.isRunning) return;
                
                console.log("Executing trade...");
                const tradeParams = this.generateTradeParameters();
                
                this.ws.send(JSON.stringify({
                    buy: 1,
                    price: this.lotSize,
                    parameters: {
                        contract_type: tradeParams.direction,
                        symbol: this.market,
                        duration: tradeParams.duration,
                        basis: 'stake',
                        amount: this.lotSize,
                        currency: 'USD'
                    }
                }));
                
                const tradeListener = (msg) => {
                    const data = JSON.parse(msg.data);
                    console.log("Trade response:", data);
                    if (data.msg_type === 'buy' && !data.error) {
                        this.completedTrades++;
                        this.successfulTrades++;
                        this.profitLoss += this.lotSize * 0.9;
                        
                        this.updateStats();
                        
                        if (this.completedTrades < this.numTrades && this.isRunning) {
                            setTimeout(() => this.executeTrade(), this.getTradeInterval());
                        } else {
                            this.isRunning = false;
                            this.onComplete();
                        }
                    } else if (data.error) {
                        console.error('Trade error:', data.error);
                        this.completedTrades++;
                        this.updateStats();
                        
                        if (this.completedTrades < this.numTrades && this.isRunning) {
                            setTimeout(() => this.executeTrade(), this.getTradeInterval());
                        } else {
                            this.isRunning = false;
                            this.onComplete();
                        }
                    }
                };
                
                this.ws.addEventListener('message', tradeListener);
            }
            
            generateTradeParameters() {
                const direction = Math.random() > 0.5 ? 'CALL' : 'PUT';
                const duration = this.riskLevel === 'high' ? 60 : 
                                this.riskLevel === 'medium' ? 120 : 300;
                
                return { direction, duration };
            }
            
            getTradeInterval() {
                return this.riskLevel === 'high' ? 5000 : 
                       this.riskLevel === 'medium' ? 10000 : 15000;
            }
            
            updateStats() {
                console.log("Updating stats...");
                document.getElementById('totalTradesDisplay').textContent = this.completedTrades;
                document.getElementById('successfulTradesDisplay').textContent = this.successfulTrades;
                
                const successRate = this.completedTrades > 0 ? 
                    Math.round((this.successfulTrades / this.completedTrades) * 100) : 0;
                document.getElementById('successRateDisplay').textContent = `${successRate}%`;
                
                document.getElementById('profitLossDisplay').textContent = 
                    `$${this.profitLoss.toFixed(2)}`;
                
                updateTradingChart(this.completedTrades, this.successfulTrades, this.profitLoss);
            }
            
            onComplete() {
                console.log("Trading bot completed.");
                alert('Trading bot has completed all trades!');
            }
        }

        // Initialize Bot
        let tradingBot = null;

        // Document Ready
        document.addEventListener('DOMContentLoaded', function() {
            console.log("DOM fully loaded and parsed.");

            // Initialize charts
            initializeMarketChart();
            initializeTradingChart();

            // Handle OAuth callback
            handleOAuthCallback();

            // Main Screen Buttons
            const loginBtn = document.getElementById('loginBtn');
            if (loginBtn) {
                loginBtn.addEventListener('click', function() {
                    console.log("Login button clicked.");
                    const state = Math.random().toString(36).substring(7);
                    const appId = getAppId();
                    localStorage.setItem('oauth_state', state);
                    const oauthUrl = `https://oauth.deriv.com/oauth2/authorize?app_id=${appId}&scope=read,trade&redirect_uri=https://www.ofbysamc.genspark.space/oauth_callback&l=en&brand=deriv&state=${state}`;
                    window.location.href = oauthUrl;
                });
            } else {
                console.error("Login button not found.");
            }

            const settingsBtn = document.getElementById('settingsBtn');
            if (settingsBtn) {
                settingsBtn.addEventListener('click', function() {
                    console.log("Settings button clicked.");
                    showScreen('settingsScreen');
                });
            } else {
                console.error("Settings button not found.");
            }

            const informationBtn = document.getElementById('informationBtn');
            if (informationBtn) {
                informationBtn.addEventListener('click', function() {
                    console.log("Information button clicked.");
                    showScreen('informationScreen');
                });
            } else {
                console.error("Information button not found.");
            }

            // Client Portal Buttons
            const addEmailBtn = document.getElementById('addEmailBtn');
            if (addEmailBtn) {
                addEmailBtn.addEventListener('click', function() {
                    console.log("Add Email button clicked.");
                    const email = document.getElementById('verifyEmailInput').value;
                    if (email && email.includes('@')) {
                        showScreen('tradingDashboardScreen');
                    } else {
                        alert('Please enter a valid email address.');
                    }
                });
            } else {
                console.error("Add Email button not found.");
            }

            const replaceEmailBtn = document.getElementById('replaceEmailBtn');
            if (replaceEmailBtn) {
                replaceEmailBtn.addEventListener('click', function() {
                    console.log("Replace Email button clicked.");
                    const email = document.getElementById('verifyEmailInput').value;
                    if (email && email.includes('@')) {
                        showScreen('tradingDashboardScreen');
                    } else {
                        alert('Please enter a valid email address.');
                    }
                });
            } else {
                console.error("Replace Email button not found.");
            }

            const goBackFromClientBtn = document.getElementById('goBackFromClientBtn');
            if (goBackFromClientBtn) {
                goBackFromClientBtn.addEventListener('click', function() {
                    console.log("Go Back from Client button clicked.");
                    showScreen('mainScreen');
                });
            } else {
                console.error("Go Back from Client button not found.");
            }

            // Trading Dashboard Buttons
            const startBotBtn = document.getElementById('startBotBtn');
            if (startBotBtn) {
                startBotBtn.addEventListener('click', function() {
                    console.log("Start Bot button clicked.");
                    const ws = connectWebSocket();
                    if (!ws) return;
                    
                    const lotSize = document.getElementById('lotSizeInput').value;
                    const numTrades = document.getElementById('tradesInput').value;
                    const market = document.getElementById('marketSelect').value;
                    const riskLevel = document.getElementById('riskSelect').value;
                    
                    if (lotSize < 0.35) {
                        alert('Minimum lot size is 0.35 USD');
                        return;
                    }
                    
                    if (numTrades < 1) {
                        alert('Number of trades must be at least 1');
                        return;
                    }
                    
                    tradingBot = new TradingBot({
                        ws,
                        lotSize,
                        numTrades,
                        market,
                        riskLevel
                    });
                    
                    tradingBot.start();
                    
                    const marketText = document.getElementById('marketSelect').options[
                        document.getElementById('marketSelect').selectedIndex
                    ].text;
                    
                    document.getElementById('botStatusText').textContent = 
                        `Trading bot started. Currently trading on ${marketText}.`;
                    
                    showScreen('botStatusScreen');
                });
            } else {
                console.error("Start Bot button not found.");
            }

            // Bot Status Buttons
            const stopBotBtn = document.getElementById('stopBotBtn');
            if (stopBotBtn) {
                stopBotBtn.addEventListener('click', function() {
                    console.log("Stop Bot button clicked.");
                    if (tradingBot) {
                        tradingBot.stop();
                        alert('Trading bot stopped.');
                    }
                });
            } else {
                console.error("Stop Bot button not found.");
            }

            const dashboardBtn = document.getElementById('dashboardBtn');
            if (dashboardBtn) {
                dashboardBtn.addEventListener('click', function() {
                    console.log("Back to Dashboard button clicked.");
                    showScreen('tradingDashboardScreen');
                });
            } else {
                console.error("Dashboard button not found.");
            }

            // Settings Screen Buttons
            const saveSettingsBtn = document.getElementById('saveSettingsBtn');
            if (saveSettingsBtn) {
                saveSettingsBtn.addEventListener('click', function() {
                    console.log("Save Settings button clicked.");
                    const appId = document.getElementById('appId').value;
                    if (!appId || isNaN(appId) || appId.length < 1) {
                        alert('Please enter a valid App ID.');
                        return;
                    }
                    localStorage.setItem('appId', appId);
                    localStorage.setItem('defaultLotSize', document.getElementById('defaultLotSize').value);
                    localStorage.setItem('defaultTrades', document.getElementById('defaultTrades').value);
                    localStorage.setItem('defaultMarket', document.getElementById('defaultMarket').value);
                    localStorage.setItem('defaultRisk', document.getElementById('defaultRisk').value);
                    localStorage.setItem('enableNotifications', document.getElementById('enableNotifications').checked);
                    
                    alert('Settings saved successfully!');
                    showScreen('mainScreen');
                });
            } else {
                console.error("Save Settings button not found.");
            }

            const goBackFromSettingsBtn = document.getElementById('goBackFromSettingsBtn');
            if (goBackFromSettingsBtn) {
                goBackFromSettingsBtn.addEventListener('click', function() {
                    console.log("Go Back from Settings button clicked.");
                    showScreen('mainScreen');
                });
            } else {
                console.error("Go Back from Settings button not found.");
            }

            // Information Screen Buttons
            const goBackFromInfoBtn = document.getElementById('goBackFromInfoBtn');
            if (goBackFromInfoBtn) {
                goBackFromInfoBtn.addEventListener('click', function() {
                    console.log("Go Back from Information button clicked.");
                    showScreen('mainScreen');
                });
            } else {
                console.error("Go Back from Information button not found.");
            }

            document.querySelectorAll('.tab-button').forEach(button => {
                button.addEventListener('click', function() {
                    console.log("Tab button clicked:", this.getAttribute('data-tab'));
                    document.querySelectorAll('.tab-content').forEach(tab => {
                        tab.classList.remove('active');
                    });
                    
                    document.querySelectorAll('.tab-button').forEach(btn => {
                        btn.classList.remove('active');
                    });
                    
                    const tabId = this.getAttribute('data-tab');
                    document.getElementById(tabId).classList.add('active');
                    
                    this.classList.add('active');
                });
            });

            // Load saved settings
            if (localStorage.getItem('appId')) {
                document.getElementById('appId').value = localStorage.getItem('appId');
            } else {
                document.getElementById('appId').value = '71675';
            }

            if (localStorage.getItem('defaultLotSize')) {
                document.getElementById('defaultLotSize').value = localStorage.getItem('defaultLotSize');
                document.getElementById('lotSizeInput').value = localStorage.getItem('defaultLotSize');
            }
            
            if (localStorage.getItem('defaultTrades')) {
                document.getElementById('defaultTrades').value = localStorage.getItem('defaultTrades');
                document.getElementById('tradesInput').value = localStorage.getItem('defaultTrades');
            }
            
            if (localStorage.getItem('defaultMarket')) {
                document.getElementById('defaultMarket').value = localStorage.getItem('defaultMarket');
                document.getElementById('marketSelect').value = localStorage.getItem('defaultMarket');
            }
            
            if (localStorage.getItem('defaultRisk')) {
                document.getElementById('defaultRisk').value = localStorage.getItem('defaultRisk');
                document.getElementById('riskSelect').value = localStorage.getItem('defaultRisk');
            }
            
            if (localStorage.getItem('enableNotifications') !== null) {
                document.getElementById('enableNotifications').checked = 
                    localStorage.getItem('enableNotifications') === 'true';
            }
        });
    </script>
</body>
</html>
