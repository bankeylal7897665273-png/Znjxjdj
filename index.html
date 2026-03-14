<?php
// ================= BACKEND API SYSTEM (Updated for Overwrite/Update) =================
if ($_SERVER["REQUEST_METHOD"] == "POST" && isset($_POST['action'])) {
    header('Content-Type: application/json');
    $action = $_POST['action'];

    if ($action === 'check_domain') {
        $domain = preg_replace('/[^a-zA-Z0-9_-]/', '', $_POST['domain']);
        if (empty($domain)) {
            echo json_encode(["status" => "empty"]); exit;
        }
        $target_dir = "sites/" . $domain . "/";
        if (file_exists($target_dir)) {
            echo json_encode(["status" => "taken"]);
        } else {
            echo json_encode(["status" => "available"]);
        }
        exit;
    }

    if ($action === 'upload') {
        $domain = preg_replace('/[^a-zA-Z0-9_-]/', '', $_POST['domain']);
        $is_update = isset($_POST['is_update']) ? $_POST['is_update'] : 'false';

        if (empty($domain)) {
            echo json_encode(["status" => "error", "msg" => "Domain name required!"]); exit;
        }

        $target_dir = "sites/" . $domain . "/";
        
        // Agar folder pehle se hai aur "update" flag nahi hai, tabhi error do.
        // Update flag hai toh seedha andar overwrite hone do.
        if (file_exists($target_dir) && $is_update === 'false') {
            echo json_encode(["status" => "error", "msg" => "This domain is already taken!"]); exit;
        }

        if (!file_exists($target_dir)) {
            mkdir($target_dir, 0777, true);
        }

        $uploaded_files = [];
        $main_file = "";

        if (!empty($_FILES['files']['name'][0])) {
            foreach ($_FILES['files']['name'] as $key => $name) {
                $tmp_name = $_FILES['files']['tmp_name'][$key];
                $safe_name = preg_replace('/[^a-zA-Z0-9_.-]/', '', $name);
                $dest = $target_dir . $safe_name;

                $ext = strtolower(pathinfo($safe_name, PATHINFO_EXTENSION));
                if (in_array($ext, ['php', 'phtml', 'php5', 'htaccess'])) continue;

                if (move_uploaded_file($tmp_name, $dest)) {
                    if(in_array($ext, ['html', 'htm', 'txt', 'js', 'css'])) {
                        $content = file_get_contents($dest);
                        $content = str_replace(array("<?", "?>"), array("&lt;?", "?&gt;"), $content);
                        file_put_contents($dest, $content);
                    }
                    $uploaded_files[] = $safe_name;
                    if (strtolower($safe_name) == 'index.html') $main_file = $safe_name;
                }
            }
        }

        if(empty($main_file) && count($uploaded_files) > 0) {
            $main_file = $uploaded_files[0];
        }

        $protocol = isset($_SERVER['HTTPS']) && $_SERVER['HTTPS'] === 'on' ? "https" : "http";
        $base_url = $protocol . "://" . $_SERVER['HTTP_HOST'] . dirname($_SERVER['PHP_SELF']);
        $base_url = rtrim($base_url, '/');
        $site_link = $base_url . "/" . $target_dir . ($main_file == 'index.html' ? '' : $main_file);
        $site_link = preg_replace('/([^:])(\/{2,})/', '$1/', $site_link);

        $msg = ($is_update === 'true') ? "Website Updated Successfully! 🔄" : "Website Live Ho Gayi Hai 🎉";

        echo json_encode(["status" => "success", "msg" => $msg, "link" => $site_link, "domain" => $domain]);
        exit;
    }
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>B2K CODE EDITOR</title>
    <style>
        /* Modern Yellow Theme - Extra Snappy */
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; }
        body { background-color: #ffffff; color: #333; overflow-x: hidden; }
        
        :root {
            --primary: #ff9800; /* Main Yellow/Orange */
            --primary-dark: #f57c00;
            --primary-light: #ffb74d;
        }

        /* Fast Click Animations */
        button, .project-card, .file-item, .yellow-banner { transition: transform 0.1s ease, background-color 0.2s ease; }
        button:active, .project-card:active, .file-item:active, .yellow-banner:active { transform: scale(0.97); }

        .app-bar { padding: 15px 20px; display: flex; align-items: center; justify-content: space-between; background: #fff; position: sticky; top: 0; z-index: 10; box-shadow: 0 2px 5px rgba(0,0,0,0.05);}
        .app-bar h2 { font-size: 20px; font-weight: 600; display: flex; align-items: center; gap: 10px;}
        .icon-btn { background: none; border: none; font-size: 24px; color: #555; cursor: pointer; display: flex; align-items: center; justify-content: center;}
        
        .view { display: none; padding-bottom: 80px; animation: fadeIn 0.2s ease; height: 100vh; overflow-y: auto;}
        .active-view { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .home-header { text-align: center; margin-top: 20px; }
        .logo { font-size: 32px; color: var(--primary); font-weight: bold; display: flex; align-items: center; justify-content: center; gap: 10px; margin-bottom: 30px;}
        .create-btn-container { text-align: center; margin-bottom: 40px; }
        .create-btn { background: #fff; border: 2px solid #888; color: #666; padding: 10px 20px; border-radius: 30px; font-size: 16px; font-weight: 500; display: inline-flex; align-items: center; gap: 8px; cursor: pointer; }
        .create-btn:active { background: #f0f0f0; }
        
        .projects-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; padding: 0 20px; }
        .project-card { background: #fff8e1; border: 1px solid #ffe082; padding: 20px 15px; border-radius: 12px; cursor: pointer; display: flex; flex-direction: column; gap: 10px; box-shadow: 0 4px 6px rgba(255, 152, 0, 0.1);}
        .card-icon { background: var(--primary); width: 30px; height: 40px; border-radius: 4px; position: relative;}
        .card-icon::after { content: ''; position: absolute; bottom: -5px; right: -5px; width: 12px; height: 12px; background: white; border-radius: 50%; border: 2px solid #fff8e1;}
        .card-title { font-weight: 600; font-size: 16px; word-break: break-all;}
        .card-date { font-size: 12px; color: #888; }

        .modal-overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 100; align-items: center; justify-content: center; backdrop-filter: blur(2px);}
        .modal { background: #fff; width: 85%; max-width: 400px; border-radius: 16px; padding: 25px; box-shadow: 0 10px 30px rgba(0,0,0,0.2); animation: scaleUp 0.2s ease;}
        @keyframes scaleUp { from { transform: scale(0.9); opacity: 0; } to { transform: scale(1); opacity: 1; } }
        .modal h3 { margin-bottom: 20px; font-size: 20px; color: #333;}
        .input-group { margin-bottom: 20px; position: relative; }
        .input-group label { display: block; font-size: 12px; color: var(--primary-dark); margin-bottom: 5px; font-weight: 600;}
        .modal input { width: 100%; border: none; border-bottom: 2px solid #ccc; font-size: 18px; padding: 5px 0; outline: none; transition: 0.2s;}
        .modal input:focus { border-bottom-color: var(--primary); }
        .modal-actions { display: flex; justify-content: space-between; margin-top: 30px; }
        .modal-btn { background: none; border: none; font-weight: 600; font-size: 14px; color: var(--primary-dark); cursor: pointer; text-transform: uppercase;}
        .modal-btn.cancel { color: #888; }
        .modal-btn:disabled { color: #ccc; cursor: not-allowed; }

        /* Spinner & Status for Checking */
        .status-container { display: flex; align-items: center; gap: 8px; margin-top: 10px; font-size: 13px; font-weight: 600; height: 20px;}
        .spinner { display: none; width: 16px; height: 16px; border: 2px solid #ccc; border-top-color: var(--primary); border-radius: 50%; animation: spin 0.8s linear infinite; }
        @keyframes spin { to { transform: rotate(360deg); } }
        .status-msg { color: #888; }
        .status-success { color: #4CAF50; }
        .status-error { color: #F44336; }

        /* SUCCESS POPUP */
        .success-popup { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 200; align-items: center; justify-content: center; }
        .popup-box { background: white; padding: 30px; border-radius: 16px; text-align: center; width: 85%; max-width: 320px; animation: dropDown 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        @keyframes dropDown { from { transform: translateY(-100px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        .house-icon { font-size: 60px; margin-bottom: 10px; }
        .success-btns { display: flex; justify-content: center; gap: 15px; margin-top: 20px; }
        .s-btn { padding: 10px 20px; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; }
        .btn-copy { background: #f0f0f0; color: #333; }
        .btn-open { background: var(--primary); color: white; }

        .yellow-banner { background: var(--primary); color: white; margin: 10px 20px; padding: 15px; border-radius: 12px; display: flex; align-items: center; gap: 10px; font-weight: 600; font-size: 16px; cursor: pointer; box-shadow: 0 4px 10px rgba(255, 152, 0, 0.3);}
        .yellow-banner:active { background: var(--primary-dark); }
        
        .file-list { padding: 10px 20px; display: flex; flex-direction: column; gap: 15px; }
        .file-item { display: flex; align-items: center; gap: 15px; padding: 10px; background: #fff8e1; border: 1px solid #ffe082; border-radius: 8px; cursor: pointer; }
        .file-icon { font-size: 24px; color: var(--primary); }
        .file-info { flex-grow: 1; overflow: hidden;}
        .file-name { font-size: 16px; font-weight: 500; white-space: nowrap; overflow: hidden; text-overflow: ellipsis;}
        
        /* Action buttons in app bar */
        .action-group { display: flex; gap: 15px; align-items: center;}

        #editor-container { display: flex; flex-direction: column; height: 100%; }
        textarea { flex-grow: 1; width: 100%; border: none; padding: 15px; font-family: monospace; font-size: 15px; outline: none; resize: none; background: #fafafa; color: #333; line-height: 1.5;}
        
        .editor-toolbar { position: fixed; bottom: 0; left: 0; width: 100%; background: #fff8e1; border-top: 1px solid #ffe082; padding: 10px; display: flex; align-items: center; justify-content: space-between; overflow-x: auto;}
        .keys { display: flex; gap: 15px; color: var(--primary-dark); font-family: monospace; font-size: 18px; padding-left: 10px; font-weight: bold;}
        .play-btn { background: var(--primary); color: white; border: none; width: 40px; height: 40px; border-radius: 8px; display: flex; align-items: center; justify-content: center; font-size: 20px; cursor: pointer; margin-left: auto; box-shadow: 0 2px 5px rgba(255,152,0,0.4);}

        #output-frame { width: 100%; height: 100%; border: none; background: #fff; }
    </style>
</head>
<body>

    <input type="file" id="local-file-upload" multiple style="display: none;">

    <div id="home-view" class="view active-view">
        <div class="home-header">
            <div class="logo">
                <div class="card-icon" style="width:24px; height:32px;"></div> B2K CODE EDITOR
            </div>
            <div class="create-btn-container">
                <button class="create-btn" onclick="openModal('create-modal')">+ Create Project</button>
            </div>
        </div>
        <div class="projects-grid" id="projects-grid"></div>
    </div>

    <div id="create-modal" class="modal-overlay">
        <div class="modal">
            <h3>Create Project</h3>
            <div class="input-group">
                <label>Project Name</label>
                <input type="text" id="new-project-name" value="My Website">
                <div class="status-container">
                    <span class="status-msg" id="project-status"></span>
                </div>
            </div>
            <div class="modal-actions">
                <button class="modal-btn cancel" onclick="closeModal('create-modal')">CANCEL</button>
                <button class="modal-btn" id="btn-create-ok" onclick="createNewProject()">OK</button>
            </div>
        </div>
    </div>

    <div id="publish-modal" class="modal-overlay">
        <div class="modal">
            <h3>Choose Domain Name</h3>
            <div class="input-group">
                <label>Domain Name (without spaces)</label>
                <input type="text" id="domain-input" placeholder="e.g. mygame">
                <div class="status-container">
                    <div class="spinner" id="domain-spinner"></div>
                    <span class="status-msg" id="domain-status"></span>
                </div>
            </div>
            <div class="modal-actions">
                <button class="modal-btn cancel" onclick="closeModal('publish-modal')">CANCEL</button>
                <button class="modal-btn" id="btn-publish-ok" disabled onclick="startPublish()">PUBLISH</button>
            </div>
        </div>
    </div>

    <div id="update-loader" class="modal-overlay" style="z-index: 300;">
        <div style="background: white; padding: 20px 40px; border-radius: 30px; font-weight: bold; color: #ff9800; display: flex; align-items: center; gap: 10px; box-shadow: 0 10px 30px rgba(0,0,0,0.2);">
            <div class="spinner" style="display: block; border-top-color: #ff9800;"></div> Updating Website...
        </div>
    </div>

    <div id="success-popup" class="success-popup">
        <div class="popup-box">
            <div class="house-icon">🏠</div>
            <h3 id="success-title">Website Live!</h3>
            <p style="font-size: 13px; color: #666; margin-top:5px; word-break: break-all;" id="live-url-text">yourwebsite.com</p>
            <div class="success-btns">
                <button class="s-btn btn-copy" onclick="copyLink()">Copy</button>
                <button class="s-btn btn-open" onclick="openLiveSite()">Open</button>
            </div>
            <button class="modal-btn cancel" style="margin-top: 15px; width: 100%;" onclick="closeModal('success-popup')">Close</button>
        </div>
    </div>

    <div id="project-view" class="view">
        <div class="app-bar">
            <h2 id="project-title"><button class="icon-btn" onclick="goHome()">←</button> <span id="p-name" style="white-space:nowrap; overflow:hidden; text-overflow:ellipsis; max-width: 150px;">Website</span></h2>
            
            <div class="action-group">
                <button class="icon-btn" onclick="triggerFileUpload()" style="color: var(--primary); font-size: 22px;">⬆️</button>
                <button class="icon-btn" onclick="createNewFile()" style="font-size: 28px; font-weight: 300;">+</button>
            </div>
        </div>
        
        <div class="yellow-banner" onclick="handleBannerClick()">
            <span style="font-size: 20px;">↑</span> <span id="banner-text">Convert Website</span>
        </div>

        <div class="file-list" id="file-list"></div>
    </div>

    <div id="editor-view" class="view" style="padding: 0;">
        <div class="app-bar" style="border-bottom: 1px solid #ffe082;">
            <h2><button class="icon-btn" onclick="backToProject()">←</button> <span id="file-title">index.html</span></h2>
        </div>
        <div id="editor-container">
            <textarea id="code-editor" spellcheck="false"></textarea>
            
            <div class="editor-toolbar">
                <div class="keys">
                    <span>&lt;</span> <span>&gt;</span> <span>{</span> <span>}</span> <span>[</span> <span>]</span> <span>(</span> <span>)</span> <span>;</span>
                </div>
                <button class="play-btn" onclick="runCode()">▶</button>
            </div>
        </div>
    </div>

    <div id="output-view" class="view" style="padding:0;">
        <div class="app-bar" style="border-bottom: 1px solid #ddd; background: #fff8e1;">
            <h2><button class="icon-btn" onclick="backToEditor()">←</button> Result</h2>
        </div>
        <iframe id="output-frame"></iframe>
    </div>

<script>
    // Data structure: { "Project 1": { date: "...", files: {"index.html": "..."}, domain: "mygame" } }
    let appData = JSON.parse(localStorage.getItem('codeweb_data')) || {};
    let currentProj = null;
    let currentFile = null;
    let finalLiveUrl = "";

    function showView(id) {
        document.querySelectorAll('.view').forEach(v => v.classList.remove('active-view'));
        document.getElementById(id).classList.add('active-view');
    }

    function goHome() { showView('home-view'); loadProjects(); }
    function backToProject() { saveCode(); showView('project-view'); loadFiles(); setupBanner(); }
    function backToEditor() { showView('editor-view'); }

    function openModal(id) {
        document.getElementById(id).style.display = 'flex';
        if(id === 'publish-modal') {
            document.getElementById('domain-input').value = currentProj.toLowerCase().replace(/[^a-z0-9_-]/g, '');
            checkDomain(); // Auto check
        }
        if(id === 'create-modal') {
            document.getElementById('new-project-name').value = "My Website";
            checkProjectName(); // Check default name
        }
    }
    
    function closeModal(id) { 
        document.getElementById(id).style.display = 'none'; 
    }

    // --- REAL-TIME PROJECT NAME CHECKING LOGIC ---
    const projectInput = document.getElementById('new-project-name');
    const projectStatus = document.getElementById('project-status');
    const btnCreateOk = document.getElementById('btn-create-ok');

    function checkProjectName() {
        let val = projectInput.value.trim();
        if(val === '') {
            projectStatus.innerText = "Name cannot be empty!";
            projectStatus.className = "status-error";
            btnCreateOk.disabled = true;
            return;
        }
        
        // Agar isi naam ka project pehle se hai
        if(appData[val]) {
            projectStatus.innerText = "Project already exists! ❌";
            projectStatus.className = "status-error";
            btnCreateOk.disabled = true;
        } else {
            projectStatus.innerText = "Perfect! Available ✅";
            projectStatus.className = "status-success";
            btnCreateOk.disabled = false;
        }
    }

    // Har key press par check karega
    projectInput.addEventListener('input', checkProjectName);


    // --- UPLOAD FILES FROM FILE MANAGER LOGIC ---
    function triggerFileUpload() {
        document.getElementById('local-file-upload').click();
    }

    document.getElementById('local-file-upload').addEventListener('change', function(e) {
        let files = e.target.files;
        if(files.length === 0) return;

        for(let i = 0; i < files.length; i++) {
            let file = files[i];
            let reader = new FileReader();
            
            reader.onload = function(evt) {
                appData[currentProj].files[file.name] = evt.target.result;
                saveData();
                loadFiles();
            };
            
            if(file.type.match('image.*')) {
                reader.readAsDataURL(file);
            } else {
                reader.readAsText(file);
            }
        }
        this.value = '';
    });

    // --- DOMAIN CHECKING & LOCKING LOGIC ---
    function setupBanner() {
        let bannerText = document.getElementById('banner-text');
        if(appData[currentProj] && appData[currentProj].domain) {
            bannerText.innerHTML = `Update Website <span style="font-size:12px; font-weight:normal; margin-left:5px;">(${appData[currentProj].domain})</span>`;
        } else {
            bannerText.innerHTML = "Convert Website";
        }
    }

    function handleBannerClick() {
        if(appData[currentProj] && appData[currentProj].domain) {
            pushFilesToServer(appData[currentProj].domain, true);
        } else {
            openModal('publish-modal');
        }
    }

    let typingTimer;
    const domainInput = document.getElementById('domain-input');
    
    domainInput.addEventListener('input', () => {
        clearTimeout(typingTimer);
        document.getElementById('domain-spinner').style.display = 'block';
        document.getElementById('domain-status').innerText = 'Checking...';
        document.getElementById('domain-status').className = 'status-msg';
        document.getElementById('btn-publish-ok').disabled = true;
        typingTimer = setTimeout(checkDomain, 400); // Thoda aur fast kiya
    });

    async function checkDomain() {
        let val = domainInput.value.trim().toLowerCase();
        let spinner = document.getElementById('domain-spinner');
        let status = document.getElementById('domain-status');
        let btn = document.getElementById('btn-publish-ok');

        if(val.length < 3) {
            spinner.style.display = 'none';
            status.innerText = "Too short!";
            status.className = "status-error";
            return;
        }

        let fd = new FormData();
        fd.append('action', 'check_domain');
        fd.append('domain', val);

        try {
            let res = await fetch(window.location.href, { method: 'POST', body: fd });
            let data = await res.json();
            
            spinner.style.display = 'none';
            if(data.status === 'taken') {
                status.innerText = "Taken! Try a new one.";
                status.className = "status-error";
                btn.disabled = true;
            } else if(data.status === 'available') {
                status.innerText = "Available! You can take this";
                status.className = "status-success";
                btn.disabled = false;
            }
        } catch(e) {
            spinner.style.display = 'none';
            status.innerText = "Error checking domain. (Run as .php)";
            status.className = "status-error";
        }
    }

    function startPublish() {
        let domain = document.getElementById('domain-input').value.trim().toLowerCase();
        let publishBtn = document.getElementById('btn-publish-ok');
        publishBtn.innerText = "UPLOADING...";
        publishBtn.disabled = true;
        
        pushFilesToServer(domain, false, publishBtn);
    }

    async function pushFilesToServer(domain, isUpdate, publishBtnElement = null) {
        if (isUpdate) {
            document.getElementById('update-loader').style.display = 'flex';
        }

        let files = appData[currentProj].files;
        let fd = new FormData();
        fd.append('action', 'upload');
        fd.append('domain', domain);
        fd.append('is_update', isUpdate ? 'true' : 'false'); 
        
        for (let fileName in files) {
            let blob = new Blob([files[fileName]], { type: 'text/html' });
            fd.append('files[]', blob, fileName);
        }

        try {
            let res = await fetch(window.location.href, { method: 'POST', body: fd });
            let data = await res.json();
            
            if (isUpdate) document.getElementById('update-loader').style.display = 'none';

            if(data.status === 'success') {
                if(!isUpdate) {
                    appData[currentProj].domain = domain;
                    saveData();
                    setupBanner(); 
                }

                finalLiveUrl = data.link;
                if(!isUpdate) closeModal('publish-modal');
                
                document.getElementById('success-title').innerText = data.msg;
                document.getElementById('live-url-text').innerText = data.link;
                document.getElementById('success-popup').style.display = 'flex';
            } else {
                alert("Error: " + data.msg);
            }
        } catch(e) {
            if (isUpdate) document.getElementById('update-loader').style.display = 'none';
            alert("Upload failed! Ensure this file is saved as .php on a server.");
        }
        
        if(publishBtnElement) {
            publishBtnElement.innerText = "PUBLISH";
            publishBtnElement.disabled = false;
        }
    }

    function copyLink() {
        navigator.clipboard.writeText(finalLiveUrl);
        alert("Link Copied!");
    }

    function openLiveSite() {
        window.open(finalLiveUrl, '_blank');
    }

    // --- STANDARD APP LOGIC ---
    function getFormattedDate() {
        let d = new Date();
        return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')} ${String(d.getHours()).padStart(2,'0')}:${String(d.getMinutes()).padStart(2,'0')}`;
    }

    function createNewProject() {
        let name = document.getElementById('new-project-name').value.trim();
        // Validation dobara yahan bhi kardi taaki double safety rahe
        if (name && !appData[name]) {
            appData[name] = {
                date: getFormattedDate(),
                domain: null, 
                files: { "index.html": "<!DOCTYPE html>\n<html>\n<head><title>My App</title></head>\n<body>\n  <h1>Welcome to B2K</h1>\n</body>\n</html>" }
            };
            saveData(); 
            closeModal('create-modal'); 
            loadProjects();
        }
    }

    function loadProjects() {
        let grid = document.getElementById('projects-grid');
        grid.innerHTML = '';
        for (let proj in appData) {
            let card = document.createElement('div'); card.className = 'project-card'; card.onclick = () => openProject(proj);
            card.innerHTML = `<div class="card-icon"></div><div><div class="card-title">${proj}</div><div class="card-date">${appData[proj].date}</div></div>`;
            grid.appendChild(card);
        }
    }

    function openProject(name) { 
        currentProj = name; 
        document.getElementById('p-name').innerText = name; 
        showView('project-view'); 
        loadFiles(); 
        setupBanner(); 
    }

    function loadFiles() {
        let list = document.getElementById('file-list'); list.innerHTML = ''; let files = appData[currentProj].files;
        for (let file in files) {
            let item = document.createElement('div'); item.className = 'file-item'; item.onclick = () => openEditor(file);
            item.innerHTML = `<div class="file-icon">📄</div><div class="file-info"><div class="file-name">${file}</div></div>`;
            list.appendChild(item);
        }
    }

    function createNewFile() {
        let name = prompt("Enter file name (e.g. style.css):");
        if (name && !appData[currentProj].files[name]) { appData[currentProj].files[name] = ""; saveData(); loadFiles(); }
    }

    function openEditor(file) { currentFile = file; document.getElementById('file-title').innerText = file; document.getElementById('code-editor').value = appData[currentProj].files[file]; showView('editor-view'); }
    function saveCode() { if (currentProj && currentFile) { appData[currentProj].files[currentFile] = document.getElementById('code-editor').value; saveData(); } }
    
    function runCode() {
        saveCode(); 
        let codeToRun = appData[currentProj].files['index.html'] || document.getElementById('code-editor').value;
        showView('output-view');
        let doc = document.getElementById('output-frame').contentWindow.document;
        doc.open(); doc.write(codeToRun); doc.close();
    }

    function saveData() { localStorage.setItem('codeweb_data', JSON.stringify(appData)); }
    loadProjects();
</script>
</body>
</html>
