# 1.2.3

### Features
- Added a toolbox explorer pane:  
    A brand-new side panel that lets you browse your ArcGIS toolboxes directly inside VS Code — no need to open ArcGIS Pro just to inspect your tools.
    - Supports both toolbox formats:
        - Python Toolboxes (.pyt) — fully parsed from source code
        - ArcGIS Toolboxes (.atbx) — read directly from the binary ZIP structure
    - View all toolboxes in your workspace at a glance
    - Expand toolboxes to see toolsets and individual tools
    - See tool counts, parameter counts, and error indicators at a glance
    - Go to Tool Definition — jump directly to a tool's class in your .pyt file
    - Open embedded scripts from .atbx toolboxes in a temporary editor
    - Hover tooltips show tool descriptions, categories, and metadata
    - Auto-refreshes when toolbox files change
    - Create New Python Toolbox from the toolbar
- Added customizable code snippets:  
    Instantly insert battle-tested ArcPy code patterns without leaving your editor.
    - Ctrl+Alt+S — open the snippet picker from anywhere in a Python file
    - Covers common patterns including:
        - Feature class and table operations
        - Spatial reference and geometry helpers
        - Cursor patterns (Search, Insert, Update)
    - Save your own snippets — select any code block and save it as a custom snippet via Save Selection as Custom Snippet

### Other
- ArcGIS Pro Debugger status bar item is now always accessible
- ArcGIS Pro taskbar item tooltip only displays when hovering
- Reduced toast notifications