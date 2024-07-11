# WebTask2

## Description
This task involves creating a web interface to display the last recorded direction of a robot leg's movement. The direction is retrieved from a MySQL database using PHP scripts. 

## Features
- __Web Interface:__ A user-friendly webpage to display the last recorded direction of the robot leg.
- __Database Integration:__ Retrieves the last recorded direction from a MySQL database.
- __PHP Backend:__ PHP scripts handle database interactions.
- __Local Hosting:__ Uses XAMPP to host the webpage and manage the database locally.

## Installation

### Prerequisites 
- XAMPP (includes Apache server and MySQL database)
- Visual Studio Code or any other code editor
- Web browser (e.g., Chrome, Firefox)

### Steps
1. __Download the file "last.php" from the repository.__
2. __Setup XAMPP__
- Start the XAMPP Control Panel and ensure both Apache and MySQL are running.

  <img width="498" alt="image" src="https://github.com/Alaa3172/WebTask1/assets/173661540/6ce74776-3b03-4911-877a-6f4a0b9a5aa9">

3. __Move File to Project Folder__
- Copy the downloaded file __"last.php"__ to the project folder __"Robot Control"__ downloaded previously in Task 1.

  <img width="959" alt="image" src="https://github.com/user-attachments/assets/d677d251-7123-4d72-bd60-a53775cfcff4">

4. __Create the Database__ (You can skip this step if  you created the database in Task 1.)
- Open your web browser and go to http://localhost/phpmyadmin.

  <img width="959" alt="image" src="https://github.com/Alaa3172/WebTask1/assets/173661540/0a88d89f-7b6f-469e-ad0a-0ca958e8084c">

- Create a new database named __'robot_control'__.

  <img width="944" alt="image" src="https://github.com/Alaa3172/WebTask1/assets/173661540/eb73e4b8-598e-4af8-b8b9-e0a27558a34b">

- Create a table named __'directions'__ with the following structure:
  - id (INT, 11)
  - direction (VARCHAR, 50)

  <img width="777" alt="image" src="https://github.com/Alaa3172/WebTask1/assets/173661540/d00058f4-9a60-493b-9c2a-5edf0c6fa9f5">

## Usage
1. __Start the Server__
- Open the XAMPP Control Panel and ensure Apache and MySQL are running.
2. __Access the Webpage__
- Open your web browser and navigate to http://localhost/RobotControl/last.php.
- You should see a webpage displaying the last recorded direction.
3. __View Last Recorded Direction__
- The last recorded direction is fetched from the __'directions'__ table in the __'robot_control'__ database and displayed on the webpage.

## File Structure
- __last.php__ - Contains HTML, CSS, and PHP code to display the last recorded direction.

## Screenshots

  <img width="957" alt="image" src="https://github.com/user-attachments/assets/1d59cf48-11a2-4ae9-8ba8-172367d07cd3">

Figure 1: Webpage displaying the last recorded direction.

  <img width="949" alt="image" src="https://github.com/user-attachments/assets/eb37b335-5ca7-4dfc-9018-23510e1821f2">

Figure 2: Database table structure and recorded actions.

## Code Explanation

### Index Code
```
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Meta tags for character set and responsive design -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Title of the webpage -->
    <title>Last Recorded Direction</title>
```
HTML document setting character encoding, viewport for responsive design, and displaying the title "Last Recorded Direction."
```
    <!-- Internal CSS for styling the page and the direction box -->
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .direction-box {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            width: 300px;
            height: 150px;
            background-color: #FFFFFF;
            border: 2px solid transparent;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            font-size: 24px;
            font-weight: bold;
            color: #333;
            text-align: center;
            padding: 20px;
            box-sizing: border-box;
        }
    </style>
</head>
<body>
```
Internal CSS defining styles for the webpage body and the direction information box, ensuring centered alignment, specific dimensions, and visual styling for clarity and readability.
```
    <!-- Container for displaying the last recorded direction -->
    <div class="direction-box">
        <div>Last Recorded Direction:</div>
        <div>
            <?php
            // Connect to MySQL
            $servername = "localhost";
            $username = "root"; 
            $password = "";
            $dbname = "robot_control"; // Database name

            // Create connection
            $conn = new mysqli($servername, $username, $password, $dbname);

            // Check connection
            if ($conn->connect_error) {
                die("Connection failed: " . $conn->connect_error);
            }

            // Fetch last recorded direction
            $sql = "SELECT direction FROM directions ORDER BY id DESC LIMIT 1";
            $result = $conn->query($sql);

            if ($result->num_rows > 0) {
                $row = $result->fetch_assoc();
                $direction = ucfirst($row["direction"]);
                echo htmlspecialchars($direction);
            } else {
                echo "No directions recorded yet.";
            }

            // Close connection
            $conn->close();
            ?>
        </div>
    </div>
</body>
</html>
```
Display container showing the last recorded direction fetched from a MySQL database using PHP for database connectivity and result handling.
