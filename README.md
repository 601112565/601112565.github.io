<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <!-- 文档类型声明，指定HTML5 -->
    <!-- 设置页面语言为中文 -->
    
    <!-- 字符编码设置为UTF-8，支持中文字符 -->
    <meta charset="UTF-8">
    
    <!-- 响应式设计 viewport 设置，确保在移动设备上正确显示 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- 页面标题 -->
    <title>工时薪资计算系统</title>
    
    <!-- 引入 Tailwind CSS 框架，用于快速构建现代化的用户界面 -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- 自定义CSS样式 -->
    <style>
        /* 引入 Google Fonts 的 Inter 字体 */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
        
        /* 设置页面整体字体为 Inter */
        body {
            font-family: 'Inter', sans-serif;
        }
        
        /* 定义标签页按钮的活动状态样式 */
        .tab-button.active {
            background-color: #2563eb; /* 蓝色背景 */
            color: white; /* 白色文字 */
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1); /* 添加阴影效果 */
        }
        
        /* 定义标签页按钮的非活动状态样式 */
        .tab-button:not(.active) {
            color: #4b5563; /* 灰色文字 */
            transition: all 0.2s; /* 添加过渡动画 */
        }
        
        /* 定义鼠标悬停时的样式变化 */
        .tab-button:not(.active):hover {
            color: #2563eb; /* 悬停时变为蓝色 */
        }
    </style>
</head>
<body class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 py-3 px-2">
    <!-- 页面主体，设置最小高度为屏幕高度，背景为蓝色渐变，内边距为8和4 -->
    
    <!-- 最大宽度容器，居中显示，最大宽度为6xl -->
    <div class="max-w-6xl mx-auto">
        
        <!-- 标题区域，文字居中，下边距为8 -->
        <div class="text-center mb-3">
            <!-- 主标题，4xl大小，粗体，深灰色，下边距2 -->
            <h1 class="text-4xl font-bold text-gray-800 mb-2">工时薪资计算系统</h1>
            <!-- 副标题，灰色 -->
            <p class="text-gray-600">精准计算您的薪资与加班费用</p>
        </div>

        <!-- 标签页导航区域 -->
        <div class="flex justify-center mb-3">
            <!-- 白色背景，圆角，阴影，内边距为1，水平排列 -->
            <div class="bg-white rounded-xl shadow-lg p-1 flex">
                <!-- 薪资计算标签页按钮 -->
                <button onclick="switchTab('salary')" id="salaryTab" class="tab-button px-6 py-3 rounded-lg font-medium flex items-center">
                    <!-- 图标 -->
                    <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"></path>
                    </svg>
                    薪资计算
                </button>
                
                <!-- 工时信息标签页按钮 -->
                <button onclick="switchTab('workHour')" id="workHourTab" class="tab-button px-6 py-3 rounded-lg font-medium flex items-center">
                    <!-- 图标 -->
                    <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                    </svg>
                    工时信息
                </button>
                
                <!-- 计算结果标签页按钮 -->
                <button onclick="" id="resultTab" class="tab-button px-0 py-0 rounded-lg font-medium flex items-center">
                </button>
            </div>
        </div>

        <!-- 主要内容区域，分为两列，间距为8 -->
        <div class="grid lg:grid-cols-2 gap-3">
            <!-- 薪资计算内容区域 -->
            <div id="salaryContent">
                <!-- 基础薪资信息卡片 -->
                <div class="bg-white rounded-xl shadow-lg p-3 mb-3">
                    <!-- 标题，包含图标 -->
                    <h2 class="text-2xl font-semibold text-gray-800 mb-3 flex items-center">
                        <svg class="w-6 h-6 mr-2 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"></path>
                        </svg>
                        基础薪资信息
                    </h2>
                    <!-- 表单内容 -->
                    <div class="space-y-4">
                        <!-- 底薪和正班天数输入行 -->
                        <div class="grid grid-cols-2 gap-2">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">底薪 (元)</label>
                                <!-- 底薪输入框，初始值2600，值改变时调用calculate函数 -->
                                <input type="number" id="baseSalary" value="2600" onchange="calculate()" class="w-full px-3 py-1 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">正班天数</label>
                                <!-- 正班天数输入框，初始值22，值改变时调用calculate函数 -->
                                <input type="number" id="regularDays" value="22" onchange="calculate()" class="w-full px-3 py-1 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                        </div>
                        <!-- 时薪显示 -->
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">时薪 (元/小时)</label>
                            <!-- 时薪显示框，只读 -->
                            <input type="text" id="hourlyRate" readonly class="w-full px-3 py-1 border border-gray-300 rounded-lg bg-gray-100 text-gray-700">
                        </div>
                    </div>
                </div>

                <!-- 加班信息卡片 -->
                <div class="bg-white rounded-xl shadow-lg p-3">
                    <!-- 标题，包含图标 -->
                    <h2 class="text-2xl font-semibold text-gray-800 mb-3 flex items-center">
                        <svg class="w-6 h-6 mr-2 text-orange-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                        </svg>
                        加班信息
                    </h2>
                    <!-- 加班信息表格 -->
                    <div class="space-y-4">
                        <!-- G1加班行 -->
                        <div class="grid grid-cols-3 gap-2">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-1">G1 (元/小时)</label>
                                <!-- G1加班费率输入 -->
                                <input type="number" id="g1Rate" value="22.41" step="0.01" onchange="calculate()" readonly class="w-full px-3 py-1 border bg-gray-100 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-1">工时 (小时)</label>
                                <!-- G1加班工时输入 -->
                                <input type="number" id="g1Hours" value="40" onchange="calculate()" class="w-full px-3 py-1 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-1">薪资 (元)</label>
                                <!-- G1加班薪资显示 -->
                                <input type="text" id="g1Pay" readonly class="w-full px-3 py-1 border border-gray-300 rounded-lg bg-gray-100 text-gray-700">
                            </div>
                        </div>
                        <!-- G2加班行 -->
                        <div class="grid grid-cols-3 gap-3">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-1">G2 (元/小时)</label>
                                <!-- G2加班费率输入 -->
                                <input type="text" id="g2Rate" value="29.89" step="0.01" onchange="calculate()" readonly class="w-full px-3 py-1 border bg-gray-100 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-1">工时 (小时)</label>
                                <!-- G2加班工时输入 -->
                                <input type="number" id="g2Hours" value="40" onchange="calculate()" class="w-full px-3 py-1 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-1">薪资 (元)</label>
                                <!-- G2加班薪资显示 -->
                                <input type="text" id="g2Pay" readonly class="w-full px-3 py-1 border border-gray-300 rounded-lg bg-gray-100 text-gray-700">
                            </div>
                        </div>
                        <!-- G3加班行 -->
                        <div class="grid grid-cols-3 gap-3">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-1">G3 (元/小时)</label>
                                <!-- G3加班费率输入 -->
                                <input type="text" id="g3Rate" value="44.83" step="0.01" onchange="calculate()" readonly class="w-full px-3 py-1 border bg-gray-100 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-1">工时 (小时)</label>
                                <!-- G3加班工时输入 -->
                                <input type="number" id="g3Hours" value="0" onchange="calculate()" class="w-full px-3 py-1 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-1">薪资 (元)</label>
                                <!-- G3加班薪资显示 -->
                                <input type="text" id="g3Pay" readonly class="w-full px-3 py-1 border border-gray-300 rounded-lg bg-gray-100 text-gray-700">
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 工时信息内容区域 -->
            <div id="workHourContent">
                <!-- 工时工资计算卡片 -->
                <div class="bg-white rounded-xl shadow-lg p-6 mb-3">
                    <!-- 标题，包含图标 -->
                    <h2 class="text-2xl font-semibold text-gray-800 mb-3 flex items-center">
                        <svg class="w-6 h-6 mr-2 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                        </svg>
                        工时工资计算
                    </h2>
                    <!-- 工时信息表单 -->
                    <div class="space-y-4">
                        <!-- 总工时和工价输入行 -->
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">总工时 (小时)</label>
                                <!-- 总工时输入 -->
                                <input type="number" id="workHours" value="256" onchange="calculate()" class="w-full px-3 py-1 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">工价 (元/小时)</label>
                                <!-- 工价输入 -->
                                <input type="number" id="workPrice" value="23" step="0.01" onchange="calculate()" class="w-full px-3 py-1 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                        </div>
                        <!-- 补贴输入 -->
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">补贴 (元)</label>
                            <!-- 补贴输入 -->
                            <input type="number" id="subsidy" value="0" onchange="calculate()" class="w-full px-3 py-1 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                        </div>
                    </div>
                </div>

                <!-- 详细数据表格卡片 -->
                <div class="bg-white rounded-xl shadow-lg p-6">
                    <!-- 标题 -->
                    <h2 class="text-2xl font-semibold text-gray-800 mb-3">详细数据表格</h2>
                    <!-- 响应式表格 -->
                    <div class="overflow-x-auto">
                        <table class="w-full text-sm">
                            <!-- 表头 -->
                            <thead>
                                <tr class="border-b border-gray-200">
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">项目</th>
                                    <th class="text-right py-3 px-4 font-semibold text-gray-700">数值</th>
                                </tr>
                            </thead>
                            <!-- 表体 -->
                            <tbody class="divide-y divide-gray-200">
                                <!-- 各项数据行 -->
                                <tr>
                                    <td class="py-3 px-4 text-gray-600">底薪</td>
                                    <td class="py-3 px-4 text-right font-medium" id="tableBaseSalary">2600 元</td>
                                </tr>
                                <tr>
                                    <td class="py-3 px-4 text-gray-600">正班天数</td>
                                    <td class="py-3 px-4 text-right font-medium" id="tableRegularDays">22 天</td>
                                </tr>
                                <tr>
                                    <td class="py-3 px-4 text-gray-600">总工时</td>
                                    <td class="py-3 px-4 text-right font-medium" id="tableTotalHours">256 小时</td>
                                </tr>
                                <tr>
                                    <td class="py-3 px-4 text-gray-600">G1 加班工时</td>
                                    <td class="py-3 px-4 text-right font-medium" id="tableG1Hours">40 小时</td>
                                </tr>
                                <tr>
                                    <td class="py-3 px-4 text-gray-600">G2 加班工时</td>
                                    <td class="py-3 px-4 text-right font-medium" id="tableG2Hours">40 小时</td>
                                </tr>
                                <tr>
                                    <td class="py-3 px-4 text-gray-600">G3 加班工时</td>
                                    <td class="py-3 px-4 text-right font-medium" id="tableG3Hours">0 小时</td>
                                </tr>
                                <tr>
                                    <td class="py-3 px-4 text-gray-600">工价</td>
                                    <td class="py-3 px-4 text-right font-medium" id="tableWorkPrice">23 元/小时</td>
                                </tr>
                                <tr>
                                    <td class="py-3 px-4 text-gray-600">补贴</td>
                                    <td class="py-3 px-4 text-right font-medium" id="tableSubsidy">0 元</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- 计算结果内容区域，占据两列 -->
            <div id="resultContent" class="lg:col-span-2">
                <!-- 计算结果卡片 -->
                <div class="bg-white rounded-xl shadow-lg p-6 mb-3">
                    <!-- 标题，包含图标 -->
                    <h2 class="text-2xl font-semibold text-gray-800 mb-3 flex items-center">
                        <svg class="w-6 h-6 mr-2 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"></path>
                        </svg>
                        计算结果
                    </h2>
                    <!-- 结果显示区域 -->
                    <div class="space-y-4">
                        <!-- 加班薪资显示 -->
                        <div class="bg-blue-50 rounded-lg p-4 border-l-4 border-blue-500">
                            <div class="flex justify-between items-center">
                                <span class="text-gray-700 font-medium">加班薪资</span>
                                <span class="text-2xl font-bold text-blue-600" id="overtimePay">0 元</span>
                            </div>
                        </div>
                        <!-- 总计显示 -->
                        <div class="bg-green-50 rounded-lg p-4 border-l-4 border-green-500">
                            <div class="flex justify-between items-center">
                                <span class="text-gray-700 font-medium">总计 (底薪+加班)</span>
                                <span class="text-2xl font-bold text-green-600" id="totalPay">0 元</span>
                            </div>
                        </div>
                        <!-- 工时工资显示 -->
                        <div class="bg-purple-50 rounded-lg p-4 border-l-4 border-purple-500">
                            <div class="flex justify-between items-center">
                                <span class="text-gray-700 font-medium">小时工薪资</span>
                                <span class="text-2xl font-bold text-purple-600" id="workSalary">0 元</span>
                            </div>
                        </div>
                        <!-- 加G3薪资显示 -->
                        <div class="bg-orange-50 rounded-lg p-4 border-l-4 border-orange-500">
                            <div class="flex justify-between items-center">
                                <span class="text-gray-700 font-medium">加G3薪资</span>
                                <span class="text-2xl font-bold text-orange-600" id="totalWithG3">0 元</span>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- 统计图表卡片 -->
                <div class="bg-white rounded-xl shadow-lg p-6">
                    <!-- 标题 -->
                    <h2 class="text-2xl font-semibold text-gray-800 mb-3">薪资构成分析</h2>
                    <!-- 进度条图表 -->
                    <div class="space-y-4">
                        <!-- 底薪占比 -->
                        <div>
                            <div class="flex justify-between text-sm mb-1">
                                <span>底薪</span>
                                <span id="basePercent">0%</span>
                            </div>
                            <div class="w-full bg-gray-200 rounded-full h-3">
                                <div id="baseBar" class="bg-blue-500 h-3 rounded-full" style="width: 0%"></div>
                            </div>
                        </div>
                        <!-- G1加班占比 -->
                        <div>
                            <div class="flex justify-between text-sm mb-1">
                                <span>G1 加班</span>
                                <span id="g1Percent">0%</span>
                            </div>
                            <div class="w-full bg-gray-200 rounded-full h-3">
                                <div id="g1Bar" class="bg-green-500 h-3 rounded-full" style="width: 0%"></div>
                            </div>
                        </div>
                        <!-- G2加班占比 -->
                        <div>
                            <div class="flex justify-between text-sm mb-1">
                                <span>G2 加班</span>
                                <span id="g2Percent">0%</span>
                            </div>
                            <div class="w-full bg-gray-200 rounded-full h-3">
                                <div id="g2Bar" class="bg-purple-500 h-3 rounded-full" style="width: 0%"></div>
                            </div>
                        </div>
                        <!-- G3加班占比 -->
                        <div>
                            <div class="flex justify-between text-sm mb-1">
                                <span>G3 加班</span>
                                <span id="g3Percent">0%</span>
                            </div>
                            <div class="w-full bg-gray-200 rounded-full h-3">
                                <div id="g3Bar" class="bg-orange-500 h-3 rounded-full" style="width: 0%"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- JavaScript 代码 -->
    <script>
        // 初始化数据对象，存储所有表单数据
        let formData = {
            baseSalary: 2600,        // 底薪
            regularDays: 22,         // 正班天数
            totalHours: 256,         // 总工时
            g1Hours: 40,             // G1加班工时
            g2Hours: 40,             // G2加班工时
            g3Hours: 0,              // G3加班工时
            hourlyRate: 2600 / 21.75 / 8,       // 时薪
            g1Rate: 22.41,           // G1加班费率
            g2Rate: 29.89,           // G2加班费率
            g3Rate: 44.83,           // G3加班费率
            workHours: 256,          // 工时
            workPrice: 23,           // 工价
            subsidy: 0               // 补贴
        };

        // 结果数据对象，存储计算结果
        let results = {
            overtimePay: 0,          // 加班薪资
            totalPay: 0,             // 总计
            workSalary: 0,           // 工时工资
            totalWithG3: 0           // 加G3工资
        };

        // 当前活动的标签页
        let activeTab = 'salary';

        // 切换标签页函数
        function switchTab(tabName) {
            // 更新当前活动标签页
            activeTab = tabName;
            
            // 重置所有标签页按钮样式
            document.getElementById('salaryTab').className = 'tab-button px-6 py-3 rounded-lg font-medium flex items-center';
            document.getElementById('workHourTab').className = 'tab-button px-6 py-3 rounded-lg font-medium flex items-center';
            document.getElementById('resultTab').className = 'tab-button px-6 py-3 rounded-lg font-medium flex items-center';
            
            // 为当前标签页添加活动样式
            document.getElementById(tabName + 'Tab').className += ' active';

            // 隐藏所有内容区域
            document.getElementById('salaryContent').style.display = 'none';
            document.getElementById('workHourContent').style.display = 'none';
            document.getElementById('resultContent').style.display = 'none';

            // 根据标签页显示相应内容
            if (tabName === 'salary') {
                document.getElementById('salaryContent').style.display = 'block';
                document.getElementById('resultContent').style.display = 'block';
            } else if (tabName === 'workHour') {
                document.getElementById('workHourContent').style.display = 'block';
                document.getElementById('resultContent').style.display = 'block';
            } else if (tabName === 'result') {
                document.getElementById('salaryContent').style.display = 'block';
                document.getElementById('resultContent').style.display = 'block';
            }
        }

        // 计算函数
        function calculate() {
            // 获取表单数据并转换为数字
            formData.baseSalary = parseFloat(document.getElementById('baseSalary').value) || 0;
            formData.regularDays = parseFloat(document.getElementById('regularDays').value) || 0;
            formData.g1Hours = parseFloat(document.getElementById('g1Hours').value) || 0;
            formData.g2Hours = parseFloat(document.getElementById('g2Hours').value) || 0;
            formData.g3Hours = parseFloat(document.getElementById('g3Hours').value) || 0;
            formData.g1Rate = parseFloat(document.getElementById('g1Rate').value) || 0;
            formData.g2Rate = parseFloat(document.getElementById('g2Rate').value) || 0;
            formData.g3Rate = parseFloat(document.getElementById('g3Rate').value) || 0;
            formData.workHours = parseFloat(document.getElementById('workHours').value) || 0;
            formData.workPrice = parseFloat(document.getElementById('workPrice').value) || 0;
            formData.subsidy = parseFloat(document.getElementById('subsidy').value) || 0;

            // 计算时薪：底薪 / (正班天数 * 8小时)
            formData.hourlyRate = formData.baseSalary / (formData.regularDays * 8);
            // 显示时薪，保留两位小数
            document.getElementById('hourlyRate').value = formData.hourlyRate.toFixed(2);

            // 计算各项加班薪资
            const g1Pay = formData.g1Hours * formData.g1Rate;
            const g2Pay = formData.g2Hours * formData.g2Rate;
            const g3Pay = formData.g3Hours * formData.g3Rate;
            
            // 显示各项加班薪资
            document.getElementById('g1Pay').value = g1Pay.toFixed(2);
            document.getElementById('g2Pay').value = g2Pay.toFixed(2);
            document.getElementById('g3Pay').value = g3Pay.toFixed(2);

            // 计算总加班薪资
            results.overtimePay = g1Pay + g2Pay + g3Pay;
            // 计算总计：底薪 + 加班薪资
            results.totalPay = formData.baseSalary + results.overtimePay;
            // 计算工时工资：工时 * 工价 + 补贴
            results.workSalary = (formData.workHours * formData.workPrice) + formData.subsidy;
            // 计算加G3工资：工时工资 + G3加班薪资
            results.totalWithG3 = results.workSalary + g3Pay;

            // 更新结果显示
            document.getElementById('overtimePay').textContent = results.overtimePay.toFixed(2) + ' 元';
            document.getElementById('totalPay').textContent = results.totalPay.toFixed(2) + ' 元';
            document.getElementById('workSalary').textContent = results.workSalary.toFixed(2) + ' 元';
            document.getElementById('totalWithG3').textContent = results.totalWithG3.toFixed(2) + ' 元';

            // 更新表格中的数据
            document.getElementById('tableBaseSalary').textContent = formData.baseSalary + ' 元';
            document.getElementById('tableRegularDays').textContent = formData.regularDays + ' 天';
            document.getElementById('tableTotalHours').textContent = formData.totalHours + ' 小时';
            document.getElementById('tableG1Hours').textContent = formData.g1Hours + ' 小时';
            document.getElementById('tableG2Hours').textContent = formData.g2Hours + ' 小时';
            document.getElementById('tableG3Hours').textContent = formData.g3Hours + ' 小时';
            document.getElementById('tableWorkPrice').textContent = formData.workPrice + ' 元/小时';
            document.getElementById('tableSubsidy').textContent = formData.subsidy + ' 元';

            // 更新图表
            const total = results.totalPay;
            if (total > 0) {
                // 计算各项占比并更新显示
                document.getElementById('basePercent').textContent = ((formData.baseSalary / total) * 100).toFixed(1) + '%';
                document.getElementById('g1Percent').textContent = ((g1Pay / total) * 100).toFixed(1) + '%';
                document.getElementById('g2Percent').textContent = ((g2Pay / total) * 100).toFixed(1) + '%';
                document.getElementById('g3Percent').textContent = ((g3Pay / total) * 100).toFixed(1) + '%';
                
                // 更新进度条宽度
                document.getElementById('baseBar').style.width = (formData.baseSalary / total) * 100 + '%';
                document.getElementById('g1Bar').style.width = (g1Pay / total) * 100 + '%';
                document.getElementById('g2Bar').style.width = (g2Pay / total) * 100 + '%';
                document.getElementById('g3Bar').style.width = (g3Pay / total) * 100 + '%';
            }
        }

        // 页面加载完成后执行的函数
        window.onload = function() {
            // 默认显示薪资计算标签页
            switchTab('salary');
            // 执行一次计算，初始化数据显示
            calculate();
        };
    </script>
</body>
</html>
