<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>注音書寫打卡系統</title>
    <style>
        body {
            font-family: 'Microsoft JhengHei', Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        h1 {
            color: #333;
            text-align: center;
        }
        .card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            padding: 20px;
            margin-bottom: 20px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input, textarea, select {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #45a049;
        }
        button.danger {
            background-color: #f44336;
        }
        button.danger:hover {
            background-color: #d32f2f;
        }
        button.secondary {
            background-color: #2196F3;
        }
        button.secondary:hover {
            background-color: #0b7dda;
        }
        .tabs {
            display: flex;
            flex-wrap: wrap;
            margin-bottom: 20px;
        }
        .tab {
            padding: 10px 20px;
            border: 1px solid #ddd;
            background-color: #f1f1f1;
            cursor: pointer;
        }
        .tab.active {
            background-color: white;
            border-bottom: none;
        }
        .tab-content {
            display: none;
        }
        .tab-content.active {
            display: block;
        }
        #result-message {
            padding: 10px;
            margin-top: 10px;
            border-radius: 4px;
            display: none;
        }
        .success {
            background-color: #dff0d8;
            color: #3c763d;
        }
        .error {
            background-color: #f2dede;
            color: #a94442;
        }
        .mobile-warning {
            background-color: #FFEB3B;
            padding: 10px;
            border-radius: 4px;
            margin-bottom: 15px;
            text-align: center;
            display: none;
        }
        .version {
            text-align: center;
            font-size: 12px;
            color: #888;
            margin-top: 30px;
        }
        @media (max-width: 600px) {
            .mobile-warning {
                display: block;
            }
            .tabs {
                justify-content: center;
            }
            .tab {
                flex: 1 0 auto;
                text-align: center;
                margin-bottom: 2px;
            }
        }
    </style>
</head>
<body>
    <h1>注音書寫打卡小程式</h1>
    
    <div class="mobile-warning">
        您正在使用行動裝置。完成打卡後，請務必關閉跳出的確認頁面。
    </div>
    
    <div class="tabs">
        <div class="tab active" onclick="openTab('tab-checkin')">打卡</div>
        <div class="tab" onclick="openTab('tab-history')">記錄</div>
        <div class="tab" onclick="openTab('tab-stats')">統計</div>
        <div class="tab" onclick="openTab('tab-admin')">管理</div>
        <div class="tab" onclick="openTab('tab-about')">關於</div>
    </div>

    <div id="tab-checkin" class="tab-content active">
        <div class="card">
            <!-- 使用最簡單的表單提交方式，避免任何JS兼容性問題 -->
            <form method="POST" action="https://script.google.com/macros/s/AKfycbxNqakyn8KhIV9o41W5qFqvy6p0Sw_pmij7aN3UmhVQpxZAt5mNxM51XWeFEBwqyO61/exec" target="_blank">
                <div class="form-group">
                    <label for="name">姓名：</label>
                    <input type="text" id="name" name="name" placeholder="請輸入你的姓名" required>
                </div>
                <div class="form-group">
                    <label for="activity">打卡項目：</label>
                    <select id="activity" name="activity">
                        <option value="注音書寫">注音書寫</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="description">備註：</label>
                    <textarea id="description" name="description" rows="3" placeholder="請輸入打卡備註（選填）"></textarea>
                </div>
                <button type="submit">打卡</button>
            </form>
        </div>
    </div>

    <div id="tab-history" class="tab-content">
        <div class="card">
            <h2>打卡歷史記錄</h2>
            <p>點擊下方按鈕查看所有打卡記錄：</p>
            <button class="secondary" onclick="window.open('https://script.google.com/macros/s/AKfycbxNqakyn8KhIV9o41W5qFqvy6p0Sw_pmij7aN3UmhVQpxZAt5mNxM51XWeFEBwqyO61/exec?action=viewRecords', '_blank')">查看打卡記錄</button>
        </div>
    </div>

    <div id="tab-stats" class="tab-content">
        <div class="card">
            <h2>打卡統計</h2>
            <p>點擊下方按鈕查看打卡統計：</p>
            <button class="secondary" onclick="window.open('https://script.google.com/macros/s/AKfycbxNqakyn8KhIV9o41W5qFqvy6p0Sw_pmij7aN3UmhVQpxZAt5mNxM51XWeFEBwqyO61/exec?action=viewStats', '_blank')">查看打卡統計</button>
        </div>
    </div>

    <div id="tab-admin" class="tab-content">
        <div class="card">
            <h2>管理功能</h2>
            <p>警告：清除記錄操作無法撤銷，請謹慎使用。</p>
            <button class="danger" onclick="if(confirm('確定要清除所有打卡記錄嗎？此操作無法撤銷！')) { window.open('https://script.google.com/macros/s/AKfycbxNqakyn8KhIV9o41W5qFqvy6p0Sw_pmij7aN3UmhVQpxZAt5mNxM51XWeFEBwqyO61/exec?action=clearRecords', '_blank'); }">清除所有記錄</button>
        </div>
    </div>

    <div id="tab-about" class="tab-content">
        <div class="card">
            <h2>關於此打卡系統</h2>
            <p>這是一個多人共享的注音書寫打卡系統，專為網頁託管環境優化。</p>
            <h3>使用說明</h3>
            <ol>
                <li>在「打卡」頁籤輸入姓名和備註</li>
                <li>點擊「打卡」按鈕提交</li>
                <li>確認後關閉跳出的確認頁面</li>
                <li>在「記錄」頁籤可查看所有打卡記錄</li>
                <li>在「統計」頁籤可查看打卡統計</li>
            </ol>
            <p>此系統使用 Google Sheets 作為後端數據存儲。</p>
            <p>API URL: https://script.google.com/macros/s/AKfycbxNqakyn8KhIV9o41W5qFqvy6p0Sw_pmij7aN3UmhVQpxZAt5mNxM51XWeFEBwqyO61/exec</p>
        </div>
    </div>

    <div class="version">
        注音書寫打卡系統 v3.0 (超簡化版)
    </div>

    <script>
        // 只保留最基本的頁籤切換功能
        function openTab(tabId) {
            // 隱藏所有頁籤內容
            var tabContents = document.getElementsByClassName('tab-content');
            for (var i = 0; i < tabContents.length; i++) {
                tabContents[i].classList.remove('active');
            }

            // 取消所有頁籤的活躍狀態
            var tabs = document.getElementsByClassName('tab');
            for (var i = 0; i < tabs.length; i++) {
                tabs[i].classList.remove('active');
            }

            // 顯示選中的頁籤
            document.getElementById(tabId).classList.add('active');
            
            // 設置選中頁籤的活躍狀態
            for (var i = 0; i < tabs.length; i++) {
                if (tabs[i].getAttribute('onclick').indexOf(tabId) > -1) {
                    tabs[i].classList.add('active');
                }
            }
        }

        // 儲存上次輸入的姓名到本地存儲
        if (localStorage.getItem('lastName')) {
            document.getElementById('name').value = localStorage.getItem('lastName');
        }

        document.querySelector('form').addEventListener('submit', function() {
            var name = document.getElementById('name').value;
            if (name) {
                localStorage.setItem('lastName', name);
            }
        });
    </script>
</body>
</html>
