// Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyD1_f5mkPPdPF0bZcJQT69gWX8KdAHR4c8",
  authDomain: "cardboard-mania.firebaseapp.com",
  projectId: "cardboard-mania",
  storageBucket: "cardboard-mania.firebasestorage.app",
  messagingSenderId: "940513136308",
  appId: "1:940513136308:web:51ea71edd7a13d8f9ad1e1",
  measurementId: "G-SQP6ZRYM3W"
};

// Initialize Firebase
firebase.initializeApp(firebaseConfig);

// Initialize services
const auth = firebase.auth();
const db = firebase.firestore();
const storage = firebase.storage();

let currentUser = null;
let currentFolder = null;
let allCards = [];

const loginPage = document.getElementById('loginPage');
const dashboardPage = document.getElementById('dashboardPage');
const cardsPage = document.getElementById('cardsPage');

auth.onAuthStateChanged(user => {
  if (user) {
    currentUser = user;
    showDashboard();
    loadFolders();
  } else {
    currentUser = null;
    currentFolder = null;
    allCards = [];
    showLogin();
  }
});

function showLogin() {
  loginPage.classList.remove('hidden');
  dashboardPage.classList.add('hidden');
  cardsPage.classList.add('hidden');
}

function showDashboard() {
  loginPage.classList.add('hidden');
  dashboardPage.classList.remove('hidden');
  cardsPage.classList.add('hidden');
  clearFolderInputs();
}

function showCards(folderName) {
  loginPage.classList.add('hidden');
  dashboardPage.classList.add('hidden');
  cardsPage.classList.remove('hidden');
  currentFolder = folderName;
  document.getElementById('folderTitle').textContent = folderName;
  clearCardInputs();
  loadCards(folderName);
}

function login() {
  const email = document.getElementById("email").value.trim();
  const password = document.getElementById("password").value;
  if (!email.includes("@")) return alert("Invalid email format.");
  auth.signInWithEmailAndPassword(email, password).catch(err => alert(err.message));
}

function signup() {
  const email = document.getElementById("email").value.trim();
  const password = document.getElementById("password").value;
  if (!email.includes("@")) return alert("Invalid email format.");
  if (password.length < 6) return alert("Password must be at least 6 characters.");
  auth.createUserWithEmailAndPassword(email, password).catch(err => alert(err.message));
}

function logout() {
  auth.signOut();
}

function loadFolders() {
  if (!currentUser) return;
  db.collection("users").doc(currentUser.uid).collection("folders").orderBy("createdAt", "desc")
    .onSnapshot(snapshot => {
      const foldersList = document.getElementById("foldersList");
      foldersList.innerHTML = "";
      snapshot.forEach(doc => {
        const folder = doc.data().name;
        const div = document.createElement("div");
        div.textContent = folder;
        div.style.cursor = "pointer";
        div.style.padding = "8px";
        div.style.borderBottom = "1px solid #444";
        div.onclick = () => showCards(folder);
        foldersList.appendChild(div);
      });
    });
}

function addFolder() {
  const folderName = document.getElementById("newFolderName").value.trim();
  if (!folderName) return alert("Folder name cannot be empty.");
  db.collection("users").doc(currentUser.uid).collection("folders")
    .add({ name: folderName, createdAt: firebase.firestore.FieldValue.serverTimestamp() })
    .then(() => {
      document.getElementById("newFolderName").value = "";
    })
    .catch(err => alert(err.message));
}

function clearFolderInputs() {
  document.getElementById("newFolderName").value = "";
}

function addCard() {
  if (!currentUser) return alert("Please log in.");
  if (!currentFolder) return alert("Please select a folder.");

  const data = {
    folder: currentFolder,
    cardName: document.getElementById("cardName").value.trim(),
    cardType: document.getElementById("cardType").value.trim(),
    condition: document.getElementById("condition").value.trim(),
    purchasePrice: parseFloat(document.getElementById("purchasePrice").value),
    ebaySearch: document.getElementById("ebaySearch").value.trim(),
    createdAt: firebase.firestore.FieldValue.serverTimestamp()
  };

  const file = document.getElementById("cardImage").files[0];
  if (file) {
    const ref = storage.ref("cards/" + currentUser.uid + "/" + file.name);
    ref.put(file)
      .then(snap => snap.ref.getDownloadURL())
      .then(url => {
        data.imageUrl = url;
        db.collection("users").doc(currentUser.uid).collection("cards").add(data);
      });
  } else {
    db.collection("users").doc(currentUser.uid).collection("cards").add(data);
  }
  clearCardInputs();
}

function clearCardInputs() {
  document.getElementById("cardName").value = "";
  document.getElementById("cardType").value = "";
  document.getElementById("condition").value = "";
  document.getElementById("purchasePrice").value = "";
  document.getElementById("ebaySearch").value = "";
  document.getElementById("cardImage").value = "";
  document.getElementById("preview").style.display = "none";
  document.getElementById("searchFilter").value = "";
}

function loadCards(folderName) {
  if (!currentUser) return;
  db.collection("users").doc(currentUser.uid).collection("cards")
    .where("folder", "==", folderName)
    .orderBy("createdAt", "desc")
    .onSnapshot(snapshot => {
      allCards = [];
      snapshot.forEach(doc => {
        let card = doc.data();
        card.id = doc.id;
        allCards.push(card);
      });
      renderCards(allCards);
    });
}

function renderCards(cards) {
  const list = document.getElementById("cardList");
  list.innerHTML = "";
  cards.forEach(d => {
    const priceInfo = `
      <p>eBay price: <span id="ebay-price-${d.id}">Loading...</span></p>
      <p>Goldin price: <span id="goldin-price-${d.id}">Loading...</span></p>`;

    list.innerHTML += `
      <div class="card">
        <button class="delete-btn" onclick="deleteCard('${d.id}')">Delete</button>
        <h3>${d.cardName}</h3>
        <p>${d.cardType} - $${d.purchasePrice}</p>
        <p>Condition: ${d.condition}</p>
        <p>Folder: ${d.folder}</p>
        <a href='https://www.ebay.com/sch/i.html?_nkw=${encodeURIComponent(d.ebaySearch)}' target='_blank'>eBay Search</a>
        ${d.imageUrl ? `<img src='${d.imageUrl}' class='preview'>` : ""}
        ${priceInfo}
      </div>
    `;
    fetchEbayPrice(d.ebaySearch, d.id);
    fetchGoldinPrice(d.ebaySearch, d.id);
  });
}

function deleteCard(cardId) {
  if (!currentUser) return alert("Please log in.");
  db.collection("users").doc(currentUser.uid).collection("cards").doc(cardId).delete()
    .catch(err => alert(err.message));
}

function fetchEbayPrice(searchTerm, cardId) {
  // Placeholder - simulate price fetching
  setTimeout(() => {
    document.getElementById(`ebay-price-${cardId}`).innerText = `$${(Math.random() * 100).toFixed(2)}`;
  }, 1000);
}

function fetchGoldinPrice(searchTerm, cardId) {
  // Placeholder - simulate price fetching
  setTimeout(() => {
    document.getElementById(`goldin-price-${cardId}`).innerText = `$${(Math.random() * 150).toFixed(2)}`;
  }, 1200);
}

function filterCards() {
  const filterText = document.getElementById("searchFilter").value.toLowerCase();
  const filtered = allCards.filter(card =>
    card.cardName.toLowerCase().includes(filterText) ||
    card.folder.toLowerCase().includes(filterText) ||
    card.cardType.toLowerCase().includes(filterText)
  );
  renderCards(filtered);
}

function scanCard() {
  const file = document.getElementById("cardImage").files[0];
  if (!file) return alert("Upload an image first.");

  const reader = new FileReader();
  reader.onload = function (e) {
    document.getElementById("preview").src = e.target.result;
    document.getElementById("preview").style.display = "block";

    Tesseract.recognize(e.target.result, 'eng').then(({ data: { text } }) => {
      const lines = text.split("\n").filter(Boolean);
      if (lines.length > 0) {
        document.getElementById("cardName").value = lines[0];
        document.getElementById("ebaySearch").value = lines[0];
      }
    });
  };
  reader.readAsDataURL(file);
}
