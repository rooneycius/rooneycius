<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crypto Exchange - Secure Login</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h2>Crypto Exchange - Secure Login</h2>
        
        <p id="price">Today's BTC Price: Loading...</p>
        
        <label for="email">Email:</label>
        <input type="email" id="email" placeholder="Enter your email">
        
        <label for="phone">Phone Number:</label>
        <input type="tel" id="phone" placeholder="Enter your phone number">
        
        <button class="animated-button" onclick="sendVerificationCode()">Send Verification Code</button>
        
        <label for="otp">Enter OTP:</label>
        <input type="text" id="otp" placeholder="Enter OTP received">
        
        <button class="animated-button" onclick="verifyOTP()">Verify & Login</button>
        
        <h3 id="authResult"></h3>
    </div>

    <script>
        async function fetchCryptoPrice() {
            try {
                const response = await fetch('https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=usd');
                const data = await response.json();
                document.getElementById("price").textContent = `Today's BTC Price: $${data.bitcoin.usd}`;
            } catch (error) {
                document.getElementById("price").textContent = "Error fetching price.";
            }
        }

        async function sendVerificationCode() {
            const email = document.getElementById("email").value;
            const phone = document.getElementById("phone").value;
            const authResult = document.getElementById("authResult");

            if (!email || !phone) {
                authResult.textContent = "Please enter a valid email and phone number.";
                return;
            }

            try {
                authResult.textContent = "Verification code sent to your email and phone.";
            } catch (error) {
                authResult.textContent = "Error sending verification code. Try again.";
            }
        }

        async function verifyOTP() {
            const otp = document.getElementById("otp").value;
            const authResult = document.getElementById("authResult");

            if (!otp) {
                authResult.textContent = "Please enter the OTP.";
                return;
            }

            try {
                authResult.textContent = "Verification successful. You are logged in!";
            } catch (error) {
                authResult.textContent = "Invalid OTP. Please try again.";
            }
        }

        window.onload = fetchCryptoPrice;
    </script>

    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #000;
            color: orange;
        }
        .container {
            background: #222;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(255, 165, 0, 0.5);
            text-align: center;
            width: 300px;
        }
        input, select, button {
            margin: 10px;
            padding: 10px;
            width: calc(100% - 20px);
            border-radius: 5px;
            border: 1px solid orange;
            box-sizing: border-box;
        }
        button {
            background-color: orange;
            color: black;
            border: none;
            cursor: pointer;
            transition: transform 0.2s ease-in-out;
        }
        .animated-button:hover {
            transform: scale(1.05);
            background-color: #ff8c00;
        }
    </style>
</body>
</html>
