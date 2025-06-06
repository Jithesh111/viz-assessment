# viz-assessment
https://codepen.io/Jithu-J/pen/OPVmqWX

//code for viz assessment

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Employee Performance Dashboard</title>
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
            padding: 20px;
        }
        
        .dashboard {
            max-width: 1400px;
            margin: 0 auto;
        }
        
        .header {
            text-align: center;
            color: white;
            margin-bottom: 30px;
        }
        
        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .stats-overview {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .stat-card {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            color: white;
            border: 1px solid rgba(255,255,255,0.2);
        }
        
        .stat-value {
            font-size: 2rem;
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .filters {
            display: flex;
            gap: 15px;
            margin-bottom: 25px;
            flex-wrap: wrap;
        }
        
        .filter-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            background: rgba(255,255,255,0.2);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            backdrop-filter: blur(5px);
        }
        
        .filter-btn:hover, .filter-btn.active {
            background: rgba(255,255,255,0.3);
            transform: translateY(-2px);
        }
        
        .employee-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 20px;
        }
        
        .employee-card {
            background: rgba(255,255,255,0.95);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            border-left: 5px solid;
        }
        
        .employee-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0,0,0,0.2);
        }
        
        .employee-card.engineering { border-left-color: #3498db; }
        .employee-card.marketing { border-left-color: #e74c3c; }
        .employee-card.sales { border-left-color: #2ecc71; }
        
        .employee-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .employee-name {
            font-size: 1.3rem;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .employee-team {
            font-size: 0.9rem;
            color: #7f8c8d;
            background: #ecf0f1;
            padding: 4px 12px;
            border-radius: 12px;
        }
        
        .performance-score {
            text-align: center;
            margin-bottom: 20px;
        }
        
        .score-circle {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 10px;
            font-size: 1.5rem;
            font-weight: bold;
            color: white;
        }
        
        .score-excellent { background: #27ae60; }
        .score-good { background: #f39c12; }
        .score-average { background: #e74c3c; }
        
        .metrics {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
        
        .metric {
            text-align: center;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 10px;
        }
        
        .metric-value {
            font-size: 1.4rem;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 5px;
        }
        
        .metric-label {
            font-size: 0.85rem;
            color: #7f8c8d;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .efficiency-bar {
            margin-top: 15px;
            background: #ecf0f1;
            height: 8px;
            border-radius: 4px;
            overflow: hidden;
        }
        
        .efficiency-fill {
            height: 100%;
            background: linear-gradient(90deg, #3498db, #2ecc71);
            transition: width 1s ease;
        }
        
        .top-performer {
            position: relative;
            overflow: hidden;
        }
        
        .top-performer::before {
            content: '⭐';
            position: absolute;
            top: 10px;
            right: 15px;
            font-size: 1.5rem;
            animation: sparkle 2s infinite;
        }
        
        @keyframes sparkle {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.7; transform: scale(1.2); }
        }
        
        .insights {
            margin-top: 30px;
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 25px;
            color: white;
        }
        
        .insight-title {
            font-size: 1.5rem;
            margin-bottom: 15px;
            text-align: center;
        }
        
        .insight-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
        }
        
        .insight-item {
            background: rgba(255,255,255,0.1);
            padding: 15px;
            border-radius: 10px;
            border-left: 4px solid #f39c12;
        }
    </style>
</head>
<body>
    <div class="dashboard">
        <div class="header">
            <h1>Individual Employee Performance Analysis</h1>
            <p>Detailed insights for strategic decision making</p>
        </div>
        
        <div class="stats-overview">
            <div class="stat-card">
                <div class="stat-value">14</div>
                <div>Total Employees</div>
            </div>
            <div class="stat-card">
                <div class="stat-value">87.5</div>
                <div>Avg Performance</div>
            </div>
            <div class="stat-card">
                <div class="stat-value">₹102.9L</div>
                <div>Avg Budget</div>
            </div>
            <div class="stat-card">
                <div class="stat-value">4.1</div>
                <div>Avg Projects</div>
            </div>
        </div>
        
        <div class="filters">
            <button class="filter-btn active" onclick="filterEmployees('all')">All Employees</button>
            <button class="filter-btn" onclick="filterEmployees('engineering')">Engineering</button>
            <button class="filter-btn" onclick="filterEmployees('marketing')">Marketing</button>
            <button class="filter-btn" onclick="filterEmployees('sales')">Sales</button>
            <button class="filter-btn" onclick="filterEmployees('top-performers')">Top Performers (90+)</button>
        </div>
        
        <div class="employee-grid" id="employeeGrid">
            <!-- Employee cards will be generated by JavaScript -->
        </div>
        
        <div class="insights">
            <h3 class="insight-title">Key Individual Insights</h3>
            <div class="insight-grid">
                <div class="insight-item">
                    <strong>Efficiency Champions:</strong> Grace Wilson (Marketing) delivers 91 performance with only ₹80L budget - highest ROI in organization
                </div>
                <div class="insight-item">
                    <strong>Investment Mismatch:</strong> Carol Williams has highest budget (₹150L) but lowest performance (85) - needs immediate support
                </div>
                <div class="insight-item">
                    <strong>Mentoring Opportunities:</strong> Pair Bob Smith and Monica White (both 92 performance) with underperforming team members
                </div>
                <div class="insight-item">
                    <strong>Team Dynamics:</strong> Significant within-team performance gaps suggest need for process standardization and knowledge sharing
                </div>
            </div>
        </div>
    </div>

    <script>
        const employees = [
            {name: "Alice Johnson", team: "Frontend", department: "engineering", budget: 120, projects: 5, performance: 88},
            {name: "Bob Smith", team: "Frontend", department: "engineering", budget: 120, projects: 5, performance: 92},
            {name: "Carol Williams", team: "Backend", department: "engineering", budget: 150, projects: 6, performance: 85},
            {name: "David Brown", team: "Backend", department: "engineering", budget: 150, projects: 6, performance: 90},
            {name: "Eva Davis", team: "DevOps", department: "engineering", budget: 100, projects: 4, performance: 87},
            {name: "Frank Miller", team: "DevOps", department: "engineering", budget: 100, projects: 4, performance: 89},
            {name: "Grace Wilson", team: "Content", department: "marketing", budget: 80, projects: 3, performance: 91},
            {name: "Henry Moore", team: "Content", department: "marketing", budget: 80, projects: 3, performance: 86},
            {name: "Irene Taylor", team: "SEO", department: "marketing", budget: 70, projects: 2, performance: 88},
            {name: "Jack Anderson", team: "SEO", department: "marketing", budget: 70, projects: 2, performance: 84},
            {name: "Karen Thomas", team: "Domestic", department: "sales", budget: 90, projects: 4, performance: 90},
            {name: "Larry Jackson", team: "Domestic", department: "sales", budget: 90, projects: 4, performance: 85},
            {name: "Monica White", team: "International", department: "sales", budget: 110, projects: 5, performance: 92},
            {name: "Nathan Harris", team: "International", department: "sales", budget: 110, projects: 5, performance: 89}
        ];

        function getScoreClass(score) {
            if (score >= 90) return 'score-excellent';
            if (score >= 87) return 'score-good';
            return 'score-average';
        }

        function getEfficiency(employee) {
            return Math.round((employee.performance / employee.budget) * 100);
        }

        function isTopPerformer(performance) {
            return performance >= 90;
        }

        function createEmployeeCard(employee) {
            const efficiency = getEfficiency(employee);
            const efficiencyPercent = Math.min(efficiency, 100);
            
            return `
                <div class="employee-card ${employee.department} ${isTopPerformer(employee.performance) ? 'top-performer' : ''}" data-department="${employee.department}" data-performance="${employee.performance}">
                    <div class="employee-header">
                        <div class="employee-name">${employee.name}</div>
                        <div class="employee-team">${employee.team}</div>
                    </div>
                    
                    <div class="performance-score">
                        <div class="score-circle ${getScoreClass(employee.performance)}">
                            ${employee.performance}
                        </div>
                        <div>Performance Score</div>
                    </div>
                    
                    <div class="metrics">
                        <div class="metric">
                            <div class="metric-value">₹${employee.budget}L</div>
                            <div class="metric-label">Budget</div>
                        </div>
                        <div class="metric">
                            <div class="metric-value">${employee.projects}</div>
                            <div class="metric-label">Projects</div>
                        </div>
                    </div>
                    
                    <div class="efficiency-bar">
                        <div class="efficiency-fill" style="width: ${efficiencyPercent}%"></div>
                    </div>
                    <div style="text-align: center; margin-top: 5px; font-size: 0.85rem; color: #7f8c8d;">
                        Efficiency: ${efficiency}% (Performance/Budget)
                    </div>
                </div>
            `;
        }

        function renderEmployees(employeesToRender = employees) {
            const grid = document.getElementById('employeeGrid');
            grid.innerHTML = employeesToRender.map(createEmployeeCard).join('');
        }

        function filterEmployees(filter) {
            // Update active button
            document.querySelectorAll('.filter-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
            
            let filtered = employees;
            
            switch(filter) {
                case 'engineering':
                    filtered = employees.filter(emp => emp.department === 'engineering');
                    break;
                case 'marketing':
                    filtered = employees.filter(emp => emp.department === 'marketing');
                    break;
                case 'sales':
                    filtered = employees.filter(emp => emp.department === 'sales');
                    break;
                case 'top-performers':
                    filtered = employees.filter(emp => emp.performance >= 90);
                    break;
            }
            
            renderEmployees(filtered);
        }

        // Initial render
        renderEmployees();
    </script>
</body>
</html>

