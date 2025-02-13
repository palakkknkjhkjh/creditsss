<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>✨ CREDITS ✨</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }
        body {
            text-align: center;
            background-color: #ffe4e1;
            padding: 20px;
        }
        h1 {
            color: #ff69b4;
        }
        .points-container {
            background: white;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            display: inline-block;
        }
        .member {
            margin: 10px 0;
            font-size: 1.2rem;
        }
        .hidden {
            display: none;
        }
        .admin-panel {
            margin-top: 20px;
            background: #fff0f5;
            padding: 15px;
            border-radius: 10px;
        }
        button {
            background: #ff69b4;
            color: white;
            border: none;
            padding: 10px;
            margin: 5px;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background: #ff1493;
        }
    </style>
</head>
<body>
    <h1>🌸 CREDITS 🌸</h1>
    <div class="points-container" id="pointsDisplay"></div>
    
    <div id="adminPanel" class="hidden admin-panel">
        <h2>Admin Panel 💖</h2>
        <input type="text" id="memberName" placeholder="Member Name">
        <input type="number" id="points" placeholder="Points" min="-100" max="100">
        <button onclick="addPoints()">Add Points</button>
        <button onclick="deductPoints()">Deduct Points</button>
    </div>
    
    <script>
        let members = JSON.parse(localStorage.getItem("members")) || {};
        let isAdmin = false;

        function displayPoints() {
            let container = document.getElementById("pointsDisplay");
            container.innerHTML = "";
            for (let member in members) {
                container.innerHTML += `<div class='member'>${member}: ${members[member]} pts</div>`;
            }
        }
        
        function addPoints() {
            if (!isAdmin) return;
            let name = document.getElementById("memberName").value.trim();
            let points = parseInt(document.getElementById("points").value) || 0;
            if (name) {
                members[name] = (members[name] || 0) + points;
                localStorage.setItem("members", JSON.stringify(members));
                displayPoints();
            }
        }
        
        function deductPoints() {
            if (!isAdmin) return;
            let name = document.getElementById("memberName").value.trim();
            let points = parseInt(document.getElementById("points").value) || 0;
            if (name) {
                members[name] = (members[name] || 0) - points;
                localStorage.setItem("members", JSON.stringify(members));
                displayPoints();
            }
        }
        
        function enableAdminMode() {
            let pass = prompt("Enter Admin Password:");
            if (pass === "palak@7588") { // Change to your secret password
                isAdmin = true;
                document.getElementById("adminPanel").classList.remove("hidden");
            }
        }
        
        document.addEventListener("keydown", (e) => {
            if (e.key === "a" && e.ctrlKey) {
                enableAdminMode();
            }
        });
        
        displayPoints();
    </script>
</body>
</html>
