<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2025年Q4主播综合分析</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2.0.0"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
            padding: 20px;
        }
        
        .container {
            max-width: 1600px;
            margin: 0 auto;
            background: white;
            border-radius: 12px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
            padding: 30px;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px solid #eaeaea;
        }
        
        h1 {
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 32px;
        }
        
        .subtitle {
            color: #7f8c8d;
            font-size: 18px;
            font-weight: 500;
        }
        
        .summary-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }
        
        .summary-card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            text-align: center;
            transition: transform 0.3s ease;
        }
        
        .summary-card:hover {
            transform: translateY(-5px);
        }
        
        .card-title {
            font-size: 16px;
            color: #7f8c8d;
            margin-bottom: 10px;
        }
        
        .card-value {
            font-size: 24px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .card-value.good { color: #2ecc71; }
        .card-value.warning { color: #f39c12; }
        .card-value.bad { color: #e74c3c; }
        
        .tabs-container {
            display: flex;
            margin-bottom: 30px;
            border-bottom: 1px solid #eaeaea;
            flex-wrap: wrap;
        }
        
        .tab {
            padding: 12px 24px;
            background: none;
            border: none;
            font-size: 16px;
            cursor: pointer;
            color: #7f8c8d;
            border-bottom: 3px solid transparent;
            transition: all 0.3s ease;
            white-space: nowrap;
        }
        
        .tab:hover {
            color: #3498db;
        }
        
        .tab.active {
            color: #3498db;
            border-bottom-color: #3498db;
            font-weight: 600;
        }
        
        .tab-content {
            display: none;
            animation: fadeIn 0.5s ease;
        }
        
        .tab-content.active {
            display: block;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .chart-section {
            margin-bottom: 40px;
        }
        
        .section-title {
            font-size: 22px;
            color: #2c3e50;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #3498db;
        }
        
        .charts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(600px, 1fr));
            gap: 30px;
            margin-bottom: 40px;
        }
        
        @media (max-width: 768px) {
            .charts-grid {
                grid-template-columns: 1fr;
            }
        }
        
        .chart-container {
            background: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.05);
            border: 1px solid #eee;
        }
        
        .chart-title {
            font-size: 18px;
            color: #2c3e50;
            margin-bottom: 15px;
            font-weight: 600;
        }
        
        .chart-wrapper {
            position: relative;
            height: 350px;
        }
        
        .sales-charts {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 40px;
        }
        
        @media (max-width: 1200px) {
            .sales-charts {
                grid-template-columns: 1fr;
            }
        }
        
        .legend-container {
            display: flex;
            justify-content: center;
            margin-top: 20px;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            margin-right: 20px;
        }
        
        .legend-color {
            width: 16px;
            height: 16px;
            border-radius: 3px;
            margin-right: 8px;
        }
        
        .type-badge {
            display: inline-block;
            padding: 4px 10px;
            border-radius: 12px;
            font-size: 12px;
            font-weight: 600;
        }
        
        .type-fulltime {
            background-color: rgba(52, 152, 219, 0.1);
            color: #3498db;
        }
        
        .type-parttime {
            background-color: rgba(46, 204, 113, 0.1);
            color: #2ecc71;
        }
        
        .data-table-container {
            overflow-x: auto;
            margin-top: 40px;
        }
        
        .data-table {
            width: 100%;
            border-collapse: collapse;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.05);
            border-radius: 8px;
            overflow: hidden;
        }
        
        .data-table th {
            background-color: #3498db;
            color: white;
            font-weight: 600;
            padding: 15px;
            text-align: left;
            position: sticky;
            top: 0;
        }
        
        .data-table tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        
        .data-table tr:hover {
            background-color: #f1f8ff;
        }
        
        .data-table td {
            padding: 12px 15px;
            border-bottom: 1px solid #eee;
        }
        
        .month-tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 2px solid #eaeaea;
        }
        
        .month-tab {
            padding: 10px 20px;
            background: none;
            border: none;
            cursor: pointer;
            color: #7f8c8d;
            border-bottom: 3px solid transparent;
            transition: all 0.3s ease;
        }
        
        .month-tab:hover {
            color: #3498db;
        }
        
        .month-tab.active {
            color: #3498db;
            border-bottom-color: #3498db;
            font-weight: 600;
        }
        
        .month-table {
            display: none;
        }
        
        .month-table.active {
            display: block;
        }
        
        .footer {
            text-align: center;
            margin-top: 40px;
            color: #7f8c8d;
            font-size: 14px;
            padding-top: 20px;
            border-top: 1px solid #eee;
        }
        
        .sales-amount {
            font-weight: 600;
            color: #2c3e50;
        }
        
        .percentage {
            color: #3498db;
            font-weight: 600;
        }
        
        .highlight {
            background-color: #fffacd;
            padding: 3px 6px;
            border-radius: 3px;
            font-weight: 600;
        }
        
        .settlement-rate {
            color: #2ecc71;
            font-weight: 600;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>2025年Q4主播综合分析报告</h1>
            <p class="subtitle">销售额趋势、ROI分析与结算率可视化</p>
        </header>
        
        <div class="summary-cards">
            <div class="summary-card">
                <div class="card-title">Q4销售总额</div>
                <div class="card-value">¥32,826,577.28</div>
            </div>
            <div class="summary-card">
                <div class="card-title">平均ROI</div>
                <div class="card-value good" id="avg-roi">4.03</div>
            </div>
            <div class="summary-card">
                <div class="card-title">平均结算率</div>
                <div class="card-value warning" id="avg-settlement-rate">70.17%</div>
            </div>
            <div class="summary-card">
                <div class="card-title">最高销售额</div>
                <div class="card-value">¥2.93M</div>
            </div>
            <div class="summary-card">
                <div class="card-title">平均一退率</div>
                <div class="card-value bad" id="avg-return-rate">29.83%</div>
            </div>
        </div>
        
        <div class="tabs-container">
            <button class="tab active" onclick="switchTab('performance')">业绩趋势分析</button>
            <button class="tab" onclick="switchTab('sales')">销售结构分析</button>
            <button class="tab" onclick="switchTab('data')">详细数据表</button>
        </div>
        
        <!-- 业绩趋势分析标签 -->
        <div id="performance-content" class="tab-content active">
            <div class="chart-section">
                <h2 class="section-title">前6名主播销售额变化趋势 (10-12月)</h2>
                <div class="charts-grid">
                    <div class="chart-container">
                        <div class="chart-title">销售额趋势折线图（万元）</div>
                        <div class="chart-wrapper">
                            <canvas id="salesTrendChart"></canvas>
                        </div>
                    </div>
                    <div class="chart-container">
                        <div class="chart-title">月度ROI对比 (前6名主播)</div>
                        <div class="chart-wrapper">
                            <canvas id="roiComparisonChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 销售结构分析标签 -->
        <div id="sales-content" class="tab-content">
            <div class="chart-section">
                <h2 class="section-title">月度销售结构分析</h2>
                
                <div class="sales-charts">
                    <div class="chart-container">
                        <div class="chart-title">10月前5名主播销售额占比</div>
                        <div class="chart-wrapper">
                            <canvas id="octTop5Chart"></canvas>
                        </div>
                    </div>
                    
                    <div class="chart-container">
                        <div class="chart-title">11月前5名主播销售额占比</div>
                        <div class="chart-wrapper">
                            <canvas id="novTop5Chart"></canvas>
                        </div>
                    </div>
                </div>
                
                <div class="sales-charts">
                    <div class="chart-container">
                        <div class="chart-title">12月前5名主播销售额占比</div>
                        <div class="chart-wrapper">
                            <canvas id="decTop5Chart"></canvas>
                        </div>
                    </div>
                    
                    <div class="chart-container">
                        <div class="chart-title">月度结算率对比 (前6名主播)</div>
                        <div class="chart-wrapper">
                            <canvas id="settlementRateChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 详细数据表标签 -->
        <div id="data-content" class="tab-content">
            <div class="month-tabs">
                <button class="month-tab active" onclick="switchMonthTable('october')">10月数据</button>
                <button class="month-tab" onclick="switchMonthTable('november')">11月数据</button>
                <button class="month-tab" onclick="switchMonthTable('december')">12月数据</button>
            </div>
            
            <div id="october-table" class="month-table active">
                <h3 style="margin-bottom: 20px; color: #2c3e50;">10月主播详细数据</h3>
                <div class="data-table-container">
                    <table class="data-table">
                        <thead>
                            <tr>
                                <th>排名</th>
                                <th>主播姓名</th>
                                <th>类型</th>
                                <th>销售额(元)</th>
                                <th>占比</th>
                                <th>有效销售额(元)</th>
                                <th>结算率</th>
                                <th>整体ROI</th>
                                <th>累计时长</th>
                                <th>GPM</th>
                            </tr>
                        </thead>
                        <tbody id="octoberTableBody">
                            <!-- 10月数据将通过JavaScript填充 -->
                        </tbody>
                    </table>
                </div>
            </div>
            
            <div id="november-table" class="month-table">
                <h3 style="margin-bottom: 20px; color: #2c3e50;">11月主播详细数据</h3>
                <div class="data-table-container">
                    <table class="data-table">
                        <thead>
                            <tr>
                                <th>排名</th>
                                <th>主播姓名</th>
                                <th>类型</th>
                                <th>销售额(元)</th>
                                <th>占比</th>
                                <th>有效销售额(元)</th>
                                <th>结算率</th>
                                <th>整体ROI</th>
                                <th>累计时长</th>
                                <th>GPM</th>
                            </tr>
                        </thead>
                        <tbody id="novemberTableBody">
                            <!-- 11月数据将通过JavaScript填充 -->
                        </tbody>
                    </table>
                </div>
            </div>
            
            <div id="december-table" class="month-table">
                <h3 style="margin-bottom: 20px; color: #2c3e50;">12月主播详细数据</h3>
                <div class="data-table-container">
                    <table class="data-table">
                        <thead>
                            <tr>
                                <th>排名</th>
                                <th>主播姓名</th>
                                <th>类型</th>
                                <th>销售额(元)</th>
                                <th>占比</th>
                                <th>有效销售额(元)</th>
                                <th>结算率</th>
                                <th>整体ROI</th>
                                <th>累计时长</th>
                                <th>GPM</th>
                            </tr>
                        </thead>
                        <tbody id="decemberTableBody">
                            <!-- 12月数据将通过JavaScript填充 -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
        
        <div class="footer">
            <p>2025年第四季度主播综合分析报告 | 数据可视化基于Chart.js生成 | 最后更新：2025年12月31日</p>
        </div>
    </div>

    <script>
        // 数据定义 - 包含ROI、结算率和一退率（修正版）
        const monthlyData = {
            october: {
                title: "10月主播数据",
                total: 10394951.24,
                anchors: [
                    { name: "郭晚秋", type: "fulltime", sales: 1950512.87, percentage: 18.77, effectiveSales: 503991.16, effectiveSalesBeforeDelivery: 1249254.80, roi: 4.36, duration: "88小时57分", gpm: 5206.23 },
                    { name: "杨情", type: "fulltime", sales: 1625725.25, percentage: 15.64, effectiveSales: 405613.35, effectiveSalesBeforeDelivery: 1055780.89, roi: 3.90, duration: "88小时13分", gpm: 4315.50 },
                    { name: "龙美凤", type: "fulltime", sales: 1492402.14, percentage: 14.36, effectiveSales: 413945.26, effectiveSalesBeforeDelivery: 985544.60, roi: 3.89, duration: "89小时30分", gpm: 3953.39 },
                    { name: "蒋俊涛", type: "fulltime", sales: 1464334.02, percentage: 14.10, effectiveSales: 422789.40, effectiveSalesBeforeDelivery: 980740.61, roi: 3.92, duration: "87小时28分", gpm: 4047.51 },
                    { name: "郭晓斌", type: "fulltime", sales: 1139356.38, percentage: 10.96, effectiveSales: 355096.73, effectiveSalesBeforeDelivery: 804381.64, roi: 4.16, duration: "84小时10分", gpm: 4263.58 },
                    { name: "郭志阳", type: "fulltime", sales: 1021813.94, percentage: 9.83, effectiveSales: 224090.49, effectiveSalesBeforeDelivery: 557179.07, roi: 4.63, duration: "17小时", gpm: 6039.98 },
                    { name: "徐梦洁", type: "parttime", sales: 575662.08, percentage: 5.54, effectiveSales: 159100.00, effectiveSalesBeforeDelivery: 404841.92, roi: 4.64, duration: "50小时54分", gpm: 3762.40 },
                    { name: "辜楠蝶", type: "parttime", sales: 536085.13, percentage: 5.16, effectiveSales: 179959.19, effectiveSalesBeforeDelivery: 382468.03, roi: 4.45, duration: "56小时55分", gpm: 3234.24 },
                    { name: "郑欣然", type: "fulltime", sales: 208107.14, percentage: 2.00, effectiveSales: 68425.10, effectiveSalesBeforeDelivery: 146750.54, roi: 3.11, duration: "29小时58分", gpm: 2847.82 },
                    { name: "兼职佳玲", type: "parttime", sales: 159432.19, percentage: 1.53, effectiveSales: 55621.99, effectiveSalesBeforeDelivery: 121899.19, roi: 7.62, duration: "35小时42分", gpm: 2429.67 },
                    { name: "王帆", type: "parttime", sales: 153811.06, percentage: 1.48, effectiveSales: 52628.00, effectiveSalesBeforeDelivery: 120191.07, roi: 4.81, duration: "19小时", gpm: 2659.48 },
                    { name: "陈志俊", type: "parttime", sales: 98965.38, percentage: 0.95, effectiveSales: 23035.15, effectiveSalesBeforeDelivery: 61804.29, roi: 3.92, duration: "26小时30分", gpm: 2603.87 },
                    { name: "刘辉", type: "parttime", sales: 91388.93, percentage: 0.88, effectiveSales: 27900.02, effectiveSalesBeforeDelivery: 65744.88, roi: 3.99, duration: "8小时", gpm: 3930.20 },
                    { name: "牟连柳", type: "fulltime", sales: 83498.08, percentage: 0.80, effectiveSales: 23406.12, effectiveSalesBeforeDelivery: 59018.62, roi: 3.69, duration: "4小时", gpm: 4366.37 },
                    { name: "吴振林", type: "fulltime", sales: 52747.81, percentage: 0.51, effectiveSales: 21037.54, effectiveSalesBeforeDelivery: 40422.11, roi: 3.35, duration: "4小时", gpm: 3105.55 },
                    { name: "陈志俊2", type: "parttime", sales: 37524.33, percentage: 0.36, effectiveSales: 12311.16, effectiveSalesBeforeDelivery: 28280.86, roi: 3.16, duration: "16小时", gpm: 1644.94 },
                    { name: "李鸿辉", type: "fulltime", sales: 34063.00, percentage: 0.33, effectiveSales: 9586.00, effectiveSalesBeforeDelivery: 25246.00, roi: 10.55, duration: "5小时", gpm: 2443.54 }
                ]
            },
            november: {
                title: "11月主播数据",
                total: 11706196.31,
                anchors: [
                    { name: "郭晚秋", type: "fulltime", sales: 1765075.76, percentage: 15.08, effectiveSales: 487735.95, effectiveSalesBeforeDelivery: 1227167.64, roi: 4.00, duration: "86小时55分", gpm: 5985.15 },
                    { name: "蒋俊涛", type: "fulltime", sales: 1591061.81, percentage: 13.60, effectiveSales: 417605.73, effectiveSalesBeforeDelivery: 1024047.30, roi: 3.91, duration: "88小时46分", gpm: 5266.86 },
                    { name: "龙美凤", type: "fulltime", sales: 1516862.07, percentage: 12.95, effectiveSales: 396103.87, effectiveSalesBeforeDelivery: 1001953.45, roi: 3.74, duration: "96小时48分", gpm: 4510.24 },
                    { name: "杨情", type: "fulltime", sales: 1342540.85, percentage: 11.47, effectiveSales: 331151.50, effectiveSalesBeforeDelivery: 849126.84, roi: 3.60, duration: "86小时22分", gpm: 4781.23 },
                    { name: "郭晓斌", type: "fulltime", sales: 1162963.12, percentage: 9.93, effectiveSales: 351633.13, effectiveSalesBeforeDelivery: 801524.27, roi: 3.60, duration: "90小时59分", gpm: 4165.49 },
                    { name: "郭志阳", type: "fulltime", sales: 1133697.98, percentage: 9.69, effectiveSales: 304371.19, effectiveSalesBeforeDelivery: 716128.38, roi: 4.31, duration: "41小时25分", gpm: 5904.62 },
                    { name: "徐梦洁", type: "parttime", sales: 520391.05, percentage: 4.44, effectiveSales: 128225.12, effectiveSalesBeforeDelivery: 317052.58, roi: 4.02, duration: "35小时1分", gpm: 4860.47 },
                    { name: "辜楠蝶", type: "parttime", sales: 518325.10, percentage: 4.43, effectiveSales: 158871.24, effectiveSalesBeforeDelivery: 366770.97, roi: 3.86, duration: "41小时", gpm: 4511.10 },
                    { name: "王晨帆", type: "parttime", sales: 348106.30, percentage: 2.97, effectiveSales: 97346.20, effectiveSalesBeforeDelivery: 219204.00, roi: 4.52, duration: "26小时1分", gpm: 5500.53 },
                    { name: "刘辉", type: "parttime", sales: 211436.46, percentage: 1.81, effectiveSales: 74319.60, effectiveSalesBeforeDelivery: 153175.60, roi: 3.93, duration: "20小时", gpm: 4109.55 },
                    { name: "陈志俊", type: "parttime", sales: 163121.27, percentage: 1.39, effectiveSales: 58788.02, effectiveSalesBeforeDelivery: 119629.27, roi: 2.94, duration: "56小时", gpm: 1743.64 },
                    { name: "李鸿辉", type: "fulltime", sales: 66196.47, percentage: 0.56, effectiveSales: 17919.00, effectiveSalesBeforeDelivery: 46777.47, roi: 3.78, duration: "14小时", gpm: 2529.96 },
                    { name: "蔡继红", type: "parttime", sales: 41894.00, percentage: 0.36, effectiveSales: 14642.00, effectiveSalesBeforeDelivery: 26572.00, roi: 3.76, duration: "12小时8分", gpm: 2593.25 },
                    { name: "陈泺伊", type: "parttime", sales: 13279.00, percentage: 0.11, effectiveSales: 5142.00, effectiveSalesBeforeDelivery: 11382.00, roi: 3.57, duration: "2小时", gpm: 4010.57 }
                ]
            },
            december: {
                title: "12月主播数据",
                total: 10725429.73,
                anchors: [
                    { name: "郭志阳", type: "fulltime", sales: 2929364.65, percentage: 27.08, effectiveSales: 809482.22, effectiveSalesBeforeDelivery: 1878238.16, roi: 4.10, duration: "83小时23分", gpm: 6733.17 },
                    { name: "郭晚秋", type: "fulltime", sales: 2360862.67, percentage: 21.74, effectiveSales: 623879.24, effectiveSalesBeforeDelivery: 1541555.71, roi: 3.78, duration: "97小时56分", gpm: 6332.72 },
                    { name: "蒋俊涛", type: "fulltime", sales: 2026755.70, percentage: 18.63, effectiveSales: 608751.97, effectiveSalesBeforeDelivery: 1357226.01, roi: 3.77, duration: "94小时", gpm: 5678.08 },
                    { name: "杨情", type: "fulltime", sales: 960036.15, percentage: 8.95, effectiveSales: 281913.19, effectiveSalesBeforeDelivery: 678972.35, roi: 3.44, duration: "80小时1分", gpm: 4953.36 },
                    { name: "龙美凤", type: "fulltime", sales: 879072.83, percentage: 8.17, effectiveSales: 293738.09, effectiveSalesBeforeDelivery: 652231.39, roi: 3.68, duration: "70小时33分", gpm: 5547.04 },
                    { name: "郭晓斌", type: "fulltime", sales: 665233.90, percentage: 6.15, effectiveSales: 206550.98, effectiveSalesBeforeDelivery: 468149.95, roi: 3.03, duration: "57小时", gpm: 4815.62 },
                    { name: "蔡继红", type: "parttime", sales: 506902.99, percentage: 4.68, effectiveSales: 142129.98, effectiveSalesBeforeDelivery: 318159.05, roi: 3.59, duration: "109小时51分", gpm: 3916.27 },
                    { name: "辜楠蝶", type: "parttime", sales: 470510.22, percentage: 4.39, effectiveSales: 152183.38, effectiveSalesBeforeDelivery: 330258.13, roi: 3.61, duration: "38小时", gpm: 4964.65 },
                    { name: "王晨帆", type: "parttime", sales: 413079.91, percentage: 3.85, effectiveSales: 122715.00, effectiveSalesBeforeDelivery: 282599.19, roi: 4.12, duration: "26小时", gpm: 6257.65 },
                    { name: "贾浩洋", type: "parttime", sales: 250226.09, percentage: 2.35, effectiveSales: 88114.27, effectiveSalesBeforeDelivery: 194949.43, roi: 3.76, duration: "17小时", gpm: 6167.15 },
                    { name: "徐梦洁", type: "parttime", sales: 142739.00, percentage: 1.33, effectiveSales: 52494.00, effectiveSalesBeforeDelivery: 96703.00, roi: 3.36, duration: "15小时51分", gpm: 5135.97 },
                    { name: "刘辉", type: "parttime", sales: 61774.00, percentage: 0.58, effectiveSales: 23036.00, effectiveSalesBeforeDelivery: 44702.00, roi: 3.94, duration: "6小时", gpm: 4441.30 },
                    { name: "李鸿辉", type: "fulltime", sales: 29155.20, percentage: 0.27, effectiveSales: 7757.00, effectiveSalesBeforeDelivery: 17547.03, roi: 2.99, duration: "4小时", gpm: 3965.61 },
                    { name: "谢嘉裕", type: "parttime", sales: 10483.00, percentage: 0.10, effectiveSales: 0.00, effectiveSalesBeforeDelivery: 5491.00, roi: 2.88, duration: "2小时", gpm: 1971.97 }
                ]
            }
        };

        // 计算结算率：有效销售额 / 销售额
        function calculateSettlementRate(sales, effectiveSales) {
            if (sales === 0) return 0;
            return ((effectiveSales / sales) * 100).toFixed(2);
        }

        // 计算一退率：1 - (有效销售额（发货前） / 销售额)
        function calculateReturnRate(sales, effectiveSalesBeforeDelivery) {
            if (sales === 0) return 0;
            return ((1 - effectiveSalesBeforeDelivery / sales) * 100).toFixed(2);
        }

        // 初始化数据，计算结算率和一退率
        Object.values(monthlyData).forEach(month => {
            month.anchors.forEach(anchor => {
                anchor.settlementRate = calculateSettlementRate(anchor.sales, anchor.effectiveSales);
                anchor.returnRate = calculateReturnRate(anchor.sales, anchor.effectiveSalesBeforeDelivery);
            });
        });

        // 计算顶栏数据
        function calculateHeaderData() {
            let totalSales = 0;
            let totalEffectiveSales = 0;
            let totalROI = 0;
            let totalReturnRate = 0;
            let anchorCount = 0;
            
            // 遍历三个月的数据
            Object.values(monthlyData).forEach(month => {
                month.anchors.forEach(anchor => {
                    totalSales += anchor.sales;
                    totalEffectiveSales += anchor.effectiveSales;
                    totalROI += anchor.roi;
                    totalReturnRate += parseFloat(anchor.returnRate);
                    anchorCount++;
                });
            });
            
            // 计算平均结算率（按总销售额加权平均）
            const avgSettlementRate = totalSales > 0 ? (totalEffectiveSales / totalSales * 100).toFixed(2) : 0;
            
            // 计算平均ROI（简单平均）
            const avgROI = (totalROI / anchorCount).toFixed(2);
            
            // 计算平均一退率（简单平均）
            const avgReturnRate = (totalReturnRate / anchorCount).toFixed(2);
            
            return {
                avgSettlementRate,
                avgROI,
                avgReturnRate
            };
        }

        // 更新顶栏数据
        function updateHeaderData() {
            const headerData = calculateHeaderData();
            
            // 更新平均ROI
            document.getElementById('avg-roi').textContent = headerData.avgROI;
            
            // 更新平均结算率
            document.getElementById('avg-settlement-rate').textContent = `${headerData.avgSettlementRate}%`;
            
            // 更新平均一退率（根据原始定义重新计算）
            document.getElementById('avg-return-rate').textContent = `${headerData.avgReturnRate}%`;
            
            // 根据数值设置颜色
            const avgSettlementRateEl = document.getElementById('avg-settlement-rate');
            const avgReturnRateEl = document.getElementById('avg-return-rate');
            
            // 结算率：越高越好（绿色表示高）
            if (parseFloat(headerData.avgSettlementRate) >= 30) {
                avgSettlementRateEl.className = 'card-value good';
            } else if (parseFloat(headerData.avgSettlementRate) >= 25) {
                avgSettlementRateEl.className = 'card-value warning';
            } else {
                avgSettlementRateEl.className = 'card-value bad';
            }
            
            // 一退率：越低越好（绿色表示低）
            if (parseFloat(headerData.avgReturnRate) <= 70) {
                avgReturnRateEl.className = 'card-value good';
            } else if (parseFloat(headerData.avgReturnRate) <= 75) {
                avgReturnRateEl.className = 'card-value warning';
            } else {
                avgReturnRateEl.className = 'card-value bad';
            }
        }

        // 图表实例存储
        const charts = {};

        // 格式化金额显示
        function formatCurrency(num) {
            if (num >= 1000000) {
                return '¥' + (num / 1000000).toFixed(2) + 'M';
            } else if (num >= 10000) {
                return '¥' + (num / 10000).toFixed(1) + '万';
            } else {
                return '¥' + num.toLocaleString('zh-CN', { minimumFractionDigits: 0, maximumFractionDigits: 0 });
            }
        }

        // 获取销售额前6名主播（按Q4累计销售额）
        function getTop6Anchors() {
            // 计算每个主播三个月的累计销售额
            const anchorSales = {};
            
            Object.values(monthlyData).forEach(month => {
                month.anchors.forEach(anchor => {
                    if (!anchorSales[anchor.name]) {
                        anchorSales[anchor.name] = {
                            name: anchor.name,
                            type: anchor.type,
                            totalSales: 0,
                            monthlyData: {
                                october: null,
                                november: null,
                                december: null
                            }
                        };
                    }
                    anchorSales[anchor.name].totalSales += anchor.sales;
                    
                    // 记录各月数据
                    const monthKey = Object.keys(monthlyData).find(key => monthlyData[key] === month);
                    anchorSales[anchor.name].monthlyData[monthKey] = {
                        roi: anchor.roi,
                        sales: anchor.sales,
                        percentage: anchor.percentage,
                        settlementRate: parseFloat(anchor.settlementRate)
                    };
                });
            });
            
            // 转换为数组并按总销售额排序
            const anchorArray = Object.values(anchorSales);
            anchorArray.sort((a, b) => b.totalSales - a.totalSales);
            
            // 返回前6名
            return anchorArray.slice(0, 6);
        }

        // 创建销售额趋势折线图（显示前6名主播）
        function createSalesTrendChart() {
            const ctx = document.getElementById('salesTrendChart');
            if (!ctx) return;
            
            // 获取前6名主播
            const top6Anchors = getTop6Anchors();
            
            // 准备数据
            const months = ['10月', '11月', '12月'];
            const datasets = [];
            
            // 为前6名主播创建数据集
            const colors = [
                'rgba(231, 76, 60, 0.8)',    // 红色
                'rgba(230, 126, 34, 0.8)',   // 橙色
                'rgba(241, 196, 15, 0.8)',   // 黄色
                'rgba(52, 152, 219, 0.8)',   // 蓝色
                'rgba(46, 204, 113, 0.8)',   // 绿色
                'rgba(155, 89, 182, 0.8)'    // 紫色
            ];
            
            top6Anchors.forEach((anchor, index) => {
                const salesData = [
                    anchor.monthlyData.october ? anchor.monthlyData.october.sales / 10000 : null,
                    anchor.monthlyData.november ? anchor.monthlyData.november.sales / 10000 : null,
                    anchor.monthlyData.december ? anchor.monthlyData.december.sales / 10000 : null
                ];
                
                datasets.push({
                    label: anchor.name,
                    data: salesData,
                    borderColor: colors[index],
                    backgroundColor: colors[index].replace('0.8', '0.1'),
                    borderWidth: 3,
                    fill: false,
                    tension: 0.3,
                    pointRadius: 5,
                    pointHoverRadius: 8
                });
            });
            
            // 如果已有图表，先销毁
            if (charts.salesTrendChart) {
                charts.salesTrendChart.destroy();
            }
            
            charts.salesTrendChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: months,
                    datasets: datasets
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    interaction: {
                        mode: 'index',
                        intersect: false
                    },
                    plugins: {
                        legend: {
                            position: 'top',
                            labels: {
                                font: {
                                    size: 12
                                }
                            }
                        },
                        tooltip: {
                            mode: 'index',
                            intersect: false,
                            callbacks: {
                                label: function(context) {
                                    const value = context.parsed.y;
                                    const sales = value * 10000;
                                    return `${context.dataset.label}: ${formatCurrency(sales)}`;
                                }
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: '销售额（万元）'
                            }
                        },
                        x: {
                            title: {
                                display: true,
                                text: '月份'
                            }
                        }
                    },
                    animation: {
                        duration: 2000,
                        easing: 'easeOutQuart'
                    }
                }
            });
        }

        // 创建月度ROI对比柱状图（仅显示前6名主播）
        function createRoiComparisonChart() {
            const ctx = document.getElementById('roiComparisonChart');
            if (!ctx) return;
            
            // 获取前6名主播
            const top6Anchors = getTop6Anchors();
            
            // 准备数据
            const months = ['10月', '11月', '12月'];
            const datasets = [];
            
            // 为每个月创建数据集
            const monthColors = {
                '10月': 'rgba(52, 152, 219, 0.8)',
                '11月': 'rgba(231, 76, 60, 0.8)',
                '12月': 'rgba(46, 204, 113, 0.8)'
            };
            
            const monthBorderColors = {
                '10月': 'rgb(52, 152, 219)',
                '11月': 'rgb(231, 76, 60)',
                '12月': 'rgb(46, 204, 113)'
            };
            
            months.forEach(month => {
                const monthKey = month === '10月' ? 'october' : 
                                month === '11月' ? 'november' : 'december';
                
                const roiData = top6Anchors.map(anchor => {
                    return anchor.monthlyData[monthKey] ? anchor.monthlyData[monthKey].roi : 0;
                });
                
                datasets.push({
                    label: month,
                    data: roiData,
                    backgroundColor: monthColors[month],
                    borderColor: monthBorderColors[month],
                    borderWidth: 2,
                    borderRadius: 8,
                    borderSkipped: false
                });
            });
            
            // 如果已有图表，先销毁
            if (charts.roiComparisonChart) {
                charts.roiComparisonChart.destroy();
            }
            
            charts.roiComparisonChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: top6Anchors.map(a => a.name),
                    datasets: datasets
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: 'ROI'
                            }
                        },
                        x: {
                            title: {
                                display: true,
                                text: '主播姓名'
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            position: 'top',
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return `${context.dataset.label}: ${context.parsed.y.toFixed(2)}`;
                                }
                            }
                        }
                    },
                    animation: {
                        duration: 2000,
                        easing: 'easeOutBounce'
                    }
                }
            });
        }

        // 创建饼图函数（带旋转动画）
        function createPieChart(canvasId, data, title) {
            const ctx = document.getElementById(canvasId);
            if (!ctx) return null;
            
            // 如果已有图表，先销毁
            if (charts[canvasId]) {
                charts[canvasId].destroy();
            }
            
            charts[canvasId] = new Chart(ctx.getContext('2d'), {
                type: 'pie',
                data: data,
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'right',
                            labels: {
                                boxWidth: 12,
                                padding: 15,
                                font: {
                                    size: 11
                                }
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    const label = context.label || '';
                                    const value = context.raw || 0;
                                    return `${label}: ${value.toFixed(2)}%`;
                                }
                            }
                        },
                        datalabels: {
                            color: '#fff',
                            font: {
                                weight: 'bold',
                                size: 14
                            },
                            formatter: function(value, context) {
                                return value.toFixed(1) + '%';
                            }
                        }
                    },
                    animation: {
                        animateScale: true,
                        animateRotate: true,
                        duration: 2000,
                        easing: 'easeOutQuart'
                    }
                },
                plugins: [ChartDataLabels]
            });
            
            return charts[canvasId];
        }

        // 创建前5名主播饼图（带旋转动画）
        function createTop5PieCharts() {
            // 10月前5名
            const octTop5 = [...monthlyData.october.anchors]
                .sort((a, b) => b.sales - a.sales)
                .slice(0, 5);
                
            const octTop5Data = {
                labels: octTop5.map(a => a.name),
                datasets: [{
                    data: octTop5.map(a => a.percentage),
                    backgroundColor: [
                        'rgba(231, 76, 60, 0.8)',
                        'rgba(230, 126, 34, 0.8)',
                        'rgba(241, 196, 15, 0.8)',
                        'rgba(52, 152, 219, 0.8)',
                        'rgba(46, 204, 113, 0.8)'
                    ],
                    borderColor: [
                        'rgba(231, 76, 60, 1)',
                        'rgba(230, 126, 34, 1)',
                        'rgba(241, 196, 15, 1)',
                        'rgba(52, 152, 219, 1)',
                        'rgba(46, 204, 113, 1)'
                    ],
                    borderWidth: 2
                }]
            };
            
            createPieChart('octTop5Chart', octTop5Data, '10月前5名主播');
            
            // 11月前5名
            const novTop5 = [...monthlyData.november.anchors]
                .sort((a, b) => b.sales - a.sales)
                .slice(0, 5);
                
            const novTop5Data = {
                labels: novTop5.map(a => a.name),
                datasets: [{
                    data: novTop5.map(a => a.percentage),
                    backgroundColor: [
                        'rgba(231, 76, 60, 0.8)',
                        'rgba(230, 126, 34, 0.8)',
                        'rgba(241, 196, 15, 0.8)',
                        'rgba(52, 152, 219, 0.8)',
                        'rgba(46, 204, 113, 0.8)'
                    ],
                    borderColor: [
                        'rgba(231, 76, 60, 1)',
                        'rgba(230, 126, 34, 1)',
                        'rgba(241, 196, 15, 1)',
                        'rgba(52, 152, 219, 1)',
                        'rgba(46, 204, 113, 1)'
                    ],
                    borderWidth: 2
                }]
            };
            
            createPieChart('novTop5Chart', novTop5Data, '11月前5名主播');
            
            // 12月前5名
            const decTop5 = [...monthlyData.december.anchors]
                .sort((a, b) => b.sales - a.sales)
                .slice(0, 5);
                
            const decTop5Data = {
                labels: decTop5.map(a => a.name),
                datasets: [{
                    data: decTop5.map(a => a.percentage),
                    backgroundColor: [
                        'rgba(231, 76, 60, 0.8)',
                        'rgba(230, 126, 34, 0.8)',
                        'rgba(241, 196, 15, 0.8)',
                        'rgba(52, 152, 219, 0.8)',
                        'rgba(46, 204, 113, 0.8)'
                    ],
                    borderColor: [
                        'rgba(231, 76, 60, 1)',
                        'rgba(230, 126, 34, 1)',
                        'rgba(241, 196, 15, 1)',
                        'rgba(52, 152, 219, 1)',
                        'rgba(46, 204, 113, 1)'
                    ],
                    borderWidth: 2
                }]
            };
            
            createPieChart('decTop5Chart', decTop5Data, '12月前5名主播');
        }

        // 创建月度结算率对比柱状图（前6名主播）
        function createSettlementRateChart() {
            const ctx = document.getElementById('settlementRateChart');
            if (!ctx) return;
            
            // 获取前6名主播
            const top6Anchors = getTop6Anchors();
            
            // 准备数据
            const months = ['10月', '11月', '12月'];
            const datasets = [];
            
            // 为前6名主播创建数据集
            const colors = [
                'rgba(231, 76, 60, 0.8)',    // 红色
                'rgba(230, 126, 34, 0.8)',   // 橙色
                'rgba(241, 196, 15, 0.8)',   // 黄色
                'rgba(52, 152, 219, 0.8)',   // 蓝色
                'rgba(46, 204, 113, 0.8)',   // 绿色
                'rgba(155, 89, 182, 0.8)'    // 紫色
            ];
            
            top6Anchors.forEach((anchor, index) => {
                const settlementRateData = [
                    anchor.monthlyData.october ? anchor.monthlyData.october.settlementRate : null,
                    anchor.monthlyData.november ? anchor.monthlyData.november.settlementRate : null,
                    anchor.monthlyData.december ? anchor.monthlyData.december.settlementRate : null
                ];
                
                datasets.push({
                    label: anchor.name,
                    data: settlementRateData,
                    backgroundColor: colors[index],
                    borderColor: colors[index].replace('0.8', '1'),
                    borderWidth: 2,
                    borderRadius: 8,
                    borderSkipped: false
                });
            });
            
            // 如果已有图表，先销毁
            if (charts.settlementRateChart) {
                charts.settlementRateChart.destroy();
            }
            
            charts.settlementRateChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: months,
                    datasets: datasets
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: false,
                            title: {
                                display: true,
                                text: '结算率 (%)'
                            },
                            min: 20,
                            max: 100
                        },
                        x: {
                            title: {
                                display: true,
                                text: '月份'
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            position: 'top',
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return `${context.dataset.label}: ${context.parsed.y.toFixed(2)}%`;
                                }
                            }
                        }
                    },
                    animation: {
                        duration: 2000,
                        easing: 'easeOutBounce'
                    }
                }
            });
        }

        // 填充表格数据
        function populateTables() {
            // 10月数据表
            const octoberTableBody = document.getElementById('octoberTableBody');
            let octoberHtml = '';
            
            const octoberAnchors = [...monthlyData.october.anchors]
                .sort((a, b) => b.sales - a.sales);
            
            octoberAnchors.forEach((anchor, index) => {
                const rank = index + 1;
                const typeClass = anchor.type === 'fulltime' ? 'type-fulltime' : 'type-parttime';
                const typeText = anchor.type === 'fulltime' ? '全职' : '兼职';
                
                octoberHtml += `
                <tr>
                    <td>${rank}</td>
                    <td>${anchor.name}</td>
                    <td><span class="type-badge ${typeClass}">${typeText}</span></td>
                    <td class="sales-amount">${formatCurrency(anchor.sales)}</td>
                    <td>${anchor.percentage.toFixed(2)}%</td>
                    <td>${formatCurrency(anchor.effectiveSales)}</td>
                    <td class="settlement-rate">${anchor.settlementRate}%</td>
                    <td>${anchor.roi.toFixed(2)}</td>
                    <td>${anchor.duration}</td>
                    <td>${anchor.gpm.toFixed(2)}</td>
                </tr>
                `;
            });
            
            octoberTableBody.innerHTML = octoberHtml;
            
            // 11月数据表
            const novemberTableBody = document.getElementById('novemberTableBody');
            let novemberHtml = '';
            
            const novemberAnchors = [...monthlyData.november.anchors]
                .sort((a, b) => b.sales - a.sales);
            
            novemberAnchors.forEach((anchor, index) => {
                const rank = index + 1;
                const typeClass = anchor.type === 'fulltime' ? 'type-fulltime' : 'type-parttime';
                const typeText = anchor.type === 'fulltime' ? '全职' : '兼职';
                
                novemberHtml += `
                <tr>
                    <td>${rank}</td>
                    <td>${anchor.name}</td>
                    <td><span class="type-badge ${typeClass}">${typeText}</span></td>
                    <td class="sales-amount">${formatCurrency(anchor.sales)}</td>
                    <td>${anchor.percentage.toFixed(2)}%</td>
                    <td>${formatCurrency(anchor.effectiveSales)}</td>
                    <td class="settlement-rate">${anchor.settlementRate}%</td>
                    <td>${anchor.roi.toFixed(2)}</td>
                    <td>${anchor.duration}</td>
                    <td>${anchor.gpm.toFixed(2)}</td>
                </tr>
                `;
            });
            
            novemberTableBody.innerHTML = novemberHtml;
            
            // 12月数据表
            const decemberTableBody = document.getElementById('decemberTableBody');
            let decemberHtml = '';
            
            const decemberAnchors = [...monthlyData.december.anchors]
                .sort((a, b) => b.sales - a.sales);
            
            decemberAnchors.forEach((anchor, index) => {
                const rank = index + 1;
                const typeClass = anchor.type === 'fulltime' ? 'type-fulltime' : 'type-parttime';
                const typeText = anchor.type === 'fulltime' ? '全职' : '兼职';
                
                decemberHtml += `
                <tr>
                    <td>${rank}</td>
                    <td>${anchor.name}</td>
                    <td><span class="type-badge ${typeClass}">${typeText}</span></td>
                    <td class="sales-amount">${formatCurrency(anchor.sales)}</td>
                    <td>${anchor.percentage.toFixed(2)}%</td>
                    <td>${formatCurrency(anchor.effectiveSales)}</td>
                    <td class="settlement-rate">${anchor.settlementRate}%</td>
                    <td>${anchor.roi.toFixed(2)}</td>
                    <td>${anchor.duration}</td>
                    <td>${anchor.gpm.toFixed(2)}</td>
                </tr>
                `;
            });
            
            decemberTableBody.innerHTML = decemberHtml;
        }

        // 切换主标签页
        function switchTab(tabName) {
            // 移除所有标签的active类
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // 隐藏所有标签内容
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.remove('active');
            });
            
            // 激活当前标签
            const activeTab = document.querySelector(`.tab[onclick="switchTab('${tabName}')"]`);
            if (activeTab) activeTab.classList.add('active');
            
            // 显示当前标签内容
            const activeContent = document.getElementById(`${tabName}-content`);
            if (activeContent) activeContent.classList.add('active');
            
            // 根据标签初始化图表
            if (tabName === 'performance') {
                setTimeout(() => {
                    createSalesTrendChart();
                    createRoiComparisonChart();
                }, 100);
            } else if (tabName === 'sales') {
                setTimeout(() => {
                    createTop5PieCharts();
                    createSettlementRateChart();
                }, 100);
            }
        }

        // 切换月份数据表
        function switchMonthTable(month) {
            // 移除所有月份标签的active类
            document.querySelectorAll('.month-tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // 隐藏所有月份表格
            document.querySelectorAll('.month-table').forEach(table => {
                table.classList.remove('active');
            });
            
            // 激活当前月份标签
            const activeMonthTab = document.querySelector(`.month-tab[onclick="switchMonthTable('${month}')"]`);
            if (activeMonthTab) activeMonthTab.classList.add('active');
            
            // 显示当前月份表格
            const activeMonthTable = document.getElementById(`${month}-table`);
            if (activeMonthTable) activeMonthTable.classList.add('active');
        }

        // 页面加载完成后初始化
        document.addEventListener('DOMContentLoaded', function() {
            // 初始化数据表
            populateTables();
            
            // 更新顶栏数据
            updateHeaderData();
            
            // 初始化默认标签页的图表
            createSalesTrendChart();
            createRoiComparisonChart();
        });
    </script>
</body>
</html>
