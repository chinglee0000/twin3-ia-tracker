# Twin3 IA Dev Tracker - 標籤用詞與顏色對應規範

## 概述

本文件定義了 Twin3 IA Dev Tracker 中所有標籤用詞的一致性規範，以及對應的 Badge 顏色系統和按鈕樣式。

---

## 按鈕樣式規範

### Primary Button (主要按鈕)

| 屬性 | 值 |
|------|-----|
| 背景 | 透明 (transparent) |
| 邊框 | 1px solid 白色 |
| 文字顏色 | 白色 |
| 預設透明度 | 80% |
| Hover 透明度 | 100% |
| 圓角 | 8px (--radius-sm) |

```css
.btn-primary {
    background: transparent;
    color: var(--color-white);
    border: 1px solid var(--color-white);
    opacity: 0.8;
}

.btn-primary:hover {
    opacity: 1;
}
```

### 按鈕文字規範

| 按鈕用途 | 文字 | 說明 |
|----------|------|------|
| 查看詳情 | 查看 | 導航到詳細頁面 |
| 關閉彈窗 | 關閉 | 關閉 Modal |
| 確認操作 | 確認 | 確認動作 |
| 取消操作 | 取消 | 取消動作 |

---

## Badge 顏色對應規則

| Badge Class | 顏色 | 用途 | 範例 |
|-------------|------|------|------|
| `badge-cyan` | 青色 (#00d4ff) | 分類標籤、類型標識 | Widget, Section, Category, ID |
| `badge-purple` | 紫色 (#a78bfa) | 待開發狀態、Hint Bubble | 待開發, Hint Bubble |
| `badge-green` | 綠色 (#10b981) | 互動元素、已完成狀態 | 互動, 已完成 |
| `badge-orange` | 橘色 (#f59e0b) | 即將推出 | Soon |
| `badge-gray` | 灰色 (#a1a1aa) | 展示/靜態內容、草稿 | 展示, 草稿, legacy |
| `badge-pink` | 粉色 (#ec4899) | 外部連結、社群 | 外部, 社群 |

---

## 標籤用詞規範

### 元件類型 (Category)

| 用詞 | Badge | 說明 |
|------|-------|------|
| `Widget Card` | badge-cyan | Widget 卡片元件 |
| `Widget` | badge-cyan | Widget 類型標籤 |
| `Hint Bubble` | badge-purple | 提示泡泡元件 |
| `AI 提醒` | badge-pink | AI 回應提醒 |

### 開發狀態 (Status)

| 用詞 | Badge | 說明 |
|------|-------|------|
| `待開發` | badge-purple | 尚未開始開發 |
| `已完成` | badge-green | 開發完成 |
| `草稿` | badge-gray | 草稿狀態 |
| `legacy` | badge-gray | 舊版/遺留 |
| `deprecated` | badge-gray | 已棄用 |
| `Soon` | badge-orange | 即將推出 |

### 互動類型 (Interaction Type)

| 用詞 | Badge | 說明 |
|------|-------|------|
| `互動` | badge-green | 可互動元素 |
| `展示` | badge-gray | 純展示內容 |
| `動態` | badge-purple | 動態內容 |
| `動畫` | badge-orange | 動畫效果 |
| `外部` | badge-pink | 外部連結 |

### 連結類型 (Link Type)

| 用詞 | Badge | 說明 |
|------|-------|------|
| `內部` | badge-cyan | 內部連結 |
| `外部` | badge-pink | 外部連結 |
| `社群` | badge-pink | 社群平台連結 |

---

## getStatusBadge 函數對應表

```javascript
const statusMap = {
    'todo': { class: 'badge-purple', label: '待開發' },
    'active': { class: 'badge-purple', label: '待開發' },
    'pending': { class: 'badge-purple', label: '待開發' },
    'done': { class: 'badge-green', label: '已完成' },
    'draft': { class: 'badge-gray', label: '草稿' },
    'legacy': { class: 'badge-gray', label: 'legacy' },
    'deprecated': { class: 'badge-gray', label: 'deprecated' },
    'System Event': { class: 'badge-cyan', label: 'System Event' }
};
```

---

## I18N 翻譯對照

### 中文 (zh-TW)

| Key | 值 |
|-----|-----|
| `table.widget` | Widget |
| `status.hint_bubble` | Hint Bubble |
| `stats.bubbles` | Hint Bubble |
| `common.buttons.view` | 查看 |
| `common.buttons.close` | 關閉 |

### 英文 (en)

| Key | 值 |
|-----|-----|
| `table.widget` | Widget |
| `status.hint_bubble` | Hint Bubble |
| `stats.bubbles` | Hint Bubble |
| `common.buttons.view` | View |
| `common.buttons.close` | Close |

---

## 使用範例

### 按鈕
```html
<!-- 主要按鈕 -->
<button class="btn btn-primary btn-sm">查看</button>

<!-- Modal 關閉按鈕 -->
<button class="flowchart-modal-close">
    <i data-lucide="x"></i>
    <span>關閉</span>
</button>
```

### 分類標籤
```html
<span class="badge badge-cyan">Widget Card</span>
<span class="badge badge-purple">Hint Bubble</span>
```

### 狀態標籤
```html
<span class="badge badge-purple">待開發</span>
<span class="badge badge-green">已完成</span>
<span class="badge badge-orange">Soon</span>
```

### 互動類型
```html
<span class="badge badge-green">互動</span>
<span class="badge badge-gray">展示</span>
<span class="badge badge-pink">外部</span>
```

---

## 更新記錄

- 2024-12-25: 初始版本
  - 統一 `提示泡泡` → `Hint Bubble`
  - 新增 `table.widget` 翻譯 key
  - 新增 `status.hint_bubble` 翻譯 key
  - 文件化所有 Badge 顏色對應規則
  - 新增按鈕樣式規範
  - 統一按鈕文字（ESC → 關閉）
  - 統一按鈕 hover 效果（透明度 80% → 100%）
