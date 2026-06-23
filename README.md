 <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Library Management System</title>

  <style>
    * {
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      margin: 0;
      background: #f4f6f8;
    }

    header {
      background: #263238;
      color: white;
      text-align: center;
      padding: 20px;
    }

    header h1 {
      margin: 0;
    }

    .banner {
      width: 100%;
      height: 220px;
      object-fit: cover;
      display: block;
    }

    .container {
      width: 90%;
      max-width: 1100px;
      margin: 25px auto;
    }

    .form-box {
      background: white;
      padding: 25px;
      margin-bottom: 25px;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.15);
    }

    h2 {
      color: #263238;
      border-bottom: 2px solid #263238;
      padding-bottom: 8px;
    }

    .form-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 15px;
    }

    input, select {
      width: 100%;
      padding: 10px;
      border: 1px solid #aaa;
      border-radius: 5px;
      margin-top: 5px;
    }

    label {
      font-weight: bold;
    }

    button {
      margin-top: 20px;
      padding: 12px 20px;
      background: #263238;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
    }

    button:hover {
      background: #455a64;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      background: white;
      margin-top: 15px;
    }

    th, td {
      border: 1px solid #bbb;
      padding: 10px;
      text-align: center;
    }

    th {
      background: #263238;
      color: white;
    }

    .available {
      color: green;
      font-weight: bold;
    }

    .issued {
      color: red;
      font-weight: bold;
    }

    .return-btn {
      background: #d32f2f;
      padding: 8px 12px;
      margin: 0;
    }

    .return-btn:hover {
      background: #b71c1c;
    }

    .book-image {
      width: 60px;
      height: 70px;
      object-fit: cover;
      border-radius: 5px;
    }

    footer {
      text-align: center;
      background: #263238;
      color: white;
      padding: 15px;
      margin-top: 30px;
    }

    @media(max-width: 700px) {
      .form-grid {
        grid-template-columns: 1fr;
      }

      table {
        font-size: 12px;
      }
    }
  </style>
</head>

<body>

  <header>
    <h1>📚 Library Management System</h1>
    <p>Manage Students, Books, Issue and Return Details</p>
  </header>

  <img class="banner"
       src="https://images.unsplash.com/photo-1507842217343-583bb7270b66?auto=format&fit=crop&w=1200&q=80"
       alt="Library Image">

  <div class="container">

    <div class="form-box">
      <h2>Student and Book Issue Details</h2>

      <div class="form-grid">
        <div>
          <label>Student Name</label>
          <input type="text" id="studentName" placeholder="Enter student name">
        </div>

        <div>
          <label>Student ID</label>
          <input type="text" id="studentId" placeholder="Enter student ID">
        </div>

        <div>
          <label>Book Name</label>
          <input type="text" id="bookName" placeholder="Enter book name">
        </div>

        <div>
          <label>Book ID</label>
          <input type="text" id="bookId" placeholder="Enter book ID">
        </div>

        <div>
          <label>Availability</label>
          <select id="availability">
            <option value="Available">Available</option>
            <option value="Issued">Issued</option>
          </select>
        </div>

        <div>
          <label>Issue Date</label>
          <input type="date" id="issueDate">
        </div>

        <div>
          <label>Due Date</label>
          <input type="date" id="dueDate">
        </div>
      </div>

      <button onclick="addBook()">Issue Book</button>
    </div>

    <div class="form-box">
      <h2>Books List</h2>

      <table id="bookTable">
        <thead>
          <tr>
            <th>Book Image</th>
            <th>Student Name</th>
            <th>Student ID</th>
            <th>Book Name</th>
            <th>Book ID</th>
            <th>Availability</th>
            <th>Issue Date</th>
            <th>Due Date</th>
            <th>Return</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>
              <img class="book-image"
                   src="https://images.unsplash.com/photo-1544947950-fa07a98d237f?auto=format&fit=crop&w=200&q=80"
                   alt="Book">
            </td>
            <td>Tejaswini</td>
            <td>STU101</td>
            <td>Python Programming</td>
            <td>BK101</td>
            <td class="issued">Issued</td>
            <td>2026-06-20</td>
            <td>2026-07-05</td>
            <td><button class="return-btn" onclick="returnBook(this)">Return</button></td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>

  <footer>
    <p>© 2026 Library Management System</p>
  </footer>

  <script>
    function addBook() {
      let studentName = document.getElementById("studentName").value;
      let studentId = document.getElementById("studentId").value;
      let bookName = document.getElementById("bookName").value;
      let bookId = document.getElementById("bookId").value;
      let availability = document.getElementById("availability").value;
      let issueDate = document.getElementById("issueDate").value;
      let dueDate = document.getElementById("dueDate").value;

      if (studentName === "" || studentId === "" || bookName === "" || bookId === "") {
        alert("Please fill all student and book details.");
        return;
      }

      let table = document.getElementById("bookTable").getElementsByTagName("tbody")[0];
      let row = table.insertRow();

      let statusClass = availability === "Available" ? "available" : "issued";

      row.innerHTML = `
        <td>
          <img class="book-image"
               src="https://images.unsplash.com/photo-1544947950-fa07a98d237f?auto=format&fit=crop&w=200&q=80"
               alt="Book">
        </td>
        <td>${studentName}</td>
        <td>${studentId}</td>
        <td>${bookName}</td>
        <td>${bookId}</td>
        <td class="${statusClass}">${availability}</td>
        <td>${issueDate}</td>
        <td>${dueDate}</td>
        <td><button class="return-btn" onclick="returnBook(this)">Return</button></td>
      `;

      document.getElementById("studentName").value = "";
      document.getElementById("studentId").value = "";
      document.getElementById("bookName").value = "";
      document.getElementById("bookId").value = "";
      document.getElementById("issueDate").value = "";
      document.getElementById("dueDate").value = "";

      alert("Book details added successfully!");
    }

    function returnBook(button) {
      let row = button.parentElement.parentElement;
      let availabilityCell = row.cells[5];

      availabilityCell.innerHTML = "Available";
      availabilityCell.className = "available";

      button.innerHTML = "Returned";
      button.disabled = true;
      button.style.background = "green";

      alert("Book returned successfully!");
    }
  </script>

</body>
</html>
