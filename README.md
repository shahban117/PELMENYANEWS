# PELMENYANEWS
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Новости Пельмении - Генератор новостей ИИ</title>
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
        
        .form-control {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
            transition: all 0.3s ease;
        }
        
        .form-control:focus {
            border-color: var(--secondary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
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
        
        .news-preview img {
            width: 100%;
            border-radius: 8px;
            margin-bottom: 15px;
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
        
        /* Share Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }
        
        .modal-content {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            max-width: 500px;
            width: 90%;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .modal-title {
            font-size: 1.5rem;
            color: var(--primary);
        }
        
        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #7f8c8d;
        }
        
        .share-options {
            display: flex;
            gap: 15px;
            margin-top: 20px;
            justify-content: center;
        }
        
        .share-option {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            padding: 10px;
            border-radius: 8px;
        }
        
        .share-option:hover {
            background-color: var(--light);
        }
        
        .share-icon {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            color: white;
        }
        
        .share-vk {
            background-color: #4c75a3;
        }
        
        .share-telegram {
            background-color: #0088cc;
        }
        
        .share-whatsapp {
            background-color: #25d366;
        }
        
        .share-twitter {
            background-color: #1da1f2;
        }
        
        /* Responsive */
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
            
            .share-options {
                flex-wrap: wrap;
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
                        <li><a href="#"><i class="fas fa-home"></i> Главная</a></li>
                        <li><a href="#"><i class="fas fa-bolt"></i> Срочные новости</a></li>
                        <li><a href="#"><i class="fas fa-flag"></i> Политика</a></li>
                        <li><a href="#generator"><i class="fas fa-robot"></i> Генератор новостей</a></li>
                    </ul>
                </nav>
            </div>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <div class="container">
            <h2>Добро пожаловать в Пельмению!</h2>
            <p>Самая актуальная информация о событиях в нашей стране. Теперь с генератором новостей на основе искусственного интеллекта!</p>
            <a href="#generator" class="btn"><i class="fas fa-robot"></i> Создать новость с ИИ</a>
        </div>
    </section>

    <!-- Main Content -->
    <div class="container">
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

        <!-- Latest News -->
        <h2 class="section-title">Последние новости Пельмении</h2>
        <div class="news-grid" id="news-container">
            <!-- Новости будут загружаться здесь -->
        </div>
    </div>

    <!-- Share Modal -->
    <div class="modal" id="share-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Поделиться новостью</h3>
                <button class="close-modal">&times;</button>
            </div>
            <p>Поделитесь этой новостью с друзьями и знакомыми!</p>
            <div class="share-options">
                <div class="share-option" data-platform="vk">
                    <div class="share-icon share-vk">
                        <i class="fab fa-vk"></i>
                    </div>
                    <span>ВКонтакте</span>
                </div>
                <div class="share-option" data-platform="telegram">
                    <div class="share-icon share-telegram">
                        <i class="fab fa-telegram"></i>
                    </div>
                    <span>Telegram</span>
                </div>
                <div class="share-option" data-platform="whatsapp">
                    <div class="share-icon share-whatsapp">
                        <i class="fab fa-whatsapp"></i>
                    </div>
                    <span>WhatsApp</span>
                </div>
                <div class="share-option" data-platform="twitter">
                    <div class="share-icon share-twitter">
                        <i class="fab fa-twitter"></i>
                    </div>
                    <span>Twitter</span>
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
                    <p>Теперь с инновационным генератором новостей на основе ИИ!</p>
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
            const generateButton = document.getElementById('generate-news');
            const newsPreview = document.getElementById('news-preview');
            const previewContent = document.getElementById('preview-content');
            const newsContainer = document.getElementById('news-container');
            const shareModal = document.getElementById('share-modal');
            const closeModal = document.querySelector('.close-modal');
            const shareOptions = document.querySelectorAll('.share-option');
            
            // Имитация базы данных новостей (в реальном приложении это был бы сервер)
            let allNews = JSON.parse(localStorage.getItem('pelmeniaNews')) || [];
            
            // Загрузка существующих новостей при загрузке страницы
            loadNews();
            
            // Примеры новостей для генерации
            const newsTemplates = {
                politics: [
                    "Парламент Пельмении принял новый закон о {{topic}}, который, по мнению экспертов, значительно {{effect}}.",
                    "Министерство внутренних дел Пельмении объявило о {{topic}}, что вызвало {{reaction}} среди населения.",
                    "Президент Пельмении подписал указ о {{topic}}, направленный на {{purpose}}."
                ],
                economy: [
                    "Экономика Пельмении демонстрирует рост после внедрения {{topic}}, что привело к {{result}}.",
                    "Национальный банк Пельмении объявил о {{topic}}, что, по прогнозам, {{prediction}}.",
                    "Крупнейшая компания Пельмении инвестирует в {{topic}}, создавая {{jobs}} рабочих мест."
                ],
                culture: [
                    "В Пельмении открылся новый {{topic}}, который уже стал {{popularity}} среди жителей и туристов.",
                    "Известный пельменский художник представил выставку, посвященную {{topic}}, получившую {{reviews}}.",
                    "Фестиваль {{topic}} в Пельмении побил все рекорды посещаемости, собрав более {{attendees}}."
                ],
                sports: [
                    "Сборная Пельмении по {{sport}} одержала победу в {{tournament}}, обыграв команду {{opponent}}.",
                    "Легендарный пельменский спортсмен установил новый мировой рекорд в {{sport}}, превзойдя {{previous_record}}.",
                    "В Пельмении началось строительство нового {{facility}} для {{sport}}, который станет {{significance}}."
                ],
                technology: [
                    "Пельменские ученые разработали революционную технологию {{topic}}, которая может {{potential}}.",
                    "Стартап из Пельмении представил инновационное решение для {{problem}}, получившее {{funding}} финансирования.",
                    "В Технологическом институте Пельмении создан первый в мире {{invention}}, способный {{capabilities}}."
                ],
                health: [
                    "Минздрав Пельмении объявил о внедрении новой программы {{topic}}, направленной на {{goal}}.",
                    "Пельменские медики разработали новый метод лечения {{disease}}, показавший {{effectiveness}} эффективность.",
                    "В больницах Пельмении начали применять инновационное оборудование для {{procedure}}, что сократило {{metric}}."
                ]
            };
            
            // Функция для получения случайного элемента из массива
            function getRandomElement(array) {
                return array[Math.floor(Math.random() * array.length)];
            }
            
            // Функция для генерации новости
            function generateNews() {
                const category = document.getElementById('news-category').value;
                const tone = document.getElementById('news-tone').value;
                const topic = document.getElementById('news-topic').value.trim();
                const details = document.getElementById('news-details').value.trim();
                
                if (!topic) {
                    alert('Пожалуйста, введите тему новости!');
                    return;
                }
                
                // Выбор шаблона в зависимости от категории
                const template = getRandomElement(newsTemplates[category]);
                
                // Заполнение шаблона
                let newsText = template
                    .replace('{{topic}}', topic)
                    .replace('{{effect}}', getRandomElement(['улучшит экономическую ситуацию', 'повлияет на социальную сферу', 'укрепит международные позиции']))
                    .replace('{{reaction}}', getRandomElement(['оживленные дискуссии', 'широкую поддержку', 'неоднозначную реакцию']))
                    .replace('{{purpose}}', getRandomElement(['улучшение качества жизни', 'стимулирование экономики', 'развитие инфраструктуры']))
                    .replace('{{result}}', getRandomElement(['увеличению ВВП на 5%', 'снижению безработицы', 'росту инвестиций']))
                    .replace('{{prediction}}', getRandomElement(['стабилизирует финансовую систему', 'ускорит экономический рост', 'снизит инфляцию']))
                    .replace('{{jobs}}', Math.floor(Math.random() * 5000) + 1000)
                    .replace('{{popularity}}', getRandomElement(['популярным местом', 'культурным центром', 'главной достопримечательностью']))
                    .replace('{{reviews}}', getRandomElement(['восторженные отзывы', 'признание критиков', 'международное признание']))
                    .replace('{{attendees}}', Math.floor(Math.random() * 50000) + 10000 + ' человек')
                    .replace('{{sport}}', getRandomElement(['футболу', 'хоккею', 'баскетболу', 'волейболу']))
                    .replace('{{tournament}}', getRandomElement(['чемпионате мира', 'международном турнире', 'европейском кубке']))
                    .replace('{{opponent}}', getRandomElement(['Соседнии', 'Борщастана', 'Вареникова']))
                    .replace('{{previous_record}}', getRandomElement(['предыдущее достижение', 'рекорд десятилетия', 'исторический показатель']))
                    .replace('{{facility}}', getRandomElement(['стадиона', 'спортивного комплекса', 'арены']))
                    .replace('{{significance}}', getRandomElement(['крупнейшим в регионе', 'международным центром', 'гордостью нации']))
                    .replace('{{potential}}', getRandomElement(['изменить будущее энергетики', 'революционизировать промышленность', 'решить экологические проблемы']))
                    .replace('{{problem}}', getRandomElement(['улучшения городской мобильности', 'оптимизации логистики', 'повышения кибербезопасности']))
                    .replace('{{funding}}', Math.floor(Math.random() * 50) + 10 + ' миллионов пельмов')
                    .replace('{{invention}}', getRandomElement(['квантовый компьютер', 'бионический протез', 'автономный транспорт']))
                    .replace('{{capabilities}}', getRandomElement(['перерабатывать отходы с эффективностью 95%', 'генерировать энергию из воздуха', 'обучаться быстрее человека']))
                    .replace('{{goal}}', getRandomElement(['снижение заболеваемости', 'улучшение медицинского обслуживания', 'продление продолжительности жизни']))
                    .replace('{{disease}}', getRandomElement(['сердечно-сосудистых заболеваний', 'онкологических заболеваний', 'неврологических расстройств']))
                    .replace('{{effectiveness}}', Math.floor(Math.random() * 40) + 60)
                    .replace('{{procedure}}', getRandomElement(['диагностики заболеваний', 'микрохирургических операций', 'реабилитации пациентов']))
                    .replace('{{metric}}', getRandomElement(['время восстановления на 30%', 'стоимость лечения на 25%', 'риск осложнений на 40%']));
                
                // Добавление деталей, если они есть
                if (details) {
                    newsText += ` ${details}`;
                }
                
                // Применение тона
                if (tone === 'positive') {
                    newsText += " Эксперты оценивают это событие как крайне позитивное для будущего Пельмении.";
                } else if (tone === 'negative') {
                    newsText += " Критики выражают обеспокоенность по поводу возможных негативных последствий.";
                } else if (tone === 'humorous') {
                    newsText += " Жители Пельмении шутят, что это событие войдет в историю как самое обсуждаемое со времен изобретения квадратного пельменя.";
                }
                
                // Добавление даты и места
                const cities = ['столице Пельмении', 'городе Пельменск', 'курортном регионе', 'северной провинции'];
                const currentDate = new Date();
                const formattedDate = currentDate.toLocaleDateString('ru-RU');
                
                newsText = `По сообщениям наших корреспондентов из ${getRandomElement(cities)}, ${formattedDate.toLowerCase()}, ${newsText.toLowerCase()}`;
                
                // Создание объекта новости
                const newsItem = {
                    id: Date.now(),
                    title: `${topic} - важное событие в Пельмении`,
                    content: newsText,
                    category: category,
                    date: formattedDate,
                    author: 'Пользовательский контент',
                    image: 'https://images.unsplash.com/photo-1585829365295-ab7cd400c167?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80',
                    views: 0,
                    likes: 0
                };
                
                // Сохранение новости
                allNews.unshift(newsItem);
                localStorage.setItem('pelmeniaNews', JSON.stringify(allNews));
                
                // Отображение превью
                previewContent.innerHTML = `
                    <div class="news-image" style="background-image: url('${newsItem.image}'); height: 200px; border-radius: 8px; margin-bottom: 15px;"></div>
                    <p>${newsText}</p>
                    <div style="margin-top: 20px; display: flex; gap: 10px;">
                        <button class="btn" id="publish-news"><i class="fas fa-globe"></i> Опубликовать для всех</button>
                        <button class="btn btn-secondary" id="share-generated-news"><i class="fas fa-share-alt"></i> Поделиться</button>
                    </div>
                `;
                
                newsPreview.style.display = 'block';
                
                // Прокрутка к превью
                newsPreview.scrollIntoView({ behavior: 'smooth' });
                
                // Добавление обработчиков для кнопок в превью
                document.getElementById('publish-news').addEventListener('click', function() {
                    alert('Новость опубликована и теперь доступна всем пользователям!');
                    loadNews();
                });
                
                document.getElementById('share-generated-news').addEventListener('click', function() {
                    openShareModal(newsItem);
                });
            }
            
            // Функция загрузки новостей
            function loadNews() {
                newsContainer.innerHTML = '';
                
                if (allNews.length === 0) {
                    // Если новостей нет, загружаем демо-новости
                    loadDemoNews();
                } else {
                    // Отображаем существующие новости
                    allNews.forEach(news => {
                        addNewsToContainer(news);
                    });
                }
            }
            
            // Функция добавления новости в контейнер
            function addNewsToContainer(news) {
                const newsCard = document.createElement('div');
                newsCard.className = 'news-card';
                newsCard.innerHTML = `
                    <div class="news-image" style="background-image: url('${news.image}');"></div>
                    <div class="news-content">
                        <span class="news-category">${getCategoryName(news.category)}</span>
                        <h3 class="news-title">${news.title}</h3>
                        <p class="news-excerpt">${news.content.substring(0, 150)}...</p>
                        <div class="news-meta">
                            <span><i class="far fa-calendar"></i> ${news.date}</span>
                            <span><i class="far fa-eye"></i> ${news.views}</span>
                        </div>
                        <div class="news-actions">
                            <button class="action-btn like-btn" data-id="${news.id}">
                                <i class="far fa-heart"></i> <span>${news.likes}</span>
                            </button>
                            <button class="action-btn share-btn" data-id="${news.id}">
                                <i class="fas fa-share-alt"></i> Поделиться
                            </button>
                        </div>
                    </div>
                `;
                
                newsContainer.appendChild(newsCard);
                
                // Добавляем обработчики для кнопок
                const likeBtn = newsCard.querySelector('.like-btn');
                const shareBtn = newsCard.querySelector('.share-btn');
                
                likeBtn.addEventListener('click', function() {
                    const id = parseInt(this.getAttribute('data-id'));
                    likeNews(id);
                });
                
                shareBtn.addEventListener('click', function() {
                    const id = parseInt(this.getAttribute('data-id'));
                    const news = allNews.find(item => item.id === id);
                    openShareModal(news);
                });
            }
            
            // Функция лайка новости
            function likeNews(id) {
                const newsIndex = allNews.findIndex(item => item.id === id);
                if (newsIndex !== -1) {
                    allNews[newsIndex].likes++;
                    localStorage.setItem('pelmeniaNews', JSON.stringify(allNews));
                    loadNews();
                }
            }
            
            // Функция открытия модального окна для шаринга
            function openShareModal(news) {
                shareModal.style.display = 'flex';
                
                // Добавляем обработчики для опций шаринга
                shareOptions.forEach(option => {
                    option.onclick = function() {
                        const platform = this.getAttribute('data-platform');
                        shareNews(news, platform);
                    };
                });
            }
            
            // Функция шаринга новости
            function shareNews(news, platform) {
                const url = `https://pelmenia-news.pm/news/${news.id}`;
                const text = `Посмотрите эту новость из Пельмении: ${news.title}`;
                
                let shareUrl = '';
                
                switch(platform) {
                    case 'vk':
                        shareUrl = `https://vk.com/share.php?url=${encodeURIComponent(url)}&title=${encodeURIComponent(news.title)}&comment=${encodeURIComponent(news.content.substring(0, 100))}`;
                        break;
                    case 'telegram':
                        shareUrl = `https://t.me/share/url?url=${encodeURIComponent(url)}&text=${encodeURIComponent(text)}`;
                        break;
                    case 'whatsapp':
                        shareUrl = `https://api.whatsapp.com/send?text=${encodeURIComponent(text + ' ' + url)}`;
                        break;
                    case 'twitter':
                        shareUrl = `https://twitter.com/intent/tweet?text=${encodeURIComponent(text)}&url=${encodeURIComponent(url)}`;
                        break;
                }
                
                // Увеличиваем счетчик просмотров
                const newsIndex = allNews.findIndex(item => item.id === news.id);
                if (newsIndex !== -1) {
                    allNews[newsIndex].views++;
                    localStorage.setItem('pelmeniaNews', JSON.stringify(allNews));
                }
                
                window.open(shareUrl, '_blank');
                shareModal.style.display = 'none';
                alert(`Новость успешно опубликована в ${getPlatformName(platform)}!`);
            }
            
            // Функция получения имени платформы
            function getPlatformName(platform) {
                const platforms = {
                    'vk': 'ВКонтакте',
                    'telegram': 'Telegram',
                    'whatsapp': 'WhatsApp',
                    'twitter': 'Twitter'
                };
                
                return platforms[platform] || platform;
            }
            
            // Функция получения имени категории
            function getCategoryName(category) {
                const categories = {
                    'politics': 'Политика',
                    'economy': 'Экономика',
                    'culture': 'Культура',
                    'sports': 'Спорт',
                    'technology': 'Технологии',
                    'health': 'Здоровье'
                };
                
                return categories[category] || category;
            }
            
            // Загрузка демо-новостей
            function loadDemoNews() {
                const demoNews = [
                    {
                        id: 1,
                        title: 'Президент Пельмении объявил о новых реформах',
                        content: 'В ходе выступления перед парламентом, президент представил план экономических реформ, направленных на стимулирование роста и создание новых рабочих мест. Реформы включают снижение налогов для малого бизнеса и увеличение инвестиций в инфраструктуру.',
                        category: 'politics',
                        date: '15 мая 2023',
                        author: 'Редакция',
                        image: 'https://images.unsplash.com/photo-1551135049-8a33b42738b4?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80',
                        views: 2400,
                        likes: 150
                    },
                    {
                        id: 2,
                        title: 'Пельменские ученые разработали новый источник энергии',
                        content: 'Исследователи из Технологического института Пельмении представили революционную технологию получения энергии из возобновляемых источников. Новая технология позволяет значительно повысить эффективность солнечных панелей даже в условиях недостаточной освещенности.',
                        category: 'technology',
                        date: '12 мая 2023',
                        author: 'Редакция',
                        image: 'https://images.unsplash.com/photo-1516937941344-00b4e0337589?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80',
                        views: 3100,
                        likes: 210
                    },
                    {
                        id: 3,
                        title: 'Фестиваль пельменей собрал рекордное количество участников',
                        content: 'В столице Пельмении завершился ежегодный фестиваль пельменей, который в этом году посетило более 50 тысяч человек. На фестивале были представлены пельмени различных регионов страны, а также инновационные рецепты от ведущих шеф-поваров.',
                        category: 'culture',
                        date: '10 мая 2023',
                        author: 'Редакция',
                        image: 'https://images.unsplash.com/photo-1534438327276-14e5300c3a48?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80',
                        views: 4700,
                        likes: 320
                    }
                ];
                
                allNews = demoNews;
                localStorage.setItem('pelmeniaNews', JSON.stringify(allNews));
                
                demoNews.forEach(news => {
                    addNewsToContainer(news);
                });
            }
            
            // Обработчик для кнопки генерации
            generateButton.addEventListener('click', generateNews);
            
            // Обработчик для закрытия модального окна
            closeModal.addEventListener('click', function() {
                shareModal.style.display = 'none';
            });
            
            // Закрытие модального окна при клике вне его
            window.addEventListener('click', function(event) {
                if (event.target === shareModal) {
                    shareModal.style.display = 'none';
                }
            });
        });
    </script>
</body>
</html>
