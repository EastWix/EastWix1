<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>EastWix - Minecraft Server</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #0a0f2a 0%, #0a1a3a 50%, #001a4a 100%);
            font-family: 'Segoe UI', 'Minecraft', 'Tahoma', sans-serif;
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }

        /* Moving Moon */
        .moon-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }

        .moon {
            position: absolute;
            width: 120px;
            height: 120px;
            background: radial-gradient(circle at 30% 30%, #fffde7, #fff9c4, #fff59d);
            border-radius: 50%;
            box-shadow: 0 0 60px rgba(255, 245, 157, 0.8), 0 0 120px rgba(255, 235, 100, 0.4);
            animation: moveMoon 25s infinite alternate ease-in-out;
            top: 10%;
            left: -80px;
        }

        .moon::before {
            content: "";
            position: absolute;
            width: 25px;
            height: 25px;
            background: rgba(200, 180, 100, 0.3);
            border-radius: 50%;
            top: 30px;
            left: 40px;
            box-shadow: 40px 20px 0 rgba(180, 160, 80, 0.2), 70px 50px 0 rgba(190, 170, 90, 0.15);
        }

        @keyframes moveMoon {
            0% { transform: translate(0, 0); left: -80px; top: 5%; }
            50% { transform: translate(0, 30px); left: 60%; top: 20%; }
            100% { transform: translate(0, -20px); left: calc(100% + 50px); top: 70%; }
        }

        /* Blue Fire */
        .blue-fire {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 120px;
            pointer-events: none;
            z-index: 5;
        }

        .flame {
            position: absolute;
            bottom: 0;
            background: linear-gradient(0deg, #0066ff, #00ccff, #0099ff);
            border-radius: 50% 50% 20% 20%;
            opacity: 0.7;
            filter: blur(3px);
            animation: burn 0.8s infinite alternate ease-in-out;
        }

        @keyframes burn {
            0% { transform: scaleY(0.8) scaleX(0.9); opacity: 0.4; }
            100% { transform: scaleY(1.2) scaleX(1.1); opacity: 0.9; }
        }

        /* Container */
        .container {
            position: relative;
            z-index: 10;
            max-width: 1200px;
            width: 90%;
            margin: 50px auto;
            padding: 20px;
        }

        /* Glass Card */
        .glass-card {
            background: rgba(10, 20, 40, 0.7);
            backdrop-filter: blur(12px);
            border-radius: 40px;
            padding: 30px;
            margin-bottom: 30px;
            border: 1px solid rgba(0, 180, 255, 0.4);
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.3);
            transition: transform 0.3s ease;
        }

        .glass-card:hover {
            transform: translateY(-3px);
        }

        /* Server Name */
        .server-name {
            text-align: center;
            margin-bottom: 30px;
            font-size: 4rem;
            font-weight: bold;
        }
        .east { color: #00d4ff; display: inline-block; animation: wave 2s infinite; }
        .wix { color: #ffffff; display: inline-block; animation: wave 2s infinite 0.1s; }
        @keyframes wave {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-8px); }
        }

        /* Buttons */
        .btn {
            background: linear-gradient(135deg, #001f3f, #000c1a);
            border: 1px solid #00d4ff;
            color: #00d4ff;
            padding: 10px 25px;
            border-radius: 60px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 5px;
        }
        .btn:hover {
            background: #00d4ff;
            color: #000c1a;
            box-shadow: 0 0 15px #00d4ff;
        }
        .btn-danger {
            border-color: #ff4444;
            color: #ff8888;
        }
        .btn-danger:hover {
            background: #ff4444;
            color: white;
        }
        .btn-success {
            border-color: #44ff44;
            color: #88ff88;
        }
        .btn-success:hover {
            background: #44ff44;
            color: #001f3f;
        }

        /* Forms */
        input, textarea, select {
            width: 100%;
            padding: 12px;
            margin: 8px 0;
            background: rgba(0, 0, 0, 0.5);
            border: 1px solid #00d4ff;
            border-radius: 20px;
            color: white;
            font-size: 1rem;
        }
        label {
            color: #00d4ff;
            font-weight: bold;
        }

        /* Sections */
        .section-title {
            color: #00d4ff;
            font-size: 1.8rem;
            margin-bottom: 20px;
            border-left: 5px solid #00d4ff;
            padding-left: 15px;
        }

        .apply-card {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 25px;
            padding: 20px;
            margin: 15px 0;
            border: 1px solid rgba(0, 180, 255, 0.3);
        }

        .complaint-item {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 20px;
            padding: 15px;
            margin: 10px 0;
            border-left: 4px solid #ffaa44;
        }

        .rank-request {
            background: rgba(0, 0, 0, 0.5);
            border-radius: 20px;
            padding: 15px;
            margin: 10px 0;
            border: 1px solid #44ff44;
        }

        .hidden {
            display: none;
        }

        .flex-between {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
        }

        /* Instagram Footer - 3 accounts */
        .instagram-footer {
            text-align: center;
            margin-top: 30px;
            padding: 20px;
            border-top: 1px solid rgba(0, 180, 255, 0.3);
        }
        
        .social-links {
            display: flex;
            justify-content: center;
            gap: 30px;
            flex-wrap: wrap;
            margin-top: 10px;
        }
        
        .social-links a {
            color: #ff66aa;
            text-decoration: none;
            font-size: 1.1rem;
            transition: 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            background: rgba(255, 255, 255, 0.1);
            padding: 8px 20px;
            border-radius: 50px;
            backdrop-filter: blur(5px);
        }
        
        .social-links a:hover {
            color: #ff99cc;
            text-shadow: 0 0 10px #ff66aa;
            background: rgba(255, 255, 255, 0.2);
            transform: scale(1.05);
        }
        
        .footer-text {
            margin-top: 15px;
            color: #88aaff;
            font-size: 0.8rem;
        }

        .warning {
            color: #ffaa44;
            font-size: 0.9rem;
            margin-top: 10px;
        }
    </style>
</head>
<body>

<div class="moon-container">
    <div class="moon"></div>
</div>
<div class="blue-fire" id="blueFireContainer"></div>

<div class="container" id="app">
    <!-- Login / Signup Section -->
    <div id="authSection" class="glass-card">
        <div class="server-name">
            <span class="east">East</span><span class="wix">Wix</span>
        </div>
        <div style="text-align: center; margin-bottom: 20px;">
            <button class="btn" onclick="showLogin()">Login</button>
            <button class="btn" onclick="showSignup()">Sign Up</button>
        </div>

        <!-- Login Form -->
        <div id="loginForm">
            <h3 style="color:#00d4ff;">Login</h3>
            <input type="text" id="loginUsername" placeholder="Username">
            <input type="password" id="loginPassword" placeholder="Password">
            <button class="btn btn-success" onclick="login()">Login</button>
        </div>

        <!-- Signup Form -->
        <div id="signupForm" class="hidden">
            <h3 style="color:#00d4ff;">Sign Up</h3>
            <input type="text" id="signupUsername" placeholder="Username">
            <input type="password" id="signupPassword" placeholder="Password">
            <button class="btn btn-success" onclick="signup()">Sign Up</button>
        </div>
    </div>

    <!-- Dashboard (after login) -->
    <div id="dashboardSection" class="hidden">
        <div class="glass-card">
            <div class="flex-between">
                <div class="server-name" style="font-size:2rem; margin-bottom:0;">
                    <span class="east">East</span><span class="wix">Wix</span>
                </div>
                <button class="btn btn-danger" onclick="logout()">Logout</button>
            </div>
            <div style="margin: 20px 0; text-align:center;">
                <p style="color:#bbddff;">✨ The server is always open and the staff is always available. ✨</p>
                <p style="color:#88aaff;">🌐 IP: EastWix.mcserver.me:19132</p>
            </div>
        </div>

        <!-- Admin Panel (visible only to owner) -->
        <div id="adminPanel" class="glass-card hidden">
            <h2 class="section-title">🔧 Admin Control Panel</h2>
            
            <!-- Complaints Management -->
            <h3 style="color:#ffaa44;">📢 All Complaints</h3>
            <div id="adminComplaintsList"></div>

            <!-- Rank Apply Management -->
            <h3 style="color:#44ff44;">👑 Rank Applications Management</h3>
            <button class="btn btn-success" onclick="showCreateApplyForm()">+ Create New Apply</button>
            <div id="createApplyForm" class="hidden" style="margin-top:15px; padding:15px; background:rgba(0,0,0,0.5); border-radius:20px;">
                <input type="text" id="newRankName" placeholder="Rank Name (e.g., VIP, Moderator)">
                <input type="text" id="newRankTime" placeholder="Duration (e.g., 7 days, 24 hours, 30 days)">
                <button class="btn" onclick="createRankApply()">OK</button>
                <button class="btn btn-danger" onclick="hideCreateApplyForm()">Cancel</button>
            </div>
            <div id="activeAppliesList"></div>
            <h3 style="color:#88ff88; margin-top:20px;">📋 Submissions from players</h3>
            <div id="rankSubmissionsList"></div>
        </div>

        <!-- User Panel (visible to all logged in users) -->
        <div id="userPanel" class="glass-card">
            <div class="flex-between">
                <h2 class="section-title">🎮 Welcome, <span id="currentUsername"></span>!</h2>
            </div>

            <!-- Complaints Section -->
            <h3 class="section-title" style="font-size:1.4rem;">📝 Submit a Complaint</h3>
            <textarea id="complaintText" rows="3" placeholder="Write your complaint here..."></textarea>
            <button class="btn" onclick="submitComplaint()">Send Complaint</button>
            <div id="userComplaintsList" style="margin-top:20px;"></div>

            <!-- Rank Apply Section -->
            <h3 class="section-title" style="font-size:1.4rem; margin-top:30px;">👑 Rank Applications</h3>
            <div id="rankAppliesForUsers"></div>
        </div>

        <!-- Instagram Footer with 3 accounts -->
        <div class="instagram-footer">
            <div class="social-links">
                <a href="https://instagram.com/adam_d3ibes" target="_blank" rel="noopener noreferrer">
                    📷 @adam_d3ibes
                </a>
                <a href="https://www.instagram.com/_ahmad_hussie/" target="_blank" rel="noopener noreferrer">
                    📷 @_ahmad_hussien_
                </a>
                <a href="https://www.instagram.com/m07arab/" target="_blank" rel="noopener noreferrer">
                    📷 @m07arab
                </a>
            </div>
            <div class="footer-text">
                EastWix Minecraft Server | Follow us on Instagram
            </div>
        </div>
    </div>
</div>

<script>
    // Data storage (LocalStorage)
    let users = JSON.parse(localStorage.getItem('eastwix_users')) || [];
    let complaints = JSON.parse(localStorage.getItem('eastwix_complaints')) || [];
    let rankApplies = JSON.parse(localStorage.getItem('eastwix_rank_applies')) || [];
    let rankSubmissions = JSON.parse(localStorage.getItem('eastwix_rank_submissions')) || [];
    
    let currentUser = null;

    // Admin credentials
    const ADMIN_USERNAME = "owner";
    const ADMIN_PASSWORD = "eastadmin";

    // Initialize default admin if not exists
    function initAdmin() {
        if (!users.find(u => u.username === ADMIN_USERNAME)) {
            users.push({ username: ADMIN_USERNAME, password: ADMIN_PASSWORD, isAdmin: true });
            localStorage.setItem('eastwix_users', JSON.stringify(users));
        }
    }
    initAdmin();

    // UI Helpers
    function showLogin() {
        document.getElementById('loginForm').classList.remove('hidden');
        document.getElementById('signupForm').classList.add('hidden');
    }
    function showSignup() {
        document.getElementById('loginForm').classList.add('hidden');
        document.getElementById('signupForm').classList.remove('hidden');
    }

    function login() {
        const username = document.getElementById('loginUsername').value.trim();
        const password = document.getElementById('loginPassword').value.trim();
        const user = users.find(u => u.username === username && u.password === password);
        if (user) {
            currentUser = user;
            localStorage.setItem('eastwix_current_user', JSON.stringify(currentUser));
            document.getElementById('authSection').classList.add('hidden');
            document.getElementById('dashboardSection').classList.remove('hidden');
            document.getElementById('currentUsername').innerText = currentUser.username;
            if (currentUser.username === ADMIN_USERNAME) {
                document.getElementById('adminPanel').classList.remove('hidden');
            } else {
                document.getElementById('adminPanel').classList.add('hidden');
            }
            refreshAllData();
        } else {
            alert("Invalid username or password!");
        }
    }

    function signup() {
        const username = document.getElementById('signupUsername').value.trim();
        const password = document.getElementById('signupPassword').value.trim();
        if (!username || !password) {
            alert("Please fill all fields");
            return;
        }
        if (users.find(u => u.username === username)) {
            alert("Username already exists!");
            return;
        }
        users.push({ username, password, isAdmin: false });
        localStorage.setItem('eastwix_users', JSON.stringify(users));
        alert("Account created! Please login.");
        showLogin();
        document.getElementById('signupUsername').value = '';
        document.getElementById('signupPassword').value = '';
    }

    function logout() {
        currentUser = null;
        localStorage.removeItem('eastwix_current_user');
        document.getElementById('authSection').classList.remove('hidden');
        document.getElementById('dashboardSection').classList.add('hidden');
        document.getElementById('loginUsername').value = '';
        document.getElementById('loginPassword').value = '';
    }

    // Auto-login check
    function checkAutoLogin() {
        const saved = localStorage.getItem('eastwix_current_user');
        if (saved) {
            currentUser = JSON.parse(saved);
            if (currentUser && users.find(u => u.username === currentUser.username)) {
                document.getElementById('authSection').classList.add('hidden');
                document.getElementById('dashboardSection').classList.remove('hidden');
                document.getElementById('currentUsername').innerText = currentUser.username;
                if (currentUser.username === ADMIN_USERNAME) {
                    document.getElementById('adminPanel').classList.remove('hidden');
                } else {
                    document.getElementById('adminPanel').classList.add('hidden');
                }
                refreshAllData();
            } else {
                localStorage.removeItem('eastwix_current_user');
            }
        }
    }

    // Complaints
    function submitComplaint() {
        const text = document.getElementById('complaintText').value.trim();
        if (!text) {
            alert("Please write a complaint");
            return;
        }
        complaints.push({
            id: Date.now(),
            username: currentUser.username,
            text: text,
            date: new Date().toLocaleString()
        });
        localStorage.setItem('eastwix_complaints', JSON.stringify(complaints));
        document.getElementById('complaintText').value = '';
        refreshAllData();
    }

    // Rank Apply (Admin only)
    function showCreateApplyForm() {
        if (currentUser.username !== ADMIN_USERNAME) return;
        document.getElementById('createApplyForm').classList.remove('hidden');
    }
    function hideCreateApplyForm() {
        document.getElementById('createApplyForm').classList.add('hidden');
        document.getElementById('newRankName').value = '';
        document.getElementById('newRankTime').value = '';
    }
    function createRankApply() {
        let rankName = document.getElementById('newRankName').value.trim();
        let durationStr = document.getElementById('newRankTime').value.trim();
        if (!rankName || !durationStr) {
            alert("Please fill both fields");
            return;
        }
        // Parse duration
        let match = durationStr.match(/(\d+)\s*(day|days|hour|hours|minute|minutes)/i);
        let durationSeconds = 0;
        if (match) {
            let num = parseInt(match[1]);
            let unit = match[2].toLowerCase();
            if (unit.startsWith('day')) durationSeconds = num * 86400;
            else if (unit.startsWith('hour')) durationSeconds = num * 3600;
            else if (unit.startsWith('minute')) durationSeconds = num * 60;
        } else {
            alert("Use format like: 7 days, 24 hours, 30 minutes");
            return;
        }
        rankApplies.push({
            id: Date.now(),
            rankName: rankName,
            endTime: Date.now() + (durationSeconds * 1000),
            createdBy: currentUser.username,
            createdAt: Date.now()
        });
        localStorage.setItem('eastwix_rank_applies', JSON.stringify(rankApplies));
        hideCreateApplyForm();
        refreshAllData();
    }

    // User joins an apply
    function joinRankApply(applyId) {
        const apply = rankApplies.find(a => a.id === applyId);
        if (!apply) {
            alert("This application is no longer available");
            refreshAllData();
            return;
        }
        if (Date.now() > apply.endTime) {
            alert("This application deadline has passed!");
            refreshAllData();
            return;
        }
        const name = prompt("Enter your in-game name:");
        if (!name) return;
        const age = prompt("Enter your age:");
        if (!age) return;
        const why = prompt("Why do you want this rank?");
        if (!why) return;
        const country = prompt("Enter your country:");
        if (!country) return;
        
        rankSubmissions.push({
            id: Date.now(),
            applyId: applyId,
            rankName: apply.rankName,
            username: currentUser.username,
            name: name,
            age: age,
            why: why,
            country: country,
            submittedAt: new Date().toLocaleString()
        });
        localStorage.setItem('eastwix_rank_submissions', JSON.stringify(rankSubmissions));
        alert("Application submitted successfully!");
        refreshAllData();
    }

    // Delete expired rank applies
    function cleanExpiredApplies() {
        let changed = false;
        rankApplies = rankApplies.filter(a => {
            if (Date.now() > a.endTime) {
                changed = true;
                return false;
            }
            return true;
        });
        if (changed) localStorage.setItem('eastwix_rank_applies', JSON.stringify(rankApplies));
    }

    // Refresh all UI
    function refreshAllData() {
        cleanExpiredApplies();
        
        // Refresh user complaints list
        const userComplaintsDiv = document.getElementById('userComplaintsList');
        if (userComplaintsDiv) {
            const myComplaints = complaints.filter(c => c.username === currentUser.username);
            if (myComplaints.length === 0) {
                userComplaintsDiv.innerHTML = '<p style="color:#aaa;">No complaints yet.</p>';
            } else {
                userComplaintsDiv.innerHTML = myComplaints.map(c => `
                    <div class="complaint-item">
                        <strong>📅 ${c.date}</strong><br>
                        ${c.text.replace(/\n/g, '<br>')}
                    </div>
                `).join('');
            }
        }

        // Admin complaints list
        if (currentUser && currentUser.username === ADMIN_USERNAME) {
            const adminComplaintsDiv = document.getElementById('adminComplaintsList');
            if (adminComplaintsDiv) {
                if (complaints.length === 0) {
                    adminComplaintsDiv.innerHTML = '<p style="color:#aaa;">No complaints submitted yet.</p>';
                } else {
                    adminComplaintsDiv.innerHTML = complaints.map(c => `
                        <div class="complaint-item">
                            <strong>👤 ${c.username}</strong> | 📅 ${c.date}<br>
                            ${c.text.replace(/\n/g, '<br>')}
                        </div>
                    `).join('');
                }
            }

            // Active rank applies list for admin
            const activeAppliesDiv = document.getElementById('activeAppliesList');
            if (activeAppliesDiv) {
                if (rankApplies.length === 0) {
                    activeAppliesDiv.innerHTML = '<p style="color:#aaa;">No active rank applications.</p>';
                } else {
                    activeAppliesDiv.innerHTML = rankApplies.map(a => `
                        <div class="apply-card">
                            <strong>🎖️ ${a.rankName}</strong><br>
                            ⏰ Expires: ${new Date(a.endTime).toLocaleString()}<br>
                            <button class="btn btn-danger" style="margin-top:10px;" onclick="deleteRankApply(${a.id})">Delete Apply</button>
                        </div>
                    `).join('');
                }
            }

            // Submissions list for admin
            const submissionsDiv = document.getElementById('rankSubmissionsList');
            if (submissionsDiv) {
                if (rankSubmissions.length === 0) {
                    submissionsDiv.innerHTML = '<p style="color:#aaa;">No submissions yet.</p>';
                } else {
                    submissionsDiv.innerHTML = rankSubmissions.map(s => `
                        <div class="rank-request">
                            <strong>🎖️ Rank:</strong> ${s.rankName}<br>
                            <strong>👤 Applicant:</strong> ${s.username}<br>
                            <strong>🆔 IGN:</strong> ${s.name}<br>
                            <strong>📅 Age:</strong> ${s.age}<br>
                            <strong>🌍 Country:</strong> ${s.country}<br>
                            <strong>💬 Why:</strong> ${s.why}<br>
                            <strong>📅 Submitted:</strong> ${s.submittedAt}
                        </div>
                    `).join('');
                }
            }
        }

        // Rank applies for normal users
        const userAppliesDiv = document.getElementById('rankAppliesForUsers');
        if (userAppliesDiv && currentUser && currentUser.username !== ADMIN_USERNAME) {
            const activeApplies = rankApplies.filter(a => Date.now() < a.endTime);
            if (activeApplies.length === 0) {
                userAppliesDiv.innerHTML = '<p style="color:#aaa;">No open rank applications at the moment.</p>';
            } else {
                userAppliesDiv.innerHTML = activeApplies.map(a => `
                    <div class="apply-card">
                        <strong>🎖️ Rank:</strong> ${a.rankName}<br>
                        <strong>⏰ Deadline:</strong> ${new Date(a.endTime).toLocaleString()}<br>
                        <button class="btn btn-success" onclick="joinRankApply(${a.id})">Join</button>
                    </div>
                `).join('');
            }
        } else if (userAppliesDiv && currentUser && currentUser.username === ADMIN_USERNAME) {
            userAppliesDiv.innerHTML = '<p style="color:#ffaa44;">As admin, you cannot apply for ranks. Manage applications from Admin Panel.</p>';
        }
    }

    function deleteRankApply(applyId) {
        if (currentUser.username !== ADMIN_USERNAME) return;
        rankApplies = rankApplies.filter(a => a.id !== applyId);
        rankSubmissions = rankSubmissions.filter(s => s.applyId !== applyId);
        localStorage.setItem('eastwix_rank_applies', JSON.stringify(rankApplies));
        localStorage.setItem('eastwix_rank_submissions', JSON.stringify(rankSubmissions));
        refreshAllData();
    }

    // Blue Fire creation
    function createBlueFire() {
        const container = document.getElementById('blueFireContainer');
        for (let i = 0; i < 25; i++) {
            const flame = document.createElement('div');
            flame.classList.add('flame');
            flame.style.width = Math.random() * 40 + 15 + 'px';
            flame.style.height = Math.random() * 60 + 30 + 'px';
            flame.style.left = Math.random() * 100 + '%';
            flame.style.bottom = '0px';
            flame.style.animationDelay = Math.random() * 1 + 's';
            flame.style.animationDuration = Math.random() * 0.6 + 0.5 + 's';
            flame.style.opacity = Math.random() * 0.6 + 0.3;
            container.appendChild(flame);
        }
    }

    window.onload = () => {
        createBlueFire();
        checkAutoLogin();
        showLogin();
    };
</script>
</body>
</html>
