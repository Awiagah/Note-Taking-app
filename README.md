
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Awiagah Note Book 📙</title>
    
    <!-- PWA Meta Tags -->
    <meta name="description" content="A professional note-taking application that works offline">
    <meta name="theme-color" content="#4f46e5">
    <link rel="manifest" href="manifest.json">
    
    <!-- Favicon -->
    <link rel="icon" type="image/png" href="assets/icons/icon-72x72.png">
    
    <!-- CDN Libraries -->
    <!-- Quill.js Rich Text Editor -->
    <link href="https://cdn.quilljs.com/1.3.7/quill.snow.css" rel="stylesheet">
    <script src="https://cdn.quilljs.com/1.3.7/quill.js"></script>
    
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Cropper.js for image editing -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.13/cropper.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.13/cropper.min.js"></script>
    
    <!-- QR Code Generator -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    
    <!-- Local CSS -->
    <link rel="stylesheet" href="css/main.css">
    <link rel="stylesheet" href="css/editor.css">
    <link rel="stylesheet" href="css/responsive.css">
    <style>
      /* Reset and Base Styles */
      css/main.css
      /*main body css*/
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

:root {
    /* Light Theme Variables */
    --primary-color: #4f46e5;
    --primary-hover: #4338ca;
    --secondary-color: #6b7280;
    --background-color: #f9fafb;
    --sidebar-bg: #ffffff;
    --card-bg: #ffffff;
    --text-color: #111827;
    --text-secondary: #6b7280;
    --border-color: #e5e7eb;
    --hover-bg: #f3f4f6;
    --shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1);
    --shadow-lg: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
}

[data-theme="dark"] {
    /* Dark Theme Variables */
    --primary-color: #6366f1;
    --primary-hover: #818cf8;
    --secondary-color: #9ca3af;
    --background-color: #111827;
    --sidebar-bg: #1f2937;
    --card-bg: #1f2937;
    --text-color: #f9fafb;
    --text-secondary: #d1d5db;
    --border-color: #374151;
    --hover-bg: #374151;
    --shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.3);
    --shadow-lg: 0 10px 25px -5px rgba(0, 0, 0, 0.3);
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
    background-color: var(--background-color);
    color: var(--text-color);
    line-height: 1.6;
    transition: background-color 0.3s, color 0.3s;
}

/* App Layout */
.app-container {
    display: flex;
    height: 100vh;
    overflow: hidden;
}

/* Sidebar Styles */
.sidebar {
    width: 280px;
    background-color: var(--sidebar-bg);
    border-right: 1px solid var(--border-color);
    display: flex;
    flex-direction: column;
    transition: transform 0.3s ease;
    z-index: 100;
}

.sidebar-header {
    padding: 1.5rem;
    border-bottom: 1px solid var(--border-color);
}

.logo {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    margin-bottom: 1.5rem;
}

.logo i {
    font-size: 1.75rem;
    color: var(--primary-color);
}

.logo h1 {
    font-size: 1.5rem;
    font-weight: 700;
}

.btn-new-note {
    width: 100%;
    padding: 0.75rem 1rem;
    background-color: var(--primary-color);
    color: white;
    border: none;
    border-radius: 0.5rem;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    transition: background-color 0.2s;
}

.btn-new-note:hover {
    background-color: var(--primary-hover);
}

/* Search */
.search-container {
    position: relative;
    padding: 1rem 1.5rem;
    border-bottom: 1px solid var(--border-color);
}

.search-container i {
    position: absolute;
    left: 2rem;
    top: 50%;
    transform: translateY(-50%);
    color: var(--text-secondary);
}

.search-container input {
    width: 100%;
    padding: 0.75rem 1rem 0.75rem 2.5rem;
    background-color: var(--hover-bg);
    border: 1px solid var(--border-color);
    border-radius: 0.5rem;
    font-size: 0.875rem;
    color: var(--text-color);
}

.search-container input:focus {
    outline: none;
    border-color: var(--primary-color);
}

/* Navigation */
.nav-menu {
    padding: 1rem 0;
    border-bottom: 1px solid var(--border-color);
}

.nav-menu ul {
    list-style: none;
}

.nav-menu li {
    padding: 0.75rem 1.5rem;
    display: flex;
    align-items: center;
    gap: 0.75rem;
    cursor: pointer;
    transition: background-color 0.2s;
}

.nav-menu li:hover {
    background-color: var(--hover-bg);
}

.nav-menu li.active {
    background-color: var(--hover-bg);
    border-left: 3px solid var(--primary-color);
}

.nav-menu i {
    width: 1.25rem;
    color: var(--text-secondary);
}

.nav-menu .badge {
    margin-left: auto;
    background-color: var(--primary-color);
    color: white;
    padding: 0.25rem 0.5rem;
    border-radius: 1rem;
    font-size: 0.75rem;
}

/* Notebooks and Tags Sections */
.notebooks-section,
.tags-section {
    padding: 1rem 1.5rem;
    border-bottom: 1px solid var(--border-color);
}

.section-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 0.75rem;
}

.section-header h3 {
    font-size: 0.875rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--text-secondary);
}

.btn-icon {
    width: 2rem;
    height: 2rem;
    background: none;
    border: none;
    border-radius: 0.375rem;
    color: var(--text-secondary);
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s;
}

.btn-icon:hover {
    background-color: var(--hover-bg);
    color: var(--text-color);
}

.notebooks-list {
    list-style: none;
    max-height: 200px;
    overflow-y: auto;
}

.notebooks-list li {
    padding: 0.5rem 0.75rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
    border-radius: 0.375rem;
    transition: background-color 0.2s;
}

.notebooks-list li:hover {
    background-color: var(--hover-bg);
}

.notebooks-list i {
    color: var(--text-secondary);
    font-size: 0.875rem;
}

.tags-container {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
}

.tag {
    display: flex;
    align-items: center;
    gap: 0.25rem;
    padding: 0.25rem 0.5rem;
    background-color: var(--hover-bg);
    border-radius: 1rem;
    font-size: 0.75rem;
    cursor: pointer;
    transition: opacity 0.2s;
}

.tag:hover {
    opacity: 0.8;
}

.tag-color {
    width: 0.75rem;
    height: 0.75rem;
    border-radius: 50%;
}

/* App Info */
.app-info {
    margin-top: auto;
    padding: 1rem 1.5rem;
    display: flex;
    gap: 0.5rem;
    border-top: 1px solid var(--border-color);
}

/* Main Content */
.main-content {
    flex: 1;
    display: flex;
    flex-direction: column;
    overflow: hidden;
}

.notes-header {
    padding: 1rem 1.5rem;
    border-bottom: 1px solid var(--border-color);
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.header-left {
    display: flex;
    align-items: center;
    gap: 1rem;
}

.header-left h2 {
    font-size: 1.25rem;
    font-weight: 600;
}

.sort-container select {
    padding: 0.5rem;
    background-color: var(--card-bg);
    border: 1px solid var(--border-color);
    border-radius: 0.375rem;
    color: var(--text-color);
    font-size: 0.875rem;
}

/* Notes List */
.notes-list {
    flex: 1;
    padding: 1.5rem;
    overflow-y: auto;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1rem;
}

.note-card {
    background-color: var(--card-bg);
    border: 1px solid var(--border-color);
    border-radius: 0.75rem;
    padding: 1.25rem;
    cursor: pointer;
    transition: all 0.2s;
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
}

.note-card:hover {
    transform: translateY(-2px);
    box-shadow: var(--shadow-lg);
}

.note-card.selected {
    border-color: var(--primary-color);
    box-shadow: 0 0 0 2px rgba(79, 70, 229, 0.1);
}

.note-card-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
}

.note-title {
    font-weight: 600;
    font-size: 1rem;
    margin-bottom: 0.5rem;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
}

.note-content {
    color: var(--text-secondary);
    font-size: 0.875rem;
    line-height: 1.5;
    flex: 1;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
}

.note-footer {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 0.75rem;
    color: var(--text-secondary);
}

.note-tags {
    display: flex;
    gap: 0.25rem;
    flex-wrap: wrap;
}

.tag-small {
    padding: 0.125rem 0.375rem;
    border-radius: 0.75rem;
    font-size: 0.625rem;
}

.favorite-btn {
    background: none;
    border: none;
    color: var(--text-secondary);
    cursor: pointer;
    padding: 0.25rem;
}

.favorite-btn.active {
    color: #fbbf24;
}

.empty-state {
    grid-column: 1 / -1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 4rem 2rem;
    text-align: center;
}

.empty-state i {
    font-size: 4rem;
    color: var(--text-secondary);
    margin-bottom: 1.5rem;
}

.empty-state h3 {
    font-size: 1.5rem;
    margin-bottom: 0.5rem;
}

.empty-state p {
    color: var(--text-secondary);
    margin-bottom: 1.5rem;
}

/* Editor Panel */
.editor-panel {
    position: fixed;
    top: 0;
    right: 0;
    width: 70%;
    height: 100vh;
    background-color: var(--card-bg);
    box-shadow: var(--shadow-lg);
    transform: translateX(100%);
    transition: transform 0.3s ease;
    z-index: 1000;
    display: flex;
    flex-direction: column;
}

.editor-panel.active {
    transform: translateX(0);
}

.editor-header {
    padding: 1rem 1.5rem;
    border-bottom: 1px solid var(--border-color);
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.editor-title {
    flex: 1;
}

#noteTitle {
    width: 100%;
    font-size: 1.5rem;
    font-weight: 600;
    background: none;
    border: none;
    color: var(--text-color);
    margin-bottom: 0.5rem;
}

#noteTitle:focus {
    outline: none;
}

.note-meta {
    display: flex;
    gap: 1rem;
    font-size: 0.875rem;
    color: var(--text-secondary);
}

.editor-actions {
    display: flex;
    gap: 0.5rem;
}

/* Toolbar */
.toolbar {
    padding: 0.75rem 1.5rem;
    border-bottom: 1px solid var(--border-color);
    display: flex;
    flex-wrap: wrap;
    gap: 0.25rem;
    background-color: var(--sidebar-bg);
}

.toolbar-group {
    display: flex;
    align-items: center;
    border-right: 1px solid var(--border-color);
    padding-right: 0.5rem;
    margin-right: 0.5rem;
}

.toolbar-group:last-child {
    border-right: none;
    margin-right: 0;
}

.toolbar-btn {
    width: 2rem;
    height: 2rem;
    background: none;
    border: none;
    border-radius: 0.375rem;
    color: var(--text-color);
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
}

.toolbar-btn:hover {
    background-color: var(--hover-bg);
}

.toolbar-btn.active {
    background-color: var(--primary-color);
    color: white;
}

.toolbar-select {
    padding: 0.25rem;
    background-color: var(--card-bg);
    border: 1px solid var(--border-color);
    border-radius: 0.375rem;
    color: var(--text-color);
    font-size: 0.875rem;
}

/* Editor Container */
.editor-container {
    flex: 1;
    overflow: hidden;
    padding: 1.5rem;
}

#editor {
    height: 100%;
}

/* Editor Footer */
.editor-footer {
    padding: 1rem 1.5rem;
    border-top: 1px solid var(--border-color);
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 0.875rem;
    color: var(--text-secondary);
}

.editor-tags {
    display: flex;
    gap: 0.5rem;
    flex-wrap: wrap;
}

.editor-notebook select {
    padding: 0.25rem 0.5rem;
    background-color: var(--card-bg);
    border: 1px solid var(--border-color);
    border-radius: 0.375rem;
    color: var(--text-color);
    font-size: 0.875rem;
}

/* Modal Styles */
.modal {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 2000;
    align-items: center;
    justify-content: center;
}

.modal.active {
    display: flex;
}

.modal-content {
    background-color: var(--card-bg);
    border-radius: 0.75rem;
    width: 90%;
    max-width: 500px;
    max-height: 90vh;
    overflow-y: auto;
    box-shadow: var(--shadow-lg);
}

.modal-header {
    padding: 1.25rem 1.5rem;
    border-bottom: 1px solid var(--border-color);
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.modal-header h3 {
    font-size: 1.25rem;
    font-weight: 600;
}

.modal-body {
    padding: 1.5rem;
}

.input-full {
    width: 100%;
    padding: 0.75rem;
    margin-bottom: 1rem;
    background-color: var(--card-bg);
    border: 1px solid var(--border-color);
    border-radius: 0.5rem;
    color: var(--text-color);
    font-size: 1rem;
}

.input-full:focus {
    outline: none;
    border-color: var(--primary-color);
}

.color-picker {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1rem;
}

.color-option {
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    cursor: pointer;
    border: 2px solid transparent;
    transition: transform 0.2s;
}

.color-option:hover {
    transform: scale(1.1);
}

.color-option.selected {
    border-color: var(--text-color);
}

.image-editor {
    width: 100%;
    height: 300px;
    margin-bottom: 1rem;
    background-color: var(--hover-bg);
    border-radius: 0.5rem;
    overflow: hidden;
}

.image-editor img {
    width: 100%;
    height: 100%;
    object-fit: contain;
}

.image-controls {
    display: flex;
    gap: 0.5rem;
    flex-wrap: wrap;
}

.export-options {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
    gap: 1rem;
}

.export-option {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    padding: 1.5rem 1rem;
    background-color: var(--hover-bg);
    border: 1px solid var(--border-color);
    border-radius: 0.5rem;
    color: var(--text-color);
    cursor: pointer;
    transition: all 0.2s;
}

.export-option:hover {
    transform: translateY(-2px);
    border-color: var(--primary-color);
}

.export-option i {
    font-size: 2rem;
}

.setting-item {
    margin-bottom: 1.5rem;
}

.setting-item label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: 500;
}

/* Button Styles */
.btn-primary {
    padding: 0.75rem 1.5rem;
    background-color: var(--primary-color);
    color: white;
    border: none;
    border-radius: 0.5rem;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: background-color 0.2s;
}

.btn-primary:hover {
    background-color: var(--primary-hover);
}

.btn-secondary {
    padding: 0.75rem 1.5rem;
    background-color: var(--hover-bg);
    color: var(--text-color);
    border: 1px solid var(--border-color);
    border-radius: 0.5rem;
    font-size: 1rem;
    cursor: pointer;
    transition: all 0.2s;
}

.btn-secondary:hover {
    background-color: var(--border-color);
}

.btn-danger {
    padding: 0.75rem 1.5rem;
    background-color: #dc2626;
    color: white;
    border: none;
    border-radius: 0.5rem;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.2s;
}

.btn-danger:hover {
    background-color: #b91c1c;
}

/* Toast Notifications */
.toast-container {
    position: fixed;
    bottom: 1rem;
    right: 1rem;
    z-index: 3000;
}

.toast {
    padding: 1rem 1.5rem;
    background-color: var(--card-bg);
    border: 1px solid var(--border-color);
    border-radius: 0.5rem;
    box-shadow: var(--shadow-lg);
    margin-top: 0.5rem;
    animation: slideIn 0.3s ease;
    display: flex;
    align-items: center;
    gap: 0.75rem;
}

.toast.success {
    border-left: 4px solid #10b981;
}

.toast.error {
    border-left: 4px solid #ef4444;
}

.toast.info {
    border-left: 4px solid #3b82f6;
}

@keyframes slideIn {
    from {
        transform: translateX(100%);
        opacity: 0;
    }
    to {
        transform: translateX(0);
        opacity: 1;
    }
}

/* Dropdown */
.dropdown {
    position: relative;
    display: inline-block;
}

.dropdown-content {
    display: none;
    position: absolute;
    right: 0;
    background-color: var(--card-bg);
    min-width: 180px;
    box-shadow: var(--shadow-lg);
    border-radius: 0.5rem;
    z-index: 1000;
    border: 1px solid var(--border-color);
}

.dropdown-content a {
    color: var(--text-color);
    padding: 0.75rem 1rem;
    text-decoration: none;
    display: flex;
    align-items: center;
    gap: 0.75rem;
    font-size: 0.875rem;
}

.dropdown-content a:hover {
    background-color: var(--hover-bg);
}

.dropdown:hover .dropdown-content {
    display: block;
}

/* Responsive Design */
@media (max-width: 768px) {
    .sidebar {
        position: fixed;
        transform: translateX(-100%);
    }
    
    .sidebar.active {
        transform: translateX(0);
    }
    
    .editor-panel {
        width: 100%;
    }
    
    .notes-list {
        grid-template-columns: 1fr;
    }
}

/* Dark Mode Toggle Animation */
#themeToggle i {
    transition: transform 0.3s ease;
}

[data-theme="dark"] #themeToggle i {
    transform: rotate(180deg);
}

/* Scrollbar Styling */
::-webkit-scrollbar {
    width: 8px;
    height: 8px;
}

::-webkit-scrollbar-track {
    background: var(--hover-bg);
    border-radius: 4px;
}

::-webkit-scrollbar-thumb {
    background: var(--secondary-color);
    border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
    background: var(--primary-color);
}

/*editor css*/
/* Quill Editor Custom Styles */
.ql-toolbar.ql-snow {
    border: none !important;
    border-bottom: 1px solid var(--border-color) !important;
    background-color: var(--sidebar-bg) !important;
}

.ql-container.ql-snow {
    border: none !important;
    font-size: 16px;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.ql-editor {
    min-height: 400px;
    padding: 1.5rem !important;
    color: var(--text-color) !important;
    line-height: 1.6;
}

.ql-editor.ql-blank::before {
    color: var(--text-secondary) !important;
    font-style: normal !important;
    font-size: 1rem;
}

.ql-snow .ql-stroke {
    stroke: var(--text-color) !important;
}

.ql-snow .ql-fill {
    fill: var(--text-color) !important;
}

.ql-snow .ql-picker {
    color: var(--text-color) !important;
}

.ql-snow .ql-picker-options {
    background-color: var(--card-bg) !important;
    border-color: var(--border-color) !important;
}

.ql-snow .ql-picker-label {
    border-color: var(--border-color) !important;
}

.ql-snow.ql-toolbar button:hover,
.ql-snow .ql-toolbar button:hover,
.ql-snow.ql-toolbar button:focus,
.ql-snow .ql-toolbar button:focus,
.ql-snow.ql-toolbar button.ql-active,
.ql-snow .ql-toolbar button.ql-active,
.ql-snow.ql-toolbar .ql-picker-label:hover,
.ql-snow .ql-toolbar .ql-picker-label:hover,
.ql-snow.ql-toolbar .ql-picker-label.ql-active,
.ql-snow .ql-toolbar .ql-picker-label.ql-active,
.ql-snow.ql-toolbar .ql-picker-item:hover,
.ql-snow .ql-toolbar .ql-picker-item:hover,
.ql-snow.ql-toolbar .ql-picker-item.ql-selected,
.ql-snow .ql-toolbar .ql-picker-item.ql-selected {
    color: var(--primary-color) !important;
}

.ql-snow.ql-toolbar button:hover .ql-stroke,
.ql-snow .ql-toolbar button:hover .ql-stroke,
.ql-snow.ql-toolbar button:focus .ql-stroke,
.ql-snow .ql-toolbar button:focus .ql-stroke,
.ql-snow.ql-toolbar button.ql-active .ql-stroke,
.ql-snow .ql-toolbar button.ql-active .ql-stroke,
.ql-snow.ql-toolbar .ql-picker-label:hover .ql-stroke,
.ql-snow .ql-toolbar .ql-picker-label:hover .ql-stroke,
.ql-snow.ql-toolbar .ql-picker-label.ql-active .ql-stroke,
.ql-snow .ql-toolbar .ql-picker-label.ql-active .ql-stroke,
.ql-snow.ql-toolbar .ql-picker-item:hover .ql-stroke,
.ql-snow .ql-toolbar .ql-picker-item:hover .ql-stroke,
.ql-snow.ql-toolbar .ql-picker-item.ql-selected .ql-stroke,
.ql-snow .ql-toolbar .ql-picker-item.ql-selected .ql-stroke,
.ql-snow.ql-toolbar button:hover .ql-fill,
.ql-snow .ql-toolbar button:hover .ql-fill,
.ql-snow.ql-toolbar button:focus .ql-fill,
.ql-snow .ql-toolbar button:focus .ql-fill,
.ql-snow.ql-toolbar button.ql-active .ql-fill,
.ql-snow .ql-toolbar button.ql-active .ql-fill,
.ql-snow.ql-toolbar .ql-picker-label:hover .ql-fill,
.ql-snow .ql-toolbar .ql-picker-label:hover .ql-fill,
.ql-snow.ql-toolbar .ql-picker-label.ql-active .ql-fill,
.ql-snow .ql-toolbar .ql-picker-label.ql-active .ql-fill,
.ql-snow.ql-toolbar .ql-picker-item:hover .ql-fill,
.ql-snow .ql-toolbar .ql-picker-item:hover .ql-fill,
.ql-snow.ql-toolbar .ql-picker-item.ql-selected .ql-fill,
.ql-snow .ql-toolbar .ql-picker-item.ql-selected .ql-fill {
    stroke: var(--primary-color) !important;
    fill: var(--primary-color) !important;
}

/* Code Block Styling */
.ql-snow .ql-editor pre.ql-syntax {
    background-color: var(--hover-bg) !important;
    color: var(--text-color) !important;
    border-radius: 0.5rem;
    padding: 1rem !important;
    border: 1px solid var(--border-color) !important;
    font-family: 'Courier New', monospace;
    font-size: 0.875rem;
}

/* Blockquote Styling */
.ql-snow .ql-editor blockquote {
    border-left: 4px solid var(--primary-color) !important;
    margin: 1rem 0;
    padding-left: 1rem;
    color: var(--text-secondary);
}

/* List Styling */
.ql-snow .ql-editor ul,
.ql-snow .ql-editor ol {
    padding-left: 1.5rem;
    margin: 0.5rem 0;
}

.ql-snow .ql-editor li {
    margin: 0.25rem 0;
}

/* Table Styling */
.ql-snow .ql-editor table {
    border-collapse: collapse;
    width: 100%;
    margin: 1rem 0;
}

.ql-snow .ql-editor table td,
.ql-snow .ql-editor table th {
    border: 1px solid var(--border-color);
    padding: 0.5rem;
}

.ql-snow .ql-editor table th {
    background-color: var(--hover-bg);
    font-weight: 600;
}

/* Image Styling */
.ql-snow .ql-editor img {
    max-width: 100%;
    height: auto;
    border-radius: 0.5rem;
    margin: 1rem 0;
}

/* Link Styling */
.ql-snow .ql-editor a {
    color: var(--primary-color);
    text-decoration: none;
    border-bottom: 1px dotted var(--primary-color);
}

.ql-snow .ql-editor a:hover {
    border-bottom: 1px solid var(--primary-color);
}

/* Custom Toolbar Buttons */
.custom-toolbar-btn {
    position: relative;
}

.custom-toolbar-btn input[type="color"] {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0;
    cursor: pointer;
}

/* Font Size Picker */
.ql-snow .ql-picker.ql-size .ql-picker-item[data-value="small"]::before {
    content: 'Small';
    font-size: 12px;
}

.ql-snow .ql-picker.ql-size .ql-picker-item[data-value="normal"]::before {
    content: 'Normal';
    font-size: 14px;
}

.ql-snow .ql-picker.ql-size .ql-picker-item[data-value="large"]::before {
    content: 'Large';
    font-size: 18px;
}

.ql-snow .ql-picker.ql-size .ql-picker-item[data-value="huge"]::before {
    content: 'Huge';
    font-size: 24px;
}

/* Font Family Picker */
.ql-snow .ql-picker.ql-font .ql-picker-item[data-value="arial"]::before {
    content: 'Arial';
    font-family: 'Arial';
}

.ql-snow .ql-picker.ql-font .ql-picker-item[data-value="times"]::before {
    content: 'Times New Roman';
    font-family: 'Times New Roman';
}

.ql-snow .ql-picker.ql-font .ql-picker-item[data-value="georgia"]::before {
    content: 'Georgia';
    font-family: 'Georgia';
}

.ql-snow .ql-picker.ql-font .ql-picker-item[data-value="monospace"]::before {
    content: 'Monospace';
    font-family: 'Monaco', 'Courier New', monospace;
}

/* Headers */
.ql-snow .ql-editor h1 {
    font-size: 2rem;
    font-weight: 700;
    margin: 1.5rem 0 1rem;
    color: var(--text-color);
}

.ql-snow .ql-editor h2 {
    font-size: 1.75rem;
    font-weight: 600;
    margin: 1.25rem 0 0.75rem;
    color: var(--text-color);
}

.ql-snow .ql-editor h3 {
    font-size: 1.5rem;
    font-weight: 600;
    margin: 1rem 0 0.5rem;
    color: var(--text-color);
}

/* Horizontal Rule */
.ql-snow .ql-editor hr {
    border: none;
    border-top: 2px solid var(--border-color);
    margin: 2rem 0;
}

/* Custom classes for our app */
.editor-content {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    line-height: 1.6;
}

.editor-content p {
    margin-bottom: 1rem;
}

.editor-content ul,
.editor-content ol {
    margin-bottom: 1rem;
}

/* Focus state for editor */
.ql-editor:focus {
    outline: none;
}

/* Placeholder animation */
@keyframes pulse {
    0% { opacity: 0.6; }
    50% { opacity: 0.8; }
    100% { opacity: 0.6; }
}

.ql-editor.ql-blank::before {
    animation: pulse 2s infinite;
}

/* Read-only mode styling */
.ql-editor.ql-disabled {
    background-color: var(--hover-bg);
    cursor: not-allowed;
}

/* Custom scrollbar for editor */
.ql-editor::-webkit-scrollbar {
    width: 6px;
}

.ql-editor::-webkit-scrollbar-track {
    background: transparent;
}

.ql-editor::-webkit-scrollbar-thumb {
    background: var(--secondary-color);
    border-radius: 3px;
}

.ql-editor::-webkit-scrollbar-thumb:hover {
    background: var(--primary-color);
}

/* Print styles for editor content */
@media print {
    .ql-editor {
        background: white !important;
        color: black !important;
        box-shadow: none !important;
    }
    
    .ql-toolbar {
        display: none !important;
    }
}

/* Mobile optimizations for editor */
@media (max-width: 768px) {
    .ql-toolbar.ql-snow {
        padding: 0.5rem !important;
        flex-wrap: wrap;
    }
    
    .ql-toolbar.ql-snow .ql-formats {
        margin-right: 0.25rem !important;
        margin-bottom: 0.25rem !important;
    }
    
    .ql-editor {
        padding: 1rem !important;
        font-size: 16px; /* Prevent zoom on mobile */
    }
    
    .ql-snow .ql-picker-label {
        padding: 0.25rem 0.5rem !important;
    }
}

/*dark mood css*/
/* Dark Mode Specific Overrides */
[data-theme="dark"] {
    /* Quill Editor Dark Mode */
    .ql-snow .ql-tooltip {
        background-color: #1f2937;
        border-color: #374151;
        color: #f9fafb;
        box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.3);
    }
    
    .ql-snow .ql-tooltip input[type="text"] {
        background-color: #374151;
        border-color: #4b5563;
        color: #f9fafb;
    }
    
    .ql-snow .ql-tooltip a.ql-action::before {
        color: #60a5fa;
    }
    
    .ql-snow .ql-tooltip a.ql-remove::before {
        color: #f87171;
    }
    
    /* Code syntax highlighting for dark mode */
    .ql-snow .ql-editor code {
        background-color: #374151;
        color: #e5e7eb;
        padding: 0.125rem 0.25rem;
        border-radius: 0.25rem;
        font-family: 'Courier New', monospace;
    }
    
    .ql-snow .ql-editor pre {
        background-color: #1f2937;
        color: #e5e7eb;
    }
    
    /* Table styling for dark mode */
    .ql-snow .ql-editor table {
        border-color: #374151;
    }
    
    .ql-snow .ql-editor table th {
        background-color: #374151;
        color: #f9fafb;
    }
    
    .ql-snow .ql-editor table td {
        color: #e5e7eb;
    }
    
    /* Blockquote dark mode */
    .ql-snow .ql-editor blockquote {
        border-left-color: #6366f1;
        color: #d1d5db;
    }
    
    /* Selection color */
    .ql-editor ::selection {
        background-color: rgba(99, 102, 241, 0.3);
        color: #f9fafb;
    }
    
    /* Placeholder text */
    .ql-editor.ql-blank::before {
        color: #9ca3af !important;
    }
    
    /* Custom scrollbar for dark mode */
    ::-webkit-scrollbar-track {
        background: #1f2937;
    }
    
    ::-webkit-scrollbar-thumb {
        background: #4b5563;
    }
    
    ::-webkit-scrollbar-thumb:hover {
        background: #6366f1;
    }
    
    /* Modal enhancements for dark mode */
    .modal-content {
        background-color: #1f2937;
        border: 1px solid #374151;
    }
    
    /* Button states in dark mode */
    .btn-secondary:hover {
        background-color: #374151;
        border-color: #4b5563;
    }
    
    /* Input focus states */
    input:focus,
    select:focus,
    textarea:focus {
        border-color: #6366f1;
        box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
    }
    
    /* Dropdown in dark mode */
    .dropdown-content {
        background-color: #1f2937;
        border-color: #374151;
    }
    
    /* Toast notifications */
    .toast {
        background-color: #1f2937;
        border-color: #374151;
    }
    
    /* Export options */
    .export-option {
        background-color: #374151;
        border-color: #4b5563;
    }
    
    .export-option:hover {
        border-color: #6366f1;
        background-color: #4b5563;
    }
    
    /* Image editor background */
    .image-editor {
        background-color: #374151;
    }
    
    /* Color options border */
    .color-option.selected {
        border-color: #f9fafb;
    }
    
    /* Settings inputs */
    .input-full {
        background-color: #374151;
        border-color: #4b5563;
        color: #f9fafb;
    }
    
    /* Sort select */
    .sort-container select {
        background-color: #374151;
        border-color: #4b5563;
        color: #f9fafb;
    }
    
    /* Notebook select in editor */
    .editor-notebook select {
        background-color: #374151;
        border-color: #4b5563;
        color: #f9fafb;
    }
    
    /* Search input */
    .search-container input {
        background-color: #374151;
        border-color: #4b5563;
        color: #f9fafb;
    }
    
    .search-container input:focus {
        border-color: #6366f1;
    }
    
    /* Note card hover in dark mode */
    .note-card:hover {
        background-color: #374151;
    }
    
    /* Active navigation item */
    .nav-menu li.active {
        background-color: #374151;
    }
    
    /* Toolbar button hover */
    .toolbar-btn:hover {
        background-color: #374151;
    }
    
    /* Icon button hover */
    .btn-icon:hover {
        background-color: #374151;
    }
}

/* System preference detection */
@media (prefers-color-scheme: dark) {
    :root:not([data-theme="light"]) {
        /* Apply dark theme if system prefers dark and user hasn't explicitly chosen light */
        --primary-color: #6366f1;
        --primary-hover: #818cf8;
        --secondary-color: #9ca3af;
        --background-color: #111827;
        --sidebar-bg: #1f2937;
        --card-bg: #1f2937;
        --text-color: #f9fafb;
        --text-secondary: #d1d5db;
        --border-color: #374151;
        --hover-bg: #374151;
        --shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.3);
        --shadow-lg: 0 10px 25px -5px rgba(0, 0, 0, 0.3);
    }
}

/* Smooth theme transition */
* {
    transition: background-color 0.3s ease, 
                border-color 0.3s ease, 
                color 0.3s ease,
                transform 0.2s ease;
}

/* Loading state for theme switch */
body.theme-switching {
    pointer-events: none;
}

body.theme-switching::before {
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    z-index: 9999;
    opacity: 0;
    animation: fadeIn 0.3s ease forwards;
}

@keyframes fadeIn {
    to {
        opacity: 1;
    }
}

/* Theme toggle button animation */
.theme-toggle {
    position: relative;
    overflow: hidden;
}

.theme-toggle::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 0;
    height: 0;
    background: rgba(99, 102, 241, 0.2);
    border-radius: 50%;
    transform: translate(-50%, -50%);
    transition: width 0.6s, height 0.6s;
}

.theme-toggle:active::after {
    width: 100px;
    height: 100px;
}

/*css responsive or mobile responsive*/
/* Responsive Design */
@media (max-width: 1200px) {
    .editor-panel {
        width: 80%;
    }
    
    .notes-list {
        grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    }
}

@media (max-width: 992px) {
    .app-container {
        flex-direction: column;
    }
    
    .sidebar {
        width: 100%;
        height: auto;
        position: static;
        transform: none;
        border-right: none;
        border-bottom: 1px solid var(--border-color);
    }
    
    .sidebar-header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 1rem;
    }
    
    .logo {
        margin-bottom: 0;
    }
    
    .logo h1 {
        font-size: 1.25rem;
    }
    
    .btn-new-note {
        width: auto;
        padding: 0.5rem 1rem;
    }
    
    .nav-menu,
    .notebooks-section,
    .tags-section {
        display: none;
    }
    
    .sidebar.active .nav-menu,
    .sidebar.active .notebooks-section,
    .sidebar.active .tags-section {
        display: block;
    }
    
    .app-info {
        display: none;
    }
    
    .main-content {
        height: calc(100vh - 140px);
    }
    
    .notes-header {
        padding: 0.75rem 1rem;
    }
    
    #menuToggle {
        display: block;
    }
    
    .editor-panel {
        width: 100%;
    }
}

@media (max-width: 768px) {
    .sidebar {
        position: fixed;
        top: 0;
        left: 0;
        height: 100vh;
        z-index: 1000;
        transform: translateX(-100%);
        transition: transform 0.3s ease;
    }
    
    .sidebar.active {
        transform: translateX(0);
    }
    
    .sidebar-header {
        padding: 1rem;
    }
    
    .search-container {
        padding: 0.75rem 1rem;
    }
    
    .nav-menu,
    .notebooks-section,
    .tags-section {
        display: block;
    }
    
    .app-info {
        display: flex;
    }
    
    .notes-list {
        grid-template-columns: 1fr;
        padding: 1rem;
        gap: 0.75rem;
    }
    
    .note-card {
        padding: 1rem;
    }
    
    .note-title {
        font-size: 0.875rem;
    }
    
    .note-content {
        font-size: 0.75rem;
    }
    
    .editor-panel {
        width: 100%;
    }
    
    .editor-header {
        padding: 0.75rem 1rem;
        flex-wrap: wrap;
    }
    
    .editor-title {
        width: 100%;
        margin-bottom: 0.5rem;
    }
    
    .editor-actions {
        width: 100%;
        justify-content: flex-end;
    }
    
    .toolbar {
        padding: 0.5rem;
        overflow-x: auto;
        flex-wrap: nowrap;
    }
    
    .toolbar-group {
        flex-shrink: 0;
    }
    
    .editor-container {
        padding: 1rem;
    }
    
    .editor-footer {
        padding: 0.75rem 1rem;
        flex-direction: column;
        gap: 0.75rem;
        align-items: flex-start;
    }
    
    .editor-tags {
        order: 1;
    }
    
    .editor-status {
        order: 2;
    }
    
    .editor-notebook {
        order: 3;
        width: 100%;
    }
    
    .modal-content {
        width: 95%;
        margin: 0.5rem;
    }
    
    .export-options {
        grid-template-columns: repeat(2, 1fr);
    }
    
    .toast-container {
        left: 1rem;
        right: 1rem;
        bottom: 1rem;
    }
    
    .toast {
        width: 100%;
    }
}

@media (max-width: 576px) {
    .header-right {
        display: flex;
        align-items: center;
        gap: 0.5rem;
    }
    
    .sort-container select {
        font-size: 0.75rem;
        padding: 0.25rem;
    }
    
    #viewToggle {
        display: none;
    }
    
    .empty-state {
        padding: 2rem 1rem;
    }
    
    .empty-state i {
        font-size: 3rem;
    }
    
    .empty-state h3 {
        font-size: 1.25rem;
    }
    
    .empty-state p {
        font-size: 0.875rem;
    }
    
    .modal-body {
        padding: 1rem;
    }
    
    .modal-header {
        padding: 1rem;
    }
    
    .image-controls {
        flex-direction: column;
    }
    
    .image-controls button {
        width: 100%;
    }
    
    .export-options {
        grid-template-columns: 1fr;
    }
    
    .setting-item {
        margin-bottom: 1rem;
    }
    
    .setting-item button {
        width: 100%;
        margin-bottom: 0.5rem;
    }
}

@media (max-width: 400px) {
    .sidebar {
        width: 100%;
    }
    
    .notes-header {
        flex-direction: column;
        gap: 0.5rem;
        align-items: flex-start;
    }
    
    .header-left,
    .header-right {
        width: 100%;
    }
    
    .header-right {
        justify-content: space-between;
    }
    
    .toolbar-btn {
        width: 1.75rem;
        height: 1.75rem;
        font-size: 0.75rem;
    }
    
    .toolbar-select {
        font-size: 0.75rem;
        padding: 0.125rem;
    }
    
    .ql-toolbar .ql-formats {
        margin-right: 0.125rem !important;
    }
    
    .ql-toolbar .ql-formats:last-child {
        margin-right: 0 !important;
    }
}

/* Touch Device Optimizations */
@media (hover: none) and (pointer: coarse) {
    .note-card {
        min-height: 120px;
    }
    
    .btn-icon,
    .toolbar-btn,
    .favorite-btn {
        min-width: 44px;
        min-height: 44px;
    }
    
    .nav-menu li {
        min-height: 44px;
    }
    
    .notebooks-list li {
        min-height: 44px;
    }
    
    .tag {
        padding: 0.5rem 0.75rem;
        min-height: 44px;
    }
    
    input,
    select,
    textarea {
        font-size: 16px; /* Prevents zoom on iOS */
    }
    
    .search-container input {
        padding: 1rem 1rem 1rem 3rem;
        height: 44px;
    }
    
    .btn-new-note {
        height: 44px;
    }
    
    .modal-content {
        max-height: 80vh;
    }
}

/* Landscape Mode Optimizations */
@media (max-height: 600px) and (orientation: landscape) {
    .sidebar {
        overflow-y: auto;
        height: 100vh;
    }
    
    .notebooks-list {
        max-height: 100px;
    }
    
    .notes-list {
        grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    }
    
    .editor-panel {
        height: 100vh;
    }
    
    .editor-container {
        height: calc(100vh - 200px);
    }
}

/* High DPI Screens */
@media (-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi) {
    .logo i,
    .nav-menu i,
    .btn-icon i,
    .toolbar-btn i {
        font-weight: 900;
    }
    
    .note-card {
        border-width: 0.5px;
    }
    
    .modal-content {
        border-width: 0.5px;
    }
}

/* Print Styles */
@media print {
    .sidebar,
    .notes-header,
    .notes-list,
    .editor-header,
    .toolbar,
    .editor-footer,
    .modal,
    .toast-container {
        display: none !important;
    }
    
    .editor-panel {
        position: static;
        width: 100%;
        height: auto;
        transform: none;
        box-shadow: none;
    }
    
    .editor-container {
        padding: 0;
    }
    
    .ql-editor {
        padding: 0 !important;
        border: none !important;
        min-height: auto;
    }
    
    body {
        background: white !important;
        color: black !important;
    }
}

/* Reduced Motion */
@media (prefers-reduced-motion: reduce) {
    *,
    *::before,
    *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
    }
    
    .note-card:hover {
        transform: none;
    }
    
    .export-option:hover {
        transform: none;
    }
    
    .color-option:hover {
        transform: none;
    }
}

/* Dark mode system preference with reduced motion */
@media (prefers-color-scheme: dark) and (prefers-reduced-motion: reduce) {
    body {
        transition: none;
    }
}

/* Very small screens (old phones) */
@media (max-width: 320px) {
    .notes-list {
        grid-template-columns: 1fr;
        padding: 0.5rem;
    }
    
    .note-card {
        padding: 0.75rem;
    }
    
    .modal-content {
        width: 100%;
        height: 100%;
        max-height: 100vh;
        border-radius: 0;
        margin: 0;
    }
    
    .modal-header {
        padding: 0.75rem;
    }
    
    .modal-body {
        padding: 0.75rem;
    }
}

/* Foldable devices */
@media (max-width: 280px) {
    :root {
        font-size: 14px;
    }
    
    .logo h1 {
        font-size: 1rem;
    }
    
    .btn-new-note span {
        display: none;
    }
    
    .btn-new-note i {
        margin-right: 0;
    }
}


    </style>
</head>
<body>
    <!-- App Container -->
    <div class="app-container">
        <!-- Sidebar -->
        <aside class="sidebar" id="sidebar">
            <div class="sidebar-header">
                <div class="logo">
                    <i class="fas fa-book"></i>
                    <h1>Notely</h1>
                </div>
                <button class="btn-new-note" id="newNoteBtn">
                    <i class="fas fa-plus"></i> New Note
                </button>
            </div>
            
            <!-- Search -->
            <div class="search-container">
                <i class="fas fa-search"></i>
                <input type="text" id="searchInput" placeholder="Search notes...">
            </div>
            
            <!-- Navigation -->
            <nav class="nav-menu">
                <ul>
                    <li class="active" data-filter="all">
                        <i class="fas fa-home"></i> All Notes
                        <span class="badge" id="allNotesCount">0</span>
                    </li>
                    <li data-filter="favorite">
                        <i class="fas fa-star"></i> Favorites
                        <span class="badge" id="favoritesCount">0</span>
                    </li>
                    <li data-filter="notebook">
                        <i class="fas fa-folder"></i> Notebooks
                    </li>
                    <li data-filter="tag">
                        <i class="fas fa-tag"></i> Tags
                    </li>
                    <li data-filter="trash">
                        <i class="fas fa-trash"></i> Trash
                        <span class="badge" id="trashCount">0</span>
                    </li>
                </ul>
            </nav>
            
            <!-- Notebooks List -->
            <div class="notebooks-section">
                <div class="section-header">
                    <h3>Notebooks</h3>
                    <button class="btn-icon" id="addNotebookBtn">
                        <i class="fas fa-plus"></i>
                    </button>
                </div>
                <ul class="notebooks-list" id="notebooksList">
                    <!-- Notebooks will be loaded here -->
                </ul>
            </div>
            
            <!-- Tags List -->
            <div class="tags-section">
                <div class="section-header">
                    <h3>Tags</h3>
                    <button class="btn-icon" id="addTagBtn">
                        <i class="fas fa-plus"></i>
                    </button>
                </div>
                <div class="tags-container" id="tagsContainer">
                    <!-- Tags will be loaded here -->
                </div>
            </div>
            
            <!-- App Info -->
            <div class="app-info">
                <button class="btn-icon" id="themeToggle">
                    <i class="fas fa-moon"></i>
                </button>
                <button class="btn-icon" id="exportAllBtn" title="Export All">
                    <i class="fas fa-download"></i>
                </button>
                <button class="btn-icon" id="importBtn" title="Import Notes">
                    <i class="fas fa-upload"></i>
                </button>
                <button class="btn-icon" id="settingsBtn">
                    <i class="fas fa-cog"></i>
                </button>
            </div>
        </aside>
        
        <!-- Main Content -->
        <main class="main-content">
            <!-- Notes List Header -->
            <header class="notes-header">
                <div class="header-left">
                    <button class="btn-icon" id="menuToggle">
                        <i class="fas fa-bars"></i>
                    </button>
                    <h2 id="currentView">All Notes</h2>
                </div>
                <div class="header-right">
                    <div class="sort-container">
                        <select id="sortSelect">
                            <option value="date-desc">Newest First</option>
                            <option value="date-asc">Oldest First</option>
                            <option value="title-asc">Title A-Z</option>
                            <option value="title-desc">Title Z-A</option>
                        </select>
                    </div>
                    <button class="btn-icon" id="viewToggle">
                        <i class="fas fa-th-large"></i>
                    </button>
                </div>
            </header>
            
            <!-- Notes List -->
            <div class="notes-list" id="notesList">
                <!-- Notes will be loaded here dynamically -->
                <div class="empty-state" id="emptyState">
                    <i class="fas fa-sticky-note"></i>
                    <h3>No notes yet</h3>
                    <p>Create your first note to get started!</p>
                    <button class="btn-primary" id="emptyNewNoteBtn">
                        <i class="fas fa-plus"></i> Create Note
                    </button>
                </div>
            </div>
            
            <!-- Editor Panel (initially hidden) -->
            <div class="editor-panel" id="editorPanel">
                <div class="editor-header">
                    <div class="editor-title">
                        <input type="text" id="noteTitle" placeholder="Untitled Note">
                        <div class="note-meta">
                            <span id="noteDate"></span>
                            <span id="wordCount">0 words</span>
                        </div>
                    </div>
                    <div class="editor-actions">
                        <button class="btn-icon" id="favoriteBtn" title="Favorite">
                            <i class="far fa-star"></i>
                        </button>
                        <button class="btn-icon" id="deleteBtn" title="Delete">
                            <i class="far fa-trash-alt"></i>
                        </button>
                        <div class="dropdown">
                            <button class="btn-icon" id="exportDropdownBtn">
                                <i class="fas fa-download"></i>
                            </button>
                            <div class="dropdown-content">
                                <a href="#" data-export="pdf"><i class="fas fa-file-pdf"></i> Export as PDF</a>
                                <a href="#" data-export="docx"><i class="fas fa-file-word"></i> Export as Word</a>
                                <a href="#" data-export="pptx"><i class="fas fa-file-powerpoint"></i> Export as PPT</a>
                                <a href="#" data-export="html"><i class="fas fa-code"></i> Export as HTML</a>
                                <a href="#" data-export="txt"><i class="fas fa-file-alt"></i> Export as Text</a>
                            </div>
                        </div>
                        <button class="btn-icon" id="closeEditorBtn">
                            <i class="fas fa-times"></i>
                        </button>
                    </div>
                </div>
                
                <!-- Toolbar -->
                <div class="toolbar" id="toolbar">
                    <!-- Toolbar will be populated by JavaScript -->
                </div>
                
                <!-- Editor Container -->
                <div class="editor-container">
                    <div id="editor"></div>
                </div>
                
                <!-- Editor Footer -->
                <div class="editor-footer">
                    <div class="editor-status">
                        <span>Auto-saved</span>
                        <span id="saveStatus"></span>
                    </div>
                    <div class="editor-tags" id="noteTags">
                        <!-- Tags will be added here -->
                    </div>
                    <div class="editor-notebook">
                        <select id="notebookSelect">
                            <option value="">No Notebook</option>
                        </select>
                    </div>
                </div>
            </div>
        </main>
    </div>
    
    <!-- Modals -->
    <div class="modal" id="imageModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Edit Image</h3>
                <button class="btn-icon close-modal">&times;</button>
            </div>
            <div class="modal-body">
                <div class="image-editor">
                    <img id="imageToEdit" src="" alt="Image to edit">
                </div>
                <div class="image-controls">
                    <button class="btn-secondary" id="cropBtn">Crop</button>
                    <button class="btn-secondary" id="rotateBtn">Rotate 90°</button>
                    <button class="btn-secondary" id="flipBtn">Flip Horizontal</button>
                    <button class="btn-primary" id="applyImageBtn">Apply Changes</button>
                </div>
            </div>
        </div>
    </div>
    
    <div class="modal" id="tagModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Add New Tag</h3>
                <button class="btn-icon close-modal">&times;</button>
            </div>
            <div class="modal-body">
                <input type="text" id="tagName" placeholder="Tag name" class="input-full">
                <div class="color-picker">
                    <div class="color-option" data-color="#ef4444"></div>
                    <div class="color-option" data-color="#f97316"></div>
                    <div class="color-option" data-color="#eab308"></div>
                    <div class="color-option" data-color="#22c55e"></div>
                    <div class="color-option" data-color="#3b82f6"></div>
                    <div class="color-option" data-color="#8b5cf6"></div>
                    <div class="color-option" data-color="#ec4899"></div>
                    <div class="color-option" data-color="#6b7280"></div>
                </div>
                <button class="btn-primary" id="saveTagBtn">Save Tag</button>
            </div>
        </div>
    </div>
    
    <div class="modal" id="notebookModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Create Notebook</h3>
                <button class="btn-icon close-modal">&times;</button>
            </div>
            <div class="modal-body">
                <input type="text" id="notebookName" placeholder="Notebook name" class="input-full">
                <button class="btn-primary" id="saveNotebookBtn">Create Notebook</button>
            </div>
        </div>
    </div>
    
    <div class="modal" id="exportModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Export Options</h3>
                <button class="btn-icon close-modal">&times;</button>
            </div>
            <div class="modal-body">
                <div class="export-options">
                    <button class="export-option" data-type="pdf">
                        <i class="fas fa-file-pdf"></i>
                        <span>PDF</span>
                    </button>
                    <button class="export-option" data-type="docx">
                        <i class="fas fa-file-word"></i>
                        <span>Word</span>
                    </button>
                    <button class="export-option" data-type="pptx">
                        <i class="fas fa-file-powerpoint"></i>
                        <span>PowerPoint</span>
                    </button>
                    <button class="export-option" data-type="html">
                        <i class="fas fa-code"></i>
                        <span>HTML</span>
                    </button>
                    <button class="export-option" data-type="json">
                        <i class="fas fa-database"></i>
                        <span>Backup (JSON)</span>
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <div class="modal" id="settingsModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Settings</h3>
                <button class="btn-icon close-modal">&times;</button>
            </div>
            <div class="modal-body">
                <div class="setting-item">
                    <label>Auto-save interval (seconds)</label>
                    <input type="number" id="autoSaveInterval" min="5" max="300" value="30" class="input-full">
                </div>
                <div class="setting-item">
                    <label>Editor Font Size</label>
                    <select id="editorFontSize" class="input-full">
                        <option value="14px">Small</option>
                        <option value="16px" selected>Medium</option>
                        <option value="18px">Large</option>
                        <option value="20px">Extra Large</option>
                    </select>
                </div>
                <div class="setting-item">
                    <label>Default Notebook</label>
                    <select id="defaultNotebook" class="input-full">
                        <option value="">None</option>
                    </select>
                </div>
                <div class="setting-item">
                    <button class="btn-secondary" id="exportDataBtn">Export All Data</button>
                    <button class="btn-secondary" id="importDataBtn">Import Data</button>
                    <button class="btn-danger" id="clearDataBtn">Clear All Data</button>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Toast Notifications -->
    <div class="toast-container" id="toastContainer"></div>
    
    <!-- Load local JavaScript files -->
    <script src="js/utils.js"></script>
    <script src="js/storage.js"></script>
    <script src="js/editor.js"></script>
    <script src="js/export.js"></script>
    <script src="js/import.js"></script>
    <script src="js/app.js"></script>
    
    <!-- Initialize app when DOM is loaded -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            app.init();
        });
    </script>
    <script>
      // Main Application Controller
const app = {
    // Application state
    state: {
        currentNote: null,
        currentFilter: 'all',
        notes: [],
        notebooks: [],
        tags: [],
        settings: {
            autoSaveInterval: 30,
            editorFontSize: '16px',
            defaultNotebook: '',
            theme: 'light'
        },
        editor: null,
        searchQuery: '',
        sortBy: 'date-desc',
        viewMode: 'grid'
    },

    // Initialize the application
    init: function() {
        this.loadData();
        this.initTheme();
        this.initEventListeners();
        this.initEditor();
        this.renderNotesList();
        this.renderNotebooks();
        this.renderTags();
        this.updateCounts();
        this.initServiceWorker();
        
        // Show welcome message
        if (this.state.notes.length === 0) {
            this.showToast('Welcome to Notely! Create your first note to get started.', 'info');
        }
    },

    // Load data from localStorage
    loadData: function() {
        // Load notes
        const savedNotes = localStorage.getItem('notely_notes');
        if (savedNotes) {
            this.state.notes = JSON.parse(savedNotes).map(note => ({
                ...note,
                createdAt: new Date(note.createdAt),
                updatedAt: new Date(note.updatedAt)
            }));
        }

        // Load notebooks
        const savedNotebooks = localStorage.getItem('notely_notebooks');
        if (savedNotebooks) {
            this.state.notebooks = JSON.parse(savedNotebooks);
        } else {
            // Create default notebooks
            this.state.notebooks = [
                { id: '1', name: 'Personal', color: '#3b82f6', noteCount: 0 },
                { id: '2', name: 'Work', color: '#10b981', noteCount: 0 },
                { id: '3', name: 'Ideas', color: '#8b5cf6', noteCount: 0 }
            ];
            this.saveNotebooks();
        }

        // Load tags
        const savedTags = localStorage.getItem('notely_tags');
        if (savedTags) {
            this.state.tags = JSON.parse(savedTags);
        } else {
            // Create default tags
            this.state.tags = [
                { id: '1', name: 'Important', color: '#ef4444' },
                { id: '2', name: 'Todo', color: '#f97316' },
                { id: '3', name: 'Reference', color: '#22c55e' }
            ];
            this.saveTags();
        }

        // Load settings
        const savedSettings = localStorage.getItem('notely_settings');
        if (savedSettings) {
            this.state.settings = { ...this.state.settings, ...JSON.parse(savedSettings) };
        }
    },

    // Initialize theme
    initTheme: function() {
        const savedTheme = localStorage.getItem('notely_theme');
        const systemPrefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
        
        if (savedTheme) {
            this.state.settings.theme = savedTheme;
        } else if (systemPrefersDark) {
            this.state.settings.theme = 'dark';
        }
        
        document.documentElement.setAttribute('data-theme', this.state.settings.theme);
        this.updateThemeIcon();
    },

    // Toggle theme
    toggleTheme: function() {
        this.state.settings.theme = this.state.settings.theme === 'light' ? 'dark' : 'light';
        document.documentElement.setAttribute('data-theme', this.state.settings.theme);
        localStorage.setItem('notely_theme', this.state.settings.theme);
        this.updateThemeIcon();
        this.showToast(`Switched to ${this.state.settings.theme} theme`, 'success');
    },

    // Update theme icon
    updateThemeIcon: function() {
        const icon = document.querySelector('#themeToggle i');
        if (this.state.settings.theme === 'dark') {
            icon.className = 'fas fa-sun';
        } else {
            icon.className = 'fas fa-moon';
        }
    },

    // Initialize event listeners
    initEventListeners: function() {
        // Sidebar toggle
        document.getElementById('menuToggle').addEventListener('click', () => {
            document.querySelector('.sidebar').classList.toggle('active');
        });

        // New note buttons
        document.getElementById('newNoteBtn').addEventListener('click', () => this.createNewNote());
        document.getElementById('emptyNewNoteBtn').addEventListener('click', () => this.createNewNote());

        // Theme toggle
        document.getElementById('themeToggle').addEventListener('click', () => this.toggleTheme());

        // Search
        document.getElementById('searchInput').addEventListener('input', (e) => {
            this.state.searchQuery = e.target.value.toLowerCase();
            this.renderNotesList();
        });

        // Sort
        document.getElementById('sortSelect').addEventListener('change', (e) => {
            this.state.sortBy = e.target.value;
            this.renderNotesList();
        });

        // Navigation
        document.querySelectorAll('.nav-menu li').forEach(item => {
            item.addEventListener('click', (e) => {
                document.querySelectorAll('.nav-menu li').forEach(i => i.classList.remove('active'));
                e.currentTarget.classList.add('active');
                this.state.currentFilter = e.currentTarget.dataset.filter;
                document.getElementById('currentView').textContent = e.currentTarget.textContent.trim();
                this.renderNotesList();
            });
        });

        // Close editor
        document.getElementById('closeEditorBtn').addEventListener('click', () => {
            this.closeEditor();
        });

        // Export all
        document.getElementById('exportAllBtn').addEventListener('click', () => {
            this.showExportModal();
        });

        // Import
        document.getElementById('importBtn').addEventListener('click', () => {
            document.getElementById('importDataBtn').click();
        });

        // Settings
        document.getElementById('settingsBtn').addEventListener('click', () => {
            this.showSettingsModal();
        });

        // Add notebook
        document.getElementById('addNotebookBtn').addEventListener('click', () => {
            this.showNotebookModal();
        });

        // Add tag
        document.getElementById('addTagBtn').addEventListener('click', () => {
            this.showTagModal();
        });

        // Modal close buttons
        document.querySelectorAll('.close-modal').forEach(btn => {
            btn.addEventListener('click', () => {
                btn.closest('.modal').classList.remove('active');
            });
        });

        // Click outside modal to close
        document.querySelectorAll('.modal').forEach(modal => {
            modal.addEventListener('click', (e) => {
                if (e.target === modal) {
                    modal.classList.remove('active');
                }
            });
        });

        // Keyboard shortcuts
        document.addEventListener('keydown', (e) => {
            if (e.ctrlKey || e.metaKey) {
                switch(e.key) {
                    case 'n':
                        e.preventDefault();
                        this.createNewNote();
                        break;
                    case 'f':
                        e.preventDefault();
                        document.getElementById('searchInput').focus();
                        break;
                    case 's':
                        e.preventDefault();
                        if (this.state.currentNote) {
                            this.saveCurrentNote();
                        }
                        break;
                    case 'e':
                        e.preventDefault();
                        if (this.state.currentNote) {
                            this.showExportModal();
                        }
                        break;
                }
            }
            
            // Escape key to close editor
            if (e.key === 'Escape' && this.state.currentNote) {
                this.closeEditor();
            }
        });

        // Auto-save interval
        setInterval(() => {
            if (this.state.currentNote && this.state.editor) {
                this.saveCurrentNote();
            }
        }, this.state.settings.autoSaveInterval * 1000);
    },

    // Initialize Quill editor
    initEditor: function() {
        this.state.editor = new Quill('#editor', {
            theme: 'snow',
            modules: {
                toolbar: {
                    container: [
                        [{ 'font': [] }, { 'size': ['small', false, 'large', 'huge'] }],
                        ['bold', 'italic', 'underline', 'strike'],
                        [{ 'color': [] }, { 'background': [] }],
                        [{ 'list': 'ordered' }, { 'list': 'bullet' }],
                        [{ 'align': [] }],
                        ['link', 'image', 'video'],
                        ['clean']
                    ]
                }
            },
            placeholder: 'Start writing your note here...'
        });

        // Add custom image handler
        this.state.editor.getModule('toolbar').addHandler('image', () => {
            this.handleImageUpload();
        });

        // Listen for editor changes
        this.state.editor.on('text-change', () => {
            if (this.state.currentNote) {
                this.updateSaveStatus('Unsaved changes...');
            }
        });

        // Initialize toolbar with custom buttons
        this.initToolbar();
    },

    // Initialize custom toolbar
    initToolbar: function() {
        const toolbar = document.getElementById('toolbar');
        
        // Font family
        const fontGroup = document.createElement('div');
        fontGroup.className = 'toolbar-group';
        fontGroup.innerHTML = `
            <select class="toolbar-select" id="fontFamily">
                <option value="">Font</option>
                <option value="arial">Arial</option>
                <option value="georgia">Georgia</option>
                <option value="times">Times New Roman</option>
                <option value="monospace">Monospace</option>
            </select>
        `;
        toolbar.appendChild(fontGroup);

        // Font size
        const sizeGroup = document.createElement('div');
        sizeGroup.className = 'toolbar-group';
        sizeGroup.innerHTML = `
            <select class="toolbar-select" id="fontSize">
                <option value="">Size</option>
                <option value="10px">10px</option>
                <option value="12px">12px</option>
                <option value="14px">14px</option>
                <option value="16px" selected>16px</option>
                <option value="18px">18px</option>
                <option value="24px">24px</option>
                <option value="32px">32px</option>
            </select>
        `;
        toolbar.appendChild(sizeGroup);

        // Text color
        const colorGroup = document.createElement('div');
        colorGroup.className = 'toolbar-group';
        colorGroup.innerHTML = `
            <button class="toolbar-btn custom-toolbar-btn" title="Text Color">
                <i class="fas fa-palette"></i>
                <input type="color" id="textColor" value="#000000">
            </button>
        `;
        toolbar.appendChild(colorGroup);

        // Add event listeners for custom toolbar
        document.getElementById('fontFamily').addEventListener('change', (e) => {
            const range = this.state.editor.getSelection();
            if (range) {
                this.state.editor.format('font', e.target.value);
            }
        });

        document.getElementById('fontSize').addEventListener('change', (e) => {
            const range = this.state.editor.getSelection();
            if (range) {
                this.state.editor.format('size', e.target.value);
            }
        });

        document.getElementById('textColor').addEventListener('change', (e) => {
            const range = this.state.editor.getSelection();
            if (range) {
                this.state.editor.format('color', e.target.value);
            }
        });
    },

    // Create a new note
    createNewNote: function() {
        const newNote = {
            id: Date.now().toString(),
            title: 'Untitled Note',
            content: '',
            tags: [],
            notebookId: this.state.settings.defaultNotebook || '',
            favorite: false,
            createdAt: new Date(),
            updatedAt: new Date(),
            wordCount: 0
        };

        this.state.notes.unshift(newNote);
        this.saveNotes();
        this.openNote(newNote);
        this.renderNotesList();
        this.updateCounts();
        
        // Focus on title input
        setTimeout(() => {
            document.getElementById('noteTitle').focus();
            document.getElementById('noteTitle').select();
        }, 100);
    },

    // Open a note in the editor
    openNote: function(note) {
        this.state.currentNote = note;
        
        // Update UI
        document.getElementById('noteTitle').value = note.title;
        document.getElementById('noteDate').textContent = this.formatDate(note.updatedAt);
        document.getElementById('wordCount').textContent = `${note.wordCount} words`;
        
        // Update favorite button
        const favoriteBtn = document.getElementById('favoriteBtn');
        favoriteBtn.querySelector('i').className = note.favorite ? 'fas fa-star' : 'far fa-star';
        
        // Set editor content
        this.state.editor.root.innerHTML = note.content;
        
        // Update tags
        this.renderNoteTags();
        
        // Update notebook select
        this.updateNotebookSelect();
        
        // Show editor
        document.getElementById('editorPanel').classList.add('active');
        document.querySelector('.sidebar').classList.remove('active');
        
        // Update save status
        this.updateSaveStatus('Saved');
        
        // Update word count
        this.updateWordCount();
    },

    // Close the editor
    closeEditor: function() {
        if (this.state.currentNote) {
            this.saveCurrentNote();
        }
        
        document.getElementById('editorPanel').classList.remove('active');
        this.state.currentNote = null;
        this.state.editor.setText('');
        
        // Clear selection
        document.querySelectorAll('.note-card.selected').forEach(card => {
            card.classList.remove('selected');
        });
    },

    // Save current note
    saveCurrentNote: function() {
        if (!this.state.currentNote) return;

        // Update note data
        this.state.currentNote.title = document.getElementById('noteTitle').value || 'Untitled Note';
        this.state.currentNote.content = this.state.editor.root.innerHTML;
        this.state.currentNote.updatedAt = new Date();
        this.state.currentNote.wordCount = this.countWords(this.state.editor.getText());
        
        // Update notebook
        const notebookSelect = document.getElementById('notebookSelect');
        this.state.currentNote.notebookId = notebookSelect.value;
        
        // Update in notes array
        const index = this.state.notes.findIndex(n => n.id === this.state.currentNote.id);
        if (index !== -1) {
            this.state.notes[index] = this.state.currentNote;
        }
        
        // Save to localStorage
        this.saveNotes();
        
        // Update UI
        this.updateSaveStatus('Saved just now');
        this.updateWordCount();
        this.renderNotesList(); // Update the note in the list
    },

    // Delete current note
    deleteCurrentNote: function() {
        if (!this.state.currentNote || !confirm('Are you sure you want to delete this note?')) return;

        const index = this.state.notes.findIndex(n => n.id === this.state.currentNote.id);
        if (index !== -1) {
            // Move to trash (or remove permanently if already in trash)
            if (this.state.currentFilter === 'trash') {
                this.state.notes.splice(index, 1);
            } else {
                this.state.notes[index].trashed = true;
                this.state.notes[index].trashedAt = new Date();
            }
            
            this.saveNotes();
            this.closeEditor();
            this.renderNotesList();
            this.updateCounts();
            this.showToast('Note deleted', 'success');
        }
    },

    // Toggle favorite status
    toggleFavorite: function() {
        if (!this.state.currentNote) return;

        this.state.currentNote.favorite = !this.state.currentNote.favorite;
        
        // Update UI
        const favoriteBtn = document.getElementById('favoriteBtn');
        favoriteBtn.querySelector('i').className = this.state.currentNote.favorite ? 'fas fa-star' : 'far fa-star';
        
        // Save changes
        this.saveCurrentNote();
        this.renderNotesList();
        this.updateCounts();
    },

    // Update save status
    updateSaveStatus: function(status) {
        document.getElementById('saveStatus').textContent = status;
    },

    // Update word count
    updateWordCount: function() {
        if (!this.state.currentNote) return;
        
        const text = this.state.editor.getText();
        const wordCount = this.countWords(text);
        this.state.currentNote.wordCount = wordCount;
        document.getElementById('wordCount').textContent = `${wordCount} words`;
    },

    // Count words in text
    countWords: function(text) {
        return text.trim().split(/\s+/).filter(word => word.length > 0).length;
    },

    // Render notes list
    renderNotesList: function() {
        const notesList = document.getElementById('notesList');
        const emptyState = document.getElementById('emptyState');
        
        // Filter notes based on current filter
        let filteredNotes = this.state.notes.filter(note => {
            // Skip trashed notes unless we're in trash view
            if (note.trashed && this.state.currentFilter !== 'trash') return false;
            if (!note.trashed && this.state.currentFilter === 'trash') return false;
            
            switch(this.state.currentFilter) {
                case 'favorite':
                    return note.favorite && !note.trashed;
                case 'notebook':
                    // This will be handled by notebook-specific filtering
                    return !note.trashed;
                case 'tag':
                    // This will be handled by tag-specific filtering
                    return !note.trashed;
                case 'trash':
                    return note.trashed;
                default:
                    return !note.trashed;
            }
        });

        // Apply search filter
        if (this.state.searchQuery) {
            filteredNotes = filteredNotes.filter(note => 
                note.title.toLowerCase().includes(this.state.searchQuery) ||
                this.stripHtml(note.content).toLowerCase().includes(this.state.searchQuery)
            );
        }

        // Sort notes
        filteredNotes.sort((a, b) => {
            switch(this.state.sortBy) {
                case 'date-asc':
                    return a.updatedAt - b.updatedAt;
                case 'title-asc':
                    return a.title.localeCompare(b.title);
                case 'title-desc':
                    return b.title.localeCompare(a.title);
                default: // 'date-desc'
                    return b.updatedAt - a.updatedAt;
            }
        });

        // Clear current list
        notesList.innerHTML = '';

        // Show empty state if no notes
        if (filteredNotes.length === 0) {
            emptyState.style.display = 'flex';
            return;
        } else {
            emptyState.style.display = 'none';
        }

        // Render notes
        filteredNotes.forEach(note => {
            const noteCard = document.createElement('div');
            noteCard.className = 'note-card';
            if (this.state.currentNote && note.id === this.state.currentNote.id) {
                noteCard.classList.add('selected');
            }
            
            noteCard.innerHTML = `
                <div class="note-card-header">
                    <h3 class="note-title">${this.escapeHtml(note.title)}</h3>
                    <button class="favorite-btn ${note.favorite ? 'active' : ''}" data-id="${note.id}">
                        <i class="${note.favorite ? 'fas' : 'far'} fa-star"></i>
                    </button>
                </div>
                <div class="note-content">${this.truncateText(this.stripHtml(note.content), 150)}</div>
                <div class="note-footer">
                    <div class="note-tags">
                        ${note.tags.map(tagId => {
                            const tag = this.state.tags.find(t => t.id === tagId);
                            return tag ? `<span class="tag-small" style="background-color: ${tag.color}20; color: ${tag.color}">${tag.name}</span>` : '';
                        }).join('')}
                    </div>
                    <span>${this.formatDate(note.updatedAt, true)}</span>
                </div>
            `;
            
            // Add click event
            noteCard.addEventListener('click', (e) => {
                if (!e.target.closest('.favorite-btn')) {
                    this.openNote(note);
                }
            });
            
            // Add favorite button event
            const favoriteBtn = noteCard.querySelector('.favorite-btn');
            favoriteBtn.addEventListener('click', (e) => {
                e.stopPropagation();
                this.toggleNoteFavorite(note.id);
            });
            
            notesList.appendChild(noteCard);
        });
    },

    // Toggle note favorite status
    toggleNoteFavorite: function(noteId) {
        const note = this.state.notes.find(n => n.id === noteId);
        if (note) {
            note.favorite = !note.favorite;
            note.updatedAt = new Date();
            this.saveNotes();
            this.renderNotesList();
            this.updateCounts();
            
            if (this.state.currentNote && note.id === this.state.currentNote.id) {
                this.state.currentNote.favorite = note.favorite;
                const favoriteBtn = document.getElementById('favoriteBtn');
                favoriteBtn.querySelector('i').className = note.favorite ? 'fas fa-star' : 'far fa-star';
            }
        }
    },

    // Render notebooks list
    renderNotebooks: function() {
        const notebooksList = document.getElementById('notebooksList');
        const notebookSelect = document.getElementById('notebookSelect');
        const defaultNotebookSelect = document.getElementById('defaultNotebook');
        
        // Clear lists
        notebooksList.innerHTML = '';
        notebookSelect.innerHTML = '<option value="">No Notebook</option>';
        defaultNotebookSelect.innerHTML = '<option value="">None</option>';
        
        // Update note counts
        this.state.notebooks.forEach(notebook => {
            notebook.noteCount = this.state.notes.filter(n => 
                n.notebookId === notebook.id && !n.trashed
            ).length;
        });
        
        // Render notebooks list
        this.state.notebooks.forEach(notebook => {
            // Sidebar list
            const li = document.createElement('li');
            li.innerHTML = `
                <i class="fas fa-folder" style="color: ${notebook.color}"></i>
                <span>${notebook.name}</span>
                <span class="badge">${notebook.noteCount}</span>
            `;
            li.addEventListener('click', () => {
                this.filterByNotebook(notebook.id);
            });
            notebooksList.appendChild(li);
            
            // Editor notebook select
            const option = document.createElement('option');
            option.value = notebook.id;
            option.textContent = notebook.name;
            if (this.state.currentNote && notebook.id === this.state.currentNote.notebookId) {
                option.selected = true;
            }
            notebookSelect.appendChild(option);
            
            // Settings default notebook select
            const defaultOption = option.cloneNode(true);
            if (notebook.id === this.state.settings.defaultNotebook) {
                defaultOption.selected = true;
            }
            defaultNotebookSelect.appendChild(defaultOption);
        });
        
        // Save updated notebooks
        this.saveNotebooks();
    },

    // Render tags
    renderTags: function() {
        const tagsContainer = document.getElementById('tagsContainer');
        tagsContainer.innerHTML = '';
        
        this.state.tags.forEach(tag => {
            const tagEl = document.createElement('div');
            tagEl.className = 'tag';
            tagEl.innerHTML = `
                <span class="tag-color" style="background-color: ${tag.color}"></span>
                <span>${tag.name}</span>
            `;
            tagEl.addEventListener('click', () => {
                this.filterByTag(tag.id);
            });
            tagsContainer.appendChild(tagEl);
        });
    },

    // Render note tags in editor
    renderNoteTags: function() {
        const noteTags = document.getElementById('noteTags');
        noteTags.innerHTML = '';
        
        if (!this.state.currentNote) return;
        
        this.state.currentNote.tags.forEach(tagId => {
            const tag = this.state.tags.find(t => t.id === tagId);
            if (tag) {
                const tagEl = document.createElement('span');
                tagEl.className = 'tag';
                tagEl.innerHTML = `
                    <span class="tag-color" style="background-color: ${tag.color}"></span>
                    <span>${tag.name}</span>
                    <button class="btn-icon remove-tag" data-tag="${tag.id}">
                        <i class="fas fa-times"></i>
                    </button>
                `;
                
                // Add remove event
                tagEl.querySelector('.remove-tag').addEventListener('click', (e) => {
                    e.stopPropagation();
                    this.removeTagFromNote(tag.id);
                });
                
                noteTags.appendChild(tagEl);
            }
        });
    },

    // Update notebook select in editor
    updateNotebookSelect: function() {
        const notebookSelect = document.getElementById('notebookSelect');
        if (this.state.currentNote) {
            notebookSelect.value = this.state.currentNote.notebookId || '';
        }
        
        // Add change event
        notebookSelect.addEventListener('change', () => {
            if (this.state.currentNote) {
                this.state.currentNote.notebookId = notebookSelect.value;
                this.saveCurrentNote();
                this.updateCounts();
            }
        });
    },

    // Filter by notebook
    filterByNotebook: function(notebookId) {
        this.state.currentFilter = 'notebook';
        document.getElementById('currentView').textContent = 'Notebook';
        
        // Update navigation
        document.querySelectorAll('.nav-menu li').forEach(item => {
            item.classList.remove('active');
        });
        
        // Filter and render notes
        const filteredNotes = this.state.notes.filter(note => 
            note.notebookId === notebookId && !note.trashed
        );
        
        // TODO: Update notes list display for notebook-specific view
        this.renderNotesList();
    },

    // Filter by tag
    filterByTag: function(tagId) {
        this.state.currentFilter = 'tag';
        document.getElementById('currentView').textContent = 'Tag';
        
        // Update navigation
        document.querySelectorAll('.nav-menu li').forEach(item => {
            item.classList.remove('active');
        });
        
        // Filter and render notes
        const filteredNotes = this.state.notes.filter(note => 
            note.tags.includes(tagId) && !note.trashed
        );
        
        // TODO: Update notes list display for tag-specific view
        this.renderNotesList();
    },

    // Add tag to current note
    addTagToNote: function(tagId) {
        if (!this.state.currentNote || this.state.currentNote.tags.includes(tagId)) return;
        
        this.state.currentNote.tags.push(tagId);
        this.renderNoteTags();
        this.saveCurrentNote();
    },

    // Remove tag from current note
    removeTagFromNote: function(tagId) {
        if (!this.state.currentNote) return;
        
        const index = this.state.currentNote.tags.indexOf(tagId);
        if (index !== -1) {
            this.state.currentNote.tags.splice(index, 1);
            this.renderNoteTags();
            this.saveCurrentNote();
        }
    },

    // Show tag modal
    showTagModal: function() {
        document.getElementById('tagModal').classList.add('active');
        document.getElementById('tagName').value = '';
        document.getElementById('tagName').focus();
        
        // Reset color selection
        document.querySelectorAll('.color-option').forEach(option => {
            option.classList.remove('selected');
        });
        document.querySelector('.color-option').classList.add('selected');
    },

    // Save new tag
    saveNewTag: function() {
        const name = document.getElementById('tagName').value.trim();
        const color = document.querySelector('.color-option.selected').dataset.color;
        
        if (!name) {
            this.showToast('Please enter a tag name', 'error');
            return;
        }
        
        const newTag = {
            id: Date.now().toString(),
            name,
            color
        };
        
        this.state.tags.push(newTag);
        this.saveTags();
        this.renderTags();
        
        document.getElementById('tagModal').classList.remove('active');
        this.showToast('Tag created successfully', 'success');
    },

    // Show notebook modal
    showNotebookModal: function() {
        document.getElementById('notebookModal').classList.add('active');
        document.getElementById('notebookName').value = '';
        document.getElementById('notebookName').focus();
    },

    // Save new notebook
    saveNewNotebook: function() {
        const name = document.getElementById('notebookName').value.trim();
        
        if (!name) {
            this.showToast('Please enter a notebook name', 'error');
            return;
        }
        
        const colors = ['#3b82f6', '#10b981', '#8b5cf6', '#f97316', '#ef4444', '#ec4899'];
        const randomColor = colors[Math.floor(Math.random() * colors.length)];
        
        const newNotebook = {
            id: Date.now().toString(),
            name,
            color: randomColor,
            noteCount: 0
        };
        
        this.state.notebooks.push(newNotebook);
        this.saveNotebooks();
        this.renderNotebooks();
        
        document.getElementById('notebookModal').classList.remove('active');
        this.showToast('Notebook created successfully', 'success');
    },

    // Show export modal
    showExportModal: function() {
        document.getElementById('exportModal').classList.add('active');
        
        // Add event listeners to export options
        document.querySelectorAll('.export-option').forEach(option => {
            option.addEventListener('click', (e) => {
                const type = e.currentTarget.dataset.type;
                this.handleExport(type);
            });
        });
    },

    // Show settings modal
    showSettingsModal: function() {
        document.getElementById('settingsModal').classList.add('active');
        
        // Load current settings
        document.getElementById('autoSaveInterval').value = this.state.settings.autoSaveInterval;
        document.getElementById('editorFontSize').value = this.state.settings.editorFontSize;
        document.getElementById('defaultNotebook').value = this.state.settings.defaultNotebook;
        
        // Add event listeners
        document.getElementById('exportDataBtn').addEventListener('click', () => {
            this.exportAllData();
        });
        
        document.getElementById('importDataBtn').addEventListener('click', () => {
            document.getElementById('importDataBtn').click();
        });
        
        document.getElementById('clearDataBtn').addEventListener('click', () => {
            if (confirm('Are you sure you want to clear all data? This cannot be undone.')) {
                this.clearAllData();
            }
        });
        
        // Save settings on change
        document.getElementById('autoSaveInterval').addEventListener('change', (e) => {
            this.state.settings.autoSaveInterval = parseInt(e.target.value);
            this.saveSettings();
        });
        
        document.getElementById('editorFontSize').addEventListener('change', (e) => {
            this.state.settings.editorFontSize = e.target.value;
            this.state.editor.root.style.fontSize = e.target.value;
            this.saveSettings();
        });
        
        document.getElementById('defaultNotebook').addEventListener('change', (e) => {
            this.state.settings.defaultNotebook = e.target.value;
            this.saveSettings();
        });
    },

    // Handle export
    handleExport: function(type) {
        if (!this.state.currentNote) {
            this.showToast('No note selected for export', 'error');
            return;
        }
        
        switch(type) {
            case 'pdf':
                exportToPDF(this.state.currentNote);
                break;
            case 'docx':
                exportToDOCX(this.state.currentNote);
                break;
            case 'pptx':
                exportToPPTX(this.state.currentNote);
                break;
            case 'html':
                exportToHTML(this.state.currentNote);
                break;
            case 'json':
                this.exportAllData();
                break;
        }
        
        document.getElementById('exportModal').classList.remove('active');
    },

    // Export all data
    exportAllData: function() {
        const data = {
            notes: this.state.notes,
            notebooks: this.state.notebooks,
            tags: this.state.tags,
            settings: this.state.settings,
            exportDate: new Date().toISOString()
        };
        
        const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = `notely-backup-${new Date().toISOString().split('T')[0]}.json`;
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        URL.revokeObjectURL(url);
        
        this.showToast('Backup exported successfully', 'success');
    },

    // Import data
    importData: function(file) {
        const reader = new FileReader();
        reader.onload = (e) => {
            try {
                const data = JSON.parse(e.target.result);
                
                // Validate data structure
                if (!data.notes || !Array.isArray(data.notes)) {
                    throw new Error('Invalid data format');
                }
                
                // Merge data (you might want to add confirmation here)
                if (data.notes) this.state.notes = [...this.state.notes, ...data.notes];
                if (data.notebooks) this.state.notebooks = [...this.state.notebooks, ...data.notebooks];
                if (data.tags) this.state.tags = [...this.state.tags, ...data.tags];
                if (data.settings) this.state.settings = { ...this.state.settings, ...data.settings };
                
                // Save all data
                this.saveNotes();
                this.saveNotebooks();
                this.saveTags();
                this.saveSettings();
                
                // Refresh UI
                this.renderNotesList();
                this.renderNotebooks();
                this.renderTags();
                this.updateCounts();
                
                this.showToast('Data imported successfully', 'success');
            } catch (error) {
                this.showToast('Error importing data: ' + error.message, 'error');
            }
        };
        reader.readAsText(file);
    },

    // Clear all data
    clearAllData: function() {
        localStorage.clear();
        this.state.notes = [];
        this.state.notebooks = [];
        this.state.tags = [];
        this.state.currentNote = null;
        
        // Reset to defaults
        this.loadData();
        
        // Refresh UI
        this.renderNotesList();
        this.renderNotebooks();
        this.renderTags();
        this.updateCounts();
        this.closeEditor();
        
        this.showToast('All data cleared', 'success');
    },

    // Handle image upload
    handleImageUpload: function() {
        const input = document.createElement('input');
        input.type = 'file';
        input.accept = 'image/*';
        
        input.onchange = (e) => {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = (e) => {
                    // Insert image into editor
                    const range = this.state.editor.getSelection();
                    this.state.editor.insertEmbed(range.index, 'image', e.target.result);
                    
                    // Show image editor modal
                    this.showImageEditor(e.target.result);
                };
                reader.readAsDataURL(file);
            }
        };
        
        input.click();
    },

    // Show image editor
    showImageEditor: function(imageSrc) {
        document.getElementById('imageModal').classList.add('active');
        const img = document.getElementById('imageToEdit');
        img.src = imageSrc;
        
        // Initialize Cropper.js
        const cropper = new Cropper(img, {
            aspectRatio: NaN, // Free aspect ratio
            viewMode: 1,
            autoCropArea: 0.8,
            responsive: true,
            restore: true
        });
        
        // Add event listeners for image controls
        document.getElementById('cropBtn').onclick = () => {
            const croppedCanvas = cropper.getCroppedCanvas();
            img.src = croppedCanvas.toDataURL();
            cropper.destroy();
            cropper = new Cropper(img, {
                aspectRatio: NaN,
                viewMode: 1,
                autoCropArea: 0.8
            });
        };
        
        document.getElementById('rotateBtn').onclick = () => {
            cropper.rotate(90);
        };
        
        document.getElementById('flipBtn').onclick = () => {
            cropper.scaleX(-cropper.getData().scaleX || -1);
        };
        
        document.getElementById('applyImageBtn').onclick = () => {
            const croppedCanvas = cropper.getCroppedCanvas();
            const finalImage = croppedCanvas.toDataURL('image/jpeg', 0.9);
            
            // Replace the image in editor
            const range = this.state.editor.getSelection();
            this.state.editor.deleteText(range.index, 1);
            this.state.editor.insertEmbed(range.index, 'image', finalImage);
            
            cropper.destroy();
            document.getElementById('imageModal').classList.remove('active');
            this.showToast('Image edited and inserted', 'success');
        };
    },

    // Update counts in sidebar
    updateCounts: function() {
        const allNotesCount = this.state.notes.filter(n => !n.trashed).length;
        const favoritesCount = this.state.notes.filter(n => n.favorite && !n.trashed).length;
        const trashCount = this.state.notes.filter(n => n.trashed).length;
        
        document.getElementById('allNotesCount').textContent = allNotesCount;
        document.getElementById('favoritesCount').textContent = favoritesCount;
        document.getElementById('trashCount').textContent = trashCount;
    },

    // Save data to localStorage
    saveNotes: function() {
        localStorage.setItem('notely_notes', JSON.stringify(this.state.notes));
    },

    saveNotebooks: function() {
        localStorage.setItem('notely_notebooks', JSON.stringify(this.state.notebooks));
    },

    saveTags: function() {
        localStorage.setItem('notely_tags', JSON.stringify(this.state.tags));
    },

    saveSettings: function() {
        localStorage.setItem('notely_settings', JSON.stringify(this.state.settings));
    },

    // Initialize service worker
    initServiceWorker: function() {
        if ('serviceWorker' in navigator) {
            navigator.serviceWorker.register('service-worker.js')
                .then(registration => {
                    console.log('Service Worker registered with scope:', registration.scope);
                })
                .catch(error => {
                    console.log('Service Worker registration failed:', error);
                });
        }
    },

    // Show toast notification
    showToast: function(message, type = 'info') {
        const toastContainer = document.getElementById('toastContainer');
        const toast = document.createElement('div');
        toast.className = `toast ${type}`;
        toast.innerHTML = `
            <i class="fas fa-${type === 'success' ? 'check-circle' : type === 'error' ? 'exclamation-circle' : 'info-circle'}"></i>
            <span>${message}</span>
        `;
        
        toastContainer.appendChild(toast);
        
        // Remove toast after 3 seconds
        setTimeout(() => {
            toast.style.animation = 'slideIn 0.3s ease reverse';
            setTimeout(() => {
                toastContainer.removeChild(toast);
            }, 300);
        }, 3000);
    },

    // Utility functions
    formatDate: function(date, short = false) {
        if (!(date instanceof Date)) date = new Date(date);
        
        const now = new Date();
        const diffMs = now - date;
        const diffMins = Math.floor(diffMs / 60000);
        const diffHours = Math.floor(diffMs / 3600000);
        const diffDays = Math.floor(diffMs / 86400000);
        
        if (short) {
            if (diffMins < 1) return 'Just now';
            if (diffMins < 60) return `${diffMins}m ago`;
            if (diffHours < 24) return `${diffHours}h ago`;
            if (diffDays < 7) return `${diffDays}d ago`;
            return date.toLocaleDateString();
        } else {
            return date.toLocaleString();
        }
    },

    stripHtml: function(html) {
        const tmp = document.createElement('div');
        tmp.innerHTML = html;
        return tmp.textContent || tmp.innerText || '';
    },

    truncateText: function(text, length) {
        if (text.length <= length) return text;
        return text.substring(0, length) + '...';
    },

    escapeHtml: function(text) {
        const div = document.createElement('div');
        div.textContent = text;
        return div.innerHTML;
    }
};

// Make app global for event handlers
window.app = app;

// Initialize color picker
document.addEventListener('DOMContentLoaded', () => {
    // Color picker selection
    document.querySelectorAll('.color-option').forEach(option => {
        option.addEventListener('click', function() {
            document.querySelectorAll('.color-option').forEach(o => o.classList.remove('selected'));
            this.classList.add('selected');
        });
    });
    
    // Save tag button
    document.getElementById('saveTagBtn').addEventListener('click', () => app.saveNewTag());
    
    // Save notebook button
    document.getElementById('saveNotebookBtn').addEventListener('click', () => app.saveNewNotebook());
    
    // Delete note button
    document.getElementById('deleteBtn').addEventListener('click', () => app.deleteCurrentNote());
    
    // Favorite button
    document.getElementById('favoriteBtn').addEventListener('click', () => app.toggleFavorite());
    
    // Export dropdown
    document.querySelectorAll('.dropdown-content a').forEach(link => {
        link.addEventListener('click', (e) => {
            e.preventDefault();
            const exportType = e.currentTarget.dataset.export;
            app.handleExport(exportType);
        });
    });
    
    // Import file input
    const importInput = document.createElement('input');
    importInput.type = 'file';
    importInput.accept = '.json';
    importInput.style.display = 'none';
    importInput.id = 'importFileInput';
    document.body.appendChild(importInput);
    
    document.getElementById('importDataBtn').addEventListener('click', () => {
        importInput.click();
    });
    
    importInput.addEventListener('change', (e) => {
        const file = e.target.files[0];
        if (file) {
            app.importData(file);
        }
        importInput.value = '';
    });
    
    // Note title auto-save
    document.getElementById('noteTitle').addEventListener('input', () => {
        if (app.state.currentNote) {
            app.state.currentNote.title = document.getElementById('noteTitle').value;
            app.saveCurrentNote();
        }
    });
});


// Storage Management
const storage = {
    // Initialize IndexedDB for larger storage
    initDB: function() {
        return new Promise((resolve, reject) => {
            if (!window.indexedDB) {
                console.warn('IndexedDB not supported, using localStorage only');
                resolve(false);
                return;
            }

            const request = indexedDB.open('NotelyDB', 1);

            request.onerror = (event) => {
                console.error('IndexedDB error:', event.target.error);
                reject(event.target.error);
            };

            request.onupgradeneeded = (event) => {
                const db = event.target.result;
                
                // Create notes store
                if (!db.objectStoreNames.contains('notes')) {
                    const notesStore = db.createObjectStore('notes', { keyPath: 'id' });
                    notesStore.createIndex('createdAt', 'createdAt', { unique: false });
                    notesStore.createIndex('updatedAt', 'updatedAt', { unique: false });
                    notesStore.createIndex('notebookId', 'notebookId', { unique: false });
                }
                
                // Create attachments store
                if (!db.objectStoreNames.contains('attachments')) {
                    const attachmentsStore = db.createObjectStore('attachments', { keyPath: 'id' });
                    attachmentsStore.createIndex('noteId', 'noteId', { unique: false });
                }
            };

            request.onsuccess = (event) => {
                this.db = event.target.result;
                console.log('IndexedDB initialized successfully');
                resolve(true);
            };
        });
    },

    // Save note to IndexedDB
    saveNoteToDB: function(note) {
        return new Promise((resolve, reject) => {
            if (!this.db) {
                reject(new Error('IndexedDB not initialized'));
                return;
            }

            const transaction = this.db.transaction(['notes'], 'readwrite');
            const store = transaction.objectStore('notes');
            const request = store.put(note);

            request.onerror = (event) => {
                reject(event.target.error);
            };

            request.onsuccess = (event) => {
                resolve(event.target.result);
            };
        });
    },

    // Get note from IndexedDB
    getNoteFromDB: function(noteId) {
        return new Promise((resolve, reject) => {
            if (!this.db) {
                reject(new Error('IndexedDB not initialized'));
                return;
            }

            const transaction = this.db.transaction(['notes'], 'readonly');
            const store = transaction.objectStore('notes');
            const request = store.get(noteId);

            request.onerror = (event) => {
                reject(event.target.error);
            };

            request.onsuccess = (event) => {
                resolve(event.target.result);
            };
        });
    },

    // Get all notes from IndexedDB
    getAllNotesFromDB: function() {
        return new Promise((resolve, reject) => {
            if (!this.db) {
                reject(new Error('IndexedDB not initialized'));
                return;
            }

            const transaction = this.db.transaction(['notes'], 'readonly');
            const store = transaction.objectStore('notes');
            const request = store.getAll();

            request.onerror = (event) => {
                reject(event.target.error);
            };

            request.onsuccess = (event) => {
                resolve(event.target.result);
            };
        });
    },

    // Delete note from IndexedDB
    deleteNoteFromDB: function(noteId) {
        return new Promise((resolve, reject) => {
            if (!this.db) {
                reject(new Error('IndexedDB not initialized'));
                return;
            }

            const transaction = this.db.transaction(['notes'], 'readwrite');
            const store = transaction.objectStore('notes');
            const request = store.delete(noteId);

            request.onerror = (event) => {
                reject(event.target.error);
            };

            request.onsuccess = (event) => {
                resolve(true);
            };
        });
    },

    // Save attachment to IndexedDB
    saveAttachment: function(attachment) {
        return new Promise((resolve, reject) => {
            if (!this.db) {
                reject(new Error('IndexedDB not initialized'));
                return;
            }

            const transaction = this.db.transaction(['attachments'], 'readwrite');
            const store = transaction.objectStore('attachments');
            const request = store.put(attachment);

            request.onerror = (event) => {
                reject(event.target.error);
            };

            request.onsuccess = (event) => {
                resolve(event.target.result);
            };
        });
    },

    // Get attachments for note
    getNoteAttachments: function(noteId) {
        return new Promise((resolve, reject) => {
            if (!this.db) {
                reject(new Error('IndexedDB not initialized'));
                return;
            }

            const transaction = this.db.transaction(['attachments'], 'readonly');
            const store = transaction.objectStore('attachments');
            const index = store.index('noteId');
            const request = index.getAll(noteId);

            request.onerror = (event) => {
                reject(event.target.error);
            };

            request.onsuccess = (event) => {
                resolve(event.target.result);
            };
        });
    },

    // Delete attachment
    deleteAttachment: function(attachmentId) {
        return new Promise((resolve, reject) => {
            if (!this.db) {
                reject(new Error('IndexedDB not initialized'));
                return;
            }

            const transaction = this.db.transaction(['attachments'], 'readwrite');
            const store = transaction.objectStore('attachments');
            const request = store.delete(attachmentId);

            request.onerror = (event) => {
                reject(event.target.error);
            };

            request.onsuccess = (event) => {
                resolve(true);
            };
        });
    },

    // Backup all data to JSON
    backupAllData: function() {
        return new Promise(async (resolve, reject) => {
            try {
                const notes = await this.getAllNotesFromDB();
                const attachments = await this.getAllAttachments();
                
                const backup = {
                    notes: notes,
                    attachments: attachments,
                    metadata: {
                        backupDate: new Date().toISOString(),
                        version: '1.0',
                        totalNotes: notes.length,
                        totalAttachments: attachments.length
                    }
                };
                
                resolve(backup);
            } catch (error) {
                reject(error);
            }
        });
    },

    // Get all attachments
    getAllAttachments: function() {
        return new Promise((resolve, reject) => {
            if (!this.db) {
                reject(new Error('IndexedDB not initialized'));
                return;
            }

            const transaction = this.db.transaction(['attachments'], 'readonly');
            const store = transaction.objectStore('attachments');
            const request = store.getAll();

            request.onerror = (event) => {
                reject(event.target.error);
            };

            request.onsuccess = (event) => {
                resolve(event.target.result);
            };
        });
    },

    // Restore from backup
    restoreFromBackup: function(backupData) {
        return new Promise(async (resolve, reject) => {
            try {
                // Validate backup data
                if (!backupData.notes || !Array.isArray(backupData.notes)) {
                    throw new Error('Invalid backup format');
                }

                // Clear existing data
                await this.clearAllData();

                // Restore notes
                for (const note of backupData.notes) {
                    await this.saveNoteToDB(note);
                }

                // Restore attachments if present
                if (backupData.attachments && Array.isArray(backupData.attachments)) {
                    for (const attachment of backupData.attachments) {
                        await this.saveAttachment(attachment);
                    }
                }

                resolve(true);
            } catch (error) {
                reject(error);
            }
        });
    },

    // Clear all data from IndexedDB
    clearAllData: function() {
        return new Promise((resolve, reject) => {
            if (!this.db) {
                reject(new Error('IndexedDB not initialized'));
                return;
            }

            const transaction = this.db.transaction(['notes', 'attachments'], 'readwrite');
            
            // Clear notes
            const notesStore = transaction.objectStore('notes');
            const notesRequest = notesStore.clear();
            
            // Clear attachments
            const attachmentsStore = transaction.objectStore('attachments');
            const attachmentsRequest = attachmentsStore.clear();

            notesRequest.onerror = (event) => {
                reject(event.target.error);
            };

            attachmentsRequest.onerror = (event) => {
                reject(event.target.error);
            };

            transaction.oncomplete = () => {
                resolve(true);
            };

            transaction.onerror = (event) => {
                reject(event.target.error);
            };
        });
    },

    // Get storage usage
    getStorageUsage: function() {
        return new Promise((resolve, reject) => {
            if (!navigator.storage || !navigator.storage.estimate) {
                resolve({ usage: 0, quota: 0, percent: 0 });
                return;
            }

            navigator.storage.estimate().then(estimate => {
                resolve({
                    usage: estimate.usage || 0,
                    quota: estimate.quota || 0,
                    percent: estimate.quota ? (estimate.usage / estimate.quota * 100) : 0
                });
            }).catch(error => {
                reject(error);
            });
        });
    },

    // Check if storage is low
    isStorageLow: function() {
        return new Promise((resolve, reject) => {
            if (!navigator.storage || !navigator.storage.estimate) {
                resolve(false);
                return;
            }

            navigator.storage.estimate().then(estimate => {
                const percentUsed = estimate.quota ? (estimate.usage / estimate.quota * 100) : 0;
                resolve(percentUsed > 90); // Consider low if over 90% used
            }).catch(error => {
                reject(error);
            });
        });
    },

    // Migrate from localStorage to IndexedDB
    migrateFromLocalStorage: function() {
        return new Promise(async (resolve, reject) => {
            try {
                // Check if migration is needed
                const localStorageNotes = localStorage.getItem('notely_notes');
                if (!localStorageNotes) {
                    resolve(false); // No data to migrate
                    return;
                }

                const notes = JSON.parse(localStorageNotes);
                
                // Initialize IndexedDB if not already
                if (!this.db) {
                    await this.initDB();
                }

                // Migrate notes
                for (const note of notes) {
                    await this.saveNoteToDB(note);
                }

                // Clear localStorage after successful migration
                localStorage.removeItem('notely_notes');
                
                resolve(true);
            } catch (error) {
                reject(error);
            }
        });
    },

    // Export data as downloadable file
    exportToFile: function(filename = 'notely-backup.json') {
        return new Promise(async (resolve, reject) => {
            try {
                const backup = await this.backupAllData();
                const blob = new Blob([JSON.stringify(backup, null, 2)], { type: 'application/json' });
                const url = URL.createObjectURL(blob);
                
                const a = document.createElement('a');
                a.href = url;
                a.download = filename;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                
                resolve(true);
            } catch (error) {
                reject(error);
            }
        });
    },

    // Import data from file
    importFromFile: function(file) {
        return new Promise((resolve, reject) => {
            const reader = new FileReader();
            
            reader.onload = async (event) => {
                try {
                    const backupData = JSON.parse(event.target.result);
                    await this.restoreFromBackup(backupData);
                    resolve(true);
                } catch (error) {
                    reject(error);
                }
            };
            
            reader.onerror = (error) => {
                reject(error);
            };
            
            reader.readAsText(file);
        });
    },

    // Search notes with advanced filters
    searchNotes: function(query, filters = {}) {
        return new Promise(async (resolve, reject) => {
            try {
                let notes = await this.getAllNotesFromDB();
                
                // Apply text search
                if (query) {
                    const searchTerms = query.toLowerCase().split(' ').filter(term => term.length > 0);
                    notes = notes.filter(note => {
                        const text = (note.title + ' ' + this.stripHtml(note.content)).toLowerCase();
                        return searchTerms.every(term => text.includes(term));
                    });
                }
                
                // Apply filters
                if (filters.notebookId) {
                    notes = notes.filter(note => note.notebookId === filters.notebookId);
                }
                
                if (filters.tags && filters.tags.length > 0) {
                    notes = notes.filter(note => {
                        return filters.tags.every(tagId => note.tags.includes(tagId));
                    });
                }
                
                if (filters.favorite !== undefined) {
                    notes = notes.filter(note => note.favorite === filters.favorite);
                }
                
                if (filters.dateFrom) {
                    const dateFrom = new Date(filters.dateFrom);
                    notes = notes.filter(note => new Date(note.updatedAt) >= dateFrom);
                }
                
                if (filters.dateTo) {
                    const dateTo = new Date(filters.dateTo);
                    notes = notes.filter(note => new Date(note.updatedAt) <= dateTo);
                }
                
                // Apply sorting
                if (filters.sortBy) {
                    notes.sort((a, b) => {
                        switch (filters.sortBy) {
                            case 'title-asc':
                                return a.title.localeCompare(b.title);
                            case 'title-desc':
                                return b.title.localeCompare(a.title);
                            case 'date-asc':
                                return new Date(a.updatedAt) - new Date(b.updatedAt);
                            case 'date-desc':
                            default:
                                return new Date(b.updatedAt) - new Date(a.updatedAt);
                        }
                    });
                }
                
                resolve(notes);
            } catch (error) {
                reject(error);
            }
        });
    },

    // Helper function to strip HTML
    stripHtml: function(html) {
        const tmp = document.createElement('div');
        tmp.innerHTML = html;
        return tmp.textContent || tmp.innerText || '';
    }
};

// Initialize storage when page loads
document.addEventListener('DOMContentLoaded', () => {
    storage.initDB().then(success => {
        if (success) {
            console.log('Storage initialized successfully');
            
            // Check if we need to migrate from localStorage
            storage.migrateFromLocalStorage().then(migrated => {
                if (migrated) {
                    console.log('Successfully migrated data from localStorage to IndexedDB');
                }
            });
        }
    }).catch(error => {
        console.error('Failed to initialize storage:', error);
    });
});

// Export storage object
window.storage = storage;


// Export Functions
const exportToPDF = function(note) {
    // Check if required libraries are loaded
    if (typeof jsPDF === 'undefined') {
        // Dynamically load jsPDF and html2canvas
        const script1 = document.createElement('script');
        script1.src = 'https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js';
        
        const script2 = document.createElement('script');
        script2.src = 'https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js';
        
        Promise.all([
            new Promise(resolve => { script1.onload = resolve; }),
            new Promise(resolve => { script2.onload = resolve; })
        ]).then(() => {
            // Now libraries are loaded, call the function again
            exportToPDF(note);
        });
        
        document.head.appendChild(script1);
        document.head.appendChild(script2);
        return;
    }
    
    // Create a temporary div for rendering
    const tempDiv = document.createElement('div');
    tempDiv.style.position = 'absolute';
    tempDiv.style.left = '-9999px';
    tempDiv.style.top = '0';
    tempDiv.style.width = '210mm'; // A4 width
    tempDiv.style.padding = '20mm';
    tempDiv.style.backgroundColor = 'white';
    tempDiv.style.color = 'black';
    tempDiv.style.fontFamily = 'Arial, sans-serif';
    
    // Create PDF content
    tempDiv.innerHTML = `
        <div style="margin-bottom: 20px; border-bottom: 2px solid #333; padding-bottom: 10px;">
            <h1 style="margin: 0; font-size: 24px; color: #333;">${note.title}</h1>
            <p style="margin: 5px 0 0 0; font-size: 12px; color: #666;">
                Created: ${new Date(note.createdAt).toLocaleString()} | 
                Updated: ${new Date(note.updatedAt).toLocaleString()} | 
                Words: ${note.wordCount}
            </p>
        </div>
        <div style="font-size: 12px; line-height: 1.6;">${note.content}</div>
        <div style="margin-top: 30px; padding-top: 10px; border-top: 1px solid #ccc; font-size: 10px; color: #666;">
            Exported from Notely - ${new Date().toLocaleString()}
        </div>
    `;
    
    document.body.appendChild(tempDiv);
    
    // Convert to canvas and then to PDF
    html2canvas(tempDiv, {
        scale: 2,
        useCORS: true,
        logging: false
    }).then(canvas => {
        const imgData = canvas.toDataURL('image/png');
        const pdf = new jsPDF.jsPDF({
            orientation: 'portrait',
            unit: 'mm',
            format: 'a4'
        });
        
        const imgWidth = 210; // A4 width in mm
        const pageHeight = 295; // A4 height in mm
        const imgHeight = canvas.height * imgWidth / canvas.width;
        
        let heightLeft = imgHeight;
        let position = 0;
        
        pdf.addImage(imgData, 'PNG', 0, position, imgWidth, imgHeight);
        heightLeft -= pageHeight;
        
        // Add additional pages if needed
        while (heightLeft >= 0) {
            position = heightLeft - imgHeight;
            pdf.addPage();
            pdf.addImage(imgData, 'PNG', 0, position, imgWidth, imgHeight);
            heightLeft -= pageHeight;
        }
        
        // Save the PDF
        pdf.save(`${note.title.replace(/[^a-z0-9]/gi, '_').toLowerCase()}.pdf`);
        
        // Clean up
        document.body.removeChild(tempDiv);
        
        // Show success message
        app.showToast('PDF exported successfully', 'success');
    }).catch(error => {
        console.error('Error generating PDF:', error);
        app.showToast('Error exporting PDF', 'error');
        document.body.removeChild(tempDiv);
    });
};

const exportToDOCX = function(note) {
    // Check if required library is loaded
    if (typeof docx === 'undefined') {
        // Dynamically load docx.js
        const script = document.createElement('script');
        script.src = 'https://cdnjs.cloudflare.com/ajax/libs/docx/7.8.0/docx.min.js';
        script.onload = () => {
            // Now library is loaded, call the function again
            exportToDOCX(note);
        };
        document.head.appendChild(script);
        return;
    }
    
    try {
        // Create a new document
        const doc = new docx.Document({
            sections: [{
                properties: {},
                children: [
                    new docx.Paragraph({
                        text: note.title,
                        heading: docx.HeadingLevel.TITLE,
                        spacing: {
                            after: 200
                        }
                    }),
                    new docx.Paragraph({
                        text: `Created: ${new Date(note.createdAt).toLocaleString()} | Updated: ${new Date(note.updatedAt).toLocaleString()} | Words: ${note.wordCount}`,
                        size: 20
                    }),
                    new docx.Paragraph({
                        text: '',
                        spacing: {
                            before: 200,
                            after: 200
                        }
                    }),
                    // Add note content (simplified - for full HTML to DOCX conversion, you'd need a more complex parser)
                    new docx.Paragraph({
                        text: stripHtmlTags(note.content).substring(0, 5000), // Limit content for demo
                        spacing: {
                            line: 300
                        }
                    }),
                    new docx.Paragraph({
                        text: `\n\nExported from Notely - ${new Date().toLocaleString()}`,
                        size: 20,
                        color: "666666"
                    })
                ]
            }]
        });
        
        // Generate and download the DOCX file
        docx.Packer.toBlob(doc).then(blob => {
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `${note.title.replace(/[^a-z0-9]/gi, '_').toLowerCase()}.docx`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            app.showToast('Word document exported successfully', 'success');
        });
    } catch (error) {
        console.error('Error generating DOCX:', error);
        app.showToast('Error exporting Word document', 'error');
    }
};

const exportToPPTX = function(note) {
    // Check if required library is loaded
    if (typeof PptxGenJS === 'undefined') {
        // Dynamically load PptxGenJS
        const script = document.createElement('script');
        script.src = 'https://cdn.jsdelivr.net/npm/pptxgenjs@3.12.0/dist/pptxgen.bundle.js';
        script.onload = () => {
            // Now library is loaded, call the function again
            exportToPPTX(note);
        };
        document.head.appendChild(script);
        return;
    }
    
    try {
        // Create a new presentation
        const pptx = new PptxGenJS();
        
        // Add a slide
        const slide = pptx.addSlide();
        
        // Add title
        slide.addText(note.title, {
            x: 0.5,
            y: 0.5,
            w: '90%',
            h: 1,
            fontSize: 24,
            bold: true,
            color: '363636'
        });
        
        // Add metadata
        slide.addText(
            `Created: ${new Date(note.createdAt).toLocaleDateString()}\nUpdated: ${new Date(note.updatedAt).toLocaleDateString()}\nWords: ${note.wordCount}`,
            {
                x: 0.5,
                y: 1.5,
                w: '90%',
                h: 0.8,
                fontSize: 12,
                color: '666666'
            }
        );
        
        // Add content (simplified)
        const content = stripHtmlTags(note.content).substring(0, 2000); // Limit content
        slide.addText(content, {
            x: 0.5,
            y: 2.5,
            w: '90%',
            h: 4,
            fontSize: 14,
            color: '000000'
        });
        
        // Add footer
        slide.addText(
            `Exported from Notely - ${new Date().toLocaleDateString()}`,
            {
                x: 0.5,
                y: 6.8,
                w: '90%',
                h: 0.3,
                fontSize: 10,
                color: '999999',
                align: 'center'
            }
        );
        
        // Generate and download the PPTX file
        pptx.writeFile({
            fileName: `${note.title.replace(/[^a-z0-9]/gi, '_').toLowerCase()}.pptx`
        }).then(() => {
            app.showToast('PowerPoint exported successfully', 'success');
        });
    } catch (error) {
        console.error('Error generating PPTX:', error);
        app.showToast('Error exporting PowerPoint', 'error');
    }
};

const exportToHTML = function(note) {
    // Create HTML content
    const htmlContent = `
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>${note.title} - Notely Export</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            line-height: 1.6;
            color: #333;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        .header {
            border-bottom: 2px solid #4f46e5;
            padding-bottom: 20px;
            margin-bottom: 30px;
        }
        h1 {
            color: #4f46e5;
            margin: 0 0 10px 0;
        }
        .meta {
            color: #666;
            font-size: 14px;
            margin-bottom: 20px;
        }
        .content {
            font-size: 16px;
        }
        .footer {
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid #eee;
            color: #999;
            font-size: 12px;
            text-align: center;
        }
        img {
            max-width: 100%;
            height: auto;
        }
        table {
            border-collapse: collapse;
            width: 100%;
            margin: 20px 0;
        }
        table th, table td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        table th {
            background-color: #f5f5f5;
        }
        code {
            background-color: #f5f5f5;
            padding: 2px 4px;
            border-radius: 4px;
            font-family: 'Courier New', monospace;
        }
        pre {
            background-color: #f5f5f5;
            padding: 15px;
            border-radius: 4px;
            overflow: auto;
        }
        blockquote {
            border-left: 4px solid #4f46e5;
            margin: 20px 0;
            padding-left: 20px;
            color: #666;
            font-style: italic;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>${note.title}</h1>
        <div class="meta">
            Created: ${new Date(note.createdAt).toLocaleString()} | 
            Updated: ${new Date(note.updatedAt).toLocaleString()} | 
            Words: ${note.wordCount}
        </div>
    </div>
    <div class="content">
        ${note.content}
    </div>
    <div class="footer">
        Exported from Notely on ${new Date().toLocaleString()}
    </div>
</body>
</html>`;
    
    // Create and download the HTML file
    const blob = new Blob([htmlContent], { type: 'text/html' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `${note.title.replace(/[^a-z0-9]/gi, '_').toLowerCase()}.html`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
    
    app.showToast('HTML exported successfully', 'success');
};

const exportToTXT = function(note) {
    // Create plain text content
    const textContent = `${note.title}\n${'='.repeat(note.title.length)}\n\n` +
        `Created: ${new Date(note.createdAt).toLocaleString()}\n` +
        `Updated: ${new Date(note.updatedAt).toLocaleString()}\n` +
        `Words: ${note.wordCount}\n\n` +
        `${'─'.repeat(50)}\n\n` +
        `${stripHtmlTags(note.content)}\n\n` +
        `${'─'.repeat(50)}\n` +
        `Exported from Notely on ${new Date().toLocaleString()}`;
    
    // Create and download the TXT file
    const blob = new Blob([textContent], { type: 'text/plain' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `${note.title.replace(/[^a-z0-9]/gi, '_').toLowerCase()}.txt`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
    
    app.showToast('Text file exported successfully', 'success');
};

const exportToMarkdown = function(note) {
    // Convert HTML to Markdown (simplified)
    let markdownContent = `# ${note.title}\n\n` +
        `**Created:** ${new Date(note.createdAt).toLocaleString()}  \n` +
        `**Updated:** ${new Date(note.updatedAt).toLocaleString()}  \n` +
        `**Words:** ${note.wordCount}\n\n` +
        `---\n\n`;
    
    // Basic HTML to Markdown conversion
    let content = note.content
        .replace(/<h1[^>]*>(.*?)<\/h1>/gi, '# $1\n\n')
        .replace(/<h2[^>]*>(.*?)<\/h2>/gi, '## $1\n\n')
        .replace(/<h3[^>]*>(.*?)<\/h3>/gi, '### $1\n\n')
        .replace(/<strong[^>]*>(.*?)<\/strong>/gi, '**$1**')
        .replace(/<b[^>]*>(.*?)<\/b>/gi, '**$1**')
        .replace(/<em[^>]*>(.*?)<\/em>/gi, '*$1*')
        .replace(/<i[^>]*>(.*?)<\/i>/gi, '*$1*')
        .replace(/<a href="([^"]*)"[^>]*>(.*?)<\/a>/gi, '[$2]($1)')
        .replace(/<ul[^>]*>(.*?)<\/ul>/gis, (match, p1) => {
            return p1.replace(/<li[^>]*>(.*?)<\/li>/gi, '* $1\n');
        })
        .replace(/<ol[^>]*>(.*?)<\/ol>/gis, (match, p1) => {
            let counter = 1;
            return p1.replace(/<li[^>]*>(.*?)<\/li>/gi, () => `${counter++}. $1\n`);
        })
        .replace(/<p[^>]*>(.*?)<\/p>/gi, '$1\n\n')
        .replace(/<br\s*\/?>/gi, '\n')
        .replace(/<[^>]*>/g, '') // Remove remaining HTML tags
        .replace(/&nbsp;/g, ' ')
        .replace(/&amp;/g, '&')
        .replace(/&lt;/g, '<')
        .replace(/&gt;/g, '>')
        .replace(/&quot;/g, '"')
        .replace(/&#39;/g, "'");
    
    markdownContent += content + `\n\n---\n\n*Exported from Notely on ${new Date().toLocaleString()}*`;
    
    // Create and download the Markdown file
    const blob = new Blob([markdownContent], { type: 'text/markdown' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
      }
    </script>
</body>
</html>
