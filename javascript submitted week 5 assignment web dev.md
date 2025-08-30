 javascript file
 
 <script>
        
        PART 1: JAVASCRIPT BASICS
   
        
        // Variables to store user data
        let userData = {
            name: '',
            age: 0,
            favoriteColor: '',
            isAdult: false
        };

        /**
         * Function to process and analyze user input data
         * Demonstrates variables, data types, operators, and conditionals
         */
        function processUserData() {
            // Get user input values
            const nameInput = document.getElementById('userName').value;
            const ageInput = document.getElementById('userAge').value;
            const colorInput = document.getElementById('favoriteColor').value;
            
            // Input validation using conditionals
            if (!nameInput.trim()) {
                displayError('userAnalysis', 'Please enter your name!');
                return;
            }
            
            if (!ageInput || ageInput < 1 || ageInput > 150) {
                displayError('userAnalysis', 'Please enter a valid age (1-150)!');
                return;
            }
            
            if (!colorInput) {
                displayError('userAnalysis', 'Please select your favorite color!');
                return;
            }
            
            // Store data in variables
            userData.name = nameInput.trim();
            userData.age = parseInt(ageInput);
            userData.favoriteColor = colorInput;
            userData.isAdult = userData.age >= 18; // Boolean operator
            
            // Process data using conditionals and operators
            let ageCategory = '';
            if (userData.age < 13) {
                ageCategory = 'child';
            } else if (userData.age < 18) {
                ageCategory = 'teenager';
            } else if (userData.age < 65) {
                ageCategory = 'adult';
            } else {
                ageCategory = 'senior';
            }
            
            // Create personalized message using template literals
            const analysis = `
🎉 Hello ${userData.name}!

📊 Your Profile Analysis:
• Age: ${userData.age} years old (${ageCategory})
• Adult Status: ${userData.isAdult ? 'Yes' : 'No'}
• Favorite Color: ${userData.favoriteColor}
• Birth Year: ${new Date().getFullYear() - userData.age}

🎨 Color Personality:
${getColorPersonality(userData.favoriteColor)}

💡 Fun Fact: You've been alive for approximately ${userData.age * 365} days!
            `;
            
            displaySuccess('userAnalysis', analysis);
            console.log('User data processed:', userData);
        }

        // ===========================================
        // PART 2: JAVASCRIPT FUNCTIONS
        // ===========================================
        
        /**
         * Function 1: Calculator with multiple operations
         * Demonstrates function parameters, return values, and switch statements
         */
        function calculate(num1, num2, operation) {
            // Convert strings to numbers
            const a = parseFloat(num1);
            const b = parseFloat(num2);
            
            // Input validation
            if (isNaN(a) || isNaN(b)) {
                return { error: 'Please enter valid numbers!' };
            }
            
            // Switch statement for different operations
            switch (operation) {
                case 'add':
                    return { result: a + b, formula: `${a} + ${b} = ${a + b}` };
                case 'subtract':
                    return { result: a - b, formula: `${a} - ${b} = ${a - b}` };
                case 'multiply':
                    return { result: a * b, formula: `${a} × ${b} = ${a * b}` };
                case 'divide':
                    if (b === 0) {
                        return { error: 'Cannot divide by zero!' };
                    }
                    return { result: a / b, formula: `${a} ÷ ${b} = ${(a / b).toFixed(2)}` };
                default:
                    return { error: 'Invalid operation!' };
            }
        }
        
        /**
         * Function to handle calculator button click
         */
        function performCalculation() {
            const num1 = document.getElementById('num1').value;
            const num2 = document.getElementById('num2').value;
            const operation = document.getElementById('operation').value;
            
            const result = calculate(num1, num2, operation);
            
            if (result.error) {
                displayError('calculatorResult', result.error);
            } else {
                displaySuccess('calculatorResult', `✅ ${result.formula}\nResult: ${result.result}`);
            }
        }
        
        /**
         * Function 2: Text formatter with multiple transformation options
         * Demonstrates string methods and function overloading concept
         */
        function transformText(text, format) {
            if (!text || text.trim() === '') {
                return { error: 'Please enter some text!' };
            }
            
            switch (format) {
                case 'uppercase':
                    return { result: text.toUpperCase(), description: 'Converted to UPPERCASE' };
                case 'lowercase':
                    return { result: text.toLowerCase(), description: 'Converted to lowercase' };
                case 'title':
                    return { 
                        result: text.toLowerCase().replace(/\b\w/g, char => char.toUpperCase()),
                        description: 'Converted to Title Case'
                    };
                case 'reverse':
                    return { 
                        result: text.split('').reverse().join(''),
                        description: 'Text reversed'
                    };
                default:
                    return { error: 'Invalid format!' };
            }
        }
        
        /**
         * Function to handle text formatting
         */
        function formatText(format) {
            const text = document.getElementById('textInput').value;
            const result = transformText(text, format);
            
            if (result.error) {
                displayError('textResult', result.error);
            } else {
                const output = `${result.description}:\n"${result.result}"`;
                displaySuccess('textResult', output);
            }
        }
        
        /**
         * Helper function: Get color personality description
         */
        function getColorPersonality(color) {
            const personalities = {
                red: 'Passionate and energetic! You love excitement and adventure.',
                blue: 'Calm and trustworthy! You value peace and stability.',
                green: 'Natural and balanced! You appreciate growth and harmony.',
                purple: 'Creative and mysterious! You have a unique perspective.',
                orange: 'Enthusiastic and friendly! You bring joy to others.'
            };
            
            return personalities[color] || 'You have excellent taste in colors!';
        }

        // ===========================================
        // PART 3: JAVASCRIPT LOOPS
        // ===========================================
        
        /**
         * Loop Example 1: For loop to generate patterns
         */
        function generatePattern() {
            const size = parseInt(document.getElementById('patternSize').value);
            
            if (!size || size < 1 || size > 10) {
                displayError('patternOutput', 'Please enter a valid size (1-10)!');
                return;
            }
            
            let pattern = '';
            
            // Nested for loops to create a triangle pattern
            for (let i = 1; i <= size; i++) {
                // Add spaces for centering
                for (let j = 1; j <= size - i; j++) {
                    pattern += ' ';
                }
                // Add stars
                for (let k = 1; k <= 2 * i - 1; k++) {
                    pattern += '*';
                }
                pattern += '\n';
            }
            
            const output = `Generated ${size}-level triangle pattern:\n\n${pattern}`;
            displaySuccess('patternOutput', output);
            console.log('Pattern generated with nested for loops');
        }
        
        /**
         * Loop Example 2: While loop for counter
         */
        let counterValue = 0;
        let counterInterval = null;
        
        function startCounter() {
            if (counterInterval) return; // Prevent multiple intervals
            
            counterInterval = setInterval(() => {
                counterValue++;
                document.getElementById('counterDisplay').textContent = counterValue;
                
                // Stop automatically at 100 (while loop concept)
                if (counterValue >= 100) {
                    stopCounter();
                    displaySuccess('counterDisplay', '🎉 Counter reached 100!');
                }
            }, 100);
            
            console.log('Counter started using while loop concept');
        }
        
        function stopCounter() {
            if (counterInterval) {
                clearInterval(counterInterval);
                counterInterval = null;
            }
        }
        
        function resetCounter() {
            stopCounter();
            counterValue = 0;
            document.getElementById('counterDisplay').textContent = '0';
        }
        
        /**
         * Loop Example 3: forEach loop for array processing
         */
        function processNumbers() {
            const input = document.getElementById('numbersInput').value;
            
            if (!input.trim()) {
                displayError('arrayResults', 'Please enter some numbers!');
                return;
            }
            
            // Convert input to array of numbers
            const numbers = input.split(',').map(num => parseFloat(num.trim())).filter(num => !isNaN(num));
            
            if (numbers.length === 0) {
                displayError('arrayResults', 'Please enter valid numbers separated by commas!');
                return;
            }
            
            let sum = 0;
            let product = 1;
            let evens = [];
            let odds = [];
            
            // Using forEach loop to process each number
            numbers.forEach((num, index) => {
                sum += num; // Calculate sum
                product *= num; // Calculate product
                
                // Separate evens and odds
                if (num % 2 === 0) {
                    evens.push(num);
                } else {
                    odds.push(num);
                }
                
                console.log(`Processing number ${index + 1}: ${num}`);
            });
            
            const average = sum / numbers.length;
            
            const results = `
📊 Array Processing Results:
• Original Array: [${numbers.join(', ')}]
• Length: ${numbers.length} numbers
• Sum: ${sum}
• Average: ${average.toFixed(2)}
• Product: ${product}
• Even Numbers: [${evens.join(', ') || 'none'}]
• Odd Numbers: [${odds.join(', ') || 'none'}]
• Min Value: ${Math.min(...numbers)}
• Max Value: ${Math.max(...numbers)}
            `;
            
            displaySuccess('arrayResults', results);
        }

        // ===========================================
        // PART 4: DOM MANIPULATION
        // ===========================================
        
        // Array to store tasks
        let tasks = [];
        let taskIdCounter = 0;
        
        /**
         * DOM Interaction 1: Add new task to the list
         */
        function addTask() {
            const taskInput = document.getElementById('newTask');
            const taskText = taskInput.value.trim();
            
            if (!taskText) {
                displayError('newTask', 'Please enter a task!');
                return;
            }
            
            // Create task object
            const task = {
                id: ++taskIdCounter,
                text: taskText,
                completed: false,
                createdAt: new Date().toLocaleTimeString()
            };
            
            // Add to tasks array
            tasks.push(task);
            
            // Clear input
            taskInput.value = '';
            
            // Update DOM
            renderTasks();
            console.log('Task added:', task);
        }
        
        /**
         * DOM Interaction 2: Render tasks dynamically
         */
        function renderTasks() {
            const taskList = document.getElementById('taskList');
            taskList.innerHTML = ''; // Clear existing content
            
            // Loop through tasks and create DOM elements
            tasks.forEach(task => {
                const listItem = document.createElement('li');
                listItem.className = `task-item ${task.completed ? 'completed' : ''}`;
                listItem.innerHTML = `
                    <strong>${task.text}</strong>
                    <small style="display: block; color: #666; margin-top: 5px;">
                        Created: ${task.createdAt} | ID: ${task.id}
                    </small>
                `;
                
                // Add click event listener to toggle completion
                listItem.addEventListener('click', () => toggleTask(task.id));
                
                // Add animation class
                listItem.classList.add('fade-in');
                
                taskList.appendChild(listItem);
            });
            
            // Update task statistics
            updateTaskStats();
        }
        
        /**
         * DOM Interaction 3: Toggle task completion status
         */
        function toggleTask(taskId) {
            // Find and toggle task
            const task = tasks.find(t => t.id === taskId);
            if (task) {
                task.completed = !task.completed;
                renderTasks(); // Re-render to show changes
                console.log(`Task ${taskId} toggled:`, task.completed);
            }
        }
        
        /**
         * Clear completed tasks
         */
        function clearCompletedTasks() {
            const initialLength = tasks.length;
            tasks = tasks.filter(task => !task.completed);
            const removedCount = initialLength - tasks.length;
            
            if (removedCount > 0) {
                renderTasks();
                console.log(`Removed ${removedCount} completed tasks`);
            }
        }
        
        /**
         * Update task statistics
         */
        function updateTaskStats() {
            const total = tasks.length;
            const completed = tasks.filter(task => task.completed).length;
            const remaining = total - completed;
            
            console.log(`Task Stats - Total: ${total}, Completed: ${completed}, Remaining: ${remaining}`);
        }
        
        /**
         * DOM Interaction 4: Add random inspirational quotes
         */
        function addRandomQuote() {
            const quotes = [
                "The best way to predict the future is to create it. - Peter Drucker",
                "Code is like humor. When you have to explain it, it's bad. - Cory House",
                "Learning never exhausts the mind. - Leonardo da Vinci",
                "The only way to do great work is to love what you do. - Steve Jobs",
                "Innovation distinguishes between a leader and a follower. - Steve Jobs"
            ];
            
            const randomQuote = quotes[Math.floor(Math.random() * quotes.length)];
            
            // Create new quote element
            const quoteElement = document.createElement('div');
            quoteElement.style.cssText = `
                background: linear-gradient(45deg, #667eea, #764ba2);
                color: white;
                padding: 20px;
                margin: 15px 0;
                border-radius: 10px;
                font-style: italic;
                text-align: center;
                animation: fadeIn 0.5s ease-in;
            `;
            quoteElement.innerHTML = `<p>"${randomQuote}"</p>`;
            
            // Add to dynamic content area
            document.getElementById('dynamicContent').appendChild(quoteElement);
            console.log('Random quote added:', randomQuote);
        }
        
        /**
         * DOM Interaction 5: Toggle between light and dark theme
         */
        let isDarkTheme = false;
        
        function changeTheme() {
            const container = document.querySelector('.container');
            
            if (!isDarkTheme) {
                // Switch to dark theme
                container.style.background = 'rgba(45, 55, 72, 0.95)';
                container.style.color = '#e2e8f0';
                document.body.style.background = 'linear-gradient(135deg, #2d3748 0%, #4a5568 100%)';
                isDarkTheme = true;
                console.log('Switched to dark theme');
            } else {
                // Switch back to light theme
                container.style.background = 'rgba(255, 255, 255, 0.95)';
                container.style.color = '#333';
                document.body.style.background = 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)';
                isDarkTheme = false;
                console.log('Switched to light theme');
            }
        }
        
        /**
         * DOM Interaction 6: Create new elements dynamically
         */
        function createElements() {
            const dynamicContent = document.getElementById('dynamicContent');
            
            // Create a container for new elements
            const elementContainer = document.createElement('div');
            elementContainer.style.cssText = `
                background: #f0fff4;
                border: 2px solid #48bb78;
                border-radius: 10px;
                padding: 20px;
                margin: 15px 0;
            `;
            
            // Create different types of elements
            const heading = document.createElement('h4');
            heading.textContent = '🎨 Dynamically Created Elements';
            heading.style.color = '#38a169';
            
            const paragraph = document.createElement('p');
            paragraph.innerHTML = `
                Created at: <strong>${new Date().toLocaleString()}</strong><br>
                Random number: <strong>${Math.floor(Math.random() * 1000)}</strong>
            `;
            
            const button = document.createElement('button');
            button.textContent = 'Remove This Element';
            button.style.background = '#e53e3e';
            button.onclick = () => elementContainer.remove();
            
            // Append elements
            elementContainer.appendChild(heading);
            elementContainer.appendChild(paragraph);
            elementContainer.appendChild(button);
            dynamicContent.appendChild(elementContainer);
            
            console.log('New elements created dynamically');
        }
        
        // ===========================================
        // UTILITY FUNCTIONS
        // ===========================================
        
        /**
         * Display error message in specified element
         */
        function displayError(elementId, message) {
            const element = document.getElementById(elementId);
            element.className = 'output error';
            element.textContent = `❌ ${message}`;
        }
        
        /**
         * Display success message in specified element
         */
        function displaySuccess(elementId, message) {
            const element = document.getElementById(elementId);
            element.className = 'output success';
            element.textContent = message;
        }
        
        // ===========================================
        // EVENT LISTENERS AND INITIALIZATION
        // ===========================================
        
        // Add keyboard event listeners for better UX
        document.addEventListener('DOMContentLoaded', function() {
            console.log('🚀 JavaScript Fundamentals Project Loaded!');
            console.log('This project demonstrates:');
            console.log('✅ Variables, data types, and conditionals');
            console.log('✅ Custom functions with parameters and return values');
            console.log('✅ For loops, while loops, and forEach iterations');
            console.log('✅ DOM element selection, creation, and manipulation');
            console.log('✅ Event handling and dynamic content updates');
            
            // Add Enter key support for inputs
            document.getElementById('newTask').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    addTask();
                }
            });
            
            document.getElementById('userName').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    processUserData();
                }
            });
            
            document.getElementById('numbersInput').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    processNumbers();
                }
            });
        });
html file

  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JavaScript Fundamentals Project</title>
   \\
    <script src="js/script.js"></script>
</head>
<body>
    <div class="container">
        <h1>JavaScript Fundamentals Project</h1>
        
        <!-- User Data Analysis Section -->
        <section id="userDataSection">
            <h2>👤 User Data Analysis</h2>
            <div class="input-group">
                <input type="text" id="userName" placeholder="Enter your name">
                <input type="number" id="userAge" placeholder="Enter your age" min="1" max="150">
                <input type="color" id="favoriteColor" value="#ff0000">
                <button onclick="processUserData()">Analyze Data</button>
            </div>
            <pre id="userAnalysis" class="output"></pre>
        </section>
        
        <!-- Calculator Section -->
        <section id="calculatorSection">
            <h2>🧮 Calculator</h2>
            <div class="input-group">
                <input type="text" id="num1" placeholder="Enter first number">
                <input type="text" id="num2" placeholder="Enter second number">
                <select id="operation">
                    <option value="add">Add</option>
                    <option value="subtract">Subtract</option>
                    <option value="multiply">Multiply</option>
                    <option value="divide">Divide</option>
                </select>
                <button onclick="performCalculation()">Calculate</button>
            </div>
            <pre id="calculatorResult" class="output"></pre>
        </section>
        
        <!-- Text Formatter Section -->
        <section id="textFormatterSection">
            <h2>🔤 Text Formatter</h2>
            <div class="input-group">
                <input type="text" id="textInput" placeholder="Enter text to format">
                <select id="textFormat">
                    <option value="uppercase">UPPERCASE</option>
                    <option value="lowercase">lowercase</option>
                    <option value="title">Title Case</option>
                    <option value="reverse">Reverse Text</option>
                </select>
                <button onclick="formatText(document.getElementById('textFormat').value)">Format Text</button>
            </div>
            <pre id="textResult" class="output"></pre>
        </section>
        
        <!-- Pattern Generator Section -->
        <section id="patternGeneratorSection">
            <h2>🔶 Pattern Generator</h2>
            <div class="input-group">
                <input type="number" id="patternSize" placeholder="Enter pattern size (1-10)" min="1" max="10">
                <button onclick="generatePattern()">Generate Pattern</button>
            </div>
            <pre id="patternOutput" class="output"></pre>
        </section>
        
        <!-- Number Processor Section -->
        <section id="numberProcessorSection">
            <h2>🔢 Number Processor</h2>
            <div class="input-group">
                <input type="text" id="numbersInput" placeholder="Enter numbers separated by commas">
                <button onclick="processNumbers()">Process Numbers</button>
            </div>
            <pre id="arrayResults" class="output"></pre>
        </section>
        
        <!-- Task Manager Section -->
        <section id="taskManagerSection">
            <h2>🗒️ Task Manager</h2>
            <div class="input-group">
                <input type="text" id="newTask" placeholder="Enter a new task">
                <button onclick="addTask()">Add Task</button>
            </div>
            <ul id="taskList"></ul>
            <button onclick="clearCompletedTasks()">Clear Completed Tasks</button>
        </section>
        
        <!-- Dynamic Content Section -->
        <section id="dynamicContentSection">
            <h2>✨ Dynamic Content</h2>
            <div id="dynamicContent"></div>
            <button onclick="addRandomQuote()">Add Random Quote</button>
            <button onclick="createElements()">Create Random Elements</button>
        </section>
        
        <!-- Theme Changer Section -->
        <section id="themeChangerSection">
            <h2>🎨 Theme Changer</h2>
            <button onclick="changeTheme()">Toggle Dark/Light Theme</button>
        </section>
        
        <!-- Footer Section -->
        <footer>
            <p>JavaScript Fundamentals Project - Demonstrating core JavaScript concepts and DOM manipulation.</p>
        </footer>
    </div>
    
    <!-- If you have inline JS, use a separate <script> block, but do NOT put <script src=...> inside it -->
    <script>
        // Your inline JavaScript code here (if any)
        // Do NOT include <script src=...> inside this block!
    </script>
</body>
</html>

