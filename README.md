<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>代码练习工具</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            height: 100vh;
            overflow: hidden;
        }

        .container {
            display: flex;
            height: 100%;
        }

        .editor-pane, .preview-pane {
            flex: 1;
            padding: 20px;
            border: 1px solid #ccc;
            height: 100%;
        }

        #run-btn {
            position: fixed;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            padding: 12px 24px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            z-index: 100;
        }

        #run-btn:hover {
            background-color: #45a049;
        }

        .code-editor {
            height: calc(100% - 40px);
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            font-family: 'Courier New', Courier, monospace;
            margin-bottom: 10px;
        }

        #preview {
            width: 100%;
            height: 100%;
            border: none;
        }

        .editor-section {
            height: 50%;
        }

        .editor-section:first-child {
            margin-bottom: 20px;
        }

        .editor-section h3 {
            margin-bottom: 10px;
            color: #666;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="editor-pane">
            <div class="editor-section">
                <h3>HTML 代码</h3>
                <textarea class="code-editor" id="html-code" placeholder="输入HTML代码..."></textarea>
            </div>
            <div class="editor-section">
                <h3>CSS 代码</h3>
                <textarea class="code-editor" id="css-code" placeholder="输入CSS代码..."></textarea>
            </div>
        </div>
        
        <button id="run-btn">运行 ▶</button>
        
        <div class="preview-pane">
            <iframe id="preview"></iframe>
        </div>
    </div>

    <script>
        const runBtn = document.getElementById('run-btn');
        const htmlEditor = document.getElementById('html-code');
        const cssEditor = document.getElementById('css-code');
        const preview = document.getElementById('preview');

        function updatePreview() {
            const html = htmlEditor.value;
            const css = cssEditor.value;
            
            const fullCode = `
                <!DOCTYPE html>
                <html>
                <head>
                    <style>${css}</style>
                </head>
                <body>
                    ${html}
                </body>
                </html>
            `;

            preview.srcdoc = fullCode;
        }

        runBtn.addEventListener('click', updatePreview);
        
        // 初始示例代码
        htmlEditor.value = `<h1>欢迎使用代码练习工具</h1>\n<p>点击运行按钮查看效果</p>`;
        cssEditor.value = `body { padding: 20px; }\nh1 { color: #2196F3; }\np { color: #666; }`;
        updatePreview();
    </script>
</body>
</html>
