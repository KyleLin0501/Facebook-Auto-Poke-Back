# Facebook-Auto-Poke-Back
# Facebook 自動戳回去腳本（Auto Poke Back）

這是一個使用 JavaScript 撰寫的小工具，可自動執行 Facebook 上的「戳回去」動作，適用於桌面版瀏覽器。當網頁中出現「戳回去」的按鈕時，腳本會自動點擊，並在完成後重新載入頁面，以便載入更多的戳回去對象。

## 🔧 功能特色

- ✅ 每次隨機間隔戳回（模擬真人操作）
- ✅ 最多戳回 10 次後自動重新載入頁面
- ✅ 支援自動捲動頁面以載入更多「戳回去」按鈕

---

## 📜 使用方式

1. 打開瀏覽器並登入 Facebook
2. 前往「戳一下」的頁面（例如：https://www.facebook.com/pokes）
3. 打開開發者工具（F12 或右鍵 → 檢查 → Console）
4. 將下方程式碼貼上並按下 Enter 鍵執行：

```javascript
function getRandom(n, m) {
    return Math.floor(Math.random() * (m - n + 1) + n);
}

function autoPoke() {
    const maxTimes = 10;
    const random_number = getRandom(3000, 5000); // 每次間隔

    for (let i = 0; i < maxTimes; i++) {
        (function (i) {
            setTimeout(function () {
                try {
                    const button = document.querySelector('[aria-label="戳回去"]');
                    if (button) {
                        button.click();
                        console.log(`戳回去：第 ${i + 1} 次`);
                    } else {
                        window.scrollTo(0, document.body.scrollHeight);
                    }
                } catch (e) {
                    console.error('錯誤：', e);
                }

                // 如果是最後一次，就 reload
                if (i === maxTimes - 1) {
                    setTimeout(() => location.reload(), 2000);
                }
            }, random_number * i);
        })(i);
    }
}

autoPoke();



