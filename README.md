<!DOCTYPE html>
<html lang="bn">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>সঠিক খবর লাইভ</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <!-- Header Section -->
  <header>
    <h1>সঠিক খবর লাইভ</h1>
    <marquee behavior="scroll" direction="left" class="headline">
      ব্রেকিং নিউজ: আজকের সবচেয়ে বড় খবর এখানেই পড়ুন!
    </marquee>
  </header>

  <!-- Navigation Section -->
  <nav>
    <ul>
      <li class="politics">রাজনীতি</li>
      <li class="sports">খেলাধুলা</li>
      <li class="entertainment">বিনোদন</li>
      <li class="tech">প্রযুক্তি</li>
      <li class="economy">অর্থনীতি</li>
    </ul>
  </nav>

  <!-- Main Content Section -->
  <main>
    <!-- News Posting Form -->
    <section class="news-section">
      <h2>নিউজ পোস্ট করুন</h2>
      <form id="newsForm" enctype="multipart/form-data">
        <input type="text" id="headline" placeholder="হেডলাইন লিখুন" required>
        <textarea id="description" placeholder="নিউজের বিস্তারিত লিখুন" required></textarea>
        <input type="file" id="image" accept="image/*" required>
        <button type="submit">পোস্ট করুন</button>
      </form>

      <!-- Display Posted News -->
      <div id="postedNews"></div>
    </section>

    <!-- Admin Panel Section -->
    <section id="adminPanel">
      <h2>Admin Panel</h2>
      <input type="password" id="adminPassword" placeholder="অ্যাডমিন পাসওয়ার্ড দিন">
      <button id="adminLoginBtn">লগ ইন করুন</button>
    </section>
  </main>

  <!-- Footer Section -->
  <footer>
    <p>&copy; ২০২৫ সঠিক খবর লাইভ</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
/* General Styling */
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #fff;
  color: #333;
}

/* Header Styling */
header {
  background-color: #ff3333; /* হেডলাইন এর আকর্ষণীয় রং */
  color: white;
  text-align: center;
  padding: 10px 0;
}

.headline {
  font-size: 20px;
  color: yellow;
  background-color: #000; /* চলমান হেডলাইন এর ব্যাকগ্রাউন্ড */
  padding: 5px 0;
}

/* Navigation Styling */
nav ul {
  display: flex;
  justify-content: space-around;
  padding: 10px;
  background-color: #333;
  list-style: none;
  margin: 0;
}

nav li {
  padding: 10px;
  color: white;
  cursor: pointer;
  border-radius: 5px;
}

/* Category Colors */
.politics   { background-color: #ff6347; }  /* উদাহরণস্বরূপ, রাজনীতির জন্য */
.sports     { background-color: #32cd32; }  /* খেলাধুলার জন্য */
.entertainment { background-color: #ff69b4; } /* বিনোদনের জন্য */
.tech       { background-color: #1e90ff; }  /* প্রযুক্তির জন্য */
.economy    { background-color: #ffd700; }  /* অর্থনীতির জন্য */

/* Main Content Styling */
main {
  padding: 20px;
  text-align: center;
}

.news-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

#newsForm {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

#newsForm input, #newsForm textarea {
  margin: 10px 0;
  padding: 10px;
  font-size: 16px;
  width: 100%;
  max-width: 600px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

#newsForm button {
  padding: 10px;
  background-color: #ff3333;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 18px;
  border-radius: 5px;
}

/* Posted News Styling */
#postedNews {
  width: 100%;
  max-width: 600px;
  margin-top: 20px;
}

#postedNews div {
  margin-bottom: 20px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

#postedNews img {
  max-width: 100%;
  height: auto;
}

/* Admin Panel Styling */
#adminPanel {
  margin-top: 20px;
  text-align: center;
}

#adminPanel input {
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

#adminPanel button {
  padding: 10px;
  background-color: #ff3333;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 18px;
  border-radius: 5px;
}

/* Footer Styling */
footer {
  text-align: center;
  padding: 10px 0;
  background-color: #333;
  color: white;
}

/* Responsive Design for Mobile */
@media screen and (max-width: 768px) {
  nav ul {
    flex-direction: column;
    align-items: center;
  }
  nav li {
    width: 100%;
    text-align: center;
    margin: 5px 0;
  }
  .news-section, #postedNews {
    width: 100%;
    padding: 0 10px;
  }
}// --- Admin Panel Logic ---
const adminPassword = "admin123"; // এই পাসওয়ার্ড দিয়ে অ্যাডমিন লগইন হবে

document.getElementById("adminLoginBtn").addEventListener("click", function() {
  const password = document.getElementById("adminPassword").value;
  if (password === adminPassword) {
    alert("লগ ইন সফল হয়েছে!");
    // অ্যাডমিন প্যানেলের UI পরিবর্তন করে ম্যানেজমেন্ট অপশন দেখানো
    document.getElementById("adminPanel").innerHTML = `
      <h3>Admin Panel</h3>
      <button id="deleteNewsBtn">সকল নিউজ মুছে ফেলুন</button>
    `;
    document.getElementById("deleteNewsBtn").addEventListener("click", deleteNews);
  } else {
    alert("পাসওয়ার্ড ভুল!");
  }
});

// --- নিউজ পোস্ট করার ফর্ম লজিক ---
document.getElementById("newsForm").addEventListener("submit", function(e) {
  e.preventDefault();

  const headline = document.getElementById("headline").value;
  const description = document.getElementById("description").value;
  const imageFile = document.getElementById("image").files[0];

  if (!headline || !description || !imageFile) {
    alert("সব তথ্য পূর্ণ করুন!");
    return;
  }

  // ছবি প্রদর্শনের জন্য URL তৈরি করা
  const imageURL = URL.createObjectURL(imageFile);

  // নিউজ আইটেম DOM এ যোগ করা
  const postedNewsDiv = document.getElementById("postedNews");
  const newsItem = document.createElement("div");
  newsItem.innerHTML = `
    <h3>${headline}</h3>
    <img src="${imageURL}" alt="নিউজ ছবি" style="width:100%; max-height:300px; object-fit:cover;">
    <p>${description}</p>
  `;
  postedNewsDiv.appendChild(newsItem);

  // ফর্ম রিসেট করা
  document.getElementById("newsForm").reset();
});

// --- নিউজ মুছে ফেলার ফাংশন (Admin) ---
function deleteNews() {
  if (confirm("সকল নিউজ মুছে ফেলার জন্য আপনি নিশ্চিত?")) {
    document.getElementById("postedNews").innerHTML = "";
  }
}
