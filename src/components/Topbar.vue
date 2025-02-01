<template>
    <div class="topbar">
      <p class="topbar-text">Next day delivery to home or free to store.*</p>
      <div class="topbar-links">
        <a href="#" class="topbar-link">Store Location</a>
        <a href="#" class="topbar-link">Help</a>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "Topbar",
  };
  </script>
  
  <style scoped>
  .topbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #f8f9fa; /* Light background */
    padding: 8px 15px;
    font-size: 13px;
    font-family: "Poppins", sans-serif;
    color: #333;
    height: auto;
    min-height: 35px;
    flex-wrap: wrap;
  }
  
  .topbar-text {
    flex: 1;
    text-align: center;
    font-weight: bold;
    font-size: 13px;
  }
  
  .topbar-links {
    display: flex;
    gap: 15px;
  }
  
  .topbar-link {
    text-decoration: none;
    color: #000000;
    font-weight: 500;
    transition: color 0.3s ease;
  }
  
  .topbar-link:hover {
    color: #0056b3;
  }
  
  /* Mobile Responsive */
  @media (max-width: 768px) {
    .topbar {
      flex-direction: column;
      text-align: center;
      gap: 5px;
      padding: 10px;
    }
  
    .topbar-text {
      font-size: 12px;
    }
  
    .topbar-links {
      gap: 10px;
      flex-direction: row;
      justify-content: center;
    }
  
    .topbar-link {
      font-size: 12px;
    }
  }
  </style>
  