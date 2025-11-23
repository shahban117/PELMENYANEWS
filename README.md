<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Новости Пельмении - Система сообщений и почты</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --accent: #e74c3c;
            --light: #ecf0f1;
            --dark: #2c3e50;
            --success: #2ecc71;
            --warning: #f39c12;
            --chat-bg: #f0f2f5;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        /* Header */
        header {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            padding: 20px 0;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo i {
            font-size: 2.5rem;
            color: var(--accent);
        }
        
        .logo h1 {
            font-size: 1.8rem;
        }
        
        .logo span {
            color: var(--accent);
        }
        
        .user-menu {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--accent);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
        }
        
        .notification-badge {
            position: absolute;
            top: -5px;
            right: -5px;
            background: var(--accent);
            color: white;
            border-radius: 50%;
            width: 18px;
            height: 18px;
            font-size: 0.7rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        nav ul {
            display: flex;
            list-style: none;
            gap: 25px;
        }
        
        nav a {
            color: white;
            text-decoration: none;
            font-weight: 500;
            transition: all 0.3s ease;
            padding: 5px 10px;
            border-radius: 4px;
        }
        
        nav a:hover {
            background-color: rgba(255, 255, 255, 0.1);
        }
        
        /* Hero Section */
        .hero {
            background: linear-gradient(rgba(44, 62, 80, 0.8), rgba(44, 62, 80, 0.9)), url('https://images.unsplash.com/photo-1504711434969-e33886168f5c?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80');
            background-size: cover;
            background-position: center;
            color: white;
            padding: 80px 0;
            text-align: center;
            margin-bottom: 40px;
        }
        
        .hero h2 {
            font-size: 2.5rem;
            margin-bottom: 20px;
        }
        
        .hero p {
            font-size: 1.2rem;
            max-width: 700px;
            margin: 0 auto 30px;
        }
        
        .btn {
            display: inline-block;
            background-color: var(--accent);
            color: white;
            padding: 12px 30px;
            border-radius: 50px;
            text-decoration: none;
            font-weight: 600;
            transition: all 0.3s ease;
            border: none;
            cursor: pointer;
            font-size: 1rem;
        }
        
        .btn:hover {
            background-color: #c0392b;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .btn-secondary {
            background-color: var(--secondary);
        }
        
        .btn-secondary:hover {
            background-color: #2980b9;
        }
        
        .btn-success {
            background-color: var(--success);
        }
        
        .btn-success:hover {
            background-color: #27ae60;
        }
        
        /* Messaging System */
        .messaging-system {
            background: white;
            border-radius: 10px;
            padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            margin-bottom: 40px;
            display: none;
        }
        
        .messaging-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        
        .messaging-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .messaging-tab {
            padding: 10px 20px;
            background: var(--light);
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .messaging-tab.active {
            background: var(--secondary);
            color: white;
        }
        
        .messaging-content {
            display: grid;
            grid-template-columns: 300px 1fr;
            gap: 20px;
            height: 500px;
        }
        
        .conversations-list {
            border-right: 1px solid #eee;
            padding-right: 20px;
            overflow-y: auto;
        }
        
        .conversation-item {
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 1px solid #eee;
        }
        
        .conversation-item:hover {
            background: var(--light);
        }
        
        .conversation-item.active {
            background: var(--secondary);
            color: white;
        }
        
        .conversation-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 5px;
        }
        
        .conversation-preview {
            color: #666;
            font-size: 0.9rem;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        
        .conversation-item.active .conversation-preview {
            color: rgba(255, 255, 255, 0.8);
        }
        
        .chat-area {
            display: flex;
            flex-direction: column;
        }
        
        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 15px;
            background: var(--chat-bg);
            border-radius: 8px;
            margin-bottom: 15px;
        }
        
        .message {
            margin-bottom: 15px;
            display: flex;
            flex-direction: column;
            max-width: 80%;
        }
        
        .message-sender {
            font-weight: 600;
            font-size: 0.85rem;
            margin-bottom: 5px;
            color: var(--primary);
        }
        
        .message-content {
            background: white;
            padding: 10px 15px;
            border-radius: 18px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        
        .message-time {
            font-size: 0.7rem;
            color: #888;
            margin-top: 5px;
            align-self: flex-end;
        }
        
        .message.own {
            align-self: flex-end;
            align-items: flex-end;
        }
        
        .message.own .message-content {
            background: var(--secondary);
            color: white;
        }
        
        .chat-input {
            display: flex;
            gap: 10px;
        }
        
        .chat-input input {
            flex: 1;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 25px;
            outline: none;
        }
        
        .send-btn {
            background: var(--secondary);
            color: white;
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        /* Email System */
        .email-system {
            background: white;
            border-radius: 10px;
            padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            margin-bottom: 40px;
            display: none;
        }
        
        .email-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        
        .email-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .email-content {
            display: grid;
            grid-template-columns: 250px 1fr;
            gap: 20px;
            height: 500px;
        }
        
        .email-folders {
            border-right: 1px solid #eee;
            padding-right: 20px;
        }
        
        .email-folder {
            padding: 12px 15px;
            border-radius: 5px;
            margin-bottom: 5px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .email-folder:hover {
            background: var(--light);
        }
        
        .email-folder.active {
            background: var(--secondary);
            color: white;
        }
        
        .email-count {
            margin-left: auto;
            background: var(--accent);
            color: white;
            border-radius: 10px;
            padding: 2px 8px;
            font-size: 0.8rem;
        }
        
        .email-folder.active .email-count {
            background: white;
            color: var(--secondary);
        }
        
        .email-list {
            overflow-y: auto;
            border-right: 1px solid #eee;
            padding-right: 20px;
        }
        
        .email-item {
            padding: 15px;
            border-bottom: 1px solid #eee;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .email-item:hover {
            background: var(--light);
        }
        
        .email-item.unread {
            background: #e8f4fd;
            font-weight: 600;
        }
        
        .email-sender {
            font-weight: 600;
            margin-bottom: 5px;
        }
        
        .email-subject {
            margin-bottom: 5px;
        }
        
        .email-preview {
            color: #666;
            font-size: 0.9rem;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        
        .email-view {
            padding-left: 20px;
            overflow-y: auto;
        }
        
        .email-view-header {
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
            margin-bottom: 15px;
        }
        
        .compose-email {
            background: var(--light);
            padding: 20px;
            border-radius: 8px;
        }
        
        .compose-form .form-group {
            margin-bottom: 15px;
        }
        
        .compose-form label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }
        
        .form-control {
            width: 100%;
            padding: 10px 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }
        
        /* News Generator */
        .news-generator {
            background-color: white;
            border-radius: 10px;
            padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            margin-bottom: 40px;
        }
        
        .news-generator h2 {
            color: var(--primary);
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .generator-form {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark);
        }
        
        .full-width {
            grid-column: 1 / -1;
        }
        
        .news-preview {
            background-color: var(--light);
            border-radius: 8px;
            padding: 20px;
            margin-top: 20px;
            display: none;
        }
        
        .news-preview h3 {
            color: var(--primary);
            margin-bottom: 15px;
        }
        
        /* News Filters */
        .news-filters {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            margin-bottom: 30px;
        }
        
        .filters-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .filters-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
        }
        
        .filter-group {
            margin-bottom: 15px;
        }
        
        .filter-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark);
        }
        
        .filter-actions {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }
        
        .filter-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 15px;
        }
        
        .filter-tag {
            background-color: var(--secondary);
            color: white;
            padding: 5px 10px;
            border-radius: 15px;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .filter-tag i {
            cursor: pointer;
        }
        
        /* News Grid */
        .section-title {
            color: var(--primary);
            margin-bottom: 30px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--secondary);
            display: inline-block;
        }
        
        .news-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 30px;
            margin-bottom: 50px;
        }
        
        .news-card {
            background-color: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .news-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
        }
        
        .news-image {
            height: 200px;
            background-size: cover;
            background-position: center;
        }
        
        .news-content {
            padding: 20px;
        }
        
        .news-category {
            display: inline-block;
            background-color: var(--secondary);
            color: white;
            padding: 5px 10px;
            border-radius: 4px;
            font-size: 0.8rem;
            margin-bottom: 10px;
        }
        
        .news-title {
            font-size: 1.2rem;
            margin-bottom: 10px;
            color: var(--dark);
        }
        
        .news-excerpt {
            color: #666;
            margin-bottom: 15px;
            font-size: 0.95rem;
        }
        
        .news-meta {
            display: flex;
            justify-content: space-between;
            color: #888;
            font-size: 0.85rem;
        }
        
        .news-actions {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }
        
        .action-btn {
            background: none;
            border: none;
            color: #7f8c8d;
            cursor: pointer;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 5px;
            transition: all 0.3s ease;
        }
        
        .action-btn:hover {
            color: var(--secondary);
        }
        
        .news-stats {
            display: flex;
            gap: 15px;
            margin-top: 10px;
            font-size: 0.85rem;
            color: #7f8c8d;
        }
        
        /* News Modal */
        .news-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1000;
            overflow-y: auto;
            padding: 20px;
        }
        
        .modal-content {
            background-color: white;
            max-width: 800px;
            margin: 40px auto;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            animation: modalFadeIn 0.3s ease;
        }
        
        @keyframes modalFadeIn {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .modal-header {
            padding: 20px 30px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .modal-close {
            background: none;
            border: none;
            color: white;
            font-size: 1.5rem;
            cursor: pointer;
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            transition: all 0.3s ease;
        }
        
        .modal-close:hover {
            background-color: rgba(255, 255, 255, 0.2);
        }
        
        .modal-body {
            padding: 30px;
            max-height: 70vh;
            overflow-y: auto;
        }
        
        .modal-image {
            width: 100%;
            height: 400px;
            background-size: cover;
            background-position: center;
            border-radius: 8px;
            margin-bottom: 20px;
        }
        
        .modal-meta {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        
        .modal-author {
            font-weight: 600;
            color: var(--primary);
        }
        
        .modal-date {
            color: #7f8c8d;
        }
        
        .modal-text {
            line-height: 1.8;
            font-size: 1.1rem;
            margin-bottom: 30px;
        }
        
        .modal-stats {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
            padding: 15px;
            background-color: var(--light);
            border-radius: 8px;
        }
        
        .modal-actions {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }
        
        /* Footer */
        footer {
            background-color: var(--primary);
            color: white;
            padding: 40px 0 20px;
        }
        
        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
            margin-bottom: 30px;
        }
        
        .footer-section h3 {
            margin-bottom: 20px;
            color: var(--accent);
        }
        
        .footer-section p {
            margin-bottom: 15px;
        }
        
        .social-links {
            display: flex;
            gap: 15px;
        }
        
        .social-links a {
            color: white;
            font-size: 1.2rem;
            transition: all 0.3s ease;
        }
        
        .social-links a:hover {
            color: var(--accent);
        }
        
        .copyright {
            text-align: center;
            padding-top: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.9rem;
            color: #ccc;
        }
        
        /* Utility Classes */
        .hidden {
            display: none;
        }
        
        .notification-icon {
            position: relative;
            cursor: pointer;
        }
        
        @media (max-width: 768px) {
            .header-content {
                flex-direction: column;
                gap: 20px;
            }
            
            nav ul {
                gap: 15px;
            }
            
            .generator-form {
                grid-template-columns: 1fr;
            }
            
            .hero h2 {
                font-size: 2rem;
            }
            
            .messaging-content, .email-content {
                grid-template-columns: 1fr;
            }
            
            .conversations-list, .email-folders, .email-list {
                border-right: none;
                border-bottom: 1px solid #eee;
                padding-right: 0;
                padding-bottom: 20px;
                max-height: 200px;
            }
            
            .filters-content {
                grid-template-columns: 1fr;
            }
            
            .modal-content {
                margin: 20px auto;
            }
            
            .modal-body {
                padding: 20px;
            }
            
            .modal-image {
                height: 200px;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo">
                    <i class="fas fa-newspaper"></i>
                    <h1>Новости <span>Пельмении</span></h1>
                </div>
                <nav>
                    <ul>
                        <li><a href="#" class="nav-main"><i class="fas fa-home"></i> Главная</a></li>
                        <li><a href="#" class="nav-messages"><i class="fas fa-comments"></i> Сообщения <span class="notification-badge">3</span></a></li>
                        <li><a href="#" class="nav-email"><i class="fas fa-envelope"></i> Почта <span class="notification-badge">5</span></a></li>
                        <li><a href="#generator" class="nav-generator"><i class="fas fa-robot"></i> Генератор новостей</a></li>
                    </ul>
                </nav>
                <div class="user-menu">
                    <div class="user-avatar">ИИ</div>
                    <span>Иван Иванов</span>
                </div>
            </div>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <div class="container">
            <h2>Добро пожаловать в Пельмению!</h2>
            <p>Самая актуальная информация о событиях в нашей стране. Общайтесь с другими пользователями через систему сообщений и почты!</p>
            <button class="btn nav-messages"><i class="fas fa-comments"></i> Написать сообщение</button>
        </div>
    </section>

    <!-- Main Content -->
    <div class="container">
        <!-- Messaging System -->
        <section class="messaging-system" id="messaging-system">
            <div class="messaging-header">
                <h2><i class="fas fa-comments"></i> Система сообщений</h2>
                <button class="btn btn-success" id="new-conversation"><i class="fas fa-plus"></i> Новый чат</button>
            </div>
            
            <div class="messaging-tabs">
                <button class="messaging-tab active" data-tab="chats">Чаты</button>
                <button class="messaging-tab" data-tab="contacts">Контакты</button>
            </div>
            
            <div class="messaging-content">
                <div class="conversations-list" id="conversations-list">
                    <!-- Список чатов будет здесь -->
                </div>
                
                <div class="chat-area">
                    <div class="chat-messages" id="chat-messages">
                        <!-- Сообщения будут здесь -->
                    </div>
                    <div class="chat-input">
                        <input type="text" id="message-input" placeholder="Введите ваше сообщение...">
                        <button class="send-btn" id="send-message">
                            <i class="fas fa-paper-plane"></i>
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- Email System -->
        <section class="email-system" id="email-system">
            <div class="email-header">
                <h2><i class="fas fa-envelope"></i> Система почты</h2>
                <button class="btn btn-success" id="compose-email"><i class="fas fa-edit"></i> Написать письмо</button>
            </div>
            
            <div class="email-tabs">
                <button class="messaging-tab active" data-tab="inbox">Входящие</button>
                <button class="messaging-tab" data-tab="sent">Отправленные</button>
                <button class="messaging-tab" data-tab="drafts">Черновики</button>
            </div>
            
            <div class="email-content">
                <div class="email-folders">
                    <div class="email-folder active" data-folder="inbox">
                        <i class="fas fa-inbox"></i> Входящие
                        <span class="email-count">5</span>
                    </div>
                    <div class="email-folder" data-folder="sent">
                        <i class="fas fa-paper-plane"></i> Отправленные
                    </div>
                    <div class="email-folder" data-folder="drafts">
                        <i class="fas fa-file"></i> Черновики
                        <span class="email-count">2</span>
                    </div>
                    <div class="email-folder" data-folder="spam">
                        <i class="fas fa-exclamation-circle"></i> Спам
                    </div>
                    <div class="email-folder" data-folder="trash">
                        <i class="fas fa-trash"></i> Корзина
                    </div>
                </div>
                
                <div class="email-list" id="email-list">
                    <!-- Список писем будет здесь -->
                </div>
                
                <div class="email-view" id="email-view">
                    <!-- Просмотр письма или создание нового -->
                </div>
            </div>
        </section>

        <!-- News Generator -->
        <section class="news-generator" id="generator">
            <h2><i class="fas fa-magic"></i> Генератор новостей ИИ</h2>
            <p>Создайте свою собственную новость о Пельмении с помощью искусственного интеллекта. Просто заполните форму ниже!</p>
            
            <div class="generator-form">
                <div class="form-group">
                    <label for="news-category">Категория новости</label>
                    <select id="news-category" class="form-control">
                        <option value="politics">Политика</option>
                        <option value="economy">Экономика</option>
                        <option value="culture">Культура</option>
                        <option value="sports">Спорт</option>
                        <option value="technology">Технологии</option>
                        <option value="health">Здоровье</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="news-tone">Тон новости</label>
                    <select id="news-tone" class="form-control">
                        <option value="neutral">Нейтральный</option>
                        <option value="positive">Позитивный</option>
                        <option value="negative">Негативный</option>
                        <option value="humorous">Юмористический</option>
                    </select>
                </div>
                
                <div class="form-group full-width">
                    <label for="news-topic">Тема новости</label>
                    <input type="text" id="news-topic" class="form-control" placeholder="Например: открытие нового музея, изменения в налоговом кодексе...">
                </div>
                
                <div class="form-group full-width">
                    <label for="news-details">Дополнительные детали (необязательно)</label>
                    <textarea id="news-details" class="form-control" rows="3" placeholder="Любая дополнительная информация, которую вы хотите включить в новость..."></textarea>
                </div>
            </div>
            
            <button id="generate-news" class="btn"><i class="fas fa-bolt"></i> Сгенерировать новость</button>
            
            <div class="news-preview" id="news-preview">
                <h3>Ваша сгенерированная новость:</h3>
                <div id="preview-content">
                    <!-- Сгенерированная новость появится здесь -->
                </div>
            </div>
        </section>

        <!-- News Filters -->
        <section class="news-filters" id="news-filters">
            <div class="filters-header">
                <h2><i class="fas fa-filter"></i> Фильтры новостей</h2>
                <button class="btn btn-secondary" id="reset-filters"><i class="fas fa-redo"></i> Сбросить</button>
            </div>
            
            <div class="filters-content">
                <div class="filter-group">
                    <label for="category-filter">Категория</label>
                    <select id="category-filter" class="form-control">
                        <option value="all">Все категории</option>
                        <option value="politics">Политика</option>
                        <option value="economy">Экономика</option>
                        <option value="culture">Культура</option>
                        <option value="sports">Спорт</option>
                        <option value="technology">Технологии</option>
                        <option value="health">Здоровье</option>
                    </select>
                </div>
                
                <div class="filter-group">
                    <label for="date-filter">Дата публикации</label>
                    <select id="date-filter" class="form-control">
                        <option value="all">За все время</option>
                        <option value="today">Сегодня</option>
                        <option value="week">За неделю</option>
                        <option value="month">За месяц</option>
                    </select>
                </div>
                
                <div class="filter-group">
                    <label for="sort-filter">Сортировка</label>
                    <select id="sort-filter" class="form-control">
                        <option value="newest">Сначала новые</option>
                        <option value="oldest">Сначала старые</option>
                        <option value="popular">По популярности</option>
                    </select>
                </div>
                
                <div class="filter-group">
                    <label for="search-filter">Поиск по ключевым словам</label>
                    <input type="text" id="search-filter" class="form-control" placeholder="Введите ключевые слова...">
                </div>
            </div>
            
            <div class="filter-actions">
                <button class="btn" id="apply-filters"><i class="fas fa-check"></i> Применить фильтры</button>
                <button class="btn btn-secondary" id="toggle-advanced">Расширенные фильтры</button>
            </div>
            
            <div class="filter-tags" id="filter-tags">
                <!-- Активные фильтры будут отображаться здесь -->
            </div>
            
            <div class="advanced-filters hidden" id="advanced-filters">
                <div class="filters-content">
                    <div class="filter-group">
                        <label for="author-filter">Автор</label>
                        <select id="author-filter" class="form-control">
                            <option value="all">Все авторы</option>
                            <option value="ivan">Иван Иванов</option>
                            <option value="maria">Мария Петрова</option>
                            <option value="alex">Алексей Смирнов</option>
                        </select>
                    </div>
                    
                    <div class="filter-group">
                        <label for="rating-filter">Минимальный рейтинг</label>
                        <select id="rating-filter" class="form-control">
                            <option value="0">Любой рейтинг</option>
                            <option value="3">3+ звезды</option>
                            <option value="4">4+ звезды</option>
                            <option value="5">5 звезд</option>
                        </select>
                    </div>
                    
                    <div class="filter-group">
                        <label>
                            <input type="checkbox" id="featured-filter">
                            Только избранные новости
                        </label>
                    </div>
                </div>
            </div>
        </section>

        <!-- Latest News -->
        <h2 class="section-title">Последние новости Пельмении</h2>
        <div class="news-grid" id="news-container">
            <!-- Новости будут загружаться здесь -->
        </div>
    </div>

    <!-- News Modal -->
    <div class="news-modal" id="news-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="modal-title">Заголовок новости</h2>
                <button class="modal-close" id="modal-close">&times;</button>
            </div>
            <div class="modal-body">
                <div class="modal-image" id="modal-image"></div>
                <div class="modal-meta">
                    <div class="modal-author" id="modal-author">Автор</div>
                    <div class="modal-date" id="modal-date">Дата</div>
                </div>
                <div class="modal-text" id="modal-text">
                    Полный текст новости будет здесь...
                </div>
                <div class="modal-stats">
                    <div><i class="fas fa-heart"></i> <span id="modal-likes">0</span> лайков</div>
                    <div><i class="fas fa-comment"></i> <span id="modal-comments">0</span> комментариев</div>
                    <div><i class="fas fa-star"></i> <span id="modal-rating">0</span> рейтинг</div>
                </div>
                <div class="modal-actions">
                    <button class="btn" id="modal-like"><i class="fas fa-heart"></i> Нравится</button>
                    <button class="btn btn-secondary" id="modal-share"><i class="fas fa-share"></i> Поделиться</button>
                    <button class="btn btn-secondary" id="modal-save"><i class="fas fa-bookmark"></i> Сохранить</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-section">
                    <h3>О нас</h3>
                    <p>Новости Пельмении - ведущее новостное издание вымышленной страны Пельмении. Мы предоставляем самую актуальную информацию о событиях в нашей стране.</p>
                    <p>Теперь с системой сообщений и почты для общения между пользователями!</p>
                </div>
                
                <div class="footer-section">
                    <h3>Категории</h3>
                    <p>Политика</p>
                    <p>Экономика</p>
                    <p>Культура</p>
                    <p>Спорт</p>
                    <p>Технологии</p>
                </div>
                
                <div class="footer-section">
                    <h3>Контакты</h3>
                    <p><i class="fas fa-map-marker-alt"></i> Столица Пельмении, ул. Центральная, 1</p>
                    <p><i class="fas fa-phone"></i> +7 (800) 123-45-67</p>
                    <p><i class="fas fa-envelope"></i> info@pelmenia-news.pm</p>
                    <div class="social-links">
                        <a href="#"><i class="fab fa-vk"></i></a>
                        <a href="#"><i class="fab fa-telegram"></i></a>
                        <a href="#"><i class="fab fa-youtube"></i></a>
                        <a href="#"><i class="fab fa-instagram"></i></a>
                    </div>
                </div>
            </div>
            
            <div class="copyright">
                <p>&copy; 2023 Новости Пельмении. Все права защищены. Вымышленный проект.</p>
            </div>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Элементы навигации
            const navMain = document.querySelector('.nav-main');
            const navMessages = document.querySelector('.nav-messages');
            const navEmail = document.querySelector('.nav-email');
            const navGenerator = document.querySelector('.nav-generator');
            
            // Системы
            const messagingSystem = document.getElementById('messaging-system');
            const emailSystem = document.getElementById('email-system');
            const newsGenerator = document.getElementById('generator');
            const newsContainer = document.getElementById('news-container');
            const newsFilters = document.getElementById('news-filters');
            
            // Модальное окно новости
            const newsModal = document.getElementById('news-modal');
            const modalClose = document.getElementById('modal-close');
            
            // Данные пользователей (в реальном приложении это было бы на сервере)
            const users = [
                { id: 1, name: 'Мария Петрова', email: 'maria@example.com', avatar: 'МП', online: true },
                { id: 2, name: 'Алексей Смирнов', email: 'alex@example.com', avatar: 'АС', online: false },
                { id: 3, name: 'Елена Козлова', email: 'elena@example.com', avatar: 'ЕК', online: true },
                { id: 4, name: 'Дмитрий Иванов', email: 'dmitry@example.com', avatar: 'ДИ', online: true },
                { id: 5, name: 'Ольга Новикова', email: 'olga@example.com', avatar: 'ОН', online: false }
            ];
            
            // Текущий пользователь
            const currentUser = { id: 0, name: 'Иван Иванов', email: 'ivan@example.com', avatar: 'ИИ' };
            
            // Данные сообщений
            let conversations = JSON.parse(localStorage.getItem('pelmeniaConversations')) || [];
            
            // Данные почты
            let emails = JSON.parse(localStorage.getItem('pelmeniaEmails')) || [];
            
            // Данные новостей
            let allNews = JSON.parse(localStorage.getItem('pelmeniaNews')) || [];
            
            // Активные фильтры
            let activeFilters = {
                category: 'all',
                date: 'all',
                sort: 'newest',
                search: '',
                author: 'all',
                rating: 0,
                featured: false
            };
            
            // Полные тексты новостей
            const newsFullTexts = {
                1: `В столице Пельмении сегодня состоялось торжественное открытие крупнейшего в мире музея, посвященного пельменям. Новый культурный центр, расположенный в историческом здании бывшего вокзала, предлагает посетителям уникальное путешествие в мир национального блюда.

Экспозиция музея включает более 10 000 экспонатов, рассказывающих об истории пельменей от древних времен до наших дней. Особый интерес представляет коллекция старинных рецептов, некоторые из которых датируются XV веком.

"Это не просто музей, это настоящий культурный центр, где каждый может не только узнать интересные факты, но и принять участие в мастер-классах по лепке пельменей", - заявил на открытии министр культуры Пельмении.

В рамках открытия музея был организован фестиваль, на котором шеф-повара из разных регионов страны представили свои уникальные рецепты. Посетители смогли продегустировать более 50 видов пельменей с самыми разнообразными начинками.

Музей будет работать ежедневно, а по выходным здесь планируют проводить тематические мероприятия и кулинарные шоу.`,

                2: `Правительство Пельмении представило сегодня пакет экономических реформ, направленных на стимулирование малого бизнеса и привлечение иностранных инвестиций. Основные изменения коснутся налоговой системы и процедуры регистрации предприятий.

Согласно новому плану, налоговая нагрузка на малый бизнес будет снижена на 15%, а процесс открытия нового предприятия сократится с 30 до 5 рабочих дней. Также вводится программа льготного кредитования для стартапов в сфере технологий и сельского хозяйства.

"Мы создаем максимально комфортные условия для предпринимателей, чтобы Пельмения стала привлекательной для инвестиций страной", - заявил министр экономики на пресс-конференции.

Эксперты уже оценили потенциальный эффект от реформ. По прогнозам, в течение следующего года количество зарегистрированных малых предприятий может вырасти на 25%, а объем иностранных инвестиций - на 40%.

Реформы вступят в силу с начала следующего квартала после окончательного утверждения парламентом.`,

                3: `Сборная Пельмении по футболу одержала уверенную победу в товарищеском матче против команды соседней страны. Игра, проходившая на центральном стадионе столицы, завершилась со счетом 2:1 в пользу хозяев поля.

Первый гол был забит уже на 15-й минуте капитаном команды, который эффектным ударом отправил мяч в верхний угол ворот. Соперник сравнял счет перед самым перерывом, но во втором тайме пельменские футболисты смогли вырвать победу благодаря точному удару молодого нападающего.

"Я доволен игрой команды, особенно во втором тайме. Ребята показали характер и волю к победе", - прокомментировал игру главный тренер сборной.

Это уже третья победа подряд для пельменских футболистов в рамках подготовки к предстоящему чемпионату региона. Следующий товарищеский матч команда проведет через две недели против действующих чемпионов континента.

Болельщики, заполнившие трибуны стадиона, тепло приветствовали команду и выразили надежду на успешное выступление в официальных турнирах.`,

                4: `Ученые Пельмении совершили прорыв в кулинарной науке, разработав инновационный способ приготовления пельменей. Новая технология позволяет сохранить все полезные свойства начинки и значительно сокращает время приготовления.

Метод, получивший название "крио-заморозка с импульсным нагревом", основан на использовании сверхнизких температур для быстрой заморозки и специальных электромагнитных импульсов для равномерного прогрева.

"Наша технология позволяет сократить время приготовления пельменей в три раза, при этом сохраняя максимум витаминов и питательных веществ", - объяснил руководитель исследовательской группы.

Разработка уже引起了 интерес у крупных производителей пищевой продукции. Несколько компаний выразили готовность внедрить новую технологию на своих производствах.

Ученые уверены, что их изобретение не только улучшит качество готовой продукции, но и позволит существенно экономить энергию при промышленном производстве пельменей.`,

                5: `В столице Пельмении стартовал масштабный фестиваль уличного искусства, который превратит город в огромную галерею под открытым небом. Художники со всей страны уже начали работу над созданием граффити на стенах зданий в центральных районах города.

Организаторы фестиваля выделили 15 стен для художественного оформления. Темы работ варьируются от национальных символов Пельмении до абстрактных композиций, отражающих современные тенденции в искусстве.

"Мы хотим показать, что уличное искусство - это не вандализм, а полноценная форма художественного выражения", - заявил куратор фестиваля.

Помимо создания граффити, в программе фестиваля мастер-классы для начинающих художников, лекции об истории уличного искусства и конкурс на лучшую работу. Победитель получит грант на реализацию своего следующего проекта.

Фестиваль продлится до конца месяца, после чего все работы останутся на стенах как постоянные элементы городского пейзажа.`,

                6: `Министерство здравоохранения Пельмении опубликовало обновленные рекомендации по питанию, в которых особое внимание уделяется сбалансированному потреблению белков, жиров и углеводов. Новые нормы разработаны с учетом последних научных исследований в области диетологии.

Основные изменения касаются рекомендуемого количества овощей и фруктов - теперь их доля в рационе увеличена до 50%. Также специалисты советуют сократить потребление красного мяса и увеличить количество рыбы и морепродуктов.

"Сбалансированное питание - это основа здоровья нации. Мы постарались сделать рекомендации максимально практичными и доступными для каждого", - отметил главный диетолог министерства.

В новых рекомендациях также впервые учтены национальные особенности питания пельменцев, включая традиционное потребление пельменей. Специалисты разработали оптимальную частоту употребления этого блюда для поддержания здоровья.

Министерство планирует распространить памятки с новыми рекомендациями через поликлиники, школы и общественные центры по всей стране.`
            };
            
            // Инициализация данных, если их нет
            initializeData();
            
            // Навигация
            navMain.addEventListener('click', function(e) {
                e.preventDefault();
                showSection('main');
            });
            
            navMessages.addEventListener('click', function(e) {
                e.preventDefault();
                showSection('messages');
            });
            
            navEmail.addEventListener('click', function(e) {
                e.preventDefault();
                showSection('email');
            });
            
            navGenerator.addEventListener('click', function(e) {
                e.preventDefault();
                showSection('generator');
            });
            
            // Закрытие модального окна
            modalClose.addEventListener('click', function() {
                newsModal.style.display = 'none';
            });
            
            // Закрытие модального окна при клике вне его
            newsModal.addEventListener('click', function(e) {
                if (e.target === newsModal) {
                    newsModal.style.display = 'none';
                }
            });
            
            // Функция показа секции
            function showSection(section) {
                // Скрыть все системы
                messagingSystem.style.display = 'none';
                emailSystem.style.display = 'none';
                newsGenerator.style.display = 'none';
                newsContainer.style.display = 'none';
                newsFilters.style.display = 'none';
                
                // Показать выбранную систему
                if (section === 'messages') {
                    messagingSystem.style.display = 'block';
                    loadConversations();
                } else if (section === 'email') {
                    emailSystem.style.display = 'block';
                    loadEmailInbox();
                } else if (section === 'generator') {
                    newsGenerator.style.display = 'block';
                    newsContainer.style.display = 'grid';
                    newsFilters.style.display = 'block';
                } else {
                    // Главная страница - показать новости и фильтры
                    newsContainer.style.display = 'grid';
                    newsFilters.style.display = 'block';
                }
            }
            
            // Инициализация данных
            function initializeData() {
                // Если нет разговоров, создаем демо-данные
                if (conversations.length === 0) {
                    conversations = [
                        {
                            id: 1,
                            participants: [currentUser.id, 1],
                            messages: [
                                {
                                    id: 1,
                                    sender: 1,
                                    text: 'Привет! Видела твою новость про фестиваль пельменей, очень интересно!',
                                    timestamp: new Date(Date.now() - 3600000).toISOString()
                                },
                                {
                                    id: 2,
                                    sender: currentUser.id,
                                    text: 'Спасибо! Да, фестиваль получился отличный, много людей пришло.',
                                    timestamp: new Date(Date.now() - 3500000).toISOString()
                                },
                                {
                                    id: 3,
                                    sender: 1,
                                    text: 'Обязательно схожу в следующем году!',
                                    timestamp: new Date(Date.now() - 3400000).toISOString()
                                }
                            ],
                            lastMessage: 'Обязательно схожу в следующем году!',
                            lastMessageTime: new Date(Date.now() - 3400000).toISOString(),
                            unread: 0
                        },
                        {
                            id: 2,
                            participants: [currentUser.id, 2],
                            messages: [
                                {
                                    id: 1,
                                    sender: 2,
                                    text: 'Здравствуйте! Хотел обсудить вашу статью о новых технологиях.',
                                    timestamp: new Date(Date.now() - 86400000).toISOString()
                                },
                                {
                                    id: 2,
                                    sender: currentUser.id,
                                    text: 'Конечно, с удовольствием! Что именно вас заинтересовало?',
                                    timestamp: new Date(Date.now() - 86000000).toISOString()
                                }
                            ],
                            lastMessage: 'Конечно, с удовольствием! Что именно вас заинтересовало?',
                            lastMessageTime: new Date(Date.now() - 86000000).toISOString(),
                            unread: 1
                        }
                    ];
                    localStorage.setItem('pelmeniaConversations', JSON.stringify(conversations));
                }
                
                // Если нет писем, создаем демо-данные
                if (emails.length === 0) {
                    emails = [
                        {
                            id: 1,
                            from: { name: 'Администрация Пельмении', email: 'admin@pelmenia.pm' },
                            to: currentUser.email,
                            subject: 'Добро пожаловать в Пельмению!',
                            body: 'Уважаемый гражданин, добро пожаловать в нашу замечательную страну! Мы рады приветствовать вас на нашем портале новостей.',
                            timestamp: new Date(Date.now() - 172800000).toISOString(),
                            read: false,
                            folder: 'inbox'
                        },
                        {
                            id: 2,
                            from: { name: 'Мария Петрова', email: 'maria@example.com' },
                            to: currentUser.email,
                            subject: 'Обсуждение новости',
                            body: 'Привет! Мне очень понравилась твоя последняя новость о фестивале пельменей. Хотела бы предложить сотрудничество!',
                            timestamp: new Date(Date.now() - 86400000).toISOString(),
                            read: false,
                            folder: 'inbox'
                        },
                        {
                            id: 3,
                            from: { name: 'Редакция новостей', email: 'news@pelmenia.pm' },
                            to: currentUser.email,
                            subject: 'Ваша новость опубликована',
                            body: 'Поздравляем! Ваша новость "Открытие нового музея" была опубликована на главной странице.',
                            timestamp: new Date(Date.now() - 43200000).toISOString(),
                            read: true,
                            folder: 'inbox'
                        }
                    ];
                    localStorage.setItem('pelmeniaEmails', JSON.stringify(emails));
                }
                
                // Если нет новостей, создаем демо-данные
                if (allNews.length === 0) {
                    allNews = [
                        {
                            id: 1,
                            title: 'В Пельмении открылся крупнейший музей пельменей',
                            excerpt: 'Новый музей посвящен истории и культуре национального блюда Пельмении. Посетители могут узнать о различных видах пельменей и даже принять участие в мастер-классах.',
                            category: 'culture',
                            author: 'Иван Иванов',
                            date: new Date(Date.now() - 86400000).toISOString(),
                            image: 'https://images.unsplash.com/photo-1551183053-bf91a1d81141?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80',
                            likes: 42,
                            comments: 12,
                            rating: 4.5,
                            featured: true
                        },
                        {
                            id: 2,
                            title: 'Правительство Пельмении объявило о новых экономических реформах',
                            excerpt: 'Министр экономики представил план по стимулированию малого бизнеса и привлечению иностранных инвестиций в страну.',
                            category: 'economy',
                            author: 'Мария Петрова',
                            date: new Date(Date.now() - 172800000).toISOString(),
                            image: 'https://images.unsplash.com/photo-1580519542036-c47de6196ba5?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80',
                            likes: 28,
                            comments: 7,
                            rating: 4.2,
                            featured: false
                        },
                        {
                            id: 3,
                            title: 'Сборная Пельмении по футболу одержала победу в товарищеском матче',
                            excerpt: 'В напряженной игре со счетом 2:1 пельменские футболисты обыграли команду соседней страны. Главный тренер доволен результатом.',
                            category: 'sports',
                            author: 'Алексей Смирнов',
                            date: new Date(Date.now() - 259200000).toISOString(),
                            image: 'https://images.unsplash.com/photo-1574629810360-7efbbe195018?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80',
                            likes: 65,
                            comments: 23,
                            rating: 4.8,
                            featured: true
                        },
                        {
                            id: 4,
                            title: 'Ученые Пельмении разработали инновационный способ приготовления пельменей',
                            excerpt: 'Новая технология позволяет сохранить все полезные свойства начинки и значительно сокращает время приготовления.',
                            category: 'technology',
                            author: 'Иван Иванов',
                            date: new Date(Date.now() - 345600000).toISOString(),
                            image: 'https://images.unsplash.com/photo-1556911220-e15b29be8c8f?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80',
                            likes: 37,
                            comments: 9,
                            rating: 4.3,
                            featured: false
                        },
                        {
                            id: 5,
                            title: 'В столице Пельмении проходит фестиваль уличного искусства',
                            excerpt: 'Художники со всей страны украшают стены зданий яркими граффити. Фестиваль продлится до конца месяца.',
                            category: 'culture',
                            author: 'Елена Козлова',
                            date: new Date(Date.now() - 432000000).toISOString(),
                            image: 'https://images.unsplash.com/photo-1513475382585-d06e58bcb0e0?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80',
                            likes: 51,
                            comments: 14,
                            rating: 4.6,
                            featured: false
                        },
                        {
                            id: 6,
                            title: 'Минздрав Пельмении рекомендует новые нормы питания',
                            excerpt: 'В обновленных рекомендациях особое внимание уделяется сбалансированному потреблению белков, жиров и углеводов.',
                            category: 'health',
                            author: 'Ольга Новикова',
                            date: new Date(Date.now() - 518400000).toISOString(),
                            image: 'https://images.unsplash.com/photo-1490818387583-1baba5e638af?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80',
                            likes: 33,
                            comments: 6,
                            rating: 4.1,
                            featured: false
                        }
                    ];
                    localStorage.setItem('pelmeniaNews', JSON.stringify(allNews));
                }
                
                // Загрузка новостей
                loadNews();
            }
            
            // Загрузка списка чатов
            function loadConversations() {
                const conversationsList = document.getElementById('conversations-list');
                conversationsList.innerHTML = '';
                
                conversations.forEach(conversation => {
                    // Найти собеседника (не текущего пользователя)
                    const participantId = conversation.participants.find(id => id !== currentUser.id);
                    const participant = users.find(user => user.id === participantId);
                    
                    const conversationElement = document.createElement('div');
                    conversationElement.className = 'conversation-item';
                    conversationElement.dataset.id = conversation.id;
                    
                    conversationElement.innerHTML = `
                        <div class="conversation-header">
                            <strong>${participant.name}</strong>
                            <span>${formatTime(conversation.lastMessageTime)}</span>
                        </div>
                        <div class="conversation-preview">${conversation.lastMessage}</div>
                        ${conversation.unread > 0 ? `<span class="notification-badge">${conversation.unread}</span>` : ''}
                    `;
                    
                    conversationElement.addEventListener('click', function() {
                        // Убрать активный класс у всех чатов
                        document.querySelectorAll('.conversation-item').forEach(item => {
                            item.classList.remove('active');
                        });
                        
                        // Добавить активный класс к выбранному чату
                        this.classList.add('active');
                        
                        // Загрузить сообщения чата
                        loadChatMessages(conversation.id);
                    });
                    
                    conversationsList.appendChild(conversationElement);
                });
                
                // Если есть чаты, загрузить первый
                if (conversations.length > 0) {
                    const firstChat = conversationsList.querySelector('.conversation-item');
                    if (firstChat) {
                        firstChat.classList.add('active');
                        loadChatMessages(conversations[0].id);
                    }
                }
            }
            
            // Загрузка сообщений чата
            function loadChatMessages(conversationId) {
                const chatMessages = document.getElementById('chat-messages');
                chatMessages.innerHTML = '';
                
                const conversation = conversations.find(c => c.id === conversationId);
                
                if (conversation) {
                    conversation.messages.forEach(message => {
                        const messageElement = document.createElement('div');
                        messageElement.className = `message ${message.sender === currentUser.id ? 'own' : ''}`;
                        
                        const sender = message.sender === currentUser.id ? currentUser : users.find(u => u.id === message.sender);
                        
                        messageElement.innerHTML = `
                            <div class="message-sender">${sender.name}</div>
                            <div class="message-content">${message.text}</div>
                            <div class="message-time">${formatTime(message.timestamp)}</div>
                        `;
                        
                        chatMessages.appendChild(messageElement);
                    });
                    
                    // Прокрутка к последнему сообщению
                    chatMessages.scrollTop = chatMessages.scrollHeight;
                    
                    // Сбросить счетчик непрочитанных
                    conversation.unread = 0;
                    localStorage.setItem('pelmeniaConversations', JSON.stringify(conversations));
                    updateNotificationBadges();
                }
            }
            
            // Отправка сообщения
            document.getElementById('send-message').addEventListener('click', sendMessage);
            document.getElementById('message-input').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    sendMessage();
                }
            });
            
            function sendMessage() {
                const messageInput = document.getElementById('message-input');
                const messageText = messageInput.value.trim();
                
                if (!messageText) return;
                
                // Найти активный чат
                const activeChat = document.querySelector('.conversation-item.active');
                if (!activeChat) return;
                
                const conversationId = parseInt(activeChat.dataset.id);
                const conversation = conversations.find(c => c.id === conversationId);
                
                if (conversation) {
                    // Создать новое сообщение
                    const newMessage = {
                        id: Date.now(),
                        sender: currentUser.id,
                        text: messageText,
                        timestamp: new Date().toISOString()
                    };
                    
                    // Добавить сообщение в чат
                    conversation.messages.push(newMessage);
                    conversation.lastMessage = messageText;
                    conversation.lastMessageTime = new Date().toISOString();
                    
                    // Обновить локальное хранилище
                    localStorage.setItem('pelmeniaConversations', JSON.stringify(conversations));
                    
                    // Очистить поле ввода
                    messageInput.value = '';
                    
                    // Перезагрузить сообщения чата
                    loadChatMessages(conversationId);
                    
                    // Обновить список чатов
                    loadConversations();
                }
            }
            
            // Загрузка почты
            function loadEmailInbox() {
                const emailList = document.getElementById('email-list');
                emailList.innerHTML = '';
                
                const inboxEmails = emails.filter(email => email.folder === 'inbox');
                
                inboxEmails.forEach(email => {
                    const emailElement = document.createElement('div');
                    emailElement.className = `email-item ${email.read ? '' : 'unread'}`;
                    emailElement.dataset.id = email.id;
                    
                    emailElement.innerHTML = `
                        <div class="email-sender">${email.from.name}</div>
                        <div class="email-subject">${email.subject}</div>
                        <div class="email-preview">${email.body.substring(0, 100)}...</div>
                    `;
                    
                    emailElement.addEventListener('click', function() {
                        viewEmail(email.id);
                    });
                    
                    emailList.appendChild(emailElement);
                });
                
                // Показать первое письмо, если есть
                if (inboxEmails.length > 0) {
                    viewEmail(inboxEmails[0].id);
                } else {
                    document.getElementById('email-view').innerHTML = '<p>Нет писем во входящих</p>';
                }
            }
            
            // Просмотр письма
            function viewEmail(emailId) {
                const email = emails.find(e => e.id === emailId);
                const emailView = document.getElementById('email-view');
                
                if (email) {
                    emailView.innerHTML = `
                        <div class="email-view-header">
                            <h3>${email.subject}</h3>
                            <p><strong>От:</strong> ${email.from.name} &lt;${email.from.email}&gt;</p>
                            <p><strong>Кому:</strong> ${email.to}</p>
                            <p><strong>Дата:</strong> ${formatTime(email.timestamp)}</p>
                        </div>
                        <div class="email-body">
                            <p>${email.body}</p>
                        </div>
                        <div style="margin-top: 20px;">
                            <button class="btn btn-secondary" id="reply-email"><i class="fas fa-reply"></i> Ответить</button>
                            <button class="btn" id="delete-email"><i class="fas fa-trash"></i> Удалить</button>
                        </div>
                    `;
                    
                    // Пометить как прочитанное
                    if (!email.read) {
                        email.read = true;
                        localStorage.setItem('pelmeniaEmails', JSON.stringify(emails));
                        updateNotificationBadges();
                        loadEmailInbox();
                    }
                    
                    // Обработчики для кнопок
                    document.getElementById('reply-email').addEventListener('click', function() {
                        composeEmail(email.from.email, `Re: ${email.subject}`, `\n\n--- Original Message ---\n${email.body}`);
                    });
                    
                    document.getElementById('delete-email').addEventListener('click', function() {
                        email.folder = 'trash';
                        localStorage.setItem('pelmeniaEmails', JSON.stringify(emails));
                        loadEmailInbox();
                    });
                }
            }
            
            // Создание нового письма
            document.getElementById('compose-email').addEventListener('click', function() {
                composeEmail();
            });
            
            function composeEmail(to = '', subject = '', body = '') {
                const emailView = document.getElementById('email-view');
                
                emailView.innerHTML = `
                    <div class="compose-email">
                        <h3>Новое письмо</h3>
                        <form class="compose-form" id="compose-form">
                            <div class="form-group">
                                <label for="email-to">Кому:</label>
                                <input type="email" id="email-to" class="form-control" value="${to}" required>
                            </div>
                            <div class="form-group">
                                <label for="email-subject">Тема:</label>
                                <input type="text" id="email-subject" class="form-control" value="${subject}" required>
                            </div>
                            <div class="form-group">
                                <label for="email-body">Текст письма:</label>
                                <textarea id="email-body" class="form-control" rows="10" required>${body}</textarea>
                            </div>
                            <div>
                                <button type="submit" class="btn btn-success"><i class="fas fa-paper-plane"></i> Отправить</button>
                                <button type="button" class="btn btn-secondary" id="save-draft"><i class="fas fa-save"></i> Сохранить черновик</button>
                            </div>
                        </form>
                    </div>
                `;
                
                document.getElementById('compose-form').addEventListener('submit', function(e) {
                    e.preventDefault();
                    
                    const to = document.getElementById('email-to').value;
                    const subject = document.getElementById('email-subject').value;
                    const body = document.getElementById('email-body').value;
                    
                    // Создать новое письмо
                    const newEmail = {
                        id: Date.now(),
                        from: { name: currentUser.name, email: currentUser.email },
                        to: to,
                        subject: subject,
                        body: body,
                        timestamp: new Date().toISOString(),
                        read: true,
                        folder: 'sent'
                    };
                    
                    // Добавить письмо в отправленные
                    emails.push(newEmail);
                    localStorage.setItem('pelmeniaEmails', JSON.stringify(emails));
                    
                    alert('Письмо отправлено!');
                    loadEmailInbox();
                });
                
                document.getElementById('save-draft').addEventListener('click', function() {
                    const to = document.getElementById('email-to').value;
                    const subject = document.getElementById('email-subject').value;
                    const body = document.getElementById('email-body').value;
                    
                    // Создать черновик
                    const draftEmail = {
                        id: Date.now(),
                        from: { name: currentUser.name, email: currentUser.email },
                        to: to,
                        subject: subject,
                        body: body,
                        timestamp: new Date().toISOString(),
                        read: true,
                        folder: 'drafts'
                    };
                    
                    // Добавить черновик
                    emails.push(draftEmail);
                    localStorage.setItem('pelmeniaEmails', JSON.stringify(emails));
                    
                    alert('Черновик сохранен!');
                    loadEmailInbox();
                });
            }
            
            // Обновление бейджей уведомлений
            function updateNotificationBadges() {
                // Сообщения
                const unreadMessages = conversations.reduce((total, conv) => total + conv.unread, 0);
                const messageBadge = document.querySelector('.nav-messages .notification-badge');
                if (unreadMessages > 0) {
                    messageBadge.textContent = unreadMessages;
                    messageBadge.style.display = 'flex';
                } else {
                    messageBadge.style.display = 'none';
                }
                
                // Почта
                const unreadEmails = emails.filter(email => !email.read && email.folder === 'inbox').length;
                const emailBadge = document.querySelector('.nav-email .notification-badge');
                if (unreadEmails > 0) {
                    emailBadge.textContent = unreadEmails;
                    emailBadge.style.display = 'flex';
                } else {
                    emailBadge.style.display = 'none';
                }
            }
            
            // Форматирование времени
            function formatTime(timestamp) {
                const date = new Date(timestamp);
                const now = new Date();
                
                if (date.toDateString() === now.toDateString()) {
                    return date.toLocaleTimeString('ru-RU', { hour: '2-digit', minute: '2-digit' });
                } else {
                    return date.toLocaleDateString('ru-RU');
                }
            }
            
            // Загрузка новостей с применением фильтров
            function loadNews() {
                const newsContainer = document.getElementById('news-container');
                newsContainer.innerHTML = '';
                
                // Применить фильтры к новостям
                let filteredNews = [...allNews];
                
                // Фильтр по категории
                if (activeFilters.category !== 'all') {
                    filteredNews = filteredNews.filter(news => news.category === activeFilters.category);
                }
                
                // Фильтр по дате
                const now = new Date();
                if (activeFilters.date !== 'all') {
                    const timeRanges = {
                        today: 24 * 60 * 60 * 1000, // 1 день
                        week: 7 * 24 * 60 * 60 * 1000, // 7 дней
                        month: 30 * 24 * 60 * 60 * 1000 // 30 дней
                    };
                    
                    if (activeFilters.date in timeRanges) {
                        const timeRange = timeRanges[activeFilters.date];
                        filteredNews = filteredNews.filter(news => {
                            const newsDate = new Date(news.date);
                            return (now - newsDate) < timeRange;
                        });
                    }
                }
                
                // Фильтр по автору
                if (activeFilters.author !== 'all') {
                    filteredNews = filteredNews.filter(news => {
                        const authorMap = {
                            ivan: 'Иван Иванов',
                            maria: 'Мария Петрова',
                            alex: 'Алексей Смирнов'
                        };
                        return news.author === authorMap[activeFilters.author];
                    });
                }
                
                // Фильтр по рейтингу
                if (activeFilters.rating > 0) {
                    filteredNews = filteredNews.filter(news => news.rating >= activeFilters.rating);
                }
                
                // Фильтр по избранным
                if (activeFilters.featured) {
                    filteredNews = filteredNews.filter(news => news.featured);
                }
                
                // Поиск по ключевым словам
                if (activeFilters.search) {
                    const searchTerm = activeFilters.search.toLowerCase();
                    filteredNews = filteredNews.filter(news => 
                        news.title.toLowerCase().includes(searchTerm) || 
                        news.excerpt.toLowerCase().includes(searchTerm)
                    );
                }
                
                // Сортировка
                if (activeFilters.sort === 'newest') {
                    filteredNews.sort((a, b) => new Date(b.date) - new Date(a.date));
                } else if (activeFilters.sort === 'oldest') {
                    filteredNews.sort((a, b) => new Date(a.date) - new Date(b.date));
                } else if (activeFilters.sort === 'popular') {
                    filteredNews.sort((a, b) => b.likes - a.likes);
                }
                
                // Отображение новостей
                if (filteredNews.length === 0) {
                    newsContainer.innerHTML = '<p style="grid-column: 1 / -1; text-align: center; padding: 40px;">Новости по выбранным фильтрам не найдены.</p>';
                    return;
                }
                
                filteredNews.forEach(news => {
                    const newsCard = document.createElement('div');
                    newsCard.className = 'news-card';
                    newsCard.dataset.id = news.id;
                    
                    const categoryNames = {
                        politics: 'Политика',
                        economy: 'Экономика',
                        culture: 'Культура',
                        sports: 'Спорт',
                        technology: 'Технологии',
                        health: 'Здоровье'
                    };
                    
                    newsCard.innerHTML = `
                        <div class="news-image" style="background-image: url('${news.image}')"></div>
                        <div class="news-content">
                            <span class="news-category">${categoryNames[news.category]}</span>
                            <h3 class="news-title">${news.title}</h3>
                            <p class="news-excerpt">${news.excerpt}</p>
                            <div class="news-meta">
                                <span>${news.author}</span>
                                <span>${formatTime(news.date)}</span>
                            </div>
                            <div class="news-stats">
                                <span><i class="fas fa-heart"></i> ${news.likes}</span>
                                <span><i class="fas fa-comment"></i> ${news.comments}</span>
                                <span><i class="fas fa-star"></i> ${news.rating}</span>
                                ${news.featured ? '<span><i class="fas fa-certificate"></i> Избранная</span>' : ''}
                            </div>
                            <div class="news-actions">
                                <button class="action-btn"><i class="fas fa-share"></i> Поделиться</button>
                                <button class="action-btn"><i class="fas fa-bookmark"></i> Сохранить</button>
                            </div>
                        </div>
                    `;
                    
                    // Добавить обработчик клика для открытия новости
                    newsCard.addEventListener('click', function(e) {
                        // Проверить, не был ли клик по кнопке действия
                        if (!e.target.closest('.action-btn')) {
                            openNewsModal(news.id);
                        }
                    });
                    
                    newsContainer.appendChild(newsCard);
                });
                
                // Обновить теги активных фильтров
                updateFilterTags();
            }
            
            // Открытие модального окна с новостью
            function openNewsModal(newsId) {
                const news = allNews.find(n => n.id === newsId);
                
                if (news) {
                    // Заполнить модальное окно данными новости
                    document.getElementById('modal-title').textContent = news.title;
                    document.getElementById('modal-image').style.backgroundImage = `url('${news.image}')`;
                    document.getElementById('modal-author').textContent = news.author;
                    document.getElementById('modal-date').textContent = formatTime(news.date);
                    document.getElementById('modal-text').textContent = newsFullTexts[newsId] || 'Полный текст новости временно недоступен.';
                    document.getElementById('modal-likes').textContent = news.likes;
                    document.getElementById('modal-comments').textContent = news.comments;
                    document.getElementById('modal-rating').textContent = news.rating;
                    
                    // Показать модальное окно
                    newsModal.style.display = 'block';
                    
                    // Добавить обработчики для кнопок в модальном окне
                    document.getElementById('modal-like').onclick = function() {
                        news.likes++;
                        document.getElementById('modal-likes').textContent = news.likes;
                        localStorage.setItem('pelmeniaNews', JSON.stringify(allNews));
                        loadNews(); // Обновить список новостей, чтобы отобразить новое количество лайков
                    };
                    
                    document.getElementById('modal-share').onclick = function() {
                        alert('Функция "Поделиться" будет реализована в будущем обновлении!');
                    };
                    
                    document.getElementById('modal-save').onclick = function() {
                        alert('Новость сохранена в избранное!');
                    };
                }
            }
            
            // Обновление тегов активных фильтров
            function updateFilterTags() {
                const filterTags = document.getElementById('filter-tags');
                filterTags.innerHTML = '';
                
                // Категория
                if (activeFilters.category !== 'all') {
                    const categoryNames = {
                        politics: 'Политика',
                        economy: 'Экономика',
                        culture: 'Культура',
                        sports: 'Спорт',
                        technology: 'Технологии',
                        health: 'Здоровье'
                    };
                    
                    const tag = document.createElement('div');
                    tag.className = 'filter-tag';
                    tag.innerHTML = `Категория: ${categoryNames[activeFilters.category]} <i class="fas fa-times" data-filter="category"></i>`;
                    filterTags.appendChild(tag);
                }
                
                // Дата
                if (activeFilters.date !== 'all') {
                    const dateNames = {
                        today: 'Сегодня',
                        week: 'За неделю',
                        month: 'За месяц'
                    };
                    
                    const tag = document.createElement('div');
                    tag.className = 'filter-tag';
                    tag.innerHTML = `Дата: ${dateNames[activeFilters.date]} <i class="fas fa-times" data-filter="date"></i>`;
                    filterTags.appendChild(tag);
                }
                
                // Сортировка
                if (activeFilters.sort !== 'newest') {
                    const sortNames = {
                        oldest: 'Сначала старые',
                        popular: 'По популярности'
                    };
                    
                    const tag = document.createElement('div');
                    tag.className = 'filter-tag';
                    tag.innerHTML = `Сортировка: ${sortNames[activeFilters.sort]} <i class="fas fa-times" data-filter="sort"></i>`;
                    filterTags.appendChild(tag);
                }
                
                // Поиск
                if (activeFilters.search) {
                    const tag = document.createElement('div');
                    tag.className = 'filter-tag';
                    tag.innerHTML = `Поиск: "${activeFilters.search}" <i class="fas fa-times" data-filter="search"></i>`;
                    filterTags.appendChild(tag);
                }
                
                // Автор
                if (activeFilters.author !== 'all') {
                    const authorNames = {
                        ivan: 'Иван Иванов',
                        maria: 'Мария Петрова',
                        alex: 'Алексей Смирнов'
                    };
                    
                    const tag = document.createElement('div');
                    tag.className = 'filter-tag';
                    tag.innerHTML = `Автор: ${authorNames[activeFilters.author]} <i class="fas fa-times" data-filter="author"></i>`;
                    filterTags.appendChild(tag);
                }
                
                // Рейтинг
                if (activeFilters.rating > 0) {
                    const tag = document.createElement('div');
                    tag.className = 'filter-tag';
                    tag.innerHTML = `Рейтинг: ${activeFilters.rating}+ <i class="fas fa-times" data-filter="rating"></i>`;
                    filterTags.appendChild(tag);
                }
                
                // Избранные
                if (activeFilters.featured) {
                    const tag = document.createElement('div');
                    tag.className = 'filter-tag';
                    tag.innerHTML = `Только избранные <i class="fas fa-times" data-filter="featured"></i>`;
                    filterTags.appendChild(tag);
                }
                
                // Добавить обработчики для удаления фильтров
                filterTags.querySelectorAll('i').forEach(icon => {
                    icon.addEventListener('click', function() {
                        const filterType = this.dataset.filter;
                        resetFilter(filterType);
                    });
                });
            }
            
            // Сброс конкретного фильтра
            function resetFilter(filterType) {
                const defaultFilters = {
                    category: 'all',
                    date: 'all',
                    sort: 'newest',
                    search: '',
                    author: 'all',
                    rating: 0,
                    featured: false
                };
                
                activeFilters[filterType] = defaultFilters[filterType];
                
                // Обновить UI элементов
                if (filterType === 'category') {
                    document.getElementById('category-filter').value = 'all';
                } else if (filterType === 'date') {
                    document.getElementById('date-filter').value = 'all';
                } else if (filterType === 'sort') {
                    document.getElementById('sort-filter').value = 'newest';
                } else if (filterType === 'search') {
                    document.getElementById('search-filter').value = '';
                } else if (filterType === 'author') {
                    document.getElementById('author-filter').value = 'all';
                } else if (filterType === 'rating') {
                    document.getElementById('rating-filter').value = '0';
                } else if (filterType === 'featured') {
                    document.getElementById('featured-filter').checked = false;
                }
                
                // Перезагрузить новости
                loadNews();
            }
            
            // Обработчики для фильтров
            document.getElementById('apply-filters').addEventListener('click', function() {
                // Получить значения фильтров
                activeFilters.category = document.getElementById('category-filter').value;
                activeFilters.date = document.getElementById('date-filter').value;
                activeFilters.sort = document.getElementById('sort-filter').value;
                activeFilters.search = document.getElementById('search-filter').value;
                
                // Применить фильтры
                loadNews();
            });
            
            document.getElementById('reset-filters').addEventListener('click', function() {
                // Сбросить все фильтры
                activeFilters = {
                    category: 'all',
                    date: 'all',
                    sort: 'newest',
                    search: '',
                    author: 'all',
                    rating: 0,
                    featured: false
                };
                
                // Сбросить UI элементов
                document.getElementById('category-filter').value = 'all';
                document.getElementById('date-filter').value = 'all';
                document.getElementById('sort-filter').value = 'newest';
                document.getElementById('search-filter').value = '';
                document.getElementById('author-filter').value = 'all';
                document.getElementById('rating-filter').value = '0';
                document.getElementById('featured-filter').checked = false;
                
                // Перезагрузить новости
                loadNews();
            });
            
            document.getElementById('toggle-advanced').addEventListener('click', function() {
                const advancedFilters = document.getElementById('advanced-filters');
                advancedFilters.classList.toggle('hidden');
                
                if (advancedFilters.classList.contains('hidden')) {
                    this.innerHTML = '<i class="fas fa-chevron-down"></i> Расширенные фильтры';
                } else {
                    this.innerHTML = '<i class="fas fa-chevron-up"></i> Скрыть расширенные фильтры';
                    
                    // Применить расширенные фильтры при открытии
                    activeFilters.author = document.getElementById('author-filter').value;
                    activeFilters.rating = parseInt(document.getElementById('rating-filter').value);
                    activeFilters.featured = document.getElementById('featured-filter').checked;
                    
                    loadNews();
                }
            });
            
            // Обработчики для расширенных фильтров
            document.getElementById('author-filter').addEventListener('change', function() {
                activeFilters.author = this.value;
                loadNews();
            });
            
            document.getElementById('rating-filter').addEventListener('change', function() {
                activeFilters.rating = parseInt(this.value);
                loadNews();
            });
            
            document.getElementById('featured-filter').addEventListener('change', function() {
                activeFilters.featured = this.checked;
                loadNews();
            });
            
            // Показать главную страницу при загрузке
            showSection('main');
            updateNotificationBadges();
        });
    </script>
</body>
</html>
