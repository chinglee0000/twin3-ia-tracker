# Twin3 設計系統統一 - 設計文檔

## 概述

本設計文檔描述了 Twin3 應用設計系統的全面統一方案。該方案將建立一個基於 Material Design 3 原則的一致性設計語言，包含完整的色彩系統、國際化支持、圖標標準化、用語規範以及組件庫。設計目標是創建一個可維護、可擴展且用戶體驗一致的設計系統。

## 架構

### 設計系統架構層次

```
設計系統架構
├── 設計令牌層 (Design Tokens)
│   ├── 色彩變量 (Color Variables)
│   ├── 間距變量 (Spacing Variables)
│   ├── 字體變量 (Typography Variables)
│   └── 陰影變量 (Shadow Variables)
├── 組件層 (Component Layer)
│   ├── 基礎組件 (Base Components)
│   ├── 複合組件 (Composite Components)
│   └── 佈局組件 (Layout Components)
├── 國際化層 (i18n Layer)
│   ├── 語言檢測 (Language Detection)
│   ├── 翻譯管理 (Translation Management)
│   └── 語言切換 (Language Switching)
└── 主題層 (Theme Layer)
    ├── 色彩主題 (Color Themes)
    ├── 組件主題 (Component Themes)
    └── 響應式主題 (Responsive Themes)
```

### 技術架構

- **前端框架**: React 19.2.0 + TypeScript
- **樣式系統**: CSS Variables + CSS Modules
- **圖標庫**: Lucide React 0.562.0
- **國際化**: React i18next (待添加)
- **狀態管理**: React Context API
- **構建工具**: Vite 7.2.4

## 組件和接口

### 設計令牌管理器

```typescript
interface DesignTokens {
  colors: {
    primary: ColorPalette;
    secondary: ColorPalette;
    semantic: SemanticColors;
    neutral: NeutralColors;
  };
  spacing: SpacingScale;
  typography: TypographyScale;
  shadows: ShadowScale;
  borderRadius: BorderRadiusScale;
}

interface ColorPalette {
  50: string;
  100: string;
  200: string;
  300: string;
  400: string;
  500: string;
  600: string;
  700: string;
  800: string;
  900: string;
}

interface SemanticColors {
  success: string;
  warning: string;
  error: string;
  info: string;
}
```

### 國際化系統

```typescript
interface I18nConfig {
  defaultLanguage: 'en' | 'zh';
  supportedLanguages: Array<'en' | 'zh'>;
  fallbackLanguage: 'en';
  storageKey: 'twin3-language';
}

interface TranslationKeys {
  common: {
    buttons: {
      viewDetails: string;
      acceptTask: string;
      cancel: string;
      back: string;
    };
    status: {
      active: string;
      completed: string;
      pending: string;
    };
  };
  tasks: {
    reward: string;
    deadline: string;
    requirements: string;
  };
}
```

### 圖標系統

```typescript
interface IconConfig {
  library: 'lucide-react';
  sizes: {
    xs: 14;
    sm: 16;
    md: 18;
    lg: 20;
    xl: 24;
  };
  semanticMapping: {
    tokens: 'Coins';
    gifts: 'Gift';
    time: 'Clock';
    users: 'Users';
    success: 'CheckCircle';
    close: 'X';
    settings: 'Settings';
    menu: 'Menu';
    send: 'Send';
  };
}
```

### 主題提供者

```typescript
interface ThemeProvider {
  theme: DesignTokens;
  language: 'en' | 'zh';
  setLanguage: (lang: 'en' | 'zh') => void;
  t: (key: string) => string;
}
```

## 數據模型

### 設計令牌數據結構

```typescript
// 色彩系統
const colorTokens = {
  // 主色系 - 基於現有白色到灰色漸變
  primary: {
    50: '#ffffff',
    100: '#f8f9fa',
    200: '#e9ecef',
    300: '#dee2e6',
    400: '#ced4da',
    500: '#adb5bd',
    600: '#8e8e93',
    700: '#6c757d',
    800: '#495057',
    900: '#343a40'
  },
  
  // 語義色彩
  semantic: {
    success: '#30d158',
    warning: '#ff9f0a',
    error: '#ff3b30',
    info: '#007aff'
  },
  
  // 中性色彩
  neutral: {
    black: '#000000',
    white: '#ffffff',
    gray: {
      50: '#f9fafb',
      100: '#f3f4f6',
      200: '#e5e7eb',
      300: '#d1d5db',
      400: '#9ca3af',
      500: '#6b7280',
      600: '#4b5563',
      700: '#374151',
      800: '#1f2937',
      900: '#111827'
    }
  }
};

// 間距系統
const spacingTokens = {
  xs: '4px',
  sm: '8px',
  md: '16px',
  lg: '24px',
  xl: '32px',
  '2xl': '48px',
  '3xl': '64px',
  '4xl': '80px'
};

// 字體系統
const typographyTokens = {
  fontFamily: {
    sans: ['Inter', '-apple-system', 'BlinkMacSystemFont', 'sans-serif']
  },
  fontSize: {
    xs: '12px',
    sm: '14px',
    base: '16px',
    lg: '18px',
    xl: '20px',
    '2xl': '24px',
    '3xl': '30px',
    '4xl': '36px'
  },
  fontWeight: {
    normal: 400,
    medium: 500,
    semibold: 600
  }
};
```

### 翻譯數據結構

```typescript
const translations = {
  en: {
    common: {
      buttons: {
        viewDetails: 'View Details',
        acceptTask: 'Accept Task',
        cancel: 'Cancel',
        back: 'Back to Home',
        submit: 'Submit',
        verify: 'Verify Submission'
      },
      status: {
        active: 'Active',
        completed: 'Completed',
        pending: 'Pending',
        verified: 'Verified',
        open: 'Open',
        closed: 'Closed'
      },
      labels: {
        reward: 'Reward',
        deadline: 'Deadline',
        requirements: 'Requirements',
        spotsLeft: 'spots left',
        daysLeft: 'days left'
      }
    },
    tasks: {
      title: 'Task Opportunities',
      submissionVerified: 'Submission Verified!',
      rewardPending: 'Reward will be released within 24 hours',
      submitProof: 'Submit Proof',
      pasteUrl: 'Paste Instagram post URL...',
      verifying: 'Verifying...',
      aiVerification: 'AI will verify content requirements automatically'
    },
    navigation: {
      home: 'Home',
      tasks: 'Tasks',
      profile: 'Profile',
      settings: 'Settings'
    }
  },
  zh: {
    common: {
      buttons: {
        viewDetails: '查看詳情',
        acceptTask: '接受任務',
        cancel: '取消',
        back: '返回首頁',
        submit: '提交',
        verify: '驗證提交'
      },
      status: {
        active: '進行中',
        completed: '已完成',
        pending: '待處理',
        verified: '已驗證',
        open: '開放中',
        closed: '已關閉'
      },
      labels: {
        reward: '獎勵',
        deadline: '截止時間',
        requirements: '要求',
        spotsLeft: '個名額剩餘',
        daysLeft: '天剩餘'
      }
    },
    tasks: {
      title: '任務機會',
      submissionVerified: '提交已驗證！',
      rewardPending: '獎勵將在24小時內發放',
      submitProof: '提交證明',
      pasteUrl: '粘貼 Instagram 帖子鏈接...',
      verifying: '驗證中...',
      aiVerification: 'AI 將自動驗證內容要求'
    },
    navigation: {
      home: '首頁',
      tasks: '任務',
      profile: '個人資料',
      settings: '設置'
    }
  }
};
```

## 正確性屬性

*屬性是一個特徵或行為，應該在系統的所有有效執行中保持為真——本質上是關於系統應該做什麼的正式陳述。屬性作為人類可讀規範和機器可驗證正確性保證之間的橋樑。*

### 屬性反思

在分析所有可測試屬性後，我識別出以下可以合併或優化的冗餘屬性：

- 屬性 1.2 和 3.5 都涉及使用設計系統顏色變量，可以合併為一個更全面的屬性
- 屬性 5.1-5.5 都是關於樣式類別的完整性檢查，可以合併為一個綜合屬性
- 屬性 6.1-6.5 都是關於 Flowchart 組件的一致性，可以合併為更少的屬性

經過反思，以下是優化後的屬性列表：

**屬性 1：設計令牌完整性**
*對於任何*設計系統配置，所有必需的設計令牌類別（色彩、間距、字體、陰影、圓角）都應該被完整定義
**驗證：需求 1.1, 5.3, 5.4, 5.5**

**屬性 2：顏色變量一致性**
*對於任何*組件或圖標，所有顏色值都應該來自統一的 CSS 變量系統，不應包含硬編碼的顏色值
**驗證：需求 1.2, 3.5**

**屬性 3：可訪問性對比度合規**
*對於任何*色彩組合，文本與背景的對比度都應該符合 WCAG 2.1 AA 標準（至少 4.5:1）
**驗證：需求 1.4**

**屬性 4：CSS 變量全局更新**
*對於任何*CSS 變量的修改，所有使用該變量的組件都應該自動反映新的值
**驗證：需求 1.5**

**屬性 5：語言自動檢測**
*對於任何*瀏覽器語言設置，應用都應該選擇最匹配的支持語言作為初始語言
**驗證：需求 2.1**

**屬性 6：語言切換完整性**
*對於任何*語言切換操作，所有界面文本都應該立即更新為目標語言，且語言偏好應該保存到本地存儲
**驗證：需求 2.2, 2.3**

**屬性 7：語言偏好持久化**
*對於任何*應用重新加載，之前保存的語言設置都應該被正確恢復和應用
**驗證：需求 2.4**

**屬性 8：翻譯完整性**
*對於任何*使用的文本鍵，都應該在所有支持的語言中有對應的翻譯
**驗證：需求 2.5**

**屬性 9：圖標庫統一性**
*對於任何*圖標使用，都應該僅來自 Lucide React 圖標庫，不應包含 emoji 或其他圖標庫
**驗證：需求 3.1, 3.2**

**屬性 10：語義圖標一致性**
*對於任何*相同語義的功能，都應該使用相同的 Lucide 圖標
**驗證：需求 3.3**

**屬性 11：圖標尺寸標準化**
*對於任何*圖標，其尺寸都應該是預定義標準中的一個（14px, 16px, 18px, 20px, 24px）
**驗證：需求 3.4**

**屬性 12：按鈕文本標準化**
*對於任何*按鈕，其文本都應該使用標準化的動作詞彙表中的詞彙
**驗證：需求 4.1**

**屬性 13：狀態描述一致性**
*對於任何*相同的狀態，都應該使用一致的描述詞彙
**驗證：需求 4.2**

**屬性 14：代幣格式統一性**
*對於任何*代幣數量顯示，都應該使用 "$twin3" 格式
**驗證：需求 4.3**

**屬性 15：Flowchart 設計系統一致性**
*對於任何*Flowchart 組件元素（節點、連接線、文本），都應該使用設計系統中定義的顏色、字體和樣式
**驗證：需求 6.1, 6.2, 6.4**

**屬性 16：Flowchart 狀態語義化**
*對於任何*Flowchart 節點狀態，都應該使用語義化的狀態顏色
**驗證：需求 6.3**

**屬性 17：Flowchart 交互一致性**
*對於任何*Flowchart 交互效果，都應該與其他組件的懸停和選中效果保持一致
**驗證：需求 6.5**

## 錯誤處理

### 設計令牌錯誤處理

- **缺失令牌**: 當組件嘗試使用未定義的設計令牌時，系統應該回退到默認值並記錄警告
- **無效顏色值**: 當顏色值格式無效時，系統應該使用最接近的有效顏色
- **循環依賴**: 當設計令牌之間存在循環依賴時，系統應該檢測並報告錯誤

### 國際化錯誤處理

- **缺失翻譯**: 當翻譯鍵不存在時，顯示鍵名並記錄警告
- **語言檢測失敗**: 當無法檢測瀏覽器語言時，使用默認語言（英文）
- **本地存儲失敗**: 當無法保存語言偏好時，仍然允許臨時語言切換

### 圖標系統錯誤處理

- **圖標不存在**: 當請求的 Lucide 圖標不存在時，使用默認圖標（如 HelpCircle）
- **尺寸無效**: 當圖標尺寸不在標準範圍內時，使用最接近的標準尺寸

## 測試策略

### 雙重測試方法

本設計採用單元測試和基於屬性的測試相結合的方法：

**單元測試**將涵蓋：
- 特定的設計令牌值驗證
- 語言切換的具體場景
- 圖標映射的正確性
- 組件樣式的具體實現

**基於屬性的測試**將涵蓋：
- 設計系統的一致性屬性
- 國際化的完整性屬性
- 圖標系統的統一性屬性
- 可訪問性的合規性屬性

### 屬性測試庫

使用 **fast-check** 作為 TypeScript/JavaScript 的屬性測試庫。每個屬性測試將運行最少 100 次迭代以確保充分的隨機性覆蓋。

### 測試標記格式

每個基於屬性的測試都將使用以下格式進行標記：
`**Feature: design-system-unification, Property {number}: {property_text}**`

例如：
`**Feature: design-system-unification, Property 2: 顏色變量一致性**`

### 測試覆蓋範圍

- **設計令牌測試**: 驗證所有令牌的完整性和一致性
- **國際化測試**: 驗證語言切換和翻譯完整性
- **圖標系統測試**: 驗證圖標使用的統一性和標準化
- **可訪問性測試**: 驗證色彩對比度和其他可訪問性標準
- **組件一致性測試**: 驗證所有組件遵循設計系統標準