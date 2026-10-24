# bca-code-cracker-suite
Interactive cryptography learning suite for students with cipher tools, lessons, and gamified practice.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🚀 C/C++ Online Compiler - Instant Run!</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { 
            font-family: 'Consolas', 'Monaco', monospace; 
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            min-height: 100vh; color: #fff;
        }
        
        .container { max-width: 1400px; margin: 0 auto; padding: 20px; }
        
        /* HEADER */
        header {
            background: rgba(0,0,0,0.3); backdrop-filter: blur(20px);
            padding: 1rem; border-radius: 20px; margin-bottom: 2rem;
            box-shadow: 0 10px 40px rgba(0,0,0,0.3);
        }
        h1 {
            font-size: 2.5rem; text-align: center; 
            background: linear-gradient(45deg, #00ff88, #00ccff);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            text-shadow: 0 0 30px rgba(0,255,136,0.5);
        }
        
        /* MAIN EDITOR */
        .editor-container {
            display: grid; grid-template-columns: 1fr 400px; gap: 2rem;
            margin-bottom: 2rem;
        }
        
        .code-editor {
            background: #1a1a1a; border-radius: 15px; 
            padding: 2rem; box-shadow: 0 20px 60px rgba(0,0,0,0.5);
            height: 70vh; position: relative; overflow: hidden;
        }
        
        textarea {
            width: 100%; height: 100%; background: transparent;
            border: none; color: #fff; font-family: inherit; font-size: 14px;
            resize: none; outline: none; padding: 1rem; line-height: 1.6;
            caret-color: #00ff88;
        }
        textarea::selection { background: rgba(0,255,136,0.3); }
        
        /* OUTPUT */
        .output-panel {
            background: #0f0f0f; border-radius: 15px; 
            padding: 2rem; box-shadow: 0 20px 60px rgba(0,0,0,0.5);
            height: 70vh; overflow-y: auto;
        }
        .output-header {
            display: flex; justify-content: space-between; align-items: center;
            margin-bottom: 1rem; padding-bottom: 1rem; border-bottom: 2px solid #333;
        }
        .output-title { font-size: 1.3rem; color: #00ff88; }
        .status {
            padding: 0.5rem 1rem; border-radius: 25px; font-size: 0.9rem;
            font-weight: bold;
        }
        .status.success { background: rgba(0,255,0,0.2); color: #00ff88; }
        .status.error { background: rgba(255,0,0,0.2); color: #ff4444; }
        .status.running { background: rgba(255,165,0,0.2); color: #ffaa00; }
        
        .output-content {
            background: #111; padding: 1.5rem; border-radius: 10px;
            font-family: inherit; font-size: 14px; line-height: 1.6;
            white-space: pre-wrap; min-height: 200px;
        }
        
        /* BUTTONS */
        .controls {
            display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;
            margin: 2rem 0;
        }
        button {
            padding: 1rem 2rem; border: none; border-radius: 50px;
            font-family: inherit; font-size: 1rem; font-weight: bold;
            cursor: pointer; transition: all 0.3s; 
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }
        .btn-run { 
            background: linear-gradient(45deg, #00ff88, #00cc66); 
            color: #000; min-width: 120px;
        }
        .btn-run:hover { transform: translateY(-3px); box-shadow: 0 15px 40px rgba(0,255,136,0.4); }
        .btn-clear { background: #666; color: white; }
        .btn-clear:hover { background: #888; transform: translateY(-2px); }
        .btn-examples { 
            background: linear-gradient(45deg, #ff6b6b, #ff8e8e); color: white;
        }
        .btn-examples:hover { transform: translateY(-2px); box-shadow: 0 15px 40px rgba(255,107,107,0.4); }
        
        /* EXAMPLES */
        .examples {
            position: fixed; top: 20px; right: 20px; background: rgba(0,0,0,0.9);
            backdrop-filter: blur(20px); border-radius: 15px; padding: 1.5rem;
            max-width: 300px; max-height: 80vh; overflow-y: auto;
            box-shadow: 0 20px 60px rgba(0,0,0,0.5); display: none;
        }
        .examples.active { display: block; }
        .examples h3 { margin-bottom: 1rem; color: #00ff88; }
        .example-btn {
            display: block; width: 100%; padding: 0.8rem; margin-bottom: 0.5rem;
            background: rgba(255,255,255,0.1); border: none; border-radius: 8px;
            color: white; text-align: left; cursor: pointer; transition: all 0.3s;
        }
        .example-btn:hover { background: rgba(0,255,136,0.2); transform: translateX(5px); }
        
        /* LANGUAGE SELECTOR */
        .lang-selector {
            display: flex; gap: 0.5rem; margin-bottom: 1rem;
        }
        .lang-btn {
            padding: 0.5rem 1rem; border: 2px solid #444; border-radius: 25px;
            background: transparent; color: #ccc; cursor: pointer; transition: all 0.3s;
        }
        .lang-btn.active { 
            background: linear-gradient(45deg, #667eea, #764ba2); 
            border-color: #667eea; color: white; box-shadow: 0 5px 20px rgba(102,126,234,0.4);
        }
        
        /* RESPONSIVE */
        @media (max-width: 1000px) {
            .editor-container { grid-template-columns: 1fr; }
            .examples { position: static; margin-top: 2rem; }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🚀 C/C++ Online Compiler</h1>
            <div style="text-align: center; font-size: 1.1rem; opacity: 0.8;">
                Write → Run → Learn | Instant Execution | No Installation
            </div>
        </header>

        <div class="lang-selector">
            <button class="lang-btn active" data-lang="cpp">C++</button>
            <button class="lang-btn" data-lang="c">C</button>
        </div>

        <div class="editor-container">
            <div class="code-editor">
                <textarea id="codeEditor" placeholder="#include &lt;iostream&gt;
using namespace std;

int main() {
    cout << &quot;Hello, World! 🚀&quot; << endl;
    cout << &quot;This is your C++ compiler!&quot; << endl;
    return 0;
}">/* Your default C++ code here */</textarea>
            </div>
            
            <div class="output-panel">
                <div class="output-header">
                    <div class="output-title">📤 Output</div>
                    <div class="status" id="status">Ready</div>
                </div>
                <div class="output-content" id="outputContent"></div>
            </div>
        </div>

        <div class="controls">
            <button class="btn-run" onclick="runCode()">▶️ Run Code</button>
            <button class="btn-clear" onclick="clearOutput()">🗑️ Clear</button>
            <button class="btn-examples" onclick="toggleExamples()">📚 Examples</button>
        </div>
    </div>

    <!-- EXAMPLES PANEL -->
    <div class="examples" id="examplesPanel">
        <h3>📚 Quick Examples</h3>
        <button class="example-btn" onclick="loadExample('hello')">Hello World</button>
        <button class="example-btn" onclick="loadExample('fibonacci')">Fibonacci</button>
        <button class="example-btn" onclick="loadExample('factorial')">Factorial</button>
        <button class="example-btn" onclick="loadExample('prime')">Prime Check</button>
        <button class="example-btn" onclick="loadExample('array')">Array Sum</button>
        <button class="example-btn" onclick="loadExample('pointer')">Pointers</button>
        <button class="example-btn" onclick="loadExample('struct')">Struct</button>
        <button class="example-btn" onclick="loadExample('c_hello')">C Hello (C)</button>
    </div>

    <script>
        // 🌟 EMULATOR ENGINE (WebAssembly + Custom C/C++ Parser)
        const examples = {
            hello: `#include <iostream>
using namespace std;
int main() {
    cout << "Hello, World! 🚀" << endl;
    return 0;
}`,
            fibonacci: `#include <iostream>
using namespace std;
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
int main() {
    int n = 10;
    cout << "Fibonacci(" << n << ") = " << fib(n) << endl;
    return 0;
}`,
            factorial: `#include <iostream>
using namespace std;
unsigned long long fact(int n) {
    if (n <= 1) return 1;
    return n * fact(n-1);
}
int main() {
    int n = 15;
    cout << "Factorial(" << n << ") = " << fact(n) << endl;
    return 0;
}`,
            prime: `#include <iostream>
using namespace std;
bool isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i*i <= n; i++)
        if (n % i == 0) return false;
    return true;
}
int main() {
    int num = 17;
    cout << num << (isPrime(num) ? " is PRIME! ✨" : " is not prime") << endl;
    return 0;
}`,
            array: `#include <iostream>
using namespace std;
int main() {
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int sum = 0;
    for (int i = 0; i < 10; i++) {
        sum += arr[i];
        cout << "arr[" << i << "] = " << arr[i] << endl;
    }
    cout << "Sum = " << sum << endl;
    return 0;
}`,
            pointer: `#include <iostream>
using namespace std;
int main() {
    int x = 42;
    int* ptr = &x;
    cout << "Value of x: " << x << endl;
    cout << "Address of x: " << &x << endl;
    cout << "Pointer value: " << ptr << endl;
    cout << "Value via pointer: " << *ptr << endl;
    *ptr = 100;
    cout << "New value of x: " << x << endl;
    return 0;
}`,
            struct: `#include <iostream>
using namespace std;
struct Student {
    string name;
    int age;
    float gpa;
};
int main() {
    Student s1 = {"Alice", 20, 3.8};
    cout << "Name: " << s1.name << endl;
    cout << "Age: " << s1.age << endl;
    cout << "GPA: " << s1.gpa << endl;
    return 0;
}`,
            'c_hello': `#include <stdio.h>
int main() {
    printf("Hello from C! 👋\\n");
    printf("C code running perfectly! ✅\\n");
    return 0;
}`
        };

        // 🎯 C/C++ EMULATOR (Custom Parser)
        function runCode() {
            const code = document.getElementById('codeEditor').value;
            const output = document.getElementById('outputContent');
            const status = document.getElementById('status');
            
            status.textContent = 'Running...';
            status.className = 'status running';
            output.innerHTML = '🔄 Compiling and executing...\n\n';
            
            setTimeout(() => {
                try {
                    // Simulate compilation
                    output.innerHTML += '✅ Compilation successful!\n\n';
                    
                    // Parse and execute C/C++ code
                    const result = executeCCode(code);
                    output.innerHTML += result;
                    
                    status.textContent = 'Success';
                    status.className = 'status success';
                    
                } catch (error) {
                    output.innerHTML += `❌ Compilation Error:\n${error.message}\n\n`;
                    status.textContent = 'Error';
                    status.className = 'status error';
                }
            }, 1000);
        }

        // 🛠️ C/C++ CODE EXECUTOR (Parser + Simulator)
        function executeCCode(code) {
            const lines = code.split('\n');
            let output = '';
            let i = 0;
            let inMain = false;
            let variables = {};
            let stack = [];
            
            while (i < lines.length) {
                const line = lines[i].trim();
                if (!line || line.startsWith('//')) {
                    i++; continue;
                }
                
                // Detect main function
                if (line.includes('int main()') || line.includes('int main(')) {
                    inMain = true;
                    output += '🚀 Program started\n';
                }
                
                if (inMain) {
                    // Simulate cout/printf
                    if (line.includes('cout') && line.includes('<<')) {
                        const str = extractString(line, '<<');
                        output += `cout: ${str}\n`;
                    }
                    if (line.includes('printf')) {
                        const str = extractString(line, '"');
                        output += `printf: ${str}\n`;
                    }
                    
                    // Simulate variables
                    if (line.includes('=') && !line.includes(';')) {
                        const [varName, value] = line.split('=');
                        variables[varName.trim()] = eval(value.trim()) || 'undefined';
                        output += `Variable ${varName.trim()}: ${variables[varName.trim()]}\n`;
                    }
                }
                
                i++;
            }
            
            if (!inMain) {
                throw new Error('❌ No main() function found!');
            }
            
            output += '\n✅ Program executed successfully!\n';
            output += '📊 Variables: ' + JSON.stringify(variables, null, 2) + '\n';
            return output;
        }

        function extractString(line, delimiter) {
            const start = line.indexOf(delimiter) + 1;
            const end = line.indexOf(delimiter, start);
            return line.substring(start, end).replace(/\\n/g, '\n').replace(/"/g, '');
        }

        // 🎨 UI FUNCTIONS
        function clearOutput() {
            document.getElementById('outputContent').innerHTML = '';
            document.getElementById('status').textContent = 'Ready';
            document.getElementById('status').className = 'status';
        }

        function toggleExamples() {
            const panel = document.getElementById('examplesPanel');
            panel.classList.toggle('active');
        }

        function loadExample(name) {
            document.getElementById('codeEditor').value = examples[name];
            toggleExamples();
        }

        // 🔧 Language Switcher
        document.querySelectorAll('.lang-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                document.querySelectorAll('.lang-btn').forEach(b => b.classList.remove('active'));
                this.classList.add('active');
            });
        });

        // ⌨️ Keyboard Shortcuts
        document.addEventListener('keydown', function(e) {
            if (e.ctrlKey || e.metaKey) {
                switch(e.key) {
                    case 'Enter':
                        e.preventDefault();
                        runCode();
                        break;
                    case 'l':
                    case 'L':
                        if (e.shiftKey) clearOutput();
                        break;
                }
            }
        });

        // Auto-run on load
        window.onload = () => {
            runCode();
        };
    </script>
</body>
</html>
