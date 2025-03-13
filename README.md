# fitness-tracking-dashboard
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Futuristic Fitness Dashboard</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet" />
  <style>
    body {
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      color: #E0E0E0;
      font-family: 'Poppins', sans-serif;
      transition: all 0.3s ease;
    }
    .card {
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(10px);
      border-radius: 15px;
      padding: 20px;
      margin-bottom: 20px;
    }
    .btn-glow {
      background: linear-gradient(to right, #FF512F, #F09819);
      box-shadow: 0 4px 15px rgba(255, 81, 47, 0.6);
      transition: all 0.3s ease;
    }
    .btn-glow:hover {
      box-shadow: 0 6px 20px rgba(255, 81, 47, 0.9);
      transform: scale(1.02);
    }
    .hidden { display: none; }
  </style>
</head>
<body>
  <div class="container mx-auto p-6">
    <h1 class="text-5xl font-bold text-center mb-8">Futuristic Fitness Dashboard</h1>
    
    <!-- Authentication Section -->
    <div id="authSection">
      <!-- Login Form -->  
      <div class="card" id="loginSection">
        <h2 class="text-2xl text-center mb-4">Login</h2>
        <form id="loginForm" class="flex flex-col gap-3">
          <input type="text" id="loginUsername" placeholder="Username" required class="border p-3 bg-gray-800 text-white rounded-lg" />
          <input type="password" id="loginPassword" placeholder="Password" required class="border p-3 bg-gray-800 text-white rounded-lg" />
          <button type="submit" class="btn-glow text-white p-3 rounded-lg">Login</button>
        </form>
        <p class="text-center mt-2">Don't have an account? 
          <span class="text-blue-400 cursor-pointer" onclick="toggleSection('signupSection')">Sign Up</span>
        </p>
      </div>
      
      <!-- Sign-Up Form -->  
      <div class="card hidden" id="signupSection">
        <h2 class="text-2xl text-center mb-4">Sign Up</h2>
        <form id="signupForm" class="flex flex-col gap-3">
          <input type="text" id="signupUsername" placeholder="Username" required class="border p-3 bg-gray-800 text-white rounded-lg" />
          <input type="password" id="signupPassword" placeholder="Password" required class="border p-3 bg-gray-800 text-white rounded-lg" />
          <button type="submit" class="btn-glow text-white p-3 rounded-lg">Sign Up</button>
        </form>
        <p class="text-center mt-2">Already have an account? 
          <span class="text-blue-400 cursor-pointer" onclick="toggleSection('loginSection')">Log In</span>
        </p>
      </div>
    </div>
    
    <!-- Dashboard Section (Visible after login) -->
    <div id="dashboardSection" class="hidden">
      <div class="card flex justify-between items-center">
        <h2 class="text-2xl">Welcome, <span id="userGreeting"></span>!</h2>
        <button class="btn-glow text-white p-2 rounded-lg" onclick="logoutUser()">Logout</button>
      </div>
      
      <!-- Workout Logging Section -->  
      <div class="card" id="workoutSection">
        <h3 class="text-xl font-semibold mb-3">Workout Logging</h3>
        <form id="workoutForm" class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <input type="text" id="exercise" placeholder="Exercise" required class="border p-3 bg-gray-800 text-white rounded-lg" />
          <input type="number" id="duration" placeholder="Duration (mins)" required class="border p-3 bg-gray-800 text-white rounded-lg" />
          <input type="number" id="intensity" placeholder="Intensity (1-10)" min="1" max="10" required class="border p-3 bg-gray-800 text-white rounded-lg" />
          <input type="number" id="calories" placeholder="Calories Burned" required class="border p-3 bg-gray-800 text-white rounded-lg" />
          <button type="submit" class="col-span-2 btn-glow text-white p-3 rounded-lg">Log Workout</button>\n        </form>\n      </div>\n      \n      <!-- Progress Visualization Section -->\n      <div class=\"card\" id=\"progressSection\">\n        <h3 class=\"text-xl font-semibold mb-3\">Progress Visualization</h3>\n        <canvas id=\"progressChart\" class=\"w-full h-64\"></canvas>\n      </div>\n      \n      <!-- Goal Tracking Section -->\n      <div class=\"card\" id=\"goalSection\">\n        <h3 class=\"text-xl font-semibold mb-3\">Goal Tracking</h3>\n        <form id=\"goalForm\" class=\"grid grid-cols-1 md:grid-cols-2 gap-4\">\n          <input type=\"text\" id=\"goalDesc\" placeholder=\"Goal Description\" required class=\"border p-3 bg-gray-800 text-white rounded-lg\" />\n          <input type=\"number\" id=\"goalTarget\" placeholder=\"Target Value\" required class=\"border p-3 bg-gray-800 text-white rounded-lg\" />\n          <button type=\"submit\" class=\"col-span-2 btn-glow text-white p-3 rounded-lg\">Set Goal</button>\n        </form>\n      </div>\n      \n      <!-- Nutrition Tracker Section -->\n      <div class=\"card\" id=\"nutritionSection\">\n        <h3 class=\"text-xl font-semibold mb-3\">Nutrition Tracker</h3>\n        <div class=\"grid grid-cols-1 md:grid-cols-3 gap-4 text-center\">\n          <div class=\"p-4 bg-gray-800 rounded-lg\">\n            <p class=\"text-2xl font-bold text-green-400\">2100</p>\n            <p>Calories</p>\n          </div>\n          <div class=\"p-4 bg-gray-800 rounded-lg\">\n            <p class=\"text-2xl font-bold text-blue-400\">180</p>\n            <p>Proteins (g)</p>\n          </div>\n          <div class=\"p-4 bg-gray-800 rounded-lg\">\n            <p class=\"text-2xl font-bold text-yellow-400\">250</p>\n            <p>Carbs (g)</p>\n          </div>\n        </div>\n      </div>\n      \n      <!-- AI Support Chat Section -->\n      <div class=\"card\" id=\"chatSection\">\n        <h3 class=\"text-xl font-semibold mb-3\">AI Support Chat</h3>\n        <div id=\"chatContainer\" class=\"border p-4 h-64 overflow-y-auto bg-gray-800 rounded-lg mb-3\">\n          <div id=\"chatMessages\"></div>\n        </div>\n        <form id=\"chatForm\" class=\"flex gap-2\">\n          <input type=\"text\" id=\"chatInput\" placeholder=\"Ask a question...\" required class=\"flex-1 border p-3 bg-gray-700 text-white rounded-lg\" />\n          <button type=\"submit\" class=\"btn-glow text-white p-3 rounded-lg\">Send</button>\n        </form>\n      </div>\n      \n      <!-- Social Sharing Section -->\n      <div class=\"card\" id=\"socialSection\">\n        <h3 class=\"text-xl font-semibold mb-3\">Social Sharing</h3>\n        <div class=\"flex gap-4\">\n          <button class=\"btn-glow text-white p-3 rounded-lg flex-1\">Share on Facebook</button>\n          <button class=\"btn-glow text-white p-3 rounded-lg flex-1\">Share on Twitter</button>\n          <button class=\"btn-glow text-white p-3 rounded-lg flex-1\">Share on Instagram</button>\n        </div>\n      </div>\n    </div>\n  \n    <script>\n      // Toggle between sections (auth and dashboard)\n      function toggleSection(sectionId) {\n        document.querySelectorAll('#authSection, #dashboardSection').forEach(sec => sec.classList.add('hidden'));\n        document.getElementById(sectionId).classList.remove('hidden');\n      }\n\n      // Simple Authentication using localStorage\n      function signupUser() {\n        const username = document.getElementById('signupUsername').value;\n        const password = document.getElementById('signupPassword').value;\n        if (!username || !password) { alert('Fill all fields'); return; }\n        if (localStorage.getItem(username)) { alert('Username exists. Choose another.'); return; }\n        localStorage.setItem(username, password);\n        alert('Signup successful! Please login.');\n        toggleSection('loginSection');\n      }\n\n      function loginUser() {\n        const username = document.getElementById('loginUsername').value;\n        const password = document.getElementById('loginPassword').value;\n        if (localStorage.getItem(username) === password) {\n          localStorage.setItem('loggedInUser', username);\n          document.getElementById('userGreeting').textContent = username;\n          document.getElementById('authSection').classList.add('hidden');\n          document.getElementById('dashboardSection').classList.remove('hidden');\n        } else {\n          alert('Invalid credentials!');\n        }\n      }\n\n      function logoutUser() {\n        localStorage.removeItem('loggedInUser');\n        // Show auth section and reset forms\n        document.getElementById('loginForm').reset();\n        document.getElementById('signupForm').reset();\n        document.getElementById('dashboardSection').classList.add('hidden');\n        document.getElementById('authSection').classList.remove('hidden');\n        toggleSection('loginSection');\n      }\n\n      // Event listeners for auth forms\n      document.getElementById('signupForm').addEventListener('submit', (e) => {\n        e.preventDefault();\n        signupUser();\n      });\n      document.getElementById('loginForm').addEventListener('submit', (e) => {\n        e.preventDefault();\n        loginUser();\n      });\n\n      // Auto-login if user is already logged in\n      window.onload = function() {\n        const user = localStorage.getItem('loggedInUser');\n        if (user) {\n          document.getElementById('userGreeting').textContent = user;\n          document.getElementById('authSection').classList.add('hidden');\n          document.getElementById('dashboardSection').classList.remove('hidden');\n        } else {\n          toggleSection('loginSection');\n        }\n      };\n\n      // Workout Logging Example\n      document.getElementById('workoutForm').addEventListener('submit', (e) => {\n        e.preventDefault();\n        const exercise = document.getElementById('exercise').value;\n        const duration = document.getElementById('duration').value;\n        const intensity = document.getElementById('intensity').value;\n        const calories = document.getElementById('calories').value;\n        if (!exercise || !duration || !intensity || !calories) { alert('Fill all workout fields'); return; }\n        alert(`Logged Workout: ${exercise}, ${duration} mins, Intensity: ${intensity}, Calories: ${calories}`);\n        document.getElementById('workoutForm').reset();\n      });\n\n      // Chart.js Progress Visualization Example\n      const ctx = document.getElementById('progressChart').getContext('2d');\n      const progressChart = new Chart(ctx, {\n        type: 'line',\n        data: {\n          labels: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],\n          datasets: [{\n            label: 'Calories Burned',\n            data: [200, 450, 300, 500, 600, 750, 800],\n            borderColor: '#FF512F',\n            backgroundColor: 'rgba(255, 81, 47, 0.5)',\n            fill: true,\n            tension: 0.3\n          }]\n        },\n        options: {\n          responsive: true,\n          maintainAspectRatio: false\n        }\n      });\n\n      // AI Support Chat Example\n      document.getElementById('chatForm').addEventListener('submit', (e) => {\n        e.preventDefault();\n        const chatInput = document.getElementById('chatInput');\n        const message = chatInput.value;\n        if (!message.trim()) return;\n        const chatMessages = document.getElementById('chatMessages');\n        const userMsg = document.createElement('div');\n        userMsg.className = 'text-right mb-2';\n        userMsg.innerHTML = `<span class=\"bg-blue-500 px-3 py-1 rounded-lg inline-block\">${message}</span>`;\n        chatMessages.appendChild(userMsg);\n        const aiMsg = document.createElement('div');\n        aiMsg.className = 'text-left mb-2';\n        aiMsg.innerHTML = `<span class=\"bg-gray-600 px-3 py-1 rounded-lg inline-block\">Thinking...</span>`;\n        chatMessages.appendChild(aiMsg);\n        setTimeout(() => {\n          aiMsg.innerHTML = `<span class=\"bg-green-500 px-3 py-1 rounded-lg inline-block\">I can help you reach your goals!</span>`;\n        }, 1000);\n        chatInput.value = '';\n        chatMessages.scrollTop = chatMessages.scrollHeight;\n      });\n    </script>\n  </div>\n</body>\n</html>\n```

---

### Overview:
- **Authentication:** The user can sign up and log in. Once authenticated, the dashboard is displayed.
- **Workout Logging:** Users can enter workout details (exercise, duration, intensity, calories).
- **Progress Visualization:** A dynamic line chart shows sample progress data using Chart.js.
- **Goal Tracking:** Users can set fitness goals via a simple form.
- **Nutrition Tracker:** A dummy section displays nutrition metrics.
- **AI Support Chat:** A basic chat interface simulates an AI response.
- **Social Sharing:** Dummy buttons are provided for sharing progress on social platforms.

Feel free to further extend or integrate real-time APIs as needed! Let me know if you have any questions or need additional adjustments.
