<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Quiz NTICx - Seguridad Digital</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
            overflow-x: hidden;
            position: relative;
        }

        /* Fondo animado para móvil */
        .mobile-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
            background-size: 400% 400%;
            animation: gradientShift 8s ease infinite;
            z-index: -1;
        }

        .container {
            width: 100%;
            min-height: 100vh;
            padding: 0;
            display: flex;
            flex-direction: column;
        }

        /* Header optimizado para móvil */
        .mobile-header {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            padding: 1rem;
            box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo-section {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .logo {
            width: 45px;
            height: 45px;
            background: linear-gradient(135deg, #4CAF50, #45a049);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.2rem;
        }

        .header-info h1 {
            font-size: 1.3rem;
            color: #2c3e50;
            font-weight: 700;
        }

        .header-info p {
            color: #666;
            font-size: 0.75rem;
        }

        .timer-display {
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            color: white;
            padding: 0.75rem 1rem;
            border-radius: 20px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
        }

        .timer {
            font-size: 1.5rem;
            font-weight: bold;
        }

        .timer-label {
            font-size: 0.7rem;
            opacity: 0.9;
        }

        /* Card principal optimizada para móvil */
        .mobile-card {
            flex: 1;
            background: rgba(255, 255, 255, 0.95);
            margin: 1rem;
            border-radius: 25px;
            padding: 1.5rem;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(20px);
            display: flex;
            flex-direction: column;
        }

        /* Formulario de registro móvil */
        .registration-form {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .form-group label {
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: #2c3e50;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.95rem;
        }

        .form-group input, 
        .form-group select {
            width: 100%;
            padding: 1rem;
            border: 2px solid #e0e0e0;
            border-radius: 15px;
            font-size: 1.1rem;
            background: rgba(255, 255, 255, 0.9);
            transition: all 0.3s ease;
        }

        .form-group input:focus, 
        .form-group select:focus {
            outline: none;
            border-color: #4CAF50;
            box-shadow: 0 0 0 3px rgba(76, 175, 80, 0.1);
            transform: scale(1.02);
        }

        /* Botón de inicio optimizado */
        .start-btn {
            background: linear-gradient(135deg, #4CAF50, #45a049);
            color: white;
            border: none;
            padding: 1.25rem 2rem;
            font-size: 1.3rem;
            font-weight: bold;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.75rem;
            margin: 1.5rem 0;
            box-shadow: 0 8px 25px rgba(76, 175, 80, 0.3);
            width: 100%;
        }

        .start-btn:active {
            transform: scale(0.98);
        }

        /* Progreso móvil */
        .progress-section {
            background: white;
            border-radius: 20px;
            padding: 1rem;
            margin: 0.5rem;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
        }

        .progress-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.75rem;
            flex-wrap: wrap;
            gap: 0.5rem;
        }

        .score-display {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .score-icon {
            width: 35px;
            height: 35px;
            background: linear-gradient(135deg, #FFD700, #FFA500);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 0.9rem;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e0e0e0;
            border-radius: 4px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4CAF50, #2196F3);
            border-radius: 4px;
            transition: width 0.5s ease;
        }

        /* Pregunta optimizada para móvil */
        .question-container {
            flex: 1;
            display: flex;
            flex-direction: column;
        }

        .question-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
            flex-wrap: wrap;
            gap: 0.5rem;
        }

        .question-number {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            font-weight: bold;
            font-size: 0.85rem;
        }

        .difficulty-badge {
            padding: 0.3rem 0.8rem;
            border-radius: 15px;
            font-size: 0.75rem;
            font-weight: bold;
            text-transform: uppercase;
        }

        .difficulty-facil { background: #d4edda; color: #155724; }
        .difficulty-medio { background: #fff3cd; color: #856404; }
        .difficulty-dificil { background: #f8d7da; color: #721c24; }

        .category-badge {
            background: linear-gradient(135deg, #17a2b8, #138496);
            color: white;
            padding: 0.3rem 0.8rem;
            border-radius: 15px;
            font-size: 0.75rem;
            font-weight: bold;
        }

        .question-text {
            font-size: 1.3rem;
            font-weight: 600;
            color: #2c3e50;
            margin-bottom: 1.5rem;
            line-height: 1.5;
            text-align: left;
        }

        /* Opciones optimizadas para táctil */
        .options {
            flex: 1;
            display: flex;
            flex-direction: column;
            gap: 0.75rem;
            margin-bottom: 1.5rem;
        }

        .option {
            background: white;
            border: 3px solid #e0e0e0;
            border-radius: 18px;
            padding: 1.25rem 1rem;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            align-items: center;
            gap: 1rem;
            min-height: 65px;
            position: relative;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
        }

        .option:active {
            transform: scale(0.98);
        }

        .option-letter {
            width: 40px;
            height: 40px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 1.1rem;
            flex-shrink: 0;
        }

        .option-text {
            flex: 1;
            font-size: 1.1rem;
            line-height: 1.4;
        }

        .option.selected {
            border-color: #4CAF50;
            background: rgba(76, 175, 80, 0.1);
            transform: scale(1.02);
            box-shadow: 0 4px 20px rgba(76, 175, 80, 0.2);
        }

        .option.selected .option-letter {
            background: linear-gradient(135deg, #4CAF50, #45a049);
        }

        .option.correct {
            border-color: #4CAF50;
            background: linear-gradient(135deg, #d4edda, #c3e6cb);
            animation: correctPulse 0.6s ease;
        }

        .option.incorrect {
            border-color: #f44336;
            background: linear-gradient(135deg, #f8d7da, #f5c6cb);
            animation: shake 0.6s ease;
        }

        /* Navegación móvil */
        .mobile-navigation {
            background: white;
            padding: 1rem;
            border-top: 1px solid #e0e0e0;
            position: sticky;
            bottom: 0;
            display: flex;
            gap: 0.75rem;
        }

        .nav-btn {
            flex: 1;
            padding: 1rem;
            border: none;
            border-radius: 15px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            min-height: 50px;
        }

        .nav-btn:active {
            transform: scale(0.95);
        }

        .prev-btn {
            background: linear-gradient(135deg, #6c757d, #5a6268);
            color: white;
        }

        .next-btn {
            background: linear-gradient(135deg, #007bff, #0056b3);
            color: white;
        }

        .submit-btn {
            background: linear-gradient(135deg, #28a745, #1e7e34);
            color: white;
        }

        .nav-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        /* Modal de resultados móvil */
        .results-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 1rem;
            opacity: 0;
            visibility: hidden;
            transition: all 0.4s ease;
        }

        .results-modal.active {
            opacity: 1;
            visibility: visible;
        }

        .results-content {
            background: white;
            border-radius: 25px;
            padding: 2rem;
            text-align: center;
            width: 100%;
            max-width: 400px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            transform: scale(0.8);
            transition: transform 0.4s ease;
        }

        .results-modal.active .results-content {
            transform: scale(1);
        }

        .results-icon {
            font-size: 4rem;
            margin-bottom: 1rem;
        }

        .results-title {
            font-size: 1.8rem;
            font-weight: bold;
            margin-bottom: 1rem;
            color: #2c3e50;
        }

        .final-score {
            font-size: 3rem;
            font-weight: bold;
            background: linear-gradient(135deg, #FFD700, #FFA500);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 1rem;
        }

        /* Panel profesor móvil */
        .teacher-access {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: rgba(0, 0, 0, 0.8);
            color: white;
            padding: 0.75rem;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            backdrop-filter: blur(10px);
            transition: all 0.3s ease;
            z-index: 200;
        }

        .teacher-access:active {
            transform: scale(0.9);
        }

        /* Vista admin móvil */
        .admin-view {
            background: #f8f9fa;
            min-height: 100vh;
            padding: 1rem;
        }

        .admin-header {
            background: white;
            padding: 1.5rem;
            border-radius: 20px;
            margin-bottom: 1rem;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
        }

        .admin-header h1 {
            font-size: 1.5rem;
            margin-bottom: 0.5rem;
        }

        .export-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
            margin-top: 1rem;
        }

        .export-btn {
            background: linear-gradient(135deg, #17a2b8, #138496);
            color: white;
            border: none;
            padding: 0.75rem 1rem;
            border-radius: 12px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.9rem;
            flex: 1;
            min-width: 120px;
            transition: all 0.2s ease;
        }

        .export-btn:active {
            transform: scale(0.95);
        }

        .students-grid {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .student-card {
            background: white;
            border-radius: 15px;
            padding: 1.25rem;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            border-left: 4px solid #4CAF50;
        }

        .student-info {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.75rem;
        }

        .student-name {
            font-weight: bold;
            font-size: 1.1rem;
        }

        .student-score {
            font-size: 1.5rem;
            font-weight: bold;
            color: #4CAF50;
        }

        .student-details {
            color: #666;
            font-size: 0.9rem;
            line-height: 1.4;
        }

        /* Instrucciones móvil */
        .instructions-card {
            background: #e3f2fd;
            padding: 1.25rem;
            border-radius: 18px;
            margin-top: 1.5rem;
            border-left: 4px solid #2196F3;
        }

        .instructions-card h4 {
            color: #1976d2;
            margin-bottom: 0.75rem;
            font-size: 1.1rem;
        }

        .instructions-card ul {
            color: #1565c0;
            line-height: 1.6;
            padding-left: 1.25rem;
        }

        .instructions-card li {
            margin-bottom: 0.5rem;
        }

        /* Utilidades */
        .hidden { display: none !important; }

        /* Animaciones */
        @keyframes gradientShift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        @keyframes correctPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.02); }
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-3px); }
            75% { transform: translateX(3px); }
        }

        /* Loading spinner */
        .loading {
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 2rem;
        }

        .spinner {
            width: 40px;
            height: 40px;
            border: 4px solid #f3f3f3;
            border-top: 4px solid #4CAF50;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Vibración táctil (para dispositivos compatibles) */
        .vibrate:active {
            animation: vibrate 0.1s ease;
        }

        @keyframes vibrate {
            0%, 100% { transform: translate(0); }
            20% { transform: translate(-1px, 1px); }
            40% { transform: translate(-1px, -1px); }
            60% { transform: translate(1px, 1px); }
            80% { transform: translate(1px, -1px); }
        }

        /* Optimizaciones adicionales para móvil */
        input[type="text"], input[type="email"], select {
            -webkit-appearance: none;
            -moz-appearance: none;
            appearance: none;
        }

        select {
            background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='currentColor' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6,9 12,15 18,9'%3e%3c/polyline%3e%3c/svg%3e");
            background-repeat: no-repeat;
            background-position: right 1rem center;
            background-size: 1rem;
            padding-right: 3rem;
        }

        /* Estilos para orientación landscape en móvil */
        @media screen and (orientation: landscape) and (max-height: 500px) {
            .mobile-header {
                padding: 0.5rem 1rem;
            }
            
            .timer {
                font-size: 1.2rem;
            }
            
            .question-text {
                font-size: 1.1rem;
                margin-bottom: 1rem;
            }
            
            .option {
                min-height: 50px;
                padding: 1rem;
            }
        }

        /* Dark mode para pantallas OLED */
        @media (prefers-color-scheme: dark) {
            .mobile-card {
                background: rgba(30, 30, 30, 0.95);
                color: #e0e0e0;
            }
            
            .option {
                background: rgba(50, 50, 50, 0.9);
                color: #e0e0e0;
                border-color: #555;
            }
            
            .question-text {
                color: #e0e0e0;
            }
        }
    </style>
</head>
<body>
    <div class="mobile-bg"></div>
    
    <div class="container">
        <!-- Header móvil -->
        <div class="mobile-header">
            <div class="header-content">
                <div class="logo-section">
                    <div class="logo">
                        <i class="fas fa-graduation-cap"></i>
                    </div>
                    <div class="header-info">
                        <h1>Quiz NTICx</h1>
                        <p>Seguridad Digital - PBA</p>
                    </div>
                </div>
                <div class="timer-display" id="timer-display" style="display: none;">
                    <div class="timer" id="timer">30:00</div>
                    <div class="timer-label">restante</div>
                </div>
            </div>
        </div>

        <!-- Pantalla de registro -->
        <div class="mobile-card" id="registration-section">
            <h2 style="text-align: center; margin-bottom: 1.5rem; color: #2c3e50; font-size: 1.6rem;">
                <i class="fas fa-user-graduate"></i> Registro de Estudiante
            </h2>
            
            <div class="registration-form">
                <div class="form-group">
                    <label for="nombre">
                        <i class="fas fa-user"></i> Nombre
                    </label>
                    <input type="text" id="nombre" placeholder="Tu nombre" required>
                </div>
                
                <div class="form-group">
                    <label for="apellido">
                        <i class="fas fa-user"></i> Apellido
                    </label>
                    <input type="text" id="apellido" placeholder="Tu apellido" required>
                </div>
                
                <div class="form-group">
                    <label for="escuela">
                        <i class="fas fa-school"></i> Escuela
                    </label>
                    <input type="text" id="escuela" placeholder="Ej: EEST N° 1 - San Martín" required>
                </div>
                
                <div class="form-group">
                    <label for="curso">
                        <i class="fas fa-users"></i> Curso
                    </label>
                    <select id="curso" required>
                        <option value="">Seleccionar curso</option>
                        <option value="4° 1°">4° 1°</option>
                        <option value="4° 2°">4° 2°</option>
                        <option value="4° 3°">4° 3°</option>
                        <option value="4° 4°">4° 4°</option>
                        <option value="4° 5°">4° 5°</option>
                        <option value="5° 1°">5° 1°</option>
                        <option value="5° 2°">5° 2°</option>
                        <option value="5° 3°">5° 3°</option>
                        <option value="5° 4°">5° 4°</option>
                        <option value="5° 5°">5° 5°</option>
                        <option value="6° 1°">6° 1°</option>
                        <option value="6° 2°">6° 2°</option>
                        <option value="6° 3°">6° 3°</option>
                        <option value="6° 4°">6° 4°</option>
                        <option value="6° 5°">6° 5°</option>
                    </select>
                </div>
            </div>
            
            <button class="start-btn vibrate" onclick="startQuiz()">
                <i class="fas fa-play"></i>
                Comenzar Quiz
            </button>
            
            <div class="instructions-card">
                <h4>
                    <i class="fas fa-info-circle"></i> Instrucciones
                </h4>
                <ul>
                    <li>Tenés <strong>30 minutos</strong> para completar el quiz</li>
                    <li>Son <strong>25 preguntas</strong> sobre seguridad digital</li>
                    <li>Cada respuesta correcta suma <strong>4 puntos</strong></li>
                    <li>Podés navegar entre preguntas</li>
                    <li>Al finalizar, enviás automáticamente al profesor</li>
                </ul>
            </div>
        </div>

        <!-- Barra de progreso -->
        <div class="progress-section hidden" id="progress-section">
            <div class="progress-header">
                <div class="score-display">
                    <div class="score-icon">
                        <i class="fas fa-star"></i>
                    </div>
                    <div>
                        <div style="font-weight: bold;">Puntaje: <span id="current-score">0</span>/100</div>
                        <div style="font-size: 0.85rem; color: #666;">
                            Pregunta <span id="question-counter">1</span> de 25
                        </div>
                    </div>
                </div>
                <div id="student-info" style="text-align: right; font-size: 0.85rem; color: #666;"></div>
            </div>
            <div class="progress-bar">
                <div class="progress-fill" id="progress-fill" style="width: 4%;"></div>
            </div>
        </div>

        <!-- Quiz container -->
        <div class="mobile-card hidden" id="quiz-section">
            <div class="question-container">
                <div class="question-header">
                    <div class="question-number" id="question-number">
                        Pregunta 1/25
                    </div>
                    <div style="display: flex; gap: 0.5rem;">
                        <div class="difficulty-badge" id="difficulty-badge">Medio</div>
                        <div class="category-badge" id="category-badge">Categoría</div>
                    </div>
                </div>
                
                <div class="question-text" id="question-text">
                    <!-- Pregunta se carga aquí -->
                </div>
                
                <div class="options" id="options-container">
                    <!-- Opciones se cargan aquí -->
                </div>
            </div>
        </div>
    </div>

    <!-- Navegación móvil fija -->
    <div class="mobile-navigation hidden" id="navigation">
        <button class="nav-btn prev-btn vibrate" onclick="previousQuestion()" id="prev-btn" disabled>
            <i class="fas fa-chevron-left"></i> Anterior
        </button>
        
        <button class="nav-btn next-btn vibrate" onclick="nextQuestion()" id="next-btn">
            Siguiente <i class="fas fa-chevron-right"></i>
        </button>
        
        <button class="nav-btn submit-btn vibrate hidden" onclick="finishQuiz()" id="submit-btn">
            <i class="fas fa-check"></i> Finalizar
        </button>
    </div>

    <!-- Acceso profesor -->
    <div class="teacher-access" onclick="showTeacherView()">
        <i class="fas fa-chalkboard-teacher"></i>
    </div>

    <!-- Modal de resultados -->
    <div class="results-modal" id="results-modal">
        <div class="results-content">
            <div class="results-icon" id="results-icon">🎉</div>
            <h2 class="results-title">¡Quiz Completado!</h2>
            <div class="final-score" id="final-score">0/100</div>
            <p id="results-message">¡Excelente trabajo!</p>
            <div style="margin-top: 2rem;">
                <button class="start-btn vibrate" onclick="resetQuiz()">
                    <i class="fas fa-redo"></i> Intentar de Nuevo
                </button>
            </div>
        </div>
