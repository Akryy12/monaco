<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Monaco Editor - FluxusZ</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            height: 100%;
            width: 100%;
            overflow: hidden;
            background-color: #1e1e1e;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
        }
        /* Tab bar styling */
        .tabs-container {
            background-color: #2d2d2d;
            border-bottom: 1px solid #3c3c3c;
            display: flex;
            flex-wrap: nowrap;
            overflow-x: auto;
            overflow-y: hidden;
            user-select: none;
        }
        .tab {
            background-color: #2d2d2d;
            color: #cccccc;
            padding: 6px 16px;
            font-size: 12px;
            font-family: inherit;
            border-right: 1px solid #3c3c3c;
            cursor: pointer;
            display: flex;
            align-items: center;
            white-space: nowrap;
        }
        .tab.active {
            background-color: #1e1e1e;
            color: white;
            border-bottom: 1px solid #007acc;
        }
        .tab:hover:not(.active) {
            background-color: #3c3c3c;
        }
        .tab-close {
            margin-left: 8px;
            font-size: 14px;
            font-weight: bold;
            opacity: 0.6;
            cursor: pointer;
            border-radius: 2px;
            width: 16px;
            text-align: center;
        }
        .tab-close:hover {
            opacity: 1;
            background-color: #e81123;
            color: white;
        }
        .new-tab-btn {
            background-color: #2d2d2d;
            color: #cccccc;
            border: none;
            padding: 6px 12px;
            font-size: 14px;
            cursor: pointer;
            border-left: 1px solid #3c3c3c;
        }
        .new-tab-btn:hover {
            background-color: #3c3c3c;
            color: white;
        }
        #editor-container {
            height: calc(100% - 35px);
            width: 100%;
        }
    </style>
</head>
<body>
    <div class="tabs-container" id="tabs-container">
        <!-- Tabs will be injected here -->
        <button class="new-tab-btn" id="newTabBtn" title="New script">+</button>
    </div>
    <div id="editor-container"></div>

    <!-- Monaco editor from CDN -->
    <script src="https://cdn.jsdelivr.net/npm/monaco-editor@0.45.0/min/vs/loader.js"></script>
    <script>
        // ---------- Tab & document management ----------
        let editor = null;
        let tabs = [];            // { id, model, title, dirty, content }
        let activeTabId = null;
        let nextTabId = 1;

        // ---------- Helper to get current model ----------
        function getCurrentModel() {
            if (!activeTabId) return null;
            const tab = tabs.find(t => t.id === activeTabId);
            return tab ? tab.model : null;
        }

        // ---------- Update UI (editor model, tab styling) ----------
        function switchToTab(tabId) {
            const tab = tabs.find(t => t.id === tabId);
            if (!tab) return;
            activeTabId = tabId;
            editor.setModel(tab.model);
            // Update tab active class
            document.querySelectorAll('.tab').forEach(el => {
                if (el.dataset.id == tabId) el.classList.add('active');
                else el.classList.remove('active');
            });
        }

        function closeTab(tabId) {
            const index = tabs.findIndex(t => t.id === tabId);
            if (index === -1) return;
            const tab = tabs[index];
            // Dispose model to free resources
            tab.model.dispose();
            tabs.splice(index, 1);
            // Remove DOM element
            const tabEl = document.querySelector(`.tab[data-id='${tabId}']`);
            if (tabEl) tabEl.remove();

            if (tabs.length === 0) {
                // No tabs left, create a new default one
                createNewTab("Untitled.lua", "");
            } else {
                // Switch to the tab that was before/after
                const newActive = tabs[Math.min(index, tabs.length - 1)];
                switchToTab(newActive.id);
            }
        }

        function createNewTab(name, content) {
            const id = nextTabId++;
            // Create Monaco model with Lua language
            const model = monaco.editor.createModel(content || "", "lua");
            const tabObj = { id, model, title: name, dirty: false, content: content || "" };
            tabs.push(tabObj);
            // Create DOM element
            const tabsContainer = document.getElementById('tabs-container');
            const tabDiv = document.createElement('div');
            tabDiv.className = 'tab';
            if (tabs.length === 1) tabDiv.classList.add('active');
            tabDiv.setAttribute('data-id', id);
            tabDiv.innerHTML = `
                <span class="tab-title">${escapeHtml(name)}</span>
                <span class="tab-close" data-id="${id}">&times;</span>
            `;
            // Insert before the new-tab button
            const newBtn = document.getElementById('newTabBtn');
            tabsContainer.insertBefore(tabDiv, newBtn);
            // Switch to this tab
            switchToTab(id);
            // Attach close event
            const closeSpan = tabDiv.querySelector('.tab-close');
            closeSpan.addEventListener('click', (e) => {
                e.stopPropagation();
                closeTab(id);
            });
            // Click on tab to switch
            tabDiv.addEventListener('click', (e) => {
                if (e.target === closeSpan) return;
                switchToTab(id);
            });
            // Listen for content changes to update dirty flag (optional)
            model.onDidChangeContent(() => {
                tabObj.dirty = true;
                const titleSpan = tabDiv.querySelector('.tab-title');
                if (!tabObj.title.endsWith('*')) {
                    tabObj.title = tabObj.title + '*';
                    titleSpan.innerText = tabObj.title;
                }
            });
            return tabObj;
        }

        function escapeHtml(str) {
            return str.replace(/[&<>]/g, function(m) {
                if (m === '&') return '&amp;';
                if (m === '<') return '&lt;';
                if (m === '>') return '&gt;';
                return m;
            });
        }

        // ---------- Lua autocomplete provider ----------
        function registerLuaCompletions() {
            // Basic Lua keywords and common Roblox API
            const luaKeywords = [
                "and", "break", "do", "else", "elseif", "end", "false", "for", "function", "goto", "if", "in", "local", "nil", "not", "or", "repeat", "return", "then", "true", "until", "while"
            ];
            const robloxGlobals = [
                "game", "workspace", "script", "Players", "ReplicatedStorage", "ReplicatedFirst", "Lighting", "SoundService", "TweenService", "RunService", "UserInputService", "ContextActionService", "CollectionService", "Debris", "HttpService", "StringService", "TeleportService", "Chat", "MarketplaceService", "DataStoreService"
            ];
            const commonFunctions = [
                "print", "warn", "error", "type", "tostring", "tonumber", "pairs", "ipairs", "next", "select", "unpack", "table.insert", "table.remove", "table.sort", "string.sub", "string.gsub", "string.match", "string.find", "math.random", "math.floor", "math.ceil", "Vector3.new", "CFrame.new", "Instance.new", "wait", "spawn", "delay", "tick", "os.time"
            ];
            const suggestions = [
                ...luaKeywords.map(k => ({ label: k, kind: monaco.languages.CompletionItemKind.Keyword, insertText: k })),
                ...robloxGlobals.map(g => ({ label: g, kind: monaco.languages.CompletionItemKind.Variable, insertText: g })),
                ...commonFunctions.map(f => ({ label: f, kind: monaco.languages.CompletionItemKind.Function, insertText: f }))
            ];
            // Also add snippets for common patterns
            suggestions.push({
                label: "for i=1,10 do",
                kind: monaco.languages.CompletionItemKind.Snippet,
                insertText: "for i=1,10 do\n\t$0\nend",
                insertTextRules: monaco.languages.CompletionItemInsertTextRule.InsertAsSnippet
            });
            suggestions.push({
                label: "if then",
                kind: monaco.languages.CompletionItemKind.Snippet,
                insertText: "if $1 then\n\t$0\nend",
                insertTextRules: monaco.languages.CompletionItemInsertTextRule.InsertAsSnippet
            });
            suggestions.push({
                label: "function name()",
                kind: monaco.languages.CompletionItemKind.Snippet,
                insertText: "function ${1:name}($2)\n\t$0\nend",
                insertTextRules: monaco.languages.CompletionItemInsertTextRule.InsertAsSnippet
            });
            suggestions.push({
                label: "local function",
                kind: monaco.languages.CompletionItemKind.Snippet,
                insertText: "local function ${1:name}($2)\n\t$0\nend",
                insertTextRules: monaco.languages.CompletionItemInsertTextRule.InsertAsSnippet
            });
            // Register provider for Lua
            monaco.languages.registerCompletionItemProvider("lua", {
                provideCompletionItems: (model, position) => {
                    return { suggestions: suggestions };
                }
            });
        }

        // ---------- Initialize Monaco ----------
        require.config({ paths: { vs: 'https://cdn.jsdelivr.net/npm/monaco-editor@0.45.0/min/vs' } });
        require(['vs/editor/editor.main'], function () {
            // Set Lua as default language
            monaco.editor.defineTheme('dark-custom', {
                base: 'vs-dark',
                inherit: true,
                rules: [
                    { token: 'comment', foreground: '6A9955' },
                    { token: 'keyword', foreground: '569CD6' },
                    { token: 'string', foreground: 'CE9178' }
                ],
                colors: {
                    'editor.background': '#1E1E1E',
                    'editorLineNumber.foreground': '#858585'
                }
            });
            monaco.editor.setTheme('dark-custom');

            // Create editor
            editor = monaco.editor.create(document.getElementById('editor-container'), {
                value: "",
                language: "lua",
                theme: "dark-custom",
                fontSize: 12,
                minimap: { enabled: false },
                automaticLayout: true,
                scrollBeyondLastLine: false,
                renderWhitespace: "selection",
                suggestOnTriggerCharacters: true,
                quickSuggestions: true,
                wordBasedSuggestions: true
            });

            // Register Lua completions
            registerLuaCompletions();

            // Create initial tab
            createNewTab("Untitled.lua", "");

            // Expose functions for WPF WebView2 to call
            window.GetText = function() {
                const model = getCurrentModel();
                if (!model) return "";
                return model.getValue();
            };
            window.SetText = function(text) {
                const model = getCurrentModel();
                if (model) model.setValue(text);
            };
            // Optional: create new tab from C# if needed
            window.NewTab = function(name, content) {
                createNewTab(name, content);
            };
            window.GetAllTabs = function() {
                return tabs.map(t => ({ id: t.id, title: t.title, content: t.model.getValue() }));
            };
        });

        // New tab button
        document.getElementById('newTabBtn').addEventListener('click', () => {
            createNewTab("Untitled.lua", "");
        });
    </script>
</body>
</html># monaco
