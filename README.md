<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tether Mining Panel</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #5d69e8;
            --secondary-color: #8a2be2;
            --success-color: #00ff88;
            --warning-color: #ffd700;
            --danger-color: #ff4757;
            --dark-color: #0a0a1a;
            --card-color: #1a1a2e;
        }
        
        body {
            background: linear-gradient(135deg, var(--dark-color), #16213e);
            color: white;
            font-family: 'Segoe UI', sans-serif;
            margin: 0;
            padding: 0;
            min-height: 100vh;
        }
        
        .login-container {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #0a0a1a, #1a1a2e);
        }
        
        .login-card {
            background: var(--card-color);
            border-radius: 20px;
            padding: 40px;
            width: 100%;
            max-width: 450px;
            box-shadow: 0 15px 30px rgba(93, 105, 232, 0.3);
            border: 1px solid #5d69e8;
        }
        
        .card {
            background: var(--card-color);
            border-radius: 15px;
            border: 1px solid #5d69e8;
            margin-bottom: 20px;
            box-shadow: 0 5px 15px rgba(93, 105, 232, 0.2);
        }
        
        .balance-display {
            font-size: 2.5rem;
            font-weight: bold;
            color: var(--primary-color);
            text-shadow: 0 0 10px rgba(93, 105, 232, 0.5);
        }
        
        .withdraw-btn {
            background: linear-gradient(45deg, #5d69e8, #8a2be2);
            border: none;
            padding: 15px 30px;
            font-size: 1.2rem;
            font-weight: bold;
            color: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(93, 105, 232, 0.4);
        }
        
        .withdraw-btn:disabled {
            background: linear-gradient(45deg, #6c757d, #495057);
            box-shadow: none;
        }
        
        .gear-animation {
            animation: rotate 2s linear infinite;
        }
        
        @keyframes rotate {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .progress-bar {
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
        }
        
        .transaction-item {
            border-bottom: 1px solid #2d2d4d;
            padding: 15px;
        }
        
        .withdraw-chart {
            background: linear-gradient(135deg, #1a1a2e, #2d2d4d);
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            border: 1px solid #5d69e8;
        }
        
        .chart-bar {
            height: 20px;
            background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
            border-radius: 10px;
            margin: 5px 0;
            transition: width 2s ease-in-out;
        }
        
        .admin-panel {
            background: #1a1a2e;
            border-radius: 10px;
            padding: 20px;
            margin-top: 20px;
            border: 1px solid #5d69e8;
        }
        
        .user-item {
            padding: 10px;
            border-bottom: 1px solid #2d2d4d;
        }
        
        .hidden {
            display: none;
        }
        
        .fee-deduction {
            background: rgba(244, 67, 54, 0.2);
            border-left: 4px solid #f44336;
        }
        
        .completed-transaction {
            background: rgba(0, 255, 136, 0.1);
            border-left: 4px solid var(--success-color);
        }
        
        .processing-transaction {
            background: rgba(255, 215, 0, 0.1);
            border-left: 4px solid var(--warning-color);
        }
        
        .transaction-parts {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 10px;
            margin: 20px 0;
        }
        
        .part-card {
            background: linear-gradient(135deg, #2d2d4d, #3d3d6d);
            border-radius: 10px;
            padding: 15px;
            text-align: center;
            border: 2px solid #5d69e8;
            transition: all 0.3s ease;
        }
        
        .part-card.active {
            border-color: var(--warning-color);
            background: linear-gradient(135deg, #3d3d6d, #4d4d8d);
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.3);
        }
        
        .part-card.completed {
            border-color: var(--success-color);
            background: linear-gradient(135deg, #2d4d4d, #3d5d5d);
        }
        
        .part-amount {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--primary-color);
        }
        
        .part-status {
            font-size: 0.8rem;
            margin-top: 5px;
            color: #b0b0ff;
        }
        
        .time-remaining {
            color: var(--warning-color);
            font-weight: bold;
            font-size: 0.9rem;
        }
        
        .countdown-timer {
            font-family: 'Courier New', monospace;
            font-size: 1.1rem;
            color: var(--warning-color);
        }
        
        .mining-countdown {
            font-size: 2rem;
            font-weight: bold;
            color: var(--warning-color);
            text-shadow: 0 0 10px rgba(255, 215, 0, 0.5);
        }
        
        .btn-primary {
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            border: none;
        }
        
        .btn-warning {
            background: linear-gradient(45deg, #ffd700, #ffa500);
            border: none;
            color: #000;
        }
        
        .btn-success {
            background: linear-gradient(45deg, var(--success-color), #00cc6a);
            border: none;
        }
        
        .btn-info {
            background: linear-gradient(45deg, #17a2b8, #138496);
            border: none;
        }
        
        .alert-info {
            background: linear-gradient(45deg, #5d69e8, #8a2be2);
            color: white;
            border: none;
        }
        
        .navbar-brand {
            color: var(--primary-color) !important;
            font-weight: bold;
        }
        
        .mining-visualization {
            background: linear-gradient(135deg, #1a1a2e, #2d2d4d);
            border-radius: 15px;
            padding: 20px;
            margin: 20px 0;
            border: 1px solid #5d69e8;
            height: 200px;
            position: relative;
            overflow: hidden;
        }
        
        .mining-particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: var(--primary-color);
            border-radius: 50%;
            animation: float 3s infinite ease-in-out;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0) translateX(0); opacity: 0; }
            50% { transform: translateY(-20px) translateX(10px); opacity: 1; }
        }
        
        .hash-rate-display {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--success-color);
        }
        
        .support-ticket {
            background: linear-gradient(135deg, #2d2d4d, #3d3d6d);
            border-radius: 10px;
            padding: 15px;
            margin: 10px 0;
            border-left: 4px solid var(--warning-color);
        }
        
        .power-level {
            font-size: 1.1rem;
            font-weight: bold;
            color: var(--warning-color);
        }
        
        .support-contact {
            background: linear-gradient(135deg, #1a1a2e, #2d2d4d);
            border-radius: 10px;
            padding: 20px;
            margin: 15px 0;
            border: 2px solid var(--primary-color);
            text-align: center;
        }
        
        .contact-number {
            font-size: 1.3rem;
            font-weight: bold;
            color: var(--success-color);
            direction: ltr;
            display: block;
            margin: 10px 0;
        }
        
        .registration-info {
            background: linear-gradient(135deg, #2d2d4d, #3d3d6d);
            border-radius: 10px;
            padding: 15px;
            margin: 10px 0;
            border-left: 4px solid var(--primary-color);
        }
        
        .whatsapp-btn {
            background: linear-gradient(45deg, #25D366, #128C7E);
            border: none;
            color: white;
            padding: 12px 20px;
            border-radius: 10px;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            font-weight: bold;
            transition: all 0.3s ease;
        }
        
        .whatsapp-btn:hover {
            background: linear-gradient(45deg, #128C7E, #25D366);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(37, 211, 102, 0.4);
        }
    </style>
</head>
<body>
    <!-- صفحه لاگین -->
    <div id="loginScreen" class="login-container">
        <div class="login-card">
            <h2 class="text-center mb-4" style="color: var(--primary-color);">
                <i class="fas fa-chart-line"></i> Tether Mining Panel
            </h2>
            
            <!-- اطلاعات ثبت نام -->
            <div class="registration-info">
                <h6><i class="fas fa-info-circle"></i> Registration Information</h6>
                <p class="small mb-2">For registration and password recovery, contact support via WhatsApp:</p>
                <a href="https://wa.me/447925632856" class="whatsapp-btn w-100 text-center justify-content-center" target="_blank">
                    <i class="fab fa-whatsapp"></i> Contact Support on WhatsApp
                </a>
                <p class="small text-muted mb-0 mt-2">24/7 Support Available</p>
            </div>
            
            <div id="userLoginForm">
                <div class="mb-3">
                    <label class="form-label">Username</label>
                    <input type="text" class="form-control" id="username" placeholder="Enter username">
                </div>
                <div class="mb-3">
                    <label class="form-label">Password</label>
                    <input type="password" class="form-control" id="password" placeholder="Enter password">
                </div>
                <button class="btn btn-primary w-100 mb-3" id="userLoginBtn">Login</button>
                <div class="text-center">
                    <a href="#" id="adminLoginLink" style="color: var(--primary-color);">Admin Login</a>
                </div>
            </div>
            
            <div id="adminLoginForm" class="hidden">
                <div class="mb-3">
                    <label class="form-label">Admin Password</label>
                    <input type="password" class="form-control" id="adminPassword" placeholder="Enter admin password">
                </div>
                <button class="btn btn-warning w-100 mb-3" id="adminLoginBtn">Login as Admin</button>
                <div class="text-center">
                    <a href="#" id="userLoginLink" style="color: var(--primary-color);">User Login</a>
                </div>
            </div>
        </div>
    </div>

    <!-- پنل کاربر -->
    <div id="userPanel" class="container mt-4 hidden">
        <!-- اطلاعات پشتیبانی -->
        <div class="support-contact">
            <h5><i class="fas fa-headset"></i> 24/7 Support</h5>
            <a href="https://wa.me/447925632856" class="whatsapp-btn" target="_blank">
                <i class="fab fa-whatsapp"></i> Contact Support on WhatsApp
            </a>
            <p class="small text-muted mb-0 mt-2">For registration, password recovery, and technical support</p>
        </div>

        <!-- هشدار سقف برداشت -->
        <div class="alert alert-info text-white">
            <i class="fas fa-info-circle"></i>
            <strong>Withdrawal Information:</strong> Minimum withdrawal: 50,000 USDT | Processing time: 5 transactions (4 hours each)
        </div>

        <div class="card p-4 mb-4">
            <div class="row">
                <div class="col-md-4">
                    <h4><i class="fas fa-wallet"></i> Account Balance</h4>
                    <div class="balance-display"><span id="currentBalance">0</span> USDT</div>
                    <div class="text-warning mt-2" id="withdrawalStatus">
                        <i class="fas fa-clock"></i> Mining in progress
                    </div>
                </div>
                
                <div class="col-md-4">
                    <h4><i class="fas fa-microchip"></i> Mining Power</h4>
                    <div class="hash-rate-display" id="hashRate">50 TH/s</div>
                    <div class="power-level" id="powerLevel">Basic Power</div>
                    <button class="btn btn-warning btn-sm mt-2" id="upgradePowerBtn">
                        <i class="fas fa-bolt"></i> Upgrade Power
                    </button>
                </div>
                
                <div class="col-md-4 text-end">
                    <h4><i class="fas fa-chart-line"></i> Mining Progress</h4>
                    <div class="mining-countdown" id="miningCountdown">--:--:--</div>
                    <div class="text-muted" id="miningTarget">Target: 50,000 USDT</div>
                    <div class="progress mt-2" style="height: 10px;">
                        <div class="progress-bar" id="miningProgressBar" style="width: 0%"></div>
                    </div>
                </div>
            </div>
        </div>

        <!-- ویژوالیزیشن ماینینگ -->
        <div class="mining-visualization" id="miningVisualization">
            <h5 class="text-center"><i class="fas fa-cog gear-animation"></i> Active Mining Process</h5>
        </div>

        <!-- پنل برداشت -->
        <div class="card p-4">
            <h4><i class="fas fa-money-bill-wave"></i> Withdrawal Panel</h4>
            
            <div class="mb-3">
                <label class="form-label">TRC20 Wallet Address</label>
                <input type="text" class="form-control" placeholder="Enter your TRC20 wallet address" id="walletAddress">
            </div>
            
            <div class="mb-3">
                <label class="form-label">Withdrawal Amount (Minimum: 50,000 USDT)</label>
                <div class="input-group">
                    <input type="number" class="form-control" id="withdrawAmount" placeholder="50000" min="50000" step="1000">
                    <span class="input-group-text" style="background: var(--primary-color); color: white;">
                        USDT
                    </span>
                </div>
                <div class="form-text text-muted">
                    Platform fee: 2% | Net amount will be sent in 5 equal parts
                </div>
            </div>

            <!-- نمایش پارت‌های برداشت -->
            <div class="transaction-parts" id="transactionParts">
                <div class="part-card" id="part1">
                    <div class="part-amount" id="partAmount1">0 USDT</div>
                    <div class="part-status">Part 1</div>
                    <div class="time-remaining countdown-timer" id="timer1">Pending</div>
                </div>
                <div class="part-card" id="part2">
                    <div class="part-amount" id="partAmount2">0 USDT</div>
                    <div class="part-status">Part 2</div>
                    <div class="time-remaining countdown-timer" id="timer2">Pending</div>
                </div>
                <div class="part-card" id="part3">
                    <div class="part-amount" id="partAmount3">0 USDT</div>
                    <div class="part-status">Part 3</div>
                    <div class="time-remaining countdown-timer" id="timer3">Pending</div>
                </div>
                <div class="part-card" id="part4">
                    <div class="part-amount" id="partAmount4">0 USDT</div>
                    <div class="part-status">Part 4</div>
                    <div class="time-remaining countdown-timer" id="timer4">Pending</div>
                </div>
                <div class="part-card" id="part5">
                    <div class="part-amount" id="partAmount5">0 USDT</div>
                    <div class="part-status">Part 5</div>
                    <div class="time-remaining countdown-timer" id="timer5">Pending</div>
                </div>
            </div>

            <!-- نمودار برداشت -->
            <div class="withdraw-chart hidden" id="withdrawChart">
                <h5 class="text-center mb-4">
                    <i class="fas fa-cog gear-animation"></i> Processing Withdrawal...
                </h5>
                <div class="chart-bar" style="width: 0%" id="chartProgress"></div>
                <div class="text-center mt-3">
                    <div id="withdrawStatus">Initializing withdrawal process...</div>
                    <small class="text-muted" id="transactionTimer"></small>
                </div>
            </div>

            <button class="btn withdraw-btn w-100" id="withdrawBtn">
                <i class="fas fa-rocket"></i> START WITHDRAWAL
            </button>
        </div>

        <!-- پنل پشتیبانی -->
        <div class="card mt-4 p-4">
            <h5><i class="fas fa-headset"></i> Support Panel</h5>
            
            <!-- اطلاعات تماس -->
            <div class="support-contact mb-4">
                <h6><i class="fas fa-headset"></i> Contact Support</h6>
                <a href="https://wa.me/447925632856" class="whatsapp-btn" target="_blank">
                    <i class="fab fa-whatsapp"></i> Contact Support on WhatsApp
                </a>
                <p class="small text-muted mb-0 mt-2">For registration, password, and technical issues</p>
            </div>
            
            <div class="mb-3">
                <label class="form-label">Request Type</label>
                <select class="form-control" id="requestType">
                    <option value="registration">New Registration</option>
                    <option value="password_recovery">Password Recovery</option>
                    <option value="power_upgrade">Power Upgrade Request</option>
                    <option value="technical_support">Technical Support</option>
                    <option value="withdrawal_issue">Withdrawal Issue</option>
                    <option value="other">Other</option>
                </select>
            </div>
            <div class="mb-3">
                <label class="form-label">Your Contact Info</label>
                <input type="text" class="form-control" id="contactInfo" placeholder="Your phone number or email">
            </div>
            <div class="mb-3">
                <label class="form-label">Message</label>
                <textarea class="form-control" id="supportMessage" rows="3" placeholder="Describe your issue..."></textarea>
            </div>
            <button class="btn btn-success w-100" id="submitSupportBtn">
                <i class="fas fa-paper-plane"></i> Submit Support Request
            </button>
            
            <div id="supportTickets" class="mt-3">
            </div>
        </div>

        <!-- تاریخچه تراکنش -->
        <div class="card mt-4 p-4">
            <h5><i class="fas fa-list"></i> Transaction History</h5>
            <div id="transactionList">
            </div>
        </div>
        
        <div class="text-end mt-3">
            <button class="btn btn-outline-primary btn-sm" id="logoutBtn">
                <i class="fas fa-sign-out-alt"></i> Logout
            </button>
        </div>
    </div>

    <!-- پنل ادمین -->
    <div id="adminPanel" class="container mt-4 hidden">
        <div class="card p-4">
            <h3 class="text-center mb-4" style="color: var(--primary-color);">
                <i class="fas fa-cog"></i> Admin Panel
            </h3>
            
            <!-- اطلاعات پشتیبانی برای ادمین -->
            <div class="support-contact mb-4">
                <h5><i class="fas fa-headset"></i> Support Contact</h5>
                <a href="https://wa.me/447925632856" class="whatsapp-btn" target="_blank">
                    <i class="fab fa-whatsapp"></i> Contact Support on WhatsApp
                </a>
                <p class="small text-muted mb-0 mt-2">User registration and support line</p>
            </div>
            
            <div class="admin-panel">
                <h5>User Management (<span id="totalUsers">0</span>)</h5>
                <div class="mb-3">
                    <input type="text" class="form-control" id="searchUser" placeholder="Search users...">
                </div>
                <div class="mb-3">
                    <button class="btn btn-info btn-sm" id="addUserBtn">
                        <i class="fas fa-user-plus"></i> Add New User
                    </button>
                </div>
                <div id="userList">
                </div>
            </div>
            
            <div class="admin-panel mt-4">
                <h5>Support Tickets (<span id="totalTickets">0</span>)</h5>
                <div id="supportTicketList">
                </div>
            </div>
            
            <div class="text-end mt-3">
                <button class="btn btn-outline-warning btn-sm" id="adminLogoutBtn">
                    <i class="fas fa-sign-out-alt"></i> Logout
                </button>
            </div>
        </div>
    </div>

    <!-- مودال اضافه کردن کاربر -->
    <div class="modal fade" id="addUserModal" tabindex="-1">
        <div class="modal-dialog">
            <div class="modal-content" style="background: var(--card-color); color: white;">
                <div class="modal-header">
                    <h5 class="modal-title"><i class="fas fa-user-plus"></i> Add New User</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <div class="mb-3">
                        <label class="form-label">Username</label>
                        <input type="text" class="form-control" id="newUsername" placeholder="Enter username">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Password</label>
                        <input type="text" class="form-control" id="newPassword" placeholder="Enter password">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Email</label>
                        <input type="email" class="form-control" id="newEmail" placeholder="Enter email">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Initial Hash Rate (TH/s)</label>
                        <input type="number" class="form-control" id="newHashRate" value="50" min="10" max="1000">
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                    <button type="button" class="btn btn-primary" id="confirmAddUser">Add User</button>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // تابع برای فراخوانی API
        const API_BASE = '/api';

        async function apiCall(endpoint, options = {}) {
            try {
                const response = await fetch(`${API_BASE}${endpoint}`, {
                    headers: {
                        'Content-Type': 'application/json',
                        ...options.headers
                    },
                    ...options
                });
                return await response.json();
            } catch (error) {
                console.error('API call failed:', error);
                return { success: false, message: 'Network error' };
            }
        }

        // المنت‌های DOM
        const loginScreen = document.getElementById('loginScreen');
        const userPanel = document.getElementById('userPanel');
        const adminPanel = document.getElementById('adminPanel');
        const userLoginForm = document.getElementById('userLoginForm');
        const adminLoginForm = document.getElementById('adminLoginForm');
        const withdrawChart = document.getElementById('withdrawChart');
        const chartProgress = document.getElementById('chartProgress');
        const withdrawStatus = document.getElementById('withdrawStatus');
        const transactionTimer = document.getElementById('transactionTimer');
        const transactionList = document.getElementById('transactionList');
        const userList = document.getElementById('userList');
        const currentBalance = document.getElementById('currentBalance');
        const transactionParts = document.getElementById('transactionParts');
        const miningCountdown = document.getElementById('miningCountdown');
        const withdrawalStatus = document.getElementById('withdrawalStatus');
        const walletAddress = document.getElementById('walletAddress');
        const withdrawBtn = document.getElementById('withdrawBtn');
        const hashRateDisplay = document.getElementById('hashRate');
        const powerLevelDisplay = document.getElementById('powerLevel');
        const miningProgressBar = document.getElementById('miningProgressBar');
        const miningTarget = document.getElementById('miningTarget');
        const miningVisualization = document.getElementById('miningVisualization');
        const withdrawAmount = document.getElementById('withdrawAmount');
        const upgradePowerBtn = document.getElementById('upgradePowerBtn');
        const supportTicketsDiv = document.getElementById('supportTickets');
        const submitSupportBtn = document.getElementById('submitSupportBtn');
        const supportTicketList = document.getElementById('supportTicketList');
        const totalUsers = document.getElementById('totalUsers');
        const totalTickets = document.getElementById('totalTickets');
        const searchUser = document.getElementById('searchUser');
        const addUserBtn = document.getElementById('addUserBtn');
        const contactInfo = document.getElementById('contactInfo');

        // متغیرهای سراسری
        let currentUser = null;
        let users = [];
        let supportTickets = [];
        let userBalance = 0;
        let userHashRate = 50;
        let userPowerLevel = 'Basic';
        let miningTimeLeft = 10368000;
        let miningInterval = null;
        let miningProgress = 0;
        let miningTargetAmount = 50000;
        let withdrawalInProgress = false;
        const PART_DURATION = 14400;

        // قدرت‌های مختلف ماینینگ
        const powerLevels = {
            'Basic': { hashRate: 50, time: 10368000, cost: 0 },
            'Advanced': { hashRate: 150, time: 3456000, cost: 1000 },
            'Pro': { hashRate: 300, time: 1728000, cost: 2500 },
            'Ultimate': { hashRate: 600, time: 864000, cost: 5000 }
        };

        // هندلر لاگین کاربر
        document.getElementById('userLoginBtn').addEventListener('click', async function() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            const result = await apiCall('/login', {
                method: 'POST',
                body: JSON.stringify({ username, password })
            });
            
            if (result.success) {
                currentUser = result.user;
                loginScreen.classList.add('hidden');
                userPanel.classList.remove('hidden');
                initializeUserPanel();
            } else {
                alert(result.message || 'Invalid username or password!');
            }
        });

        // هندلر لاگین ادمین
        document.getElementById('adminLoginBtn').addEventListener('click', async function() {
            const adminPassword = document.getElementById('adminPassword').value;
            
            const result = await apiCall('/admin/login', {
                method: 'POST',
                body: JSON.stringify({ password: adminPassword })
            });
            
            if (result.success) {
                users = result.users;
                supportTickets = result.tickets;
                loginScreen.classList.add('hidden');
                adminPanel.classList.remove('hidden');
                loadUserList();
                loadSupportTickets();
            } else {
                alert(result.message || 'Invalid admin password!');
            }
        });

        // مقداردهی اولیه پنل کاربر
        function initializeUserPanel() {
            userBalance = currentUser.balance || 0;
            userHashRate = currentUser.hashRate || 50;
            userPowerLevel = currentUser.powerLevel || 'Basic';
            miningProgress = currentUser.miningProgress || 0;
            miningTimeLeft = powerLevels[userPowerLevel].time * (1 - (miningProgress / 100));
            
            updateBalanceDisplay();
            updateMiningDisplay();
            startMining();
            createMiningParticles();
            updateWithdrawalParts();
            displayUserTickets();
            loadUserTransactions();
        }

        // شروع ماینینگ
        function startMining() {
            if (miningInterval) clearInterval(miningInterval);
            
            miningInterval = setInterval(() => {
                if (miningTimeLeft > 0) {
                    miningTimeLeft--;
                    
                    // محاسبه پیشرفت بر اساس هش ریت
                    const progressIncrement = (userHashRate / powerLevels[userPowerLevel].hashRate) * (100 / powerLevels[userPowerLevel].time);
                    miningProgress += progressIncrement;
                    
                    if (miningProgress >= 100) {
                        miningProgress = 100;
                        userBalance += miningTargetAmount;
                        currentUser.totalMined = (currentUser.totalMined || 0) + miningTargetAmount;
                        miningProgress = 0;
                        miningTimeLeft = powerLevels[userPowerLevel].time;
                        addTransaction('Mining Reward', miningTargetAmount, 'Completed');
                        updateUserData();
                    }
                    
                    updateMiningDisplay();
                }
            }, 1000);
        }

        // آپدیت کاربر در سرور
        async function updateUserData() {
            const result = await apiCall(`/users/${currentUser.username}`, {
                method: 'PUT',
                body: JSON.stringify({
                    balance: userBalance,
                    miningProgress: miningProgress,
                    totalMined: currentUser.totalMined || 0
                })
            });
            
            if (result.success) {
                currentUser = result.user;
            }
        }

        // آپدیت نمایش ماینینگ
        function updateMiningDisplay() {
            const days = Math.floor(miningTimeLeft / 86400);
            const hours = Math.floor((miningTimeLeft % 86400) / 3600);
            const minutes = Math.floor((miningTimeLeft % 3600) / 60);
            const seconds = miningTimeLeft % 60;
            
            miningCountdown.textContent = `${days}d ${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            
            hashRateDisplay.textContent = `${userHashRate} TH/s`;
            powerLevelDisplay.textContent = `${userPowerLevel} Power`;
            
            miningProgressBar.style.width = `${miningProgress}%`;
            miningTarget.textContent = `Target: ${miningTargetAmount.toLocaleString()} USDT`;
            
            updateBalanceDisplay();
        }

        // ایجاد ذرات ویژوالیزیشن ماینینگ
        function createMiningParticles() {
            miningVisualization.innerHTML = '<h5 class="text-center"><i class="fas fa-cog gear-animation"></i> Active Mining Process</h5>';
            
            for (let i = 0; i < 50; i++) {
                const particle = document.createElement('div');
                particle.className = 'mining-particle';
                particle.style.left = `${Math.random() * 100}%`;
                particle.style.top = `${Math.random() * 100}%`;
                particle.style.animationDelay = `${Math.random() * 5}s`;
                particle.style.background = i % 3 === 0 ? 'var(--primary-color)' : 
                                          i % 3 === 1 ? 'var(--success-color)' : 'var(--warning-color)';
                miningVisualization.appendChild(particle);
            }
        }

        // آپدیت نمایش موجودی
        function updateBalanceDisplay() {
            currentBalance.textContent = userBalance.toLocaleString();
            withdrawBtn.disabled = userBalance < 50000;
        }

        // آپدیت پارت‌های برداشت
        function updateWithdrawalParts() {
            const amount = parseInt(withdrawAmount.value) || 50000;
            const netAmount = amount * 0.98;
            const partAmount = netAmount / 5;
            
            for (let i = 1; i <= 5; i++) {
                document.getElementById(`partAmount${i}`).textContent = `${partAmount.toLocaleString()} USDT`;
            }
        }

        // هندلر ارتقاء قدرت
        upgradePowerBtn.addEventListener('click', async function() {
            const currentLevel = userPowerLevel;
            const levels = Object.keys(powerLevels);
            const currentIndex = levels.indexOf(currentLevel);
            
            if (currentIndex < levels.length - 1) {
                const nextLevel = levels[currentIndex + 1];
                const cost = powerLevels[nextLevel].cost;
                
                if (userBalance >= cost) {
                    if (confirm(`Upgrade to ${nextLevel} Power for ${cost} USDT?`)) {
                        userBalance -= cost;
                        userPowerLevel = nextLevel;
                        userHashRate = powerLevels[nextLevel].hashRate;
                        miningTimeLeft = powerLevels[nextLevel].time * (1 - (miningProgress / 100));
                        updateBalanceDisplay();
                        updateMiningDisplay();
                        
                        // ثبت درخواست پشتیبانی
                        const ticketResult = await apiCall('/tickets', {
                            method: 'POST',
                            body: JSON.stringify({
                                username: currentUser.username,
                                type: 'power_upgrade',
                                message: `Upgraded from ${currentLevel} to ${nextLevel} Power - Cost: ${cost} USDT`,
                                contact: currentUser.email
                            })
                        });
                        
                        // آپدیت کاربر
                        await updateUserData();
                        displayUserTickets();
                    }
                } else {
                    alert(`Insufficient balance! Need ${cost} USDT for upgrade.`);
                }
            } else {
                alert('You already have the maximum power level!');
            }
        });

        // هندلر برداشت
        withdrawBtn.addEventListener('click', async function() {
            const amount = parseInt(withdrawAmount.value);
            const wallet = walletAddress.value;
            
            if (!amount || amount < 50000) {
                alert('Minimum withdrawal amount is 50,000 USDT!');
                return;
            }
            
            if (amount > userBalance) {
                alert('Insufficient balance!');
                return;
            }
            
            if (!wallet || !wallet.startsWith('T') || wallet.length !== 34) {
                alert('Please enter a valid TRC20 wallet address!');
                return;
            }
            
            if (withdrawalInProgress) {
                alert('Withdrawal is already in progress!');
                return;
            }
            
            userBalance -= amount;
            updateBalanceDisplay();
            await updateUserData();
            
            // ثبت کارمزد
            const fee = amount * 0.02;
            await apiCall('/transactions', {
                method: 'POST',
                body: JSON.stringify({
                    username: currentUser.username,
                    description: 'Platform Fee (2%)',
                    amount: fee,
                    status: 'Completed',
                    type: 'fee'
                })
            });
            
            withdrawChart.classList.remove('hidden');
            this.disabled = true;
            this.innerHTML = '<i class="fas fa-cog gear-animation"></i> PROCESSING...';
            withdrawalInProgress = true;
            
            simulateWithdrawal(amount);
        });

        // شبیه‌سازی برداشت
        async function simulateWithdrawal(amount) {
            const fee = amount * 0.02;
            const netAmount = amount - fee;
            const partAmount = netAmount / 5;
            
            addTransaction('Platform Fee (2%)', fee, 'Completed', 'fee-deduction');
            
            for (let i = 1; i <= 5; i++) {
                document.getElementById(`partAmount${i}`).textContent = `${partAmount.toLocaleString()} USDT`;
            }
            
            let currentPart = 0;
            const totalParts = 5;
            
            const processNextPart = async () => {
                if (currentPart < totalParts) {
                    const partNumber = currentPart + 1;
                    const partElement = document.getElementById(`part${partNumber}`);
                    const timerElement = document.getElementById(`timer${partNumber}`);
                    
                    partElement.classList.add('active');
                    
                    addTransaction(`Withdrawal Part ${partNumber}`, partAmount, 'Processing (4 hours)', 'processing-transaction');
                    
                    // ثبت تراکنش در سرور
                    await apiCall('/transactions', {
                        method: 'POST',
                        body: JSON.stringify({
                            username: currentUser.username,
                            description: `Withdrawal Part ${partNumber}`,
                            amount: partAmount,
                            status: 'Processing (4 hours)',
                            type: 'withdrawal'
                        })
                    });
                    
                    const progress = (partNumber / totalParts) * 100;
                    chartProgress.style.width = progress + '%';
                    withdrawStatus.textContent = `Processing part ${partNumber}/${totalParts}`;
                    
                    startCountdown(timerElement, PART_DURATION, async () => {
                        partElement.classList.remove('active');
                        partElement.classList.add('completed');
                        timerElement.textContent = 'Completed';
                        timerElement.className = 'text-success';
                        
                        updateTransactionStatus(partNumber, 'Completed');
                        currentPart++;
                        
                        if (currentPart < totalParts) {
                            processNextPart();
                        } else {
                            withdrawStatus.innerHTML = '<i class="fas fa-check-circle text-success"></i> All transactions completed!';
                            transactionTimer.textContent = 'Withdrawal successfully sent to your wallet';
                            document.getElementById('withdrawBtn').innerHTML = '<i class="fas fa-check"></i> WITHDRAWAL COMPLETED';
                            withdrawalInProgress = false;
                        }
                    });
                    
                }
            };
            
            processNextPart();
        }

        // هندلر پشتیبانی
        submitSupportBtn.addEventListener('click', async function() {
            const requestType = document.getElementById('requestType').value;
            const message = document.getElementById('supportMessage').value;
            const contact = contactInfo.value;
            
            if (!message) {
                alert('Please enter your message!');
                return;
            }
            
            if (!contact) {
                alert('Please enter your contact information!');
                return;
            }
            
            const result = await apiCall('/tickets', {
                method: 'POST',
                body: JSON.stringify({
                    username: currentUser.username,
                    type: requestType,
                    message: message,
                    contact: contact
                })
            });
            
            if (result.success) {
                supportTickets.push(result.ticket);
                displayUserTickets();
                document.getElementById('supportMessage').value = '';
                contactInfo.value = '';
                alert('Support request submitted successfully! We will contact you soon.');
            } else {
                alert(result.message || 'Error submitting ticket!');
            }
        });

        // نمایش تیکت‌های کاربر
        function displayUserTickets() {
            supportTicketsDiv.innerHTML = '';
            const userTickets = supportTickets.filter(ticket => ticket.username === currentUser.username);
            
            if (userTickets.length === 0) {
                supportTicketsDiv.innerHTML = '<p class="text-muted text-center">No support tickets yet.</p>';
                return;
            }
            
            userTickets.forEach(ticket => {
                const ticketDiv = document.createElement('div');
                ticketDiv.className = 'support-ticket';
                ticketDiv.innerHTML = `
                    <div class="d-flex justify-content-between align-items-center">
                        <div>
                            <strong>${ticket.type.replace('_', ' ').toUpperCase()}</strong>
                            <div class="small">${ticket.message}</div>
                            <div class="small text-muted">Contact: ${ticket.contact}</div>
                        </div>
                        <div class="text-end">
                            <span class="badge ${ticket.status === 'pending' ? 'bg-warning' : 'bg-success'}">${ticket.status}</span>
                            <div class="small text-muted">${ticket.timestamp}</div>
                        </div>
                    </div>
                `;
                supportTicketsDiv.appendChild(ticketDiv);
            });
        }

        // بارگذاری تراکنش‌های کاربر
        async function loadUserTransactions() {
            const result = await apiCall(`/transactions/${currentUser.username}`);
            if (result && result.length > 0) {
                result.forEach(transaction => {
                    addTransaction(
                        transaction.description,
                        transaction.amount,
                        transaction.status,
                        transaction.type === 'fee' ? 'fee-deduction' : ''
                    );
                });
            }
        }

        // تایمر معکوس
        function startCountdown(timerElement, seconds, callback) {
            let remaining = seconds;
            
            const updateTimer = () => {
                const hours = Math.floor(remaining / 3600);
                const minutes = Math.floor((remaining % 3600) / 60);
                const secs = remaining % 60;
                
                timerElement.textContent = `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
                
                if (remaining > 0) {
                    remaining--;
                    setTimeout(updateTimer, 1000);
                } else {
                    callback();
                }
            };
            
            updateTimer();
        }

        // اضافه کردن تراکنش به تاریخچه
        function addTransaction(description, amount, status, className = '') {
            const transactionItem = document.createElement('div');
            transactionItem.className = `transaction-item ${className}`;
            transactionItem.innerHTML = `
                <div class="d-flex justify-content-between align-items-center">
                    <div>
                        <div class="fw-bold">${description}</div>
                        <small class="${status === 'Completed' ? 'text-success' : 'text-warning'}">${status}</small>
                    </div>
                    <div class="${className === 'fee-deduction' ? 'text-danger' : 'text-success'} fw-bold">
                        ${className === 'fee-deduction' ? '-' : '+'}${amount.toLocaleString()} USDT
                    </div>
                </div>
            `;
            transactionList.appendChild(transactionItem);
        }

        // آپدیت وضعیت تراکنش
        function updateTransactionStatus(transactionNumber, newStatus) {
            const transactions = transactionList.getElementsByClassName('transaction-item');
            const targetIndex = transactionNumber;
            const targetTransaction = transactions[targetIndex];
            
            if (targetTransaction && !targetTransaction.classList.contains('fee-deduction')) {
                const statusElement = targetTransaction.querySelector('small');
                if (statusElement) {
                    statusElement.textContent = newStatus;
                    statusElement.className = 'text-success';
                    targetTransaction.classList.remove('processing-transaction');
                    targetTransaction.classList.add('completed-transaction');
                }
            }
        }

        // بارگذاری لیست کاربران برای ادمین
        function loadUserList() {
            userList.innerHTML = '';
            totalUsers.textContent = users.length;
            
            users.forEach(user => {
                const userItem = document.createElement('div');
                userItem.className = 'user-item';
                userItem.innerHTML = `
                    <div class="row align-items-center">
                        <div class="col-3">
                            <strong>${user.username}</strong>
                            <div class="small text-muted">${user.email}</div>
                        </div>
                        <div class="col-2">
                            <span class="badge bg-primary">${user.hashRate} TH/s</span>
                        </div>
                        <div class="col-3">
                            <div class="progress" style="height: 10px;">
                                <div class="progress-bar" style="width: ${user.miningProgress || 0}%"></div>
                            </div>
                            <div class="small">${Math.round(user.miningProgress || 0)}%</div>
                        </div>
                        <div class="col-2">
                            <span class="badge bg-success">${(user.totalMined || 0).toLocaleString()} USDT</span>
                        </div>
                        <div class="col-2 text-end">
                            <small class="text-muted">${user.joinDate || '2024-01-01'}</small>
                        </div>
                    </div>
                `;
                userList.appendChild(userItem);
            });
        }

        // بارگذاری تیکت‌های پشتیبانی برای ادمین
        function loadSupportTickets() {
            supportTicketList.innerHTML = '';
            totalTickets.textContent = supportTickets.length;
            
            if (supportTickets.length === 0) {
                supportTicketList.innerHTML = '<p class="text-muted text-center">No support tickets yet.</p>';
                return;
            }
            
            supportTickets.forEach(ticket => {
                const ticketItem = document.createElement('div');
                ticketItem.className = 'support-ticket';
                ticketItem.innerHTML = `
                    <div class="row align-items-center">
                        <div class="col-3">
                            <strong>${ticket.username}</strong>
                            <div class="small text-muted">${ticket.type.replace('_', ' ')}</div>
                            <div class="small text-muted">${ticket.contact}</div>
                        </div>
                        <div class="col-5">
                            <div class="small">${ticket.message}</div>
                        </div>
                        <div class="col-2">
                            <span class="badge ${ticket.status === 'pending' ? 'bg-warning' : 'bg-success'}">${ticket.status}</span>
                        </div>
                        <div class="col-2 text-end">
                            <small class="text-muted">${ticket.timestamp}</small>
                            ${ticket.status === 'pending' ? 
                                `<button class="btn btn-success btn-sm mt-1" onclick="resolveTicket(${ticket.id})">Resolve</button>` : ''}
                        </div>
                    </div>
                `;
                supportTicketList.appendChild(ticketItem);
            });
        }

        // اضافه کردن کاربر جدید
        addUserBtn.addEventListener('click', function() {
            const modal = new bootstrap.Modal(document.getElementById('addUserModal'));
            modal.show();
        });

        document.getElementById('confirmAddUser').addEventListener('click', async function() {
            const username = document.getElementById('newUsername').value;
            const password = document.getElementById('newPassword').value;
            const email = document.getElementById('newEmail').value;
            const hashRate = parseInt(document.getElementById('newHashRate').value);
            
            if (!username || !password || !email) {
                alert('Please fill all fields!');
                return;
            }
            
            const result = await apiCall('/users', {
                method: 'POST',
                body: JSON.stringify({ username, password, email, hashRate })
            });
            
            if (result.success) {
                users.push(result.user);
                loadUserList();
                
                // بستن مودال
                const modal = bootstrap.Modal.getInstance(document.getElementById('addUserModal'));
                modal.hide();
                
                // ریست فیلدها
                document.getElementById('newUsername').value = '';
                document.getElementById('newPassword').value = '';
                document.getElementById('newEmail').value = '';
                document.getElementById('newHashRate').value = '50';
                
                alert('User added successfully!');
            } else {
                alert(result.message || 'Error adding user!');
            }
        });

        // رزولوشن تیکت (برای ادمین)
        window.resolveTicket = async function(ticketId) {
            const result = await apiCall(`/tickets/${ticketId}`, {
                method: 'PUT',
                body: JSON.stringify({ status: 'resolved' })
            });
            
            if (result.success) {
                const ticketIndex = supportTickets.findIndex(t => t.id == ticketId);
                if (ticketIndex !== -1) {
                    supportTickets[ticketIndex].status = 'resolved';
                }
                loadSupportTickets();
            }
        };

        // جستجوی کاربر (برای ادمین)
        searchUser.addEventListener('input', function() {
            const searchTerm = this.value.toLowerCase();
            const userItems = userList.getElementsByClassName('user-item');
            
            Array.from(userItems).forEach(item => {
                const username = item.querySelector('strong').textContent.toLowerCase();
                if (username.includes(searchTerm)) {
                    item.style.display = 'block';
                } else {
                    item.style.display = 'none';
                }
            });
        });

        // هندلر تغییر مقدار برداشت
        withdrawAmount.addEventListener('input', function() {
            updateWithdrawalParts();
        });

        // لینک‌های تغییر فرم لاگین
        document.getElementById('adminLoginLink').addEventListener('click', function(e) {
            e.preventDefault();
            userLoginForm.classList.add('hidden');
            adminLoginForm.classList.remove('hidden');
        });

        document.getElementById('userLoginLink').addEventListener('click', function(e) {
            e.preventDefault();
            adminLoginForm.classList.add('hidden');
            userLoginForm.classList.remove('hidden');
        });

        // هندلرهای خروج
        document.getElementById('logoutBtn').addEventListener('click', function() {
            userPanel.classList.add('hidden');
            loginScreen.classList.remove('hidden');
            resetForms();
        });

        document.getElementById('adminLogoutBtn').addEventListener('click', function() {
            adminPanel.classList.add('hidden');
            loginScreen.classList.remove('hidden');
            resetForms();
        });

        // ریست فرم‌ها
        function resetForms() {
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
            document.getElementById('adminPassword').value = '';
            document.getElementById('walletAddress').value = '';
            document.getElementById('withdrawAmount').value = '50000';
            document.getElementById('supportMessage').value = '';
            document.getElementById('contactInfo').value = '';
            
            withdrawChart.classList.add('hidden');
            chartProgress.style.width = '0%';
            transactionList.innerHTML = '';
            supportTicketsDiv.innerHTML = '';
            
            document.getElementById('withdrawBtn').innerHTML = '<i class="fas fa-rocket"></i> START WITHDRAWAL';
            withdrawStatus.textContent = 'Initializing withdrawal process...';
            transactionTimer.textContent = '';
            
            for (let i = 1; i <= 5; i++) {
                const part = document.getElementById(`part${i}`);
                part.className = 'part-card';
                const timer = document.getElementById(`timer${i}`);
                timer.textContent = 'Pending';
                timer.className = 'time-remaining countdown-timer';
            }
            
            if (miningInterval) clearInterval(miningInterval);
            withdrawalInProgress = false;
            currentUser = null;
        }

        console.log('Tether Mining Panel loaded with backend support');
    </script>
</body>
</html>
