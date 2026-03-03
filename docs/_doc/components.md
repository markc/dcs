# Components

All components are defined in `base.css` under `@layer components`. They use CSS variables for colors, so they automatically adapt to any scheme.

## Cards

```html
<div class="card">Basic card</div>
<div class="card card-hover">Lifts on hover</div>
<div class="card card-sm">Max 400px</div>
```

- **Mobile:** No border-radius, no side borders (edge-to-edge)
- **Desktop (768px+):** Rounded corners, full borders, shadow

## Buttons

```html
<button class="btn">Primary</button>
<button class="btn btn-outline">Outline</button>
<button class="btn btn-ghost">Ghost</button>
<button class="btn btn-success">Success</button>
<button class="btn btn-danger">Danger</button>
<button class="btn btn-sm">Small</button>
<button class="btn btn-lg">Large</button>
```

## Forms

```html
<div class="form-group">
    <label>Email</label>
    <input type="email" placeholder="you@example.com">
</div>
<div class="form-row">
    <div class="form-group"><input placeholder="First"></div>
    <div class="form-group"><input placeholder="Last"></div>
</div>
```

## Sidebar Navigation

```html
<nav>
    <a href="#" class="active"><i data-lucide="home"></i> Home</a>
    <a href="#"><i data-lucide="settings"></i> Settings</a>
    <div class="sidebar-divider"></div>
    <a href="#"><i data-lucide="log-out"></i> Logout</a>
</nav>
```

### Collapsible Groups

```html
<div class="sidebar-group">
    <div class="sidebar-group-title">
        <i data-lucide="folder"></i> Section
    </div>
    <nav><div>
        <a href="#">Item 1</a>
        <a href="#">Item 2</a>
    </div></nav>
</div>
```

Add class `collapsed` to start closed.

## Toast Notifications

```javascript
Base.toast('Saved!', 'success');
Base.toast('Error occurred', 'danger');
Base.toast('Check this', 'warning', 5000);
```

## Prose

Wrap markdown-rendered HTML in `.prose` for proper typography:

```html
<div class="prose">
    <h1>Title</h1>
    <p>Paragraph with <code>inline code</code>.</p>
    <pre><code>code block</code></pre>
</div>
```

Prose styles headings, lists, blockquotes, tables, code blocks, images, and badges.

## Tree Widget

Hierarchical navigation for file browsers, doc TOCs, and settings trees:

```html
<div class="tree">
    <div class="tree-branch">
        <div class="tree-toggle" style="--tree-depth:0">
            <i data-lucide="chevron-down" class="tree-chevron"></i>
            <i data-lucide="folder-open"></i>
            <span>Folder Name</span>
        </div>
        <div class="tree-children">
            <a class="tree-item" style="--tree-depth:1" href="#">
                <i data-lucide="file-text"></i>
                <span>file.md</span>
            </a>
        </div>
    </div>
</div>
```

- Folders use `.tree-branch` with `.tree-toggle` (clickable)
- Files use `.tree-item` (links or spans)
- Depth indentation via `--tree-depth` CSS variable
- Collapse animation uses `grid-template-rows` (same pattern as sidebar groups)
- State persists to localStorage

## Dropdowns

```html
<div class="dropdown">
    <button class="dropdown-toggle">Menu</button>
    <div class="dropdown-menu">
        <a href="#">Option 1</a>
        <a href="#">Option 2</a>
        <div class="dropdown-divider"></div>
        <a href="#">Option 3</a>
    </div>
</div>
```

## Tags

```html
<span class="tag">Default</span>
<span class="tag tag-danger">Alert</span>
```
