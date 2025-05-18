<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" />

  <meta charset="UTF-8" />
  <title>Dashboard</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    * {
      box-sizing: border-box;
    }
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #d9d9d9;
      display: flex;
      height: 100vh;
      overflow-x: hidden;
    }
    
    h1 {
      margin: 0;
    }

    .user-icon {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      object-fit: cover;
    }

    
    /* Sidebar */
  
    .sidebar {
  height: 100vh;
  width: 250px;
  position: fixed;
  top: 0;
  left: 0;
  background-color: #ffffff;
  transition: width 0.3s ease;
  overflow-x: hidden;
  z-index: 1000;
  display: flex;
  flex-direction: column;
  z-index: 1002;
}

.sidebar.collapsed {
  width: 70px;
}

.sidebar a {
  height: 50px;
  padding: 12px 20px;
  text-decoration: none;
  font-size: 17px;
  color: #000000;
  display: flex;
  align-items: center;
  gap: 12px;
  white-space: nowrap;
  overflow: hidden;
  transition: 0.3s;
}


.sidebar.collapsed a {
  justify-content: center;
  gap: 0;
}

.sidebar.collapsed a span {
  display: none;
}



/* Logo & toggle button */
.logo-section {
  padding: 10px 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative; /* optional, for absolute positioning of logo inside */
}

.logo-img {
  width: 150px;
  max-height: 150px;
  object-fit: contain;
  transition: opacity 0.3s ease, width 0.3s ease;
}


/* Hide the logo when sidebar is collapsed */
.sidebar.collapsed .logo-img {
  /* Instead of width:0, use opacity and visibility for smooth transition */
  opacity: 0;
  visibility: hidden;
  width: 0px;
  height: 0px;
}

.sidebar .logo-section {
  height: 60px;
  padding: 40px 30px 70px 43px; /* Less top padding */
  display: flex;
  align-items: center;
  justify-content: space-between;
  
}

  .sidebar.collapsed .logo-section .text {
    display: none;
  }
  
  .toggle-btn {
    background: none;
    border: none;
    font-size: 17px;
    cursor: pointer;
    color: #444;
  }

  .sidebar .menubtn {
  position: fixed; /* ← Change from absolute to fixed */
  top: 10px;
  left: 230px;
  height: 40px;
  width: 40px;
  z-index: 9999; /* ← Way above topbar (z-index 1001) */
  color: #000000;
  background: #e9e9e9;
  text-align: center;
  line-height: 42px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 17px;
  transition: left 0.3s ease;
  box-shadow: 0 12px 16px 0 rgba(99, 99, 99, 0.24), 0 17px 50px 0 rgba(99, 99, 99, 0.24);
}


/* Move button when sidebar is collapsed */
.sidebar.collapsed .menubtn {
  left: 15px; /* matches col lapsed width */
}
  
/* Nav items */
.nav-links {
  padding: 10px 0;
  flex-grow: 1;
  transition: background-color 0.2s;
}

.nav-links a {
  display: flex;
  align-items: center;
  padding: 12px 20px;
  color: #5c5c5c;
  text-decoration: none;
  font-weight: 600;
  font-size: 17px;
  border-radius: 15px;
  cursor: pointer;
  margin: 5px 10px;
  transition: background-color 0.2s;
}

.nav-links a:hover,
.nav-links a.active {
  background: #060644;
  color: #eb972b;
  backdrop-filter: blur(4px);
  transform: scale(1.02);
}


.sidebar.collapsed .nav-links a {
  justify-content: flex;
  padding: 12px 20px;
}

.nav-links a i {
  font-size: 17px;
    min-width: 22px;
    text-align: center;
}

.sidebar.collapsed .nav-links a span {
  display: none;
} 



/* User & logout section */
.user-section {
    border-top: 1px solid #ddd;
    padding: 10px 0px;
    transition: background-color 0.2s;
  }
 
  .user-section a {
    display: flex;
    align-items: center;
    padding: 12px 20px;
    color: #5c5c5c;
    text-decoration: none;
    font-weight: 600;
    font-size: 17px;
    border-radius: 15px;
    cursor:pointer;
    margin: 5px 10px;
    transition: background-color 0.2s;
  }

  .user-section a i {
    font-size: 17px;
    min-width: 22px;
    text-align: center;
  }

  .user-section a:hover {
     background: #060644;
  color: #eb972b;
    backdrop-filter: blur(4px); /* frosted glass effect for futuristic look */
    transform: scale(1.02); /* slight enlargement for effect */
  }

  .sidebar.collapsed .user-section span {
    display: none;
  }
/* Top bar styling */

.topbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #060644;
  font-size: 12px;
  color: white;
  padding: 10px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-left: 90px; /* default space when sidebar is collapsed */
  transition: padding-left 0.3s ease;
  z-index: 1001;
  box-shadow: 0 12px 16px 0 rgba(44, 44, 44, 0.24), 0 17px 50px 0 rgba(44, 44, 44, 0.24);
}

.topbar.shifted {
      padding-left: 280px; /* space when sidebar is expanded */
    }


 /* Main content wrapper */

 #mainContent {
  transition: margin-left 0.3s ease, width 0.3s ease;
  margin-left: 80px;
  margin-right: 10px;
  width: calc(100% - 90px);
  padding: 20px;
}

#mainContent.shifted {
  margin-left: 260px;
  width: calc(100% - 270px);
}

.dashboard-grid {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

/* Left Column: stack vertically */
.left-column {
  display: flex;
  flex-direction: column;
  gap: 20px;
  flex: 1;
  min-width: 250px;
}

/* Right Column: graph expands */
.graph-box {
  flex: 2;
  min-width: 300px;
  height: 100%;
}

/* Chart container should expand */
.graph-box canvas {
  width: 100%;
  height: 300px;
}

.dashboard-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  margin-top: 90px; /* leave space for fixed top bar */
  transition: margin-left 0.3s ease; /* Smooth transition when shifting content */
}


.bodycontainer {
  display: flex;
  flex-wrap: wrap; /* Allows wrapping to new line if needed */
  gap: 20px;
  margin-top: 0px;
  transition: margin-left 0.3s ease;
}

    .data-box {
      background-color: #060644;
      border: 1px solid #ccc;
      border-radius: 17px;
      box-shadow: 0 0 10px #ddd;
      padding: 20px;
      flex-direction: column;
      justify-content: flex;
      min-height: 120px;
    }

    .deposit-box {
      background-color: #eb972b;
      background-image: linear-gradient(90deg,#ffde59, #ff914d);
      border: 1px solid #ccc;
      border-radius: 17px;
      box-shadow: 0 0 10px #ddd;
      padding: 20px;
      flex-direction: column;
      justify-content: flex;
      min-height: 120px;
    }

    .data-box-content {
      display: flex;
      justify-content: space-between;
      color: #eb972b;
      align-items: center;
      padding: 10px;
    }
     .label {
      text-align: left;
      font-size: 30px;
      font-weight: bold;
      color: #eb972b;
      line-height: 1.2;
      
    }
    .count {
      font-size: 70px;
      font-weight: bold;
      text-align: right;
    }
    
    .deposit-header {
      font-weight: bold;
      font-size: 18px;
      text-align: center;
      margin-bottom: 15px;
    }
    .deposit-row {
      display: flex;
      font-family: 'Tahoma', sans-serif;
      justify-content: space-between;
      margin-bottom: 10px;
    }
.graph-box,
.pie-box {
  margin-top: 20px;
  background-color: #fdfdfd;
  border: 1px solid #ccc;
  border-radius: 17px;
  box-shadow: 0 0 10px #ddd;
  padding: 20px;
  width: 700px;
  height: auto; /* Let it expand with content */
  box-sizing: border-box;
}

canvas {
  height: 200px !important; /* Adjust as needed to fit chart size */
}


    .graph-header,
    .pie-header {
      font-weight: bold;
      font-family: 'Poppins', sans-serif;
      font-size: 18px;
      text-align: center;
      margin-bottom: 15px;
      
    }
    .shipment-controls {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 40px;
      margin-bottom: 10px;
      border-radius: 10px;
    }
    .shipment-controls .left-title {
      font-weight: bold;
      font-size: 25px;
      margin-bottom: 10px;
    }

    .shipment-controls .right-filter {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .right-filter {
      display: flex;
      align-items: center;
      margin-bottom: 5px;
      margin-top: 2px;
      margin-left: auto;
    }
    .right-filter label {
      font-size: 0.8em;
      margin-right: 8px;
    }
    .right-filter select {
      padding: 6px 10px;
      font-size: 0.8em;
      border-radius: 30px;
      background-color: #f8f9f0;
      border: 1px solid #ccc;
    }

    select {
      padding: 5px 10px;
      font-size: 16px;
    }
    .shipment-list-box {
      background-color: #fff;
      border: 1px solid #ccc;
      border-radius: 17px;
      box-shadow: 0 0 10px #ddd;
      padding: 20px;
      margin-top: 10px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
    }
    th,
    td {
      border: 1px solid #ddd;
      padding: 10px;
      font-size: 14px;
    }
    th {
      background-color: #f4f4f4;
    }
  </style>
</head>
<body>

 <!-- Sidebar -->
 <div id="mySidebar" class="sidebar collapsed">
  
  <div class="logo-section">
    <!-- Placeholder logo -->
    <img src="logoangelo.png" alt="Logo" class="logo-img" />
  
    <!-- Menu toggle button -->
    <div id="toggleSidebarBtn" class="menubtn">
      <i class="fas fa-bars"></i>
    </div>
  </div>

  <nav class="nav-links">
    <a href="Dashboard.html"  class="active"><i class="fas fa-home"></i><span>Dashboard</span></a>
    <a href="Shipment.html"><i class="fas fa-truck"></i><span>Shipments</span></a>
    <a href="Records.html"><i class="fas fa-clipboard-list"></i><span>Records</span></a>
    <a href="Analytics(Yearly).html"><i class="fas fa-chart-bar"></i><span>Analytics</span></a>
  </nav>


<div class="user-section">
   <a href="account.html"><i class="fas fa-user"></i> <span>My Account</span></a>
   <a href="#"><i class="fas fa-sign-out-alt"></i> <span>Logout</span></a>
</div>
</div>


<!-- Top Bar -->
<div class="topbar" id="topbar">
  <h1>DASHBOARD</h1>
  <img src="Sophie.jpg" alt="User" class="user-icon" />
</div>

  <!-- Main Content -->
  <div class="content" id="mainContent">
    <div class="dashboard-container">
      <div class="data-box">
        <div class="data-box-content">
          <div class="label">Count of<br />Shipments</div>
          <div class="count" id="shipmentCount">...</div>
        </div>
      </div>
      <div class="data-box">
        <div class="data-box-content">
          <div class="label">No. of<br />Containers</div>
          <div class="count" id="containerCount">...</div>
        </div>
      </div>
      <div class="deposit-box">
        <div class="deposit-header">CONTAINER DEPOSIT</div>
        <div class="deposit-row">
          <div class="deposit-label">CD</div>
          <div class="deposit-value" id="cd">...</div>
        </div>
        <div class="deposit-row">
          <div class="deposit-label">CD COLLECTED</div>
          <div class="deposit-value" id="cdCollected">...</div>
        </div>
        <div class="deposit-row">
          <div class="deposit-label">NO CD</div>
          <div class="deposit-value" id="noCd">...</div>
        </div>
      </div>
    </div>

    <div class="bodycontainer">
      <div class="graph-box"> 
        <div class="graph-header">Monthly Shipments Trend</div>
        <canvas id="shipmentTrendChart"></canvas>
      </div>
      <div class="pie-box">
        <div class="pie-header">2025 IMPORTATIONS (as of present)</div>
        <canvas id="importerPieChart"></canvas>
      </div>
    </div>
 
  

    <div class="shipment-controls">
      <div class="left-title">Shipment List</div>
      <div class="right-filter">
        <span>Show</span>
        <select id="yearSelector">
          <option value="2025">2025</option>
          <option value="2024">2024</option>
          <option value="2023">2023</option>
        </select>
      </div>
    </div>

    <div class="shipment-list-box">
      <table id="shipmentListTable">
        <thead>
          <tr>
            <th>#</th>
            <th>ENCODING DOCU PHASE</th>
            <th>FOR SHIPPING LINE/ DELIVERY PHASE</th>
            <th>IMPORTER</th>
            <th>COMMODITY</th>
            <th>NO. OF CONTAINERS</th>
            <th>CD</th>
            <th>SHIPPING LINE</th>
            <th>ETA</th>
            <th>15 DAYS</th>
          </tr>
        </thead>
        <tbody>
          <!-- Data goes here -->
        </tbody>
      </table>
    </div>
  </div>

  <script>
    const sidebar = document.getElementById("mySidebar");
    const content = document.getElementById("mainContent");
    const topbar = document.getElementById("topbar");
    const toggleBtn = document.getElementById("toggleSidebarBtn"); // One button for toggle
  
    // On page load, apply sidebar state from localStorage
    document.addEventListener('DOMContentLoaded', () => {
      const savedState = localStorage.getItem('sidebarState');
      const isCollapsed = savedState === 'collapsed';
      
      if (isCollapsed) {
        sidebar.classList.add("collapsed");
        content.classList.remove("shifted");
        topbar.classList.remove("shifted");
        
      } else {
        sidebar.classList.remove("collapsed");
        content.classList.add("shifted");
        topbar.classList.add("shifted");
        
      }
    });
  
    toggleBtn.addEventListener("click", () => {
  sidebar.classList.toggle("collapsed");
  const isCollapsed = sidebar.classList.contains("collapsed");

  // Save the state
  localStorage.setItem('sidebarState', isCollapsed ? 'collapsed' : 'expanded');

  // Toggle layout shift class
  topbar.classList.toggle("shifted", !isCollapsed);
  content.classList.toggle("shifted", !isCollapsed);
});


    // Fetch utility function
    function safeFetch(url, onSuccess, onError) {
      fetch(url)
        .then((response) => {
          if (!response.ok) throw new Error(`Fetch failed: ${response.status}`);
          return response.json();
        })
        .then(onSuccess)
        .catch((err) => {
          console.error(`Error fetching ${url}:`, err);
          if (onError) onError(err);
        });
    }

    // Fetch Summary Data
    safeFetch(
      "http://localhost/Angelogistics/api/get-shipment-count.php",
      (data) => {
        document.getElementById("shipmentCount").textContent = data.count;
      },
      () => {
        document.getElementById("shipmentCount").textContent = "Error";
      }
    );

    safeFetch(
      "http://localhost/Angelogistics/api/get-container-count.php",
      (data) => {
        document.getElementById("containerCount").textContent = data.count;
      },
      () => {
        document.getElementById("containerCount").textContent = "Error";
      }
    );

    safeFetch(
      "http://localhost/Angelogistics/api/get-container-deposit.php",
      (data) => {
        document.getElementById("cd").textContent = data.cd;
        document.getElementById("cdCollected").textContent = data.cdCollected;
        document.getElementById("noCd").textContent = data.noCd;
      },
      () => {
        document.getElementById("cd").textContent = "Error";
        document.getElementById("cdCollected").textContent = "Error";
        document.getElementById("noCd").textContent = "Error";
      }
    );

    // Chart: Monthly Shipments
    safeFetch("http://localhost/Angelogistics/api/get-monthly-shipment.php", (data) => {
      new Chart(document.getElementById("shipmentTrendChart").getContext("2d"), {
        type: "line",
        data: {
          labels: data.months,
          datasets: [
            {
              label: "Shipments per Month",
              data: data.counts,
              borderColor: "#2d8bba",
              backgroundColor: "#2d8bba",
              tension: 0.3,
              fill: true,
            },
          ],
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
        },
      });
    });

    // Chart: Importer Distribution Pie
    safeFetch("http://localhost/Angelogistics/api/get-importer-distribution.php", (data) => {
      new Chart(document.getElementById("importerPieChart").getContext("2d"), {
        type: "pie",
        data: {
          labels: data.importers,
          datasets: [
            {
              data: data.percentages,
              backgroundColor: [
                "#f8bc08",
                "#0f2d5d",
                "#eb972b",
                "#41b8d5",
                "#2d8bba",
              ],
              borderColor: "#fff",
              borderWidth: 1,
            },
          ],
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
        },
      });
    });

    // Shipment Table Fetcher
    function fetchShipments(year) {
      safeFetch(`http://localhost/Angelogistics/api/get-shipment.php?year=${year}`, (data) => {
        const tbody = document.querySelector("#shipmentListTable tbody");
        tbody.innerHTML = "";
        data.forEach((item, index) => {
          const row = `
            <tr>
              <td>${index + 1}</td>
              <td>${item.encoding_phase}</td>
              <td>${item.delivery_phase}</td>
              <td>${item.importer}</td>
              <td>${item.commodity}</td>
              <td>${item.number_of_containers}</td>
              <td>${item.deposit_status}</td>
              <td>${item.shipping_line}</td>
              <td>${item.eta}</td>
              <td>${item.due_date}</td>
            </tr>
          `;
          tbody.innerHTML += row;
        });
      }, () => {
        const tbody = document.querySelector("#shipmentListTable tbody");
        tbody.innerHTML =
          '<tr><td colspan="10">Failed to load shipment data</td></tr>';
      });
    }

    // Year dropdown listener
    document
      .getElementById("yearSelector")
      .addEventListener("change", function () {
        fetchShipments(this.value);
      });

    // Load initial shipment list (2025)
    fetchShipments(2025);
  </script>
</body>
</html>
