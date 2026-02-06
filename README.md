<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>TaskReward - Earn Points, Get Rewards</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
        }

        :root {
            --primary: #4f46e5;
            --primary-light: #818cf8;
            --secondary: #10b981;
            --accent: #f59e0b;
            --dark: #1f2937;
            --light: #f9fafb;
            --gray: #9ca3af;
            --danger: #ef4444;
            --success: #10b981;
            --warning: #f59e0b;
            --card-bg: #ffffff;
            --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            --radius: 12px;
            --transition: all 0.3s ease;
        }

        body {
            background-color: #f5f7fb;
            color: var(--dark);
            min-height: 100vh;
            padding-bottom: 80px;
            position: relative;
        }

        .container {
            max-width: 100%;
            padding: 0 16px;
            margin: 0 auto;
        }

        /* Header Styles */
        .header {
            background: linear-gradient(135deg, var(--primary), var(--primary-light));
            color: white;
            padding: 20px 16px;
            box-shadow: var(--shadow);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 1.5rem;
            font-weight: 700;
        }

        .logo i {
            font-size: 1.8rem;
        }

        .profile-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: var(--transition);
        }

        .profile-icon:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        /* Auth Screens */
        .auth-container {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 80vh;
            padding: 20px;
        }

        .auth-card {
            background: var(--card-bg);
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            width: 100%;
            max-width: 400px;
            padding: 30px;
            margin: 0 auto;
        }

        .auth-tabs {
            display: flex;
            margin-bottom: 30px;
            border-bottom: 1px solid #e5e7eb;
        }

        .auth-tab {
            flex: 1;
            text-align: center;
            padding: 12px;
            font-weight: 600;
            color: var(--gray);
            cursor: pointer;
            transition: var(--transition);
        }

        .auth-tab.active {
            color: var(--primary);
            border-bottom: 2px solid var(--primary);
        }

        .auth-form {
            display: none;
        }

        .auth-form.active {
            display: block;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark);
        }

        .form-input {
            width: 100%;
            padding: 14px;
            border: 1px solid #d1d5db;
            border-radius: 8px;
            font-size: 16px;
            transition: var(--transition);
        }

        .form-input:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
        }

        .btn {
            display: block;
            width: 100%;
            padding: 14px;
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
        }

        .btn:hover {
            background: #4338ca;
        }

        .btn-secondary {
            background: var(--secondary);
        }

        .btn-secondary:hover {
            background: #0da271;
        }

        .btn-accent {
            background: var(--accent);
        }

        .btn-accent:hover {
            background: #d97706;
        }

        /* Dashboard Styles */
        .welcome-section {
            padding: 20px 0;
            margin-bottom: 20px;
        }

        .welcome-text {
            font-size: 1.2rem;
            color: var(--gray);
        }

        .welcome-name {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--dark);
            margin-top: 5px;
        }

        .balance-card {
            background: linear-gradient(135deg, var(--primary), var(--primary-light));
            color: white;
            border-radius: var(--radius);
            padding: 24px;
            box-shadow: var(--shadow);
            margin-bottom: 20px;
        }

        .balance-label {
            font-size: 0.9rem;
            opacity: 0.9;
            margin-bottom: 8px;
        }

        .balance-amount {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .balance-subtext {
            font-size: 0.9rem;
            opacity: 0.9;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 16px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 20px;
            box-shadow: var(--shadow);
            text-align: center;
        }

        .stat-icon {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: rgba(79, 70, 229, 0.1);
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 12px;
            color: var(--primary);
            font-size: 1.5rem;
        }

        .stat-value {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--dark);
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 0.9rem;
            color: var(--gray);
        }

        .section-title {
            font-size: 1.2rem;
            font-weight: 600;
            color: var(--dark);
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .task-list {
            margin-bottom: 30px;
        }

        .task-card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 20px;
            box-shadow: var(--shadow);
            margin-bottom: 16px;
            border-left: 4px solid var(--primary);
            transition: var(--transition);
        }

        .task-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }

        .task-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 12px;
        }

        .task-title {
            font-size: 1.1rem;
            font-weight: 600;
            color: var(--dark);
        }

        .task-reward {
            background: rgba(16, 185, 129, 0.1);
            color: var(--secondary);
            padding: 6px 12px;
            border-radius: 20px;
            font-weight: 600;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .task-description {
            color: var(--gray);
            margin-bottom: 16px;
            line-height: 1.5;
        }

        .task-status {
            display: inline-block;
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
        }

        .status-pending {
            background: rgba(245, 158, 11, 0.1);
            color: var(--warning);
        }

        .status-completed {
            background: rgba(16, 185, 129, 0.1);
            color: var(--success);
        }

        .task-actions {
            display: flex;
            justify-content: flex-end;
            margin-top: 16px;
        }

        /* Wallet Styles */
        .withdraw-card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 24px;
            box-shadow: var(--shadow);
            margin-bottom: 24px;
        }

        .withdraw-methods {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 16px;
            margin: 20px 0;
        }

        .method-card {
            border: 2px solid #e5e7eb;
            border-radius: var(--radius);
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
        }

        .method-card.selected {
            border-color: var(--primary);
            background: rgba(79, 70, 229, 0.05);
        }

        .method-icon {
            font-size: 2rem;
            color: var(--primary);
            margin-bottom: 10px;
        }

        .method-name {
            font-weight: 600;
            color: var(--dark);
        }

        .withdraw-info {
            background: rgba(245, 158, 11, 0.1);
            border-radius: var(--radius);
            padding: 16px;
            margin: 20px 0;
            color: var(--dark);
        }

        .info-title {
            font-weight: 600;
            margin-bottom: 8px;
            color: var(--warning);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .history-list {
            margin-top: 30px;
        }

        .history-item {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 16px;
            box-shadow: var(--shadow);
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .history-details h4 {
            font-weight: 600;
            margin-bottom: 5px;
        }

        .history-date {
            font-size: 0.8rem;
            color: var(--gray);
        }

        .history-amount {
            font-weight: 700;
            font-size: 1.2rem;
        }

        .history-status {
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
        }

        .status-approved {
            background: rgba(16, 185, 129, 0.1);
            color: var(--success);
        }

        .status-pending {
            background: rgba(245, 158, 11, 0.1);
            color: var(--warning);
        }

        .status-rejected {
            background: rgba(239, 68, 68, 0.1);
            color: var(--danger);
        }

        /* Profile Styles */
        .profile-header {
            display: flex;
            align-items: center;
            gap: 20px;
            margin-bottom: 30px;
            padding: 20px;
            background: var(--card-bg);
            border-radius: var(--radius);
            box-shadow: var(--shadow);
        }

        .profile-avatar {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary), var(--primary-light));
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 2rem;
            font-weight: 700;
        }

        .profile-info h2 {
            font-size: 1.5rem;
            margin-bottom: 8px;
        }

        .profile-info p {
            color: var(--gray);
        }

        .profile-details {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 24px;
            box-shadow: var(--shadow);
            margin-bottom: 24px;
        }

        .detail-item {
            display: flex;
            justify-content: space-between;
            padding: 16px 0;
            border-bottom: 1px solid #f1f1f1;
        }

        .detail-item:last-child {
            border-bottom: none;
        }

        .detail-label {
            font-weight: 500;
            color: var(--dark);
        }

        .detail-value {
            color: var(--gray);
        }

        .action-buttons {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-top: 30px;
        }

        /* Refer & Earn Page Styles */
        .refer-header {
            background: linear-gradient(135deg, #8b5cf6, #a78bfa);
            color: white;
            border-radius: var(--radius);
            padding: 30px 20px;
            text-align: center;
            margin: 20px 0;
            box-shadow: var(--shadow);
        }

        .refer-header h2 {
            font-size: 1.8rem;
            margin-bottom: 10px;
        }

        .refer-header p {
            opacity: 0.9;
            margin-bottom: 20px;
        }

        .refer-reward {
            background: rgba(255, 255, 255, 0.2);
            padding: 15px;
            border-radius: var(--radius);
            display: inline-block;
            font-size: 1.2rem;
            font-weight: 700;
        }

        .refer-code-container {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 25px;
            box-shadow: var(--shadow);
            margin: 25px 0;
            text-align: center;
        }

        .refer-code {
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--primary);
            letter-spacing: 3px;
            margin: 15px 0;
            padding: 15px;
            background: #f8fafc;
            border-radius: var(--radius);
            border: 2px dashed #c7d2fe;
        }

        .copy-btn {
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 8px;
            padding: 12px 30px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin: 0 auto;
            transition: var(--transition);
        }

        .copy-btn:hover {
            background: #4338ca;
        }

        .share-section {
            margin: 30px 0;
        }

        .share-title {
            font-size: 1.3rem;
            font-weight: 600;
            margin-bottom: 20px;
            text-align: center;
            color: var(--dark);
        }

        .share-buttons {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-bottom: 30px;
        }

        .share-btn {
            background: var(--card-bg);
            border: 2px solid #e5e7eb;
            border-radius: var(--radius);
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
        }

        .share-btn:hover {
            transform: translateY(-3px);
            box-shadow: var(--shadow);
            border-color: var(--primary);
        }

        .share-icon {
            font-size: 2rem;
            margin-bottom: 5px;
        }

        .share-btn.whatsapp .share-icon {
            color: #25D366;
        }

        .share-btn.facebook .share-icon {
            color: #1877F2;
        }

        .share-btn.twitter .share-icon {
            color: #1DA1F2;
        }

        .share-btn.instagram .share-icon {
            color: #E4405F;
        }

        .share-btn.telegram .share-icon {
            color: #0088cc;
        }

        .share-btn.messenger .share-icon {
            color: #006AFF;
        }

        .share-btn.more .share-icon {
            color: var(--primary);
        }

        .share-btn-name {
            font-weight: 600;
            font-size: 0.9rem;
            color: var(--dark);
        }

        .referral-stats {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin: 30px 0;
        }

        .stat-box {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 20px;
            text-align: center;
            box-shadow: var(--shadow);
        }

        .stat-box-value {
            font-size: 2rem;
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 5px;
        }

        .stat-box-label {
            font-size: 0.9rem;
            color: var(--gray);
        }

        .referral-link-container {
            background: #f8fafc;
            border-radius: var(--radius);
            padding: 20px;
            margin: 25px 0;
            border: 1px solid #e5e7eb;
        }

        .referral-link {
            font-size: 0.9rem;
            color: var(--gray);
            word-break: break-all;
            padding: 15px;
            background: white;
            border-radius: 8px;
            border: 1px solid #d1d5db;
            margin: 15px 0;
        }

        .terms-note {
            background: rgba(245, 158, 11, 0.1);
            border-radius: var(--radius);
            padding: 15px;
            margin: 25px 0;
            font-size: 0.9rem;
            color: var(--dark);
        }

        /* Bottom Navigation */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: var(--card-bg);
            display: flex;
            justify-content: space-around;
            padding: 12px 0;
            box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
            z-index: 100;
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-decoration: none;
            color: var(--gray);
            transition: var(--transition);
            padding: 8px 16px;
            border-radius: 8px;
        }

        .nav-item.active {
            color: var(--primary);
            background: rgba(79, 70, 229, 0.1);
        }

        .nav-icon {
            font-size: 1.2rem;
            margin-bottom: 4px;
        }

        .nav-label {
            font-size: 0.8rem;
            font-weight: 500;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: white;
            border-radius: var(--radius);
            width: 90%;
            max-width: 500px;
            max-height: 90vh;
            overflow-y: auto;
            padding: 24px;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-title {
            font-size: 1.3rem;
            font-weight: 600;
            color: var(--dark);
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            color: var(--gray);
            cursor: pointer;
        }

        /* Toast Notifications */
        .toast {
            position: fixed;
            top: 20px;
            right: 20px;
            background: var(--dark);
            color: white;
            padding: 16px 24px;
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            z-index: 1001;
            display: flex;
            align-items: center;
            gap: 12px;
            transform: translateX(150%);
            transition: transform 0.3s ease;
        }

        .toast.show {
            transform: translateX(0);
        }

        .toast.success {
            background: var(--success);
        }

        .toast.error {
            background: var(--danger);
        }

        .toast.warning {
            background: var(--warning);
        }

        /* Loading Spinner */
        .spinner {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* Validation Error Styles */
        .error-message {
            color: var(--danger);
            font-size: 0.85rem;
            margin-top: 5px;
            display: none;
        }

        .error-message.show {
            display: block;
        }

        .form-input.error {
            border-color: var(--danger);
        }

        /* Conversion Info */
        .conversion-info {
            background: rgba(79, 70, 229, 0.1);
            border-radius: var(--radius);
            padding: 12px 16px;
            margin: 15px 0;
            text-align: center;
            font-size: 0.9rem;
            color: var(--primary);
            font-weight: 500;
        }

        /* Withdrawal Calculation */
        .withdrawal-calc {
            background: rgba(16, 185, 129, 0.1);
            border-radius: var(--radius);
            padding: 15px;
            margin: 15px 0;
            font-size: 0.9rem;
        }

        .calc-item {
            display: flex;
            justify-content: space-between;
            padding: 5px 0;
        }

        .calc-label {
            color: var(--gray);
        }

        .calc-value {
            font-weight: 600;
            color: var(--dark);
        }

        .calc-total {
            border-top: 1px solid #ddd;
            margin-top: 8px;
            padding-top: 8px;
            font-weight: 700;
            color: var(--success);
        }

        /* Responsive Adjustments */
        @media (min-width: 768px) {
            .container {
                max-width: 750px;
                padding: 0 20px;
            }
            
            .share-buttons {
                grid-template-columns: repeat(6, 1fr);
            }
        }

        @media (min-width: 992px) {
            .container {
                max-width: 970px;
            }
        }

        @media (min-width: 1200px) {
            .container {
                max-width: 1170px;
            }
        }
    </style>
</head>
<body><script>
  atOptions = {
    'key' : '89c3bb8b234d16552af7d434079f4d62',
    'format' : 'iframe',
    'height' : 50,
    'width' : 320,
    'params' : {}
  };
</script>
<script src="https://www.highperformanceformat.com/89c3bb8b234d16552af7d434079f4d62/invoke.js"></script>
    <!-- Onboarding / Auth Screen -->
    <div id="authScreen" class="auth-container">
        <div class="auth-card">
            <div class="auth-tabs">
                <div class="auth-tab active" id="loginTab">Login</div>
                <div class="auth-tab" id="signupTab">Sign Up</div>
            </div>
            
            <form id="loginForm" class="auth-form active">
                <h2 style="margin-bottom: 20px; text-align: center;">Welcome Back</h2>
                <div class="form-group">
                    <label class="form-label" for="loginMobile">Mobile Number</label>
                    <input type="tel" id="loginMobile" class="form-input" placeholder="Enter your mobile number" required>
                    <div class="error-message" id="loginMobileError">Please enter a valid 10-digit mobile number</div>
                </div>
                <div class="form-group">
                    <label class="form-label" for="loginPassword">Password</label>
                    <input type="password" id="loginPassword" class="form-input" placeholder="Enter your password" required>
                    <div class="error-message" id="loginPasswordError">Password must be at least 6 characters</div>
                </div>
                <button type="submit" class="btn">Login</button>
                <p style="text-align: center; margin-top: 20px; color: var(--gray);">
                    Don't have an account? <a href="#" id="switchToSignup" style="color: var(--primary); font-weight: 500;">Sign Up</a>
                </p>
            </form>
            
            <form id="signupForm" class="auth-form">
                <h2 style="margin-bottom: 20px; text-align: center;">Create Account</h2>
                <div class="form-group">
                    <label class="form-label" for="signupName">Full Name</label>
                    <input type="text" id="signupName" class="form-input" placeholder="Enter your full name" required>
                    <div class="error-message" id="signupNameError">Please enter your full name</div>
                </div>
                <div class="form-group">
                    <label class="form-label" for="signupMobile">Mobile Number</label>
                    <input type="tel" id="signupMobile" class="form-input" placeholder="Enter your mobile number" required>
                    <div class="error-message" id="signupMobileError">Please enter a valid 10-digit mobile number</div>
                </div>
                <div class="form-group">
                    <label class="form-label" for="signupPassword">Password</label>
                    <input type="password" id="signupPassword" class="form-input" placeholder="Create a strong password" required>
                    <div class="error-message" id="signupPasswordError">Password must be at least 6 characters</div>
                </div>
                <div class="form-group">
                    <label class="form-label" for="confirmPassword">Confirm Password</label>
                    <input type="password" id="confirmPassword" class="form-input" placeholder="Confirm your password" required>
                    <div class="error-message" id="confirmPasswordError">Passwords do not match</div>
                </div>
                <div class="conversion-info">
                    <i class="fas fa-coins"></i> 100 Points = ₹20.00
                </div>
                <button type="submit" class="btn btn-secondary">Sign Up</button>
                <p style="text-align: center; margin-top: 20px; color: var(--gray);">
                    Already have an account? <a href="#" id="switchToLogin" style="color: var(--primary); font-weight: 500;">Login</a>
                </p>
            </form>
        </div>
    </div>

    <!-- Main App (Initially Hidden) -->
    <div id="appScreen" style="display: none;">
        <!-- Header -->
        <header class="header">
            <div class="container header-content">
                <div class="logo">
                    <i class="fas fa-gem"></i>
                    <span>TaskReward</span>
                </div>
                <div class="profile-icon" id="profileIcon">
                    <i class="fas fa-user"></i>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <main class="container">
            <!-- Dashboard Content -->
            <div id="dashboardContent" class="page-content">
                <div class="welcome-section">
                    <div class="welcome-text">Welcome back,</div>
                    <div class="welcome-name" id="userName">User</div>
                </div>
                
                <div class="balance-card">
                    <div class="balance-label">Your Balance</div>
                    <div class="balance-amount" id="userBalance">0</div>
                    <div class="balance-subtext">100 Points = ₹20.00</div>
                </div>
                
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-icon">
                            <i class="fas fa-tasks"></i>
                        </div>
                        <div class="stat-value" id="todayTasks">0</div>
                        <div class="stat-label">Today's Tasks</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon">
                            <i class="fas fa-rupee-sign"></i>
                        </div>
                        <div class="stat-value" id="totalEarnings">₹0</div>
                        <div class="stat-label">Total Earnings</div>
                    </div>
                </div>
                
                <div class="section-title">
                    <span>Available Tasks</span>
                    <span id="viewAllTasks" style="color: var(--primary); font-size: 0.9rem; cursor: pointer;">View All</span>
                </div>
                
                <div class="task-list" id="dashboardTasks">
                    <!-- Tasks will be loaded here via JavaScript -->
                </div>
            </div>

            <!-- Tasks Content -->
            <div id="tasksContent" class="page-content" style="display: none;">
                <div class="section-title" style="margin-top: 20px;">
                    <span>All Available Tasks</span>
                </div>
                
                <div class="task-list" id="allTasksList">
                    <!-- All tasks will be loaded here via JavaScript -->
                </div>
            </div>

            <!-- Wallet Content -->
            <div id="walletContent" class="page-content" style="display: none;">
                <div class="section-title" style="margin-top: 20px;">
                    <span>Withdraw Funds</span>
                </div>
                
                <div class="withdraw-card">
                    <div class="balance-label">Available Balance</div>
                    <div class="balance-amount" id="withdrawBalance">0</div>
                    <div class="balance-subtext">Minimum withdrawal: 825 points (₹165)</div>
                    
                    <div class="withdraw-methods">
                        <div class="method-card" data-method="upi">
                            <div class="method-icon">
                                <i class="fas fa-qrcode"></i>
                            </div>
                            <div class="method-name">UPI</div>
                        </div>
                        <div class="method-card" data-method="bank">
                            <div class="method-icon">
                                <i class="fas fa-university"></i>
                            </div>
                            <div class="method-name">Bank Transfer</div>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label" for="withdrawAmount">Points to Withdraw</label>
                        <input type="number" id="withdrawAmount" class="form-input" placeholder="Enter amount (min: 825)" min="825">
                        <div class="error-message" id="withdrawAmountError">Minimum 825 points required</div>
                    </div>
                    
                    <div id="withdrawalCalculation" class="withdrawal-calc" style="display: none;">
                        <div class="calc-item">
                            <span class="calc-label">Withdrawal Amount:</span>
                            <span class="calc-value" id="calcPoints">0 points</span>
                        </div>
                        <div class="calc-item">
                            <span class="calc-label">Conversion Rate:</span>
                            <span class="calc-value">100 points = ₹20</span>
                        </div>
                        <div class="calc-item">
                            <span class="calc-label">Your Amount:</span>
                            <span class="calc-value" id="calcUserAmount">₹0</span>
                        </div>
                        <div class="calc-item">
                            <span class="calc-label">Team Commission (15₹):</span>
                            <span class="calc-value">- ₹15</span>
                        </div>
                        <div class="calc-item calc-total">
                            <span class="calc-label">You Will Receive:</span>
                            <span class="calc-value" id="calcFinalAmount">₹0</span>
                        </div>
                    </div>
                    
                    <div id="upiDetails" class="form-group" style="display: none;">
                        <label class="form-label" for="upiId">UPI ID</label>
                        <input type="text" id="upiId" class="form-input" placeholder="yourname@upi">
                        <div class="error-message" id="upiIdError">Please enter a valid UPI ID</div>
                    </div>
                    
                    <div id="bankDetails" style="display: none;">
                        <div class="form-group">
                            <label class="form-label" for="accountNumber">Account Number</label>
                            <input type="text" id="accountNumber" class="form-input" placeholder="Enter account number">
                            <div class="error-message" id="accountNumberError">Please enter a valid account number</div>
                        </div>
                        <div class="form-group">
                            <label class="form-label" for="ifscCode">IFSC Code</label>
                            <input type="text" id="ifscCode" class="form-input" placeholder="Enter IFSC code">
                            <div class="error-message" id="ifscCodeError">Please enter a valid IFSC code</div>
                        </div>
                        <div class="form-group">
                            <label class="form-label" for="accountHolder">Account Holder Name</label>
                            <input type="text" id="accountHolder" class="form-input" placeholder="Enter account holder name">
                            <div class="error-message" id="accountHolderError">Please enter account holder name</div>
                        </div>
                    </div>
                    
                    <div class="withdraw-info">
                        <div class="info-title">
                            <i class="fas fa-info-circle"></i>
                            <span>Important Information</span>
                        </div>
                        <p style="font-size: 0.9rem;">
                            • Minimum withdrawal: 825 points (₹165)<br>
                            • Team commission: ₹15 per withdrawal<br>
                            • You will receive: ₹150 per withdrawal<br>
                            • Processing time: 24-72 hours
                        </p>
                    </div>
                    
                    <button class="btn btn-accent" id="submitWithdrawal">Submit Withdrawal Request</button>
                </div>
                
                <div class="section-title">
                    <span>Withdrawal History</span>
                </div>
                
                <div class="history-list" id="withdrawalHistory">
                    <!-- Withdrawal history will be loaded here via JavaScript -->
                </div>
            </div>

            <!-- Profile Content -->
            <div id="profileContent" class="page-content" style="display: none;">
                <div class="profile-header">
                    <div class="profile-avatar" id="profileAvatar">U</div>
                    <div class="profile-info">
                        <h2 id="profileName">User</h2>
                        <p id="profileUserId">User ID: TR-00000</p>
                    </div>
                </div>
                
                <div class="profile-details">
                    <div class="detail-item">
                        <span class="detail-label">Mobile Number</span>
                        <span class="detail-value" id="profileMobile">Not set</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">Total Earnings</span>
                        <span class="detail-value" id="profileEarnings">₹0</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">Tasks Completed</span>
                        <span class="detail-value" id="profileTasksCompleted">0</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">Account Status</span>
                        <span class="detail-value" style="color: var(--success); font-weight: 600;">Active</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">Member Since</span>
                        <span class="detail-value" id="memberSince">-</span>
                    </div>
                </div>
                
                <div class="action-buttons">
                    <button class="btn" id="editProfileBtn">
                        <i class="fas fa-edit"></i> Edit Profile
                    </button>
                    <button class="btn btn-secondary" id="changePasswordBtn">
                        <i class="fas fa-lock"></i> Change Password
                    </button>
                    <button class="btn" style="background: #f1f1f1; color: var(--dark);" id="logoutBtn">
                        <i class="fas fa-sign-out-alt"></i> Logout
                    </button>
                </div>
            </div>

            <!-- Refer & Earn Content -->
            <div id="referContent" class="page-content" style="display: none;">
                <div class="refer-header">
                    <h2>Refer & Earn</h2>
                    <p>Invite your friends and earn rewards!</p>
                    <div class="refer-reward">
                        <i class="fas fa-gift"></i> Earn 125 Coins Per Referral
                    </div>
                </div>
                
                <div class="refer-code-container">
                    <h3 style="margin-bottom: 15px; color: var(--dark);">Your Referral Code</h3>
                    <div class="refer-code" id="referralCode">TR-REF-00000</div>
                    <button class="copy-btn" id="copyReferralCode">
                        <i class="fas fa-copy"></i> Copy Code
                    </button>
                </div>
                
                <div class="referral-stats">
                    <div class="stat-box">
                        <div class="stat-box-value" id="totalReferrals">0</div>
                        <div class="stat-box-label">Total Referrals</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-box-value" id="referralEarnings">0</div>
                        <div class="stat-box-label">Coins Earned</div>
                    </div>
                </div>
                
                <div class="share-section">
                    <div class="share-title">Share via</div>
                    <div class="share-buttons">
                        <div class="share-btn whatsapp" data-platform="whatsapp">
                            <div class="share-icon">
                                <i class="fab fa-whatsapp"></i>
                            </div>
                            <div class="share-btn-name">WhatsApp</div>
                        </div>
                        <div class="share-btn facebook" data-platform="facebook">
                            <div class="share-icon">
                                <i class="fab fa-facebook"></i>
                            </div>
                            <div class="share-btn-name">Facebook</div>
                        </div>
                        <div class="share-btn twitter" data-platform="twitter">
                            <div class="share-icon">
                                <i class="fab fa-twitter"></i>
                            </div>
                            <div class="share-btn-name">Twitter</div>
                        </div>
                        <div class="share-btn instagram" data-platform="instagram">
                            <div class="share-icon">
                                <i class="fab fa-instagram"></i>
                            </div>
                            <div class="share-btn-name">Instagram</div>
                        </div>
                        <div class="share-btn telegram" data-platform="telegram">
                            <div class="share-icon">
                                <i class="fab fa-telegram"></i>
                            </div>
                            <div class="share-btn-name">Telegram</div>
                        </div>
                        <div class="share-btn more" data-platform="more">
                            <div class="share-icon">
                                <i class="fas fa-share-alt"></i>
                            </div>
                            <div class="share-btn-name">More</div>
                        </div>
                    </div>
                </div>
                
                <div class="referral-link-container">
                    <h3 style="margin-bottom: 15px; color: var(--dark);">Your Referral Link</h3>
                    <div class="referral-link" id="referralLink">https://taskreward.app/ref/TR-REF-00000</div>
                    <button class="copy-btn" id="copyReferralLink">
                        <i class="fas fa-link"></i> Copy Link
                    </button>
                </div>
                
                <div class="terms-note">
                    <div class="info-title">
                        <i class="fas fa-info-circle"></i>
                        <span>How It Works</span>
                    </div>
                    <p style="margin-top: 10px; font-size: 0.9rem;">
                        • Share your referral code or link with friends<br>
                        • When they sign up using your code, you earn <strong>125 coins</strong><br>
                        • Your friend gets <strong>₹165 bonus</strong> on their first withdrawal<br>
                        • You can refer unlimited friends and earn unlimited coins!
                    </p>
                </div>
                
                <div class="section-title" style="margin-top: 30px;">
                    <span>Referral History</span>
                </div>
                
                <div class="history-list" id="referralHistory">
                    <div style="text-align: center; padding: 40px 20px; color: var(--gray);">
                        <i class="fas fa-users" style="font-size: 2rem; margin-bottom: 15px; opacity: 0.5;"></i>
                        <p>No referrals yet. Share your code to start earning!</p>
                    </div>
                </div>
            </div>
        </main>

        <!-- Bottom Navigation -->
        <nav class="bottom-nav">
            <a href="#" class="nav-item active" data-page="dashboard">
                <i class="fas fa-home nav-icon"></i>
                <span class="nav-label">Home</span>
            </a>
            <a href="#" class="nav-item" data-page="tasks">
                <i class="fas fa-tasks nav-icon"></i>
                <span class="nav-label">Tasks</span>
            </a>
            <a href="#" class="nav-item" data-page="wallet">
                <i class="fas fa-wallet nav-icon"></i>
                <span class="nav-label">Wallet</span>
            </a>
            <a href="#" class="nav-item" data-page="refer">
                <i class="fas fa-user-friends nav-icon"></i>
                <span class="nav-label">Refer</span>
            </a>
            <a href="#" class="nav-item" data-page="profile">
                <i class="fas fa-user nav-icon"></i>
                <span class="nav-label">Profile</span>
            </a>
        </nav>
    </div>

    <!-- Task Completion Modal -->
    <div class="modal" id="taskCompletionModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">Complete Task</div>
                <button class="close-modal" id="closeTaskModal">&times;</button>
            </div>
            <div id="taskModalContent">
                <!-- Content will be loaded dynamically -->
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div class="toast" id="toast">
        <i class="fas fa-check-circle" id="toastIcon"></i>
        <span id="toastMessage">Task completed successfully!</span>
    </div>

    <script>
        // Main application JavaScript
        document.addEventListener('DOMContentLoaded', function() {
            // Initialize the app
            initializeApp();
        });

        function initializeApp() {
            // Check if user is already logged in (simulated)
            const isLoggedIn = localStorage.getItem('taskRewardLoggedIn') === 'true';
            
            if (isLoggedIn) {
                showAppScreen();
                loadUserData();
                loadDashboardTasks();
                loadAllTasks();
                loadWithdrawalHistory();
                loadReferralData();
            } else {
                showAuthScreen();
            }
            
            setupEventListeners();
        }
        
        function showAuthScreen() {
            document.getElementById('authScreen').style.display = 'flex';
            document.getElementById('appScreen').style.display = 'none';
        }
        
        function showAppScreen() {
            document.getElementById('authScreen').style.display = 'none';
            document.getElementById('appScreen').style.display = 'block';
            showPage('dashboard');
        }
        
        function showPage(page) {
            // Hide all pages
            document.querySelectorAll('.page-content').forEach(el => {
                el.style.display = 'none';
            });
            
            // Remove active class from all nav items
            document.querySelectorAll('.nav-item').forEach(el => {
                el.classList.remove('active');
            });
            
            // Show selected page and activate nav item
            document.getElementById(`${page}Content`).style.display = 'block';
            document.querySelector(`.nav-item[data-page="${page}"]`).classList.add('active');
        }
        
        function setupEventListeners() {
            // Auth tabs
            document.getElementById('loginTab').addEventListener('click', () => switchAuthTab('login'));
            document.getElementById('signupTab').addEventListener('click', () => switchAuthTab('signup'));
            document.getElementById('switchToSignup').addEventListener('click', (e) => {
                e.preventDefault();
                switchAuthTab('signup');
            });
            document.getElementById('switchToLogin').addEventListener('click', (e) => {
                e.preventDefault();
                switchAuthTab('login');
            });
            
            // Auth forms
            document.getElementById('loginForm').addEventListener('submit', handleLogin);
            document.getElementById('signupForm').addEventListener('submit', handleSignup);
            
            // Navigation
            document.querySelectorAll('.nav-item').forEach(item => {
                item.addEventListener('click', (e) => {
                    e.preventDefault();
                    const page = e.currentTarget.getAttribute('data-page');
                    showPage(page);
                    
                    // Load referral data when refer page is opened
                    if (page === 'refer') {
                        loadReferralData();
                    }
                });
            });
            
            // Profile icon
            document.getElementById('profileIcon').addEventListener('click', () => {
                showPage('profile');
            });
            
            // View all tasks
            document.getElementById('viewAllTasks').addEventListener('click', () => {
                showPage('tasks');
            });
            
            // Withdrawal methods
            document.querySelectorAll('.method-card').forEach(card => {
                card.addEventListener('click', () => {
                    document.querySelectorAll('.method-card').forEach(c => c.classList.remove('selected'));
                    card.classList.add('selected');
                    
                    const method = card.getAttribute('data-method');
                    document.getElementById('upiDetails').style.display = method === 'upi' ? 'block' : 'none';
                    document.getElementById('bankDetails').style.display = method === 'bank' ? 'block' : 'none';
                });
            });
            
            // Withdrawal amount calculation
            document.getElementById('withdrawAmount').addEventListener('input', updateWithdrawalCalculation);
            
            // Submit withdrawal
            document.getElementById('submitWithdrawal').addEventListener('click', submitWithdrawal);
            
            // Edit profile
            document.getElementById('editProfileBtn').addEventListener('click', editProfile);
            
            // Change password
            document.getElementById('changePasswordBtn').addEventListener('click', changePassword);
            
            // Logout
            document.getElementById('logoutBtn').addEventListener('click', logout);
            
            // Task modal
            document.getElementById('closeTaskModal').addEventListener('click', () => {
                document.getElementById('taskCompletionModal').classList.remove('active');
            });
            
            // Refer & Earn functionality
            document.getElementById('copyReferralCode').addEventListener('click', copyReferralCode);
            document.getElementById('copyReferralLink').addEventListener('click', copyReferralLink);
            
            // Share buttons
            document.querySelectorAll('.share-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const platform = this.getAttribute('data-platform');
                    shareReferral(platform);
                });
            });
        }
        
        function switchAuthTab(tab) {
            document.querySelectorAll('.auth-tab').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.auth-form').forEach(el => el.classList.remove('active'));
            
            if (tab === 'login') {
                document.getElementById('loginTab').classList.add('active');
                document.getElementById('loginForm').classList.add('active');
            } else {
                document.getElementById('signupTab').classList.add('active');
                document.getElementById('signupForm').classList.add('active');
            }
        }
        
        // Validation functions
        function validateMobile(mobile) {
            const mobileRegex = /^[6-9]\d{9}$/;
            return mobileRegex.test(mobile.replace(/\D/g, ''));
        }
        
        function validatePassword(password) {
            return password.length >= 6;
        }
        
        function showError(elementId, message) {
            const errorElement = document.getElementById(elementId);
            errorElement.textContent = message;
            errorElement.classList.add('show');
            document.getElementById(elementId.replace('Error', '')).classList.add('error');
        }
        
        function hideError(elementId) {
            const errorElement = document.getElementById(elementId);
            errorElement.classList.remove('show');
            document.getElementById(elementId.replace('Error', '')).classList.remove('error');
        }
        
        function handleLogin(e) {
            e.preventDefault();
            const mobile = document.getElementById('loginMobile').value.trim();
            const password = document.getElementById('loginPassword').value;
            
            // Reset errors
            hideError('loginMobileError');
            hideError('loginPasswordError');
            
            let hasError = false;
            
            // Validate mobile
            if (!validateMobile(mobile)) {
                showError('loginMobileError', 'Please enter a valid 10-digit mobile number');
                hasError = true;
            }
            
            // Validate password
            if (!validatePassword(password)) {
                showError('loginPasswordError', 'Password must be at least 6 characters');
                hasError = true;
            }
            
            if (hasError) return;
            
            // Check if user exists
            const storedMobile = localStorage.getItem('taskRewardUserMobile');
            const storedPassword = localStorage.getItem('taskRewardUserPassword');
            
            if (storedMobile === mobile && storedPassword === password) {
                // Login successful
                localStorage.setItem('taskRewardLoggedIn', 'true');
                showAppScreen();
                loadUserData();
                loadDashboardTasks();
                loadAllTasks();
                loadWithdrawalHistory();
                loadReferralData();
                showToast('Login successful!', 'success');
            } else {
                showError('loginPasswordError', 'Invalid mobile number or password');
                showToast('Invalid credentials', 'error');
            }
        }
        
        function handleSignup(e) {
            e.preventDefault();
            const name = document.getElementById('signupName').value.trim();
            const mobile = document.getElementById('signupMobile').value.trim();
            const password = document.getElementById('signupPassword').value;
            const confirmPassword = document.getElementById('confirmPassword').value;
            
            // Reset errors
            hideError('signupNameError');
            hideError('signupMobileError');
            hideError('signupPasswordError');
            hideError('confirmPasswordError');
            
            let hasError = false;
            
            // Validate name
            if (name.length < 2) {
                showError('signupNameError', 'Please enter your full name');
                hasError = true;
            }
            
            // Validate mobile
            if (!validateMobile(mobile)) {
                showError('signupMobileError', 'Please enter a valid 10-digit mobile number');
                hasError = true;
            }
            
            // Validate password
            if (!validatePassword(password)) {
                showError('signupPasswordError', 'Password must be at least 6 characters');
                hasError = true;
            }
            
            // Validate confirm password
            if (password !== confirmPassword) {
                showError('confirmPasswordError', 'Passwords do not match');
                hasError = true;
            }
            
            if (hasError) return;
            
            // Check if mobile already registered
            const existingUser = localStorage.getItem('taskRewardUserMobile');
            if (existingUser === mobile) {
                showError('signupMobileError', 'Mobile number already registered');
                showToast('Mobile number already exists', 'error');
                return;
            }
            
            // Registration successful
            localStorage.setItem('taskRewardLoggedIn', 'true');
            localStorage.setItem('taskRewardUserName', name);
            localStorage.setItem('taskRewardUserMobile', mobile);
            localStorage.setItem('taskRewardUserPassword', password);
            
            // Generate a user ID
            const userId = 'TR-' + Math.floor(10000 + Math.random() * 90000);
            localStorage.setItem('taskRewardUserId', userId);
            
            // Generate referral code
            const referralCode = 'TR-REF-' + Math.floor(10000 + Math.random() * 90000);
            localStorage.setItem('taskRewardReferralCode', referralCode);
            
            // Set initial values to 0
            localStorage.setItem('taskRewardBalance', '0');
            localStorage.setItem('taskRewardEarnings', '0');
            localStorage.setItem('taskRewardTasksCompleted', '0');
            localStorage.setItem('taskRewardReferrals', '0');
            localStorage.setItem('taskRewardReferralEarnings', '0');
            
            // Set registration date
            const registrationDate = new Date().toLocaleDateString('en-IN', { 
                day: 'numeric', 
                month: 'long', 
                year: 'numeric' 
            });
            localStorage.setItem('taskRewardRegistrationDate', registrationDate);
            
            // Show app screen
            showAppScreen();
            loadUserData();
            loadDashboardTasks();
            loadAllTasks();
            loadWithdrawalHistory();
            loadReferralData();
            showToast('Registration successful!', 'success');
        }
        
        function loadUserData() {
            // Load user data from localStorage
            const userName = localStorage.getItem('taskRewardUserName') || 'User';
            const userMobile = localStorage.getItem('taskRewardUserMobile') || 'Not set';
            const userId = localStorage.getItem('taskRewardUserId') || 'TR-00000';
            const balance = parseInt(localStorage.getItem('taskRewardBalance') || '0');
            const earnings = parseFloat(localStorage.getItem('taskRewardEarnings') || '0');
            const tasksCompleted = parseInt(localStorage.getItem('taskRewardTasksCompleted') || '0');
            const registrationDate = localStorage.getItem('taskRewardRegistrationDate') || '-';
            
            // Calculate rupee value (100 points = ₹20)
            const rupeeValue = (balance / 100) * 20;
            
            // Update UI
            document.getElementById('userName').textContent = userName;
            document.getElementById('userBalance').textContent = balance.toLocaleString();
            document.getElementById('withdrawBalance').textContent = balance.toLocaleString();
            document.getElementById('profileName').textContent = userName;
            document.getElementById('profileMobile').textContent = userMobile;
            document.getElementById('profileUserId').textContent = `User ID: ${userId}`;
            document.getElementById('profileEarnings').textContent = `₹${earnings.toFixed(2)}`;
            document.getElementById('profileTasksCompleted').textContent = tasksCompleted;
            document.getElementById('totalEarnings').textContent = `₹${earnings.toFixed(2)}`;
            document.getElementById('memberSince').textContent = registrationDate;
            
            // Set profile avatar initials
            const initials = userName.split(' ').map(n => n[0]).join('').toUpperCase() || 'U';
            document.getElementById('profileAvatar').textContent = initials.substring(0, 2);
        }
        
        function loadReferralData() {
            // Load referral data
            const referralCode = localStorage.getItem('taskRewardReferralCode') || 'TR-REF-00000';
            const totalReferrals = parseInt(localStorage.getItem('taskRewardReferrals') || '0');
            const referralEarnings = parseInt(localStorage.getItem('taskRewardReferralEarnings') || '0');
            
            // Update UI
            document.getElementById('referralCode').textContent = referralCode;
            document.getElementById('referralLink').textContent = `https://taskreward.app/ref/${referralCode}`;
            document.getElementById('totalReferrals').textContent = totalReferrals;
            document.getElementById('referralEarnings').textContent = referralEarnings;
        }
        
        function loadDashboardTasks() {
            const tasksContainer = document.getElementById('dashboardTasks');
            const tasks = getSampleTasks().slice(0, 3); // Show only 3 tasks on dashboard
            
            tasksContainer.innerHTML = '';
            
            tasks.forEach(task => {
                const taskElement = createTaskElement(task);
                tasksContainer.appendChild(taskElement);
            });
            
            // Update today's tasks count
            document.getElementById('todayTasks').textContent = tasks.length;
        }
        
        function loadAllTasks() {
            const tasksContainer = document.getElementById('allTasksList');
            const tasks = getSampleTasks();
            
            tasksContainer.innerHTML = '';
            
            tasks.forEach(task => {
                const taskElement = createTaskElement(task);
                tasksContainer.appendChild(taskElement);
            });
        }
        
        function createTaskElement(task) {
            const taskElement = document.createElement('div');
            taskElement.className = 'task-card';
            taskElement.setAttribute('data-task-id', task.id);
            
            const isCompleted = localStorage.getItem(`task_${task.id}_completed`) === 'true';
            
            taskElement.innerHTML = `
                <div class="task-header">
                    <div class="task-title">${task.title}</div>
                    <div class="task-reward">
                        <i class="fas fa-coins"></i>
                        ${task.reward}
                    </div>
                </div>
                <div class="task-description">${task.description}</div>
                <div>
                    <span class="task-status ${isCompleted ? 'status-completed' : 'status-pending'}">
                        ${isCompleted ? 'Completed' : 'Pending'}
                    </span>
                </div>
                ${!isCompleted ? `
                    <div class="task-actions">
                        <button class="btn btn-accent" style="padding: 10px 20px; font-size: 0.9rem;" data-task-action="complete">
                            Complete Task
                        </button>
                    </div>
                ` : ''}
            `;
            
            // Add event listener to complete button
            if (!isCompleted) {
                const completeBtn = taskElement.querySelector('[data-task-action="complete"]');
                completeBtn.addEventListener('click', () => showTaskCompletionModal(task));
            }
            
            return taskElement;
        }
        
        function showTaskCompletionModal(task) {
            const modalContent = document.getElementById('taskModalContent');
            
            modalContent.innerHTML = `
                <h3 style="margin-bottom: 10px;">${task.title}</h3>
                <p style="margin-bottom: 20px; color: var(--gray);">${task.description}</p>
                <p style="margin-bottom: 20px;"><strong>Reward:</strong> <span style="color: var(--secondary);">${task.reward} points (₹${(parseInt(task.reward)/100*20).toFixed(2)})</span></p>
                
                ${task.instructions ? `
                    <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
                        <h4 style="margin-bottom: 10px;">Instructions:</h4>
                        <p>${task.instructions}</p>
                    </div>
                ` : ''}
                
                ${task.requiresProof ? `
                    <div class="form-group">
                        <label class="form-label" for="taskProof">Submit Proof (URL or Description)</label>
                        <input type="text" id="taskProof" class="form-input" placeholder="Enter proof of completion">
                    </div>
                ` : ''}
                
                <button class="btn btn-secondary" id="submitTaskCompletion" data-task-id="${task.id}">
                    Submit for Verification
                </button>
            `;
            
            document.getElementById('taskCompletionModal').classList.add('active');
            
            // Add event listener to submit button
            document.getElementById('submitTaskCompletion').addEventListener('click', () => completeTask(task.id));
        }
        
        function completeTask(taskId) {
            const task = getSampleTasks().find(t => t.id === taskId);
            const proofInput = document.getElementById('taskProof');
            const proof = proofInput ? proofInput.value : null;
            
            // Validate proof if required
            if (task.requiresProof && (!proof || proof.trim() === '')) {
                showToast('Please submit proof of completion', 'error');
                return;
            }
            
            // Mark task as completed
            localStorage.setItem(`task_${taskId}_completed`, 'true');
            
            // Update balance
            const currentBalance = parseInt(localStorage.getItem('taskRewardBalance') || '0');
            const reward = parseInt(task.reward);
            const newBalance = currentBalance + reward;
            localStorage.setItem('taskRewardBalance', newBalance.toString());
            
            // Update total earnings (100 points = ₹20)
            const currentEarnings = parseFloat(localStorage.getItem('taskRewardEarnings') || '0');
            const earningsInRupees = (reward / 100) * 20;
            const newEarnings = currentEarnings + earningsInRupees;
            localStorage.setItem('taskRewardEarnings', newEarnings.toFixed(2));
            
            // Update tasks completed count
            const tasksCompleted = parseInt(localStorage.getItem('taskRewardTasksCompleted') || '0');
            localStorage.setItem('taskRewardTasksCompleted', (tasksCompleted + 1).toString());
            
            // Close modal
            document.getElementById('taskCompletionModal').classList.remove('active');
            
            // Show success toast
            showToast(`Task completed! You earned ${reward} points (₹${earningsInRupees.toFixed(2)})`, 'success');
            
            // Reload data
            setTimeout(() => {
                loadUserData();
                loadDashboardTasks();
                loadAllTasks();
            }, 500);
        }
        
        function updateWithdrawalCalculation() {
            const amountInput = document.getElementById('withdrawAmount');
            const points = parseInt(amountInput.value) || 0;
            const minPoints = 825; // ₹165 minimum
            
            // Hide/show error
            if (points < minPoints) {
                document.getElementById('withdrawalCalculation').style.display = 'none';
                if (points > 0) {
                    showError('withdrawAmountError', `Minimum ${minPoints} points required (₹165)`);
                } else {
                    hideError('withdrawAmountError');
                }
                return;
            } else {
                hideError('withdrawAmountError');
                document.getElementById('withdrawalCalculation').style.display = 'block';
            }
            
            // Calculate amounts (100 points = ₹20)
            const totalRupees = (points / 100) * 20;
            const userAmount = totalRupees - 15; // ₹15 team commission
            const finalAmount = Math.max(0, userAmount); // User gets ₹150 for ₹165 withdrawal
            
            // Update calculation display
            document.getElementById('calcPoints').textContent = `${points.toLocaleString()} points`;
            document.getElementById('calcUserAmount').textContent = `₹${totalRupees.toFixed(2)}`;
            document.getElementById('calcFinalAmount').textContent = `₹${finalAmount.toFixed(2)}`;
        }
        
        function loadWithdrawalHistory() {
            const historyContainer = document.getElementById('withdrawalHistory');
            const history = getWithdrawalHistory();
            
            historyContainer.innerHTML = '';
            
            if (history.length === 0) {
                historyContainer.innerHTML = `
                    <div style="text-align: center; padding: 40px 20px; color: var(--gray);">
                        <i class="fas fa-history" style="font-size: 2rem; margin-bottom: 15px; opacity: 0.5;"></i>
                        <p>No withdrawal history yet</p>
                    </div>
                `;
                return;
            }
            
            history.forEach(item => {
                const historyElement = document.createElement('div');
                historyElement.className = 'history-item';
                
                historyElement.innerHTML = `
                    <div class="history-details">
                        <h4>${item.method} - ${item.id}</h4>
                        <div class="history-date">${item.date}</div>
                    </div>
                    <div style="text-align: right;">
                        <div class="history-amount">${item.amount} points</div>
                        <div class="history-status status-${item.status}">${item.status}</div>
                    </div>
                `;
                
                historyContainer.appendChild(historyElement);
            });
        }
        
        function submitWithdrawal() {
            const selectedMethod = document.querySelector('.method-card.selected');
            const amountInput = document.getElementById('withdrawAmount');
            const points = parseInt(amountInput.value) || 0;
            const minPoints = 825; // ₹165 minimum
            
            // Validation
            if (!selectedMethod) {
                showToast('Please select a withdrawal method', 'error');
                return;
            }
            
            if (points < minPoints) {
                showError('withdrawAmountError', `Minimum ${minPoints} points required (₹165)`);
                return;
            }
            
            const currentBalance = parseInt(localStorage.getItem('taskRewardBalance') || '0');
            
            if (points > currentBalance) {
                showError('withdrawAmountError', 'Insufficient balance');
                return;
            }
            
            const method = selectedMethod.getAttribute('data-method');
            
            // Validate method-specific details
            if (method === 'upi') {
                const upiId = document.getElementById('upiId').value.trim();
                if (!upiId || !upiId.includes('@')) {
                    showError('upiIdError', 'Please enter a valid UPI ID');
                    return;
                }
                hideError('upiIdError');
            } else if (method === 'bank') {
                const accountNumber = document.getElementById('accountNumber').value.trim();
                const ifscCode = document.getElementById('ifscCode').value.trim();
                const accountHolder = document.getElementById('accountHolder').value.trim();
                
                if (!accountNumber || accountNumber.length < 9) {
                    showError('accountNumberError', 'Please enter a valid account number');
                    return;
                }
                if (!ifscCode || ifscCode.length !== 11) {
                    showError('ifscCodeError', 'Please enter a valid IFSC code');
                    return;
                }
                if (!accountHolder || accountHolder.length < 3) {
                    showError('accountHolderError', 'Please enter account holder name');
                    return;
                }
                
                hideError('accountNumberError');
                hideError('ifscCodeError');
                hideError('accountHolderError');
            }
            
            // Simulate withdrawal request
            const withdrawalId = 'WD-' + Date.now().toString().slice(-8);
            
            // Update balance
            const newBalance = currentBalance - points;
            localStorage.setItem('taskRewardBalance', newBalance.toString());
            
            // Save withdrawal to history
            const withdrawalHistory = JSON.parse(localStorage.getItem('withdrawalHistory') || '[]');
            withdrawalHistory.unshift({
                id: withdrawalId,
                method: method === 'upi' ? 'UPI Transfer' : 'Bank Transfer',
                amount: points,
                date: new Date().toLocaleDateString('en-IN', { day: 'numeric', month: 'short', year: 'numeric' }),
                status: 'pending'
            });
            
            localStorage.setItem('withdrawalHistory', JSON.stringify(withdrawalHistory));
            
            // Calculate amounts for message
            const totalRupees = (points / 100) * 20;
            const userAmount = totalRupees - 15;
            
            // Show success message
            showToast(`Withdrawal request submitted for ${points} points. You will receive ₹${userAmount.toFixed(2)} after ₹15 team commission.`, 'success');
            
            // Reset form
            amountInput.value = '';
            document.querySelectorAll('.method-card').forEach(c => c.classList.remove('selected'));
            document.getElementById('upiDetails').style.display = 'none';
            document.getElementById('bankDetails').style.display = 'none';
            document.getElementById('withdrawalCalculation').style.display = 'none';
            
            // Clear form fields
            document.getElementById('upiId').value = '';
            document.getElementById('accountNumber').value = '';
            document.getElementById('ifscCode').value = '';
            document.getElementById('accountHolder').value = '';
            
            // Reload data
            setTimeout(() => {
                loadUserData();
                loadWithdrawalHistory();
            }, 500);
        }
        
        // Refer & Earn Functions
        function copyReferralCode() {
            const referralCode = document.getElementById('referralCode').textContent;
            navigator.clipboard.writeText(referralCode)
                .then(() => {
                    showToast('Referral code copied to clipboard!', 'success');
                })
                .catch(err => {
                    showToast('Failed to copy code', 'error');
                });
        }
        
        function copyReferralLink() {
            const referralLink = document.getElementById('referralLink').textContent;
            navigator.clipboard.writeText(referralLink)
                .then(() => {
                    showToast('Referral link copied to clipboard!', 'success');
                })
                .catch(err => {
                    showToast('Failed to copy link', 'error');
                });
        }
        
        function shareReferral(platform) {
            const referralCode = localStorage.getItem('taskRewardReferralCode') || 'TR-REF-00000';
            const referralLink = `https://taskreward.app/ref/${referralCode}`;
            const message = `Join TaskReward using my referral code ${referralCode} and earn ₹165 bonus on your first withdrawal! ${referralLink}`;
            
            let shareUrl = '';
            
            switch(platform) {
                case 'whatsapp':
                    shareUrl = `https://wa.me/?text=${encodeURIComponent(message)}`;
                    break;
                case 'facebook':
                    shareUrl = `https://www.facebook.com/sharer/sharer.php?u=${encodeURIComponent(referralLink)}&quote=${encodeURIComponent(message)}`;
                    break;
                case 'twitter':
                    shareUrl = `https://twitter.com/intent/tweet?text=${encodeURIComponent(message)}`;
                    break;
                case 'instagram':
                    // Instagram doesn't have direct sharing URL
                    showToast('Copy your referral code and share it on Instagram', 'info');
                    copyReferralCode();
                    return;
                case 'telegram':
                    shareUrl = `https://t.me/share/url?url=${encodeURIComponent(referralLink)}&text=${encodeURIComponent(message)}`;
                    break;
                case 'more':
                    // Native Web Share API
                    if (navigator.share) {
                        navigator.share({
                            title: 'Join TaskReward',
                            text: message,
                            url: referralLink
                        })
                        .then(() => console.log('Shared successfully'))
                        .catch(error => console.log('Error sharing:', error));
                    } else {
                        // Fallback to copying
                        copyReferralLink();
                        showToast('Referral link copied to clipboard. Share it anywhere!', 'success');
                    }
                    return;
                default:
                    return;
            }
            
            // Open share URL in new window
            window.open(shareUrl, '_blank', 'width=600,height=400');
            
            // Show success message
            showToast(`Sharing via ${platform}...`, 'success');
        }
        
        function editProfile() {
            showToast('Edit profile feature will be available soon', 'info');
        }
        
        function changePassword() {
            showToast('Change password feature will be available soon', 'info');
        }
        
        function logout() {
            // Clear login state
            localStorage.removeItem('taskRewardLoggedIn');
            
            // Show auth screen
            showAuthScreen();
            
            // Reset auth forms
            switchAuthTab('login');
            document.getElementById('loginForm').reset();
            document.getElementById('signupForm').reset();
            
            // Clear errors
            document.querySelectorAll('.error-message').forEach(el => el.classList.remove('show'));
            document.querySelectorAll('.form-input').forEach(el => el.classList.remove('error'));
            
            showToast('Logged out successfully', 'success');
        }
        
        function showToast(message, type = 'success') {
            const toast = document.getElementById('toast');
            const toastIcon = document.getElementById('toastIcon');
            const toastMessage = document.getElementById('toastMessage');
            
            // Set icon based on type
            if (type === 'success') {
                toastIcon.className = 'fas fa-check-circle';
                toast.className = 'toast success';
            } else if (type === 'error') {
                toastIcon.className = 'fas fa-exclamation-circle';
                toast.className = 'toast error';
            } else if (type === 'warning') {
                toastIcon.className = 'fas fa-exclamation-triangle';
                toast.className = 'toast warning';
            } else {
                toastIcon.className = 'fas fa-info-circle';
                toast.className = 'toast';
            }
            
            toastMessage.textContent = message;
            toast.classList.add('show');
            
            // Hide toast after 3 seconds
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }
        
        // Sample data functions
        function getSampleTasks() {
            return [
                {
                    id: 1,
                    title: 'Watch a 30-second ad',
                    description: 'Watch a short advertisement video to earn points.',
                    reward: '50',
                    requiresProof: false
                },
                {
                    id: 2,
                    title: 'Complete a survey',
                    description: 'Answer a quick survey about your preferences.',
                    reward: '100',
                    requiresProof: false,
                    instructions: 'Answer all questions honestly. The survey will take approximately 2-3 minutes.'
                },
                {
                    id: 3,
                    title: 'Install & open an app',
                    description: 'Install a recommended app and open it at least once.',
                    reward: '200',
                    requiresProof: true,
                    instructions: 'Install the app from the provided link, open it, and provide a screenshot as proof.'
                },
                {
                    id: 4,
                    title: 'Refer a friend',
                    description: 'Refer a friend who signs up using your referral code.',
                    reward: '500',
                    requiresProof: true,
                    instructions: 'Share your referral code with a friend. When they sign up using your code, you earn 125 coins!'
                },
                {
                    id: 5,
                    title: 'Daily check-in',
                    description: 'Check in to the app every day to earn bonus points.',
                    reward: '25',
                    requiresProof: false
                },
                {
                    id: 6,
                    title: 'Social media share',
                    description: 'Share our app on your social media profile.',
                    reward: '75',
                    requiresProof: true,
                    instructions: 'Share our app on Facebook, Instagram, or Twitter and provide the post link as proof.'
                }
            ];
        }
        
        function getWithdrawalHistory() {
            // Try to get from localStorage
            const savedHistory = localStorage.getItem('withdrawalHistory');
            if (savedHistory) {
                return JSON.parse(savedHistory);
            }
            
            // Return empty array for new users
            return [];
        }
    </script>
</body><script src="https://pl28008424.effectivegatecpm.com/6c/81/d3/6c81d30875ee68ddd9c6cd4aba888725.js"></script>
</html>
<body><script>
  atOptions = {
    'key' : '2a35f446cae89890bbe0d91ea3aec6b5',
    'format' : 'iframe',
    'height' : 300,
    'width' : 160,
    'params' : {}
  };
</script>
<script src="https://www.highperformanceformat.com/2a35f446cae89890bbe0d91ea3aec6b5/invoke.js"></script></body>
    
<body><script>
  atOptions = {
    'key' : '89c3bb8b234d16552af7d434079f4d62',
    'format' : 'iframe',
    'height' : 50,
    'width' : 320,
    'params' : {}
  };
</script>
<script src="https://www.highperformanceformat.com/89c3bb8b234d16552af7d434079f4d62/invoke.js"></script></body>
