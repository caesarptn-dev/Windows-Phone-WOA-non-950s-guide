<WOA Non-950s website>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Windows ARM Guide</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }

        nav {
            background-color: rgba(255, 255, 255, 0.95);
            padding: 0;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        nav ul {
            list-style: none;
            display: flex;
            justify-content: center;
            gap: 0;
        }

        nav li {
            flex: 1;
            max-width: 250px;
        }

        nav button {
            width: 100%;
            padding: 20px 30px;
            background: none;
            border: none;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            color: #333;
            transition: all 0.3s ease;
            border-bottom: 3px solid transparent;
        }

        nav button:hover {
            background-color: #f0f0f0;
            color: #667eea;
        }

        nav button.active {
            color: #667eea;
            border-bottom-color: #667eea;
            background-color: #f8f8f8;
        }

        .content {
            display: none;
            padding: 60px 20px;
            max-width: 800px;
            margin: 0 auto;
            animation: fadeIn 0.5s ease;
        }

        .content.active {
            display: block;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .card {
            background: white;
            border-radius: 15px;
            padding: 40px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            text-align: center;
        }

        .logo {
            width: 200px;
            height: 200px;
            margin: 0 auto 30px;
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
        }

        .win10-logo {
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 88 88"><path fill="%230078D4" d="M0 12.402l35.687-4.86.016 34.423-35.67.203zm35.67 33.529l.028 34.453L.028 75.48.026 45.7zm4.326-39.025L87.314 0v41.527l-47.318.376zm47.329 39.349l-.011 41.34-47.318-6.678-.066-34.739z"/></svg>');
        }

        .win81-logo {
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 88 88"><path fill="%2300BCF2" d="M0 12.402l35.687-4.86.016 34.423-35.67.203zm35.67 33.529l.028 34.453L.028 75.48.026 45.7zm4.326-39.025L87.314 0v41.527l-47.318.376zm47.329 39.349l-.011 41.34-47.318-6.678-.066-34.739z"/></svg>');
        }

        h1 {
            color: #333;
            margin-bottom: 20px;
            font-size: 32px;
        }

        .guide-link {
            display: inline-block;
            margin-top: 30px;
            padding: 15px 40px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            text-decoration: none;
            border-radius: 50px;
            font-weight: 600;
            font-size: 18px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        .guide-link:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(102, 126, 234, 0.6);
        }

        .coming-soon {
            color: #666;
            font-size: 24px;
            margin-top: 20px;
            font-style: italic;
        }

        .credits-list {
            text-align: left;
            margin-top: 30px;
        }

        .credit-item {
            background: #f8f8f8;
            padding: 20px;
            margin-bottom: 15px;
            border-radius: 10px;
            border-left: 4px solid #667eea;
        }

        .credit-item strong {
            color: #667eea;
            font-size: 18px;
        }

        .credit-item p {
            margin-top: 5px;
            color: #666;
        }

        .home-hero {
            text-align: center;
            margin-bottom: 30px;
        }

        .home-title {
            font-size: 42px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 15px;
        }

        .home-subtitle {
            font-size: 20px;
            color: #666;
            margin-bottom: 40px;
        }

        .lumia-showcase {
            background: #f8f8f8;
            border-radius: 15px;
            padding: 30px;
            margin: 30px 0;
        }

        .lumia-image {
            max-width: 100%;
            height: auto;
            border-radius: 10px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.15);
        }

        .os-badges {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 30px;
            flex-wrap: wrap;
        }

        .os-badge {
            display: flex;
            align-items: center;
            gap: 10px;
            background: white;
            padding: 15px 25px;
            border-radius: 50px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
        }

        .os-badge-icon {
            width: 30px;
            height: 30px;
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
        }

        .issue-link {
            display: inline-block;
            margin-top: 15px;
            padding: 10px 25px;
            background: #f0f0f0;
            color: #667eea;
            text-decoration: none;
            border-radius: 25px;
            font-size: 14px;
            transition: all 0.3s ease;
            border: 2px solid #667eea;
        }

        .issue-link:hover {
            background: #667eea;
            color: white;
        }
    </style>
</head>
<body>
    <nav>
        <ul>
            <li><button onclick="showSection('home')" class="nav-btn active" id="btn-home">Home</button></li>
            <li><button onclick="showSection('win10')" class="nav-btn" id="btn-win10">Windows 10 ARM32</button></li>
            <li><button onclick="showSection('winrt')" class="nav-btn" id="btn-winrt">Windows RT</button></li>
            <li><button onclick="showSection('credits')" class="nav-btn" id="btn-credits">Credits</button></li>
        </ul>
    </nav>

    <div id="home" class="content active">
        <div class="card">
            <div class="home-hero">
                <h1 class="home-title">Introducing Windows on ARM</h1>
                <p class="home-subtitle">Experience Windows on your Lumia devices</p>
            </div>
            
            <div class="lumia-showcase">
                <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 800 500'%3E%3Cdefs%3E%3ClinearGradient id='grad1' x1='0%25' y1='0%25' x2='100%25' y2='100%25'%3E%3Cstop offset='0%25' style='stop-color:%23667eea;stop-opacity:1' /%3E%3Cstop offset='100%25' style='stop-color:%23764ba2;stop-opacity:1' /%3E%3C/linearGradient%3E%3C/defs%3E%3Crect width='800' height='500' fill='%23f0f0f0'/%3E%3Crect x='250' y='50' width='300' height='400' rx='20' fill='%23000' opacity='0.9'/%3E%3Crect x='260' y='80' width='280' height='340' fill='%23333'/%3E%3Crect x='270' y='90' width='260' height='150' fill='url(%23grad1)'/%3E%3Ctext x='400' y='180' font-family='Segoe UI, Arial' font-size='36' fill='white' text-anchor='middle' font-weight='bold'%3EWindows 10%3C/text%3E%3Crect x='270' y='250' width='260' height='150' fill='%2300BCF2'/%3E%3Ctext x='400' y='340' font-family='Segoe UI, Arial' font-size='36' fill='white' text-anchor='middle' font-weight='bold'%3EWindows RT%3C/text%3E%3Crect x='360' y='430' width='80' height='6' rx='3' fill='%23555'/%3E%3Ctext x='400' y='480' font-family='Segoe UI, Arial' font-size='20' fill='%23666' text-anchor='middle'%3ELumia Device%3C/text%3E%3C/svg%3E" alt="Lumia device with Windows 10 and Windows RT" class="lumia-image">
                
                <div class="os-badges">
                    <div class="os-badge">
                        <div class="os-badge-icon win10-logo"></div>
                        <span>Windows 10 ARM32</span>
                    </div>
                    <div class="os-badge">
                        <div class="os-badge-icon win81-logo"></div>
                        <span>Windows RT</span>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div id="win10" class="content">
        <div class="card">
            <div class="logo win10-logo"></div>
            <h1>Windows 10 ARM32</h1>
            <a href="https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://github.com/RedGreenBlue09/WFAv7_Installer&ved=2ahUKEwjhveGr8beSAxWsjK8BHWxQCYEQFnoECA8QAQ&usg=AOvVaw2B6mwHgs9rjImN4bOdb5R-" class="guide-link" target="_blank">View Installation Guide</a>
        </div>
    </div>

    <div id="winrt" class="content">
        <div class="card">
            <div class="logo win81-logo"></div>
            <h1>Windows RT</h1>
            <a href="https://github.com/caesarptn-dev/Windows-RT-installer-for-Lumia-devices" class="guide-link" target="_blank">View Installation Guide</a>
            <br>
            <a href="https://github.com/caesarptn-dev/Windows-RT-installer-for-Lumia-devices/issues" class="issue-link" target="_blank">Report Issues</a>
        </div>
    </div>

    <div id="credits" class="content">
        <div class="card">
            <h1>Credits</h1>
            <div class="credits-list">
                <div class="credit-item">
                    <strong>@zazabutanimator</strong>
                    <p>For website (me)</p>
                </div>
                <div class="credit-item">
                    <strong>@Redgreenblue09</strong>
                    <p>For Windows 10 ARM32</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        function showSection(section) {
            // Hide all content sections
            document.querySelectorAll('.content').forEach(content => {
                content.classList.remove('active');
            });

            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });

            // Show selected section and activate button
            document.getElementById(section).classList.add('active');
            document.getElementById('btn-' + section).classList.add('active');
        }
    </script>
</body>
</html>
