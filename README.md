<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Orario Scolastico 1KB/IE</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            overflow-x: auto;
        }
        
        .container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            max-width: 1400px;
            width: 100%;
        }
        
        h1 {
            text-align: center;
            color: #2d3748;
            margin-bottom: 30px;
            font-size: 2.5em;
            text-transform: uppercase;
            letter-spacing: 3px;
            position: relative;
            overflow: hidden;
        }
        
        h1::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 4px;
            background: linear-gradient(90deg, #667eea, #764ba2);
            border-radius: 2px;
        }
        
        .timetable {
            display: grid;
            grid-template-columns: 80px repeat(6, 1fr);
            gap: 3px;
            background: #e2e8f0;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }
        
        .header-cell {
            background: #2d3748;
            color: white;
            padding: 15px 10px;
            text-align: center;
            font-weight: 700;
            font-size: 0.9em;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        .time-cell {
            background: #4a5568;
            color: white;
            padding: 15px 5px;
            text-align: center;
            font-weight: 600;
            font-size: 0.85em;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .subject-cell {
            padding: 12px 8px;
            text-align: center;
            font-size: 0.85em;
            min-height: 80px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            opacity: 0;
            transform: translateY(20px);
            animation: fadeInUp 0.5s forwards;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .subject-cell:hover {
            transform: scale(1.05);
            z-index: 10;
            box-shadow: 0 5px 20px rgba(0,0,0,0.2);
        }
        
        .subject-cell::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            transition: left 0.5s;
        }
        
        .subject-cell:hover::before {
            left: 100%;
        }
        
        @keyframes fadeInUp {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .subject-name {
            font-weight: 700;
            font-size: 1.1em;
            margin-bottom: 4px;
        }
        
        .teacher {
            font-size: 0.85em;
            opacity: 0.9;
            margin-bottom: 2px;
        }
        
        .room {
            font-size: 0.8em;
            font-weight: 600;
            opacity: 0.8;
        }
        
        /* Subject Colors */
        .scienze-terra { background: #e0f2fe; color: #0369a1; }
        .fisica { background: #dbeafe; color: #1e40af; }
        .matematica { background: #fecaca; color: #991b1b; }
        .italiano { background: #fef3c7; color: #92400e; }
        .inglese { background: #e9d5ff; color: #6b21a8; }
        .storia { background: #fce7f3; color: #9d174d; }
        .diritto { background: #fef9c3; color: #854d0e; }
        .chimica { background: #ddd6fe; color: #5b21b6; }
        .geografia { background: #d1d5db; color: #374151; }
        .religione { background: #fef3c7; color: #92400e; }
        .sport { background: #bbf7d0; color: #166534; }
        .lab { background: #c7d2fe; color: #3730a3; }
        .info { background: #fed7aa; color: #9a3412; }
        .ttrg { background: #99f6e4; color: #0f766e; }
        
        .empty {
            background: #f7fafc;
        }
        
        .controls {
            margin-top: 20px;
            text-align: center;
        }
        
        button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            font-size: 1em;
            cursor: pointer;
            margin: 0 10px;
            transition: transform 0.2s, box-shadow 0.2s;
            font-weight: 600;
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(102, 126, 234, 0.4);
        }
        
        .legend {
            margin-top: 20px;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 10px;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
            font-size: 0.85em;
            padding: 5px 10px;
            background: #f7fafc;
            border-radius: 15px;
            border: 1px solid #e2e8f0;
        }
        
        .legend-color {
            width: 15px;
            height: 15px;
            border-radius: 3px;
        }
        
        @media (max-width: 1200px) {
            .timetable {
                font-size: 0.8em;
            }
            .subject-cell {
                min-height: 60px;
                padding: 8px 4px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>1KB/IE - Orario Scolastico</h1>
        
        <div class="timetable" id="timetable">
            <!-- Header Row -->
            <div class="header-cell">Ore</div>
            <div class="header-cell">Lunedì</div>
            <div class="header-cell">Martedì</div>
            <div class="header-cell">Mercoledì</div>
            <div class="header-cell">Giovedì</div>
            <div class="header-cell">Venerdì</div>
            <div class="header-cell">Sabato</div>
            
            <!-- 8:10 Row -->
            <div class="time-cell">8:10</div>
            <div class="subject-cell scienze-terra" style="animation-delay: 0.1s">
                <div class="subject-name">Scienze d. Terra</div>
                <div class="teacher">Ianniciello M.</div>
                <div class="room">LAS</div>
            </div>
            <div class="subject-cell ttrg" style="animation-delay: 0.2s">
                <div class="subject-name">TTRG_Lab</div>
                <div class="teacher">Gatti G.<br>Ventavoli V.</div>
                <div class="room">D3</div>
            </div>
            <div class="subject-cell chimica" style="animation-delay: 0.3s">
                <div class="subject-name">Chimica_Lab</div>
                <div class="teacher">La Gamma V.<br>Toscani S.</div>
                <div class="room">LAC-B SX - turno 2-<br>R13 - TURNO 1 -</div>
            </div>
            <div class="subject-cell matematica" style="animation-delay: 0.4s">
                <div class="subject-name">Matematica</div>
                <div class="teacher">Bozzi G.</div>
                <div class="room">P20</div>
            </div>
            <div class="subject-cell chimica" style="animation-delay: 0.5s">
                <div class="subject-name">Chimica</div>
                <div class="teacher">Toscani S.</div>
                <div class="room">P 6</div>
            </div>
            <div class="subject-cell fisica" style="animation-delay: 0.6s">
                <div class="subject-name">Fisica_Lab</div>
                <div class="teacher">Battiatо V.<br>Pasquale S.</div>
                <div class="room">LAF</div>
            </div>
            
            <!-- 9:10 Row -->
            <div class="time-cell">9:10</div>
            <div class="subject-cell fisica" style="animation-delay: 0.7s">
                <div class="subject-name">Fisica</div>
                <div class="teacher">Battiatо V.</div>
                <div class="room">P 6</div>
            </div>
            <div class="subject-cell diritto" style="animation-delay: 0.8s">
                <div class="subject-name">Diritto</div>
                <div class="teacher">Grande M.</div>
                <div class="room">P 9</div>
            </div>
            <div class="subject-cell scienze-terra" style="animation-delay: 0.9s">
                <div class="subject-name">Scienze d. Terra</div>
                <div class="teacher">Ianniciello M.</div>
                <div class="room">P 1</div>
            </div>
            <div class="subject-cell matematica" style="animation-delay: 1.0s">
                <div class="subject-name">Matematica</div>
                <div class="teacher">Bozzi G.</div>
                <div class="room">P20</div>
            </div>
            <div class="subject-cell storia" style="animation-delay: 1.1s">
                <div class="subject-name">Storia</div>
                <div class="teacher">Zuccherini S.</div>
                <div class="room">S 9</div>
            </div>
            <div class="subject-cell inglese" style="animation-delay: 1.2s">
                <div class="subject-name">Inglese</div>
                <div class="teacher">Galazzo E.</div>
                <div class="room">S 5</div>
            </div>
            
            <!-- 10:10 Row -->
            <div class="time-cell">10:10</div>
            <div class="subject-cell matematica" style="animation-delay: 1.3s">
                <div class="subject-name">Matematica</div>
                <div class="teacher">Bozzi G.</div>
                <div class="room">P19</div>
            </div>
            <div class="subject-cell italiano" style="animation-delay: 1.4s">
                <div class="subject-name">Italiano</div>
                <div class="teacher">Zuccherini S.</div>
                <div class="room">S21</div>
            </div>
            <div class="subject-cell inglese" style="animation-delay: 1.5s">
                <div class="subject-name">Inglese</div>
                <div class="teacher">Galazzo E.</div>
                <div class="room">S 3 - Lab. Ling.</div>
            </div>
            <div class="subject-cell chimica" style="animation-delay: 1.6s">
                <div class="subject-name">Chimica</div>
                <div class="teacher">Toscani S.</div>
                <div class="room">P 7</div>
            </div>
            <div class="subject-cell storia" style="animation-delay: 1.7s">
                <div class="subject-name">Storia</div>
                <div class="teacher">Zuccherini S.</div>
                <div class="room">S 9</div>
            </div>
            <div class="subject-cell ttrg" style="animation-delay: 1.8s">
                <div class="subject-name">TTRG (Dis. e Tecn.)</div>
                <div class="teacher">Gatti G.</div>
                <div class="room">D2</div>
            </div>
            
            <!-- 11:10 Row -->
            <div class="time-cell">11:10</div>
            <div class="subject-cell italiano" style="animation-delay: 1.9s">
                <div class="subject-name">Italiano</div>
                <div class="teacher">Zuccherini S.</div>
                <div class="room">S 9</div>
            </div>
            <div class="subject-cell matematica" style="animation-delay: 2.0s">
                <div class="subject-name">Matematica</div>
                <div class="teacher">Bozzi G.</div>
                <div class="room">P19</div>
            </div>
            <div class="subject-cell diritto" style="animation-delay: 2.1s">
                <div class="subject-name">Diritto</div>
                <div class="teacher">Grande M.</div>
                <div class="room">P10</div>
            </div>
            <div class="subject-cell italiano" style="animation-delay: 2.2s">
                <div class="subject-name">Italiano</div>
                <div class="teacher">Zuccherini S.</div>
                <div class="room">S21</div>
            </div>
            <div class="subject-cell inglese" style="animation-delay: 2.3s">
                <div class="subject-name">Inglese</div>
                <div class="teacher">Galazzo E.</div>
                <div class="room">S 8</div>
            </div>
            <div class="empty"></div>
            
            <!-- 12:10 Row -->
            <div class="time-cell">12:10</div>
            <div class="subject-cell sport" style="animation-delay: 2.4s">
                <div class="subject-name">Sc. Motorie e Sport.</div>
                <div class="teacher">Bertuccelli A.</div>
                <div class="room">T3_ex PLATFORM</div>
            </div>
            <div class="subject-cell fisica" style="animation-delay: 2.5s">
                <div class="subject-name">Fisica</div>
                <div class="teacher">Battiatо V.</div>
                <div class="room">P 5</div>
            </div>
            <div class="subject-cell info" style="animation-delay: 2.6s">
                <div class="subject-name">Inf_Biennio_Lab</div>
                <div class="teacher">Agostini N.<br>Nesti L.</div>
                <div class="room">LAINB</div>
            </div>
            <div class="empty"></div>
            <div class="subject-cell geografia" style="animation-delay: 2.7s">
                <div class="subject-name">Geografia</div>
                <div class="teacher">Panichi S.</div>
                <div class="room">R15</div>
            </div>
            <div class="empty"></div>
            
            <!-- 13:00 Row -->
            <div class="time-cell">13:00</div>
            <div class="empty"></div>
            <div class="empty"></div>
            <div class="empty"></div>
            <div class="subject-cell info" style="animation-delay: 2.8s">
                <div class="subject-name">Inf_Biennio</div>
                <div class="teacher">Agostini N.</div>
                <div class="room">R 9</div>
            </div>
            <div class="subject-cell religione" style="animation-delay: 2.9s">
                <div class="subject-name">IRC Religione</div>
                <div class="teacher">Scamarcio N.</div>
                <div class="room">P12</div>
            </div>
            <div class="empty"></div>
        </div>
        
        <div class="controls">
            <button onclick="animateTimetable()">Rianima Orario</button>
            <button onclick="toggleHighlight()">Evidenzia Oggi</button>
        </div>
        
        <div class="legend">
            <div class="legend-item"><div class="legend-color" style="background: #e0f2fe;"></div>Scienze</div>
            <div class="legend-item"><div class="legend-color" style="background: #dbeafe;"></div>Fisica</div>
            <div class="legend-item"><div class="legend-color" style="background: #fecaca;"></div>Matematica</div>
            <div class="legend-item"><div class="legend-color" style="background: #fef3c7;"></div>Italiano</div>
            <div class="legend-item"><div class="legend-color" style="background: #e9d5ff;"></div>Inglese</div>
            <div class="legend-item"><div class="legend-color" style="background: #fce7f3;"></div>Storia</div>
            <div class="legend-item"><div class="legend-color" style="background: #fef9c3;"></div>Diritto</div>
            <div class="legend-item"><div class="legend-color" style="background: #ddd6fe;"></div>Chimica</div>
            <div class="legend-item"><div class="legend-color" style="background: #bbf7d0;"></div>Sport</div>
            <div class="legend-item"><div class="legend-color" style="background: #99f6e4;"></div>TTRG</div>
        </div>
    </div>
    
    <script>
        function animateTimetable() {
            const cells = document.querySelectorAll('.subject-cell');
            cells.forEach(cell => {
                cell.style.animation = 'none';
                setTimeout(() => {
                    cell.style.animation = '';
                }, 10);
            });
        }
        
        function toggleHighlight() {
            const today = new Date().getDay(); // 0 = Sunday, 1 = Monday, etc.
            const dayIndex = today === 0 ? 6 : today - 1; // Convert to our grid (0 = Monday)
            
            const cells = document.querySelectorAll('.subject-cell');
            cells.forEach((cell, index) => {
                const col = index % 6;
                if (col === dayIndex) {
                    cell.style.transform = 'scale(1.05)';
                    cell.style.boxShadow = '0 0 20px rgba(102, 126, 234, 0.6)';
                    cell.style.zIndex = '20';
                } else {
                    cell.style.transform = '';
                    cell.style.boxShadow = '';
                    cell.style.zIndex = '';
                }
            });
        }
        
        // Add click effect to cells
        document.querySelectorAll('.subject-cell').forEach(cell => {
            cell.addEventListener('click', function() {
                this.style.transform = 'scale(0.95)';
                setTimeout(() => {
                    this.style.transform = '';
                }, 150);
            });
        });
    </script>
</body>
</html>
