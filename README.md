<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TVET Learn KE | E-Learning & Library for Kenyan TVET Students</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        :root {
            --primary: #006400;   /* Kenya green */
            --accent: #BD0000;    /* Kenya red */
        }
        body {
            font-family: 'Segoe UI', system-ui, sans-serif;
            background-color: #f8f9fa;
        }
        .navbar {
            background-color: var(--primary);
        }
        .hero {
            background: linear-gradient(rgba(0, 100, 0, 0.85), rgba(0, 100, 0, 0.85)), url('https://picsum.photos/id/1015/2000/1200') center/cover no-repeat;
            color: white;
            padding: 120px 0;
        }
        .card-course {
            transition: all 0.3s;
        }
        .card-course:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0,0,0,0.15);
        }
        .nav-link {
            color: white !important;
        }
        .nav-link:hover, .nav-link.active {
            color: #ffd700 !important;
        }
        .modal-header {
            background-color: var(--primary);
            color: white;
        }
        .flag-stripes {
            background: repeating-linear-gradient(90deg, #000, #000 10px, #fff 10px, #fff 20px, #BD0000 20px, #BD0000 30px, #006400 30px);
        }
        .page {
            display: none;
        }
        .page.active {
            display: block;
        }
    </style>
</head>
<body>

    <!-- NAVBAR -->
    <nav class="navbar navbar-expand-lg navbar-dark sticky-top">
        <div class="container">
            <a class="navbar-brand fw-bold fs-3" href="#" onclick="showPage('home')">
                <i class="fas fa-graduation-cap"></i> TVET Learn <span class="text-warning">KE</span>
            </a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item"><a class="nav-link" href="#" onclick="showPage('home')">Home</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="showPage('courses')">Courses</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="showPage('library')">Library</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="showPage('dashboard')" id="dashboard-link" style="display:none;">Dashboard</a></li>
                    <li class="nav-item">
                        <a class="nav-link" href="#" onclick="logout()" id="logout-btn" style="display:none;">Logout</a>
                    </li>
                </ul>
                <button class="btn btn-light ms-3" onclick="showLoginModal()" id="login-btn">Login</button>
                <button class="btn btn-warning ms-2" onclick="showSignupModal()" id="signup-btn">Sign Up</button>
            </div>
        </div>
    </nav>

    <!-- HOME / HERO -->
    <div id="home" class="page active">
        <section class="hero text-center">
            <div class="container">
                <h1 class="display-4 fw-bold">Empowering TVET Students Across Kenya</h1>
                <p class="lead mb-4">Free & interactive e-learning platform with a digital library for all TVET courses.<br>Learn anytime, anywhere with your admission number.</p>
                <button class="btn btn-lg btn-warning" onclick="showSignupModal()">Join Free Today</button>
                <div class="mt-5">
                    <img src="https://picsum.photos/id/1016/800/400" alt="TVET Students" class="img-fluid rounded shadow" style="max-height: 300px;">
                </div>
            </div>
        </section>

        <section class="py-5 bg-white">
            <div class="container">
                <div class="row text-center">
                    <div class="col-md-4">
                        <i class="fas fa-book fa-3x text-success mb-3"></i>
                        <h4>Digital Library</h4>
                        <p>Thousands of KNEC past papers, notes & e-books</p>
                    </div>
                    <div class="col-md-4">
                        <i class="fas fa-laptop fa-3x text-success mb-3"></i>
                        <h4>Interactive Courses</h4>
                        <p>Video lessons, quizzes & progress tracking</p>
                    </div>
                    <div class="col-md-4">
                        <i class="fas fa-users fa-3x text-success mb-3"></i>
                        <h4>TVET Focused</h4>
                        <p>Electrical, Mechanical, ICT, Agri-Business & more</p>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <!-- COURSES PAGE -->
    <div id="courses" class="page">
        <div class="container py-5">
            <h2 class="text-center mb-4">Our TVET Courses</h2>
            <div class="row mb-4">
                <div class="col-md-6">
                    <input type="text" id="course-search" class="form-control" placeholder="Search courses..." onkeyup="filterCourses()">
                </div>
                <div class="col-md-6">
                    <select id="category-filter" class="form-select" onchange="filterCourses()">
                        <option value="">All Categories</option>
                        <option value="Engineering">Engineering</option>
                        <option value="ICT">ICT</option>
                        <option value="Agriculture">Agriculture</option>
                        <option value="Construction">Construction</option>
                    </select>
                </div>
            </div>
            <div class="row" id="courses-grid"></div>
        </div>
    </div>

    <!-- LIBRARY PAGE -->
    <div id="library" class="page">
        <div class="container py-5">
            <h2 class="text-center mb-4">TVET Digital Library</h2>
            <div class="row mb-4">
                <div class="col-md-8">
                    <input type="text" id="library-search" class="form-control" placeholder="Search notes, past papers, e-books..." onkeyup="filterLibrary()">
                </div>
            </div>
            <div class="row" id="library-grid"></div>
        </div>
    </div>

    <!-- DASHBOARD PAGE (after login) -->
    <div id="dashboard" class="page">
        <div class="container py-5">
            <div class="row">
                <div class="col-md-3">
                    <div class="card shadow-sm">
                        <div class="card-body text-center">
                            <h5 id="student-name" class="fw-bold"></h5>
                            <p class="text-muted" id="admission-no"></p>
                            <hr>
                            <button class="btn btn-outline-success w-100 mb-2" onclick="showPage('courses')">Browse Courses</button>
                            <button class="btn btn-outline-primary w-100" onclick="showPage('library')">Open Library</button>
                        </div>
                    </div>
                </div>
                <div class="col-md-9">
                    <h4>My Enrolled Courses & Progress</h4>
                    <div id="my-courses-list" class="row"></div>
                    
                    <h4 class="mt-5">Quick Resources</h4>
                    <div class="row" id="quick-library"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- FOOTER -->
    <footer class="bg-dark text-white py-5">
        <div class="container">
            <div class="row">
                <div class="col-md-4">
                    <h5>TVET Learn KE</h5>
                    <p>Built for Kenyan TVET students by a fellow Kenyan developer.<br>Empowering skills for the future.</p>
                </div>
                <div class="col-md-4">
                    <h5>Quick Links</h5>
                    <ul class="list-unstyled">
                        <li><a href="#" onclick="showPage('courses')" class="text-white">Courses</a></li>
                        <li><a href="#" onclick="showPage('library')" class="text-white">Library</a></li>
                        <li><a href="https://www.tveta.go.ke" target="_blank" class="text-white">TVETA Official</a></li>
                    </ul>
                </div>
                <div class="col-md-4 text-end">
                    <p>&copy; 2026 TVET Learn KE. All rights reserved.<br>Made with ❤️ for Kenya's TVET students.</p>
                </div>
            </div>
        </div>
    </footer>

    <!-- LOGIN MODAL -->
    <div class="modal fade" id="loginModal">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Student Login</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <div class="mb-3">
                        <label>Email or Admission Number</label>
                        <input type="text" id="login-email" class="form-control" placeholder="e.g. student@kenya.ac.ke or ADM/123/2024">
                    </div>
                    <div class="mb-3">
                        <label>Password</label>
                        <input type="password" id="login-pass" class="form-control">
                    </div>
                    <button onclick="performLogin()" class="btn btn-success w-100">Login</button>
                </div>
                <div class="modal-footer">
                    <small>Don't have an account? <a href="#" onclick="switchToSignup()" class="text-success">Sign up</a></small>
                </div>
            </div>
        </div>
    </div>

    <!-- SIGNUP MODAL -->
    <div class="modal fade" id="signupModal">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Create Student Account</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <div class="row">
                        <div class="col-6">
                            <label>Full Name</label>
                            <input type="text" id="signup-name" class="form-control">
                        </div>
                        <div class="col-6">
                            <label>Admission Number</label>
                            <input type="text" id="signup-adm" class="form-control" placeholder="ADM/123/2024">
                        </div>
                    </div>
                    <div class="mb-3">
                        <label>Email</label>
                        <input type="email" id="signup-email" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label>Password</label>
                        <input type="password" id="signup-pass" class="form-control">
                    </div>
                    <button onclick="performSignup()" class="btn btn-warning w-100">Create Account</button>
                </div>
            </div>
        </div>
    </div>

    <!-- COURSE DETAIL MODAL -->
    <div class="modal fade" id="courseModal">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="modal-course-title"></h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <img id="modal-course-img" class="img-fluid rounded mb-3" style="width:100%; height:250px; object-fit:cover;">
                    <p id="modal-course-desc"></p>
                    <div class="row">
                        <div class="col-6"><strong>Level:</strong> <span id="modal-level"></span></div>
                        <div class="col-6"><strong>Duration:</strong> <span id="modal-duration"></span></div>
                    </div>
                    <hr>
                    <h6>Sample Lecture</h6>
                    <div class="ratio ratio-16x9">
                        <iframe id="modal-video" src="" title="Lecture" allowfullscreen></iframe>
                    </div>
                </div>
                <div class="modal-footer">
                    <button class="btn btn-success" onclick="enrollCurrentCourse()">Enroll Now</button>
                </div>
            </div>
        </div>
    </div>

    <!-- BOOK DETAIL MODAL -->
    <div class="modal fade" id="bookModal">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="modal-book-title"></h5>
                </div>
                <div class="modal-body text-center">
                    <i class="fas fa-book fa-5x text-success mb-3"></i>
                    <p id="modal-book-desc"></p>
                    <button class="btn btn-primary" onclick="downloadResource()">Download PDF / Notes</button>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // Sample Data
        let courses = [
            {
                id: 1,
                title: "Diploma in Electrical Engineering (Power Option)",
                category: "Engineering",
                level: "Diploma",
                duration: "3 Years",
                desc: "Covers power generation, transmission, installation and maintenance. Aligned with KNEC & TVETA curriculum.",
                image: "https://picsum.photos/id/201/400/250",
                video: "https://www.youtube.com/embed/3QhU9jd03a0"  // Sample electricity basics
            },
            {
                id: 2,
                title: "Certificate in Information Communication Technology",
                category: "ICT",
                level: "Certificate",
                duration: "1 Year",
                desc: "Computer basics, networking, programming and office applications for TVET students.",
                image: "https://picsum.photos/id/180/400/250",
                video: "https://www.youtube.com/embed/3QhU9jd03a0"
            },
            {
                id: 3,
                title: "Agri-Business Management",
                category: "Agriculture",
                level: "Diploma",
                duration: "2 Years",
                desc: "Modern farming, value addition, marketing and sustainable agriculture practices.",
                image: "https://picsum.photos/id/133/400/250",
                video: "https://www.youtube.com/embed/3QhU9jd03a0"
            },
            {
                id: 4,
                title: "Building Technology & Construction",
                category: "Construction",
                level: "Diploma",
                duration: "3 Years",
                desc: "Architectural drawing, quantity surveying and site management.",
                image: "https://picsum.photos/id/251/400/250",
                video: "https://www.youtube.com/embed/3QhU9jd03a0"
            },
            {
                id: 5,
                title: "Automotive Engineering",
                category: "Engineering",
                level: "Diploma",
                duration: "3 Years",
                desc: "Vehicle maintenance, engine repair and diagnostics.",
                image: "https://picsum.photos/id/201/400/250",
                video: "https://www.youtube.com/embed/3QhU9jd03a0"
            }
        ];

        let libraryResources = [
            { id: 101, title: "KNEC Electrical Installation Past Papers 2020-2024", type: "Past Papers", category: "Engineering", desc: "Complete set with answers" },
            { id: 102, title: "ICT Module I Notes - Computer Applications", type: "Notes", category: "ICT", desc: "Microsoft Office & basics" },
            { id: 103, title: "Agri-Business Value Chain eBook", type: "E-Book", category: "Agriculture", desc: "PDF - 120 pages" },
            { id: 104, title: "Building Technology Schemes of Work", type: "Schemes", category: "Construction", desc: "CDACC aligned" }
        ];

        let users = JSON.parse(localStorage.getItem('tvet_users')) || [];
        let currentUser = JSON.parse(localStorage.getItem('tvet_current_user')) || null;

        // Show page function
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            const page = document.getElementById(pageId);
            if (page) page.classList.add('active');
            
            if (pageId === 'dashboard' && currentUser) {
                renderDashboard();
            }
        }

        // Render courses grid
        function renderCourses(filteredCourses) {
            const grid = document.getElementById('courses-grid');
            grid.innerHTML = '';
            filteredCourses.forEach(course => {
                const card = document.createElement('div');
                card.className = 'col-md-4 mb-4';
                card.innerHTML = `
                    <div class="card card-course h-100">
                        <img src="${course.image}" class="card-img-top" style="height:180px; object-fit:cover;">
                        <div class="card-body">
                            <h5 class="card-title">${course.title}</h5>
                            <p class="card-text small text-muted">${course.level} • ${course.duration}</p>
                            <button class="btn btn-sm btn-outline-success w-100" onclick="viewCourse(${course.id})">View Details</button>
                        </div>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function filterCourses() {
            const search = document.getElementById('course-search').value.toLowerCase();
            const category = document.getElementById('category-filter').value;
            let filtered = courses;
            if (search) {
                filtered = filtered.filter(c => c.title.toLowerCase().includes(search));
            }
            if (category) {
                filtered = filtered.filter(c => c.category === category);
            }
            renderCourses(filtered);
        }

        // View single course
        let currentCourseId = null;
        function viewCourse(id) {
            const course = courses.find(c => c.id === id);
            if (!course) return;
            currentCourseId = id;
            document.getElementById('modal-course-title').textContent = course.title;
            document.getElementById('modal-course-desc').textContent = course.desc;
            document.getElementById('modal-level').textContent = course.level;
            document.getElementById('modal-duration').textContent = course.duration;
            document.getElementById('modal-course-img').src = course.image;
            document.getElementById('modal-video').src = course.video;
            new bootstrap.Modal(document.getElementById('courseModal')).show();
        }

        function enrollCurrentCourse() {
            if (!currentUser) {
                alert("Please login first!");
                bootstrap.Modal.getInstance(document.getElementById('courseModal')).hide();
                showLoginModal();
                return;
            }
            if (!currentUser.enrolled) currentUser.enrolled = [];
            if (!currentUser.enrolled.includes(currentCourseId)) {
                currentUser.enrolled.push(currentCourseId);
                saveCurrentUser();
                alert("Enrolled successfully! Check your Dashboard.");
            } else {
                alert("You are already enrolled in this course.");
            }
            bootstrap.Modal.getInstance(document.getElementById('courseModal')).hide();
        }

        // Library
        function renderLibrary(filtered) {
            const grid = document.getElementById('library-grid');
            grid.innerHTML = '';
            filtered.forEach(res => {
                const card = document.createElement('div');
                card.className = 'col-md-4 mb-4';
                card.innerHTML = `
                    <div class="card h-100">
                        <div class="card-body">
                            <h5>${res.title}</h5>
                            <p class="small text-muted">${res.type} • ${res.category}</p>
                            <button class="btn btn-sm btn-primary" onclick="viewBook(${res.id})">View / Download</button>
                        </div>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function filterLibrary() {
            const term = document.getElementById('library-search').value.toLowerCase();
            let filtered = libraryResources.filter(r => 
                r.title.toLowerCase().includes(term) || r.desc.toLowerCase().includes(term)
            );
            renderLibrary(filtered);
        }

        let currentBookId = null;
        function viewBook(id) {
            const book = libraryResources.find(b => b.id === id);
            currentBookId = id;
            document.getElementById('modal-book-title').textContent = book.title;
            document.getElementById('modal-book-desc').textContent = book.desc;
            new bootstrap.Modal(document.getElementById('bookModal')).show();
        }

        function downloadResource() {
            alert("✅ Resource downloaded! (In real app this would trigger actual PDF download)");
            bootstrap.Modal.getInstance(document.getElementById('bookModal')).hide();
        }

        // Auth
        function showLoginModal() {
            new bootstrap.Modal(document.getElementById('loginModal')).show();
        }

        function showSignupModal() {
            new bootstrap.Modal(document.getElementById('signupModal')).show();
        }

        function switchToSignup() {
            bootstrap.Modal.getInstance(document.getElementById('loginModal')).hide();
            setTimeout(() => showSignupModal(), 500);
        }

        function performSignup() {
            const name = document.getElementById('signup-name').value.trim();
            const adm = document.getElementById('signup-adm').value.trim();
            const email = document.getElementById('signup-email').value.trim();
            const pass = document.getElementById('signup-pass').value.trim();

            if (!name || !adm || !email || !pass) {
                alert("All fields are required!");
                return;
            }

            // Check if user exists
            if (users.find(u => u.email === email || u.adm === adm)) {
                alert("Account with this email or admission number already exists!");
                return;
            }

            const newUser = {
                id: Date.now(),
                name: name,
                adm: adm,
                email: email,
                password: pass,   // In production hash this!
                enrolled: []
            };

            users.push(newUser);
            localStorage.setItem('tvet_users', JSON.stringify(users));

            alert("Account created successfully! Please login.");
            bootstrap.Modal.getInstance(document.getElementById('signupModal')).hide();
            showLoginModal();
        }

        function performLogin() {
            const input = document.getElementById('login-email').value.trim();
            const pass = document.getElementById('login-pass').value.trim();

            const user = users.find(u => 
                (u.email === input || u.adm === input) && u.password === pass
            );

            if (user) {
                currentUser = user;
                localStorage.setItem('tvet_current_user', JSON.stringify(currentUser));
                bootstrap.Modal.getInstance(document.getElementById('loginModal')).hide();
                updateUIAfterLogin();
                showPage('dashboard');
            } else {
                alert("Invalid credentials. Try again or sign up.");
            }
        }

        function logout() {
            currentUser = null;
            localStorage.removeItem('tvet_current_user');
            updateUIAfterLogin();
            showPage('home');
        }

        function saveCurrentUser() {
            localStorage.setItem('tvet_current_user', JSON.stringify(currentUser));
        }

        function updateUIAfterLogin() {
            const loginBtn = document.getElementById('login-btn');
            const signupBtn = document.getElementById('signup-btn');
            const logoutBtn = document.getElementById('logout-btn');
            const dashboardLink = document.getElementById('dashboard-link');

            if (currentUser) {
                loginBtn.style.display = 'none';
                signupBtn.style.display = 'none';
                logoutBtn.style.display = 'inline-block';
                dashboardLink.style.display = 'inline-block';
            } else {
                loginBtn.style.display = 'inline-block';
                signupBtn.style.display = 'inline-block';
                logoutBtn.style.display = 'none';
                dashboardLink.style.display = 'none';
            }
        }

        function renderDashboard() {
            // Student info
            document.getElementById('student-name').textContent = currentUser.name;
            document.getElementById('admission-no').textContent = currentUser.adm;

            // My courses
            const container = document.getElementById('my-courses-list');
            container.innerHTML = '';
            
            if (currentUser.enrolled && currentUser.enrolled.length > 0) {
                currentUser.enrolled.forEach(id => {
                    const course = courses.find(c => c.id === id);
                    if (!course) return;
                    const progress = Math.floor(Math.random() * 70) + 30; // fake progress
                    const div = document.createElement('div');
                    div.className = 'col-md-6 mb-3';
                    div.innerHTML = `
                        <div class="card">
                            <div class="card-body">
                                <h6>${course.title}</h6>
                                <div class="progress mb-2" style="height: 8px;">
                                    <div class="progress-bar bg-success" style="width: ${progress}%"></div>
                                </div>
                                <small class="text-muted">${progress}% complete</small>
                            </div>
                        </div>
                    `;
                    container.appendChild(div);
                });
            } else {
                container.innerHTML = `<div class="col-12"><p class="text-muted">You haven't enrolled in any courses yet. <a href="#" onclick="showPage('courses')">Browse courses</a></p></div>`;
            }

            // Quick library
            const quick = document.getElementById('quick-library');
            quick.innerHTML = '';
            libraryResources.slice(0, 3).forEach(res => {
                const el = document.createElement('div');
                el.className = 'col-md-4';
                el.innerHTML = `
                    <div class="card h-100">
                        <div class="card-body">
                            <small class="text-success">${res.type}</small>
                            <p class="fw-bold small">${res.title}</p>
                            <button class="btn btn-sm btn-outline-primary" onclick="viewBook(${res.id})">Access</button>
                        </div>
                    </div>
                `;
                quick.appendChild(el);
            });
        }

        // Initialize
        function init() {
            // Render public pages
            renderCourses(courses);
            renderLibrary(libraryResources);

            // Check if user already logged in
            if (currentUser) {
                updateUIAfterLogin();
            } else {
                updateUIAfterLogin();
            }

            // Show home by default
            showPage('home');

            // Demo: pre-load a few users if none exist
            if (users.length === 0) {
                users = [
                    { id: 999, name: "John Kamau", adm: "ADM/456/2024", email: "john@demo.ke", password: "123456", enrolled: [1, 2] }
                ];
                localStorage.setItem('tvet_users', JSON.stringify(users));
            }
        }

        window.onload = init;
    </script>
</body>
</html>
