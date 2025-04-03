<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>代码练习工具</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Consolas', '微软雅黑', monospace;
            height: 100vh;
            display: flex;
        }

        .editor-container {
            width: 50%;
            height: 100%;
            padding: 20px;
            background-color: #1e1e1e;
        }

        .preview-container {
            width: 50%;
            height: 100%;
            background-color: #fff;
            border-left: 2px solid #333;
        }

        .code-box {
            height: calc(50% - 15px);
            margin-bottom: 10px;
            position: relative;
        }

        .code-box label {
            color: #fff;
            display: block;
            margin-bottom: 10px;
            font-size: 14px;
        }

        textarea {
            width: 100%;
            height: calc(100% - 25px);
            background-color: #252526;
            color: #d4d4d4;
            border: 1px solid #333;
            padding: 10px;
            resize: none;
            font-family: 'Consolas', monospace;
            font-size: 14px;
        }

        #run-btn {
            position: absolute;
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
            transition: background-color 0.3s;
            z-index: 100;
        }

        #run-btn:hover {
            background-color: #45a049;
        }

        #preview-frame {
            width: 100%;
            height: 100%;
            border: none;
        }
    </style>
</head>
<body>
    <div class="editor-container">
        <div class="code-box">
            <label>HTML 代码：</label>
            <textarea id="html-code" placeholder="输入HTML代码..."></textarea>
        </div>
        <div class="code-box">
            <label>CSS 代码：</label>
            <textarea id="css-code" placeholder="输入CSS代码..."></textarea>
        </div>
    </div>

    <button id="run-btn">运行 ▶</button>

    <div class="preview-container">
        <iframe id="preview-frame"></iframe>
    </div>

    <script>
        const runBtn = document.getElementById('run-btn');
        const htmlCode = document.getElementById('html-code');
        const cssCode = document.getElementById('css-code');
        const previewFrame = document.getElementById('preview-frame');

        function updatePreview() {
            const html = htmlCode.value;
            const css = `<style>${cssCode.value}</style>`;
            const fullCode = `
                <!DOCTYPE html>
                <html>
                <head>
                    <meta charset="UTF-8">
                    ${css}
                </head>
                <body>
                    ${html}
                </body>
                </html>
            `;
            
            previewFrame.srcdoc = fullCode;
        }

        // 添加事件监听
        runBtn.addEventListener('click', updatePreview);
        
        // 初始化示例代码
        htmlCode.value = `<div class="demo-box">\n  <h1>Hello World!</h1>\n  <p>点击运行查看效果</p>\n</div>`;
        cssCode.value = `.demo-box {\n  padding: 20px;\n  background-color: #f0f8ff;\n  text-align: center;\n}\n\ndemo-box h1 {\n  color: #4CAF50;\n}`;
        updatePreview(); // 初始化运行
    </script>
</body>
</html>
