const SHRINKEARN_API = "a3ffe55f311b027be63ee9e28d188bc112cc255f";

function randomKey() {
    const chars = "abcdefghijklmnopqrstuvwxyz0123456789";
    let key = "free";
    for (let i = 0; i < 6; i++) {
        key += chars[Math.floor(Math.random() * chars.length)];
    }
    return key;
}

function saveKey(key, hours) {
    let keys = JSON.parse(localStorage.getItem("keys") || "[]");
    keys.push({
        key: key,
        expires: Date.now() + hours * 3600000
    });
    localStorage.setItem("keys", JSON.stringify(keys));
}

function getKeyLink() {
    const key = randomKey();
    saveKey(key, 24);

    const targetUrl = encodeURIComponent(
        window.location.origin + window.location.pathname + "?step=2&key=" + key
    );

    fetch(`https://shrinkearn.com/api?api=${SHRINKEARN_API}&url=${targetUrl}`)
        .then(res => res.json())
        .then(data => {
            window.location.href = data.shortenedUrl;
        });
}

function showStep2(key) {
    document.getElementById("step1").classList.add("hidden");
    document.getElementById("step2").classList.remove("hidden");
    document.getElementById("keyText").innerText = key;
}

function openAdmin() {
    document.getElementById("adminPanel").classList.toggle("hidden");
}

function adminLogin() {
    const user = document.getElementById("adminUser").value;
    if (user === "crusty") {
        document.getElementById("adminArea").classList.remove("hidden");
        updateKeyCount();
    } else {
        alert("Wrong admin user");
    }
}

function updateKeyCount() {
    let keys = JSON.parse(localStorage.getItem("keys") || "[]");
    document.getElementById("keyCount").innerText = keys.length;
}

function createCustomKey() {
    const key = document.getElementById("customKey").value;
    const hours = parseInt(document.getElementById("customHours").value);
    if (!key || !hours) return alert("Fill all fields");
    saveKey(key, hours);
    updateKeyCount();
    alert("Custom key created");
}

// STEP CHECK
const params = new URLSearchParams(window.location.search);
if (params.get("step") === "2") {
    showStep2(params.get("key"));
}
