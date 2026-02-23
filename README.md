# Antigravity Code Auto-Approve "Run" Button (Console Script)

This script automatically clicks the **Run** button inside Antigravity Code when it appears.

⚠️ Works only if the button exists in the accessible DOM (Electron renderer context).

---

## How To Use

1. Open Antigravity Code  
2. Go to: **Help → Toggle Developer Tools**
3. Open the **Console** tab
4. Paste the script below
5. Press Enter

---

## Basic Version

```javascript
(function autoApproveRun() {
    console.log("🔍 Watching for Run button...");

    const clickRun = () => {
        const buttons = Array.from(document.querySelectorAll("button"));

        for (const btn of buttons) {
            const text = btn.innerText?.trim();
            if (text === "Run" || text.startsWith("Run")) {
                console.log("✅ Auto-clicking Run");
                btn.click();
                return true;
            }
        }
        return false;
    };

    // Try immediately
    clickRun();

    // Watch for new elements
    const observer = new MutationObserver(() => {
        clickRun();
    });

    observer.observe(document.body, {
        childList: true,
        subtree: true
    });

    console.log("🚀 Auto-approve script active");
})();
