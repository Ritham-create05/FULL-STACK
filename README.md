<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Registration</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600&display=swap">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #4361ee;
            --secondary: #3f37c9;
            --success: #4cc9f0;
            --danger: #f72585;
            --light: #f8f9fa;
            --dark: #212529;
            --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            --transition: all 0.3s ease;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .registration-form {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            padding: 30px;
            width: 100%;
            max-width: 500px;
            animation: fadeIn 0.6s ease-out;
            position: relative;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        h1 {
            color: var(--dark);
            text-align: center;
            margin-bottom: 20px;
            font-weight: 600;
            font-size: 2rem;
            position: relative;
            display: inline-block;
            width: 100%;
        }

        h1::after {
            content: '';
            position: absolute;
            bottom: -8px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 4px;
            background: var(--primary);
            border-radius: 2px;
        }

        .form-group {
            margin-bottom: 20px;
            position: relative;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark);
        }

        input, select {
            width: 100%;
            padding: 15px 20px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 1rem;
            transition: var(--transition);
            background: var(--light);
            font-family: 'Poppins', sans-serif;
        }

        input:focus, select:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
        }

        input:invalid:not(:placeholder-shown) {
            border-color: var(--danger);
        }

        .error-message {
            color: var(--danger);
            font-size: 0.8rem;
            margin-top: 5px;
            display: none;
        }

        input:invalid:not(:placeholder-shown) + .error-message {
            display: block;
        }

        button {
            width: 100%;
            padding: 15px;
            border: none;
            border-radius: 10px;
            font-weight: 500;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            font-size: 1rem;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            margin-top: 10px;
        }

        button:hover {
            transform: translateY(-3px);
            box-shadow: var(--shadow);
        }

        button:active {
            transform: translateY(0);
        }

        .input-icon {
            position: absolute;
            right: 15px;
            top: 40px;
            color: var(--primary);
        }

        /* Success Popup */
        .success-popup {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.8);
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            text-align: center;
            z-index: 100;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
            max-width: 90%;
            width: 400px;
        }

        .success-popup.active {
            opacity: 1;
            visibility: visible;
            transform: translate(-50%, -50%) scale(1);
        }

        .success-icon {
            font-size: 4rem;
            color: #4cc9f0;
            margin-bottom: 20px;
            animation: bounce 0.6s;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
            40% {transform: translateY(-20px);}
            60% {transform: translateY(-10px);}
        }

        .success-popup h2 {
            color: var(--dark);
            margin-bottom: 10px;
        }

        .success-popup p {
            color: #666;
            margin-bottom: 20px;
        }

        .popup-btn {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 500;
            transition: var(--transition);
        }

        .popup-btn:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow);
        }

        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(5px);
            z-index: 99;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
        }

        .overlay.active {
            opacity: 1;
            visibility: visible;
        }

        /* Responsive design */
        @media (max-width: 480px) {
            .registration-form {
                padding: 20px;
            }
            
            .success-popup {
                width: 90%;
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="registration-form">
        <h1>Student Registration</h1>
        
        <form id="studentForm">
            <div class="form-group">
                <label for="name">Full Name</label>
                <input type="text" id="name" name="name" placeholder="your name here" required
                       pattern="[A-Za-z ]{3,}" title="At least 3 alphabetical characters">
                <i class="fas fa-user input-icon"></i>
                <div class="error-message">Please enter a valid name (minimum 3 letters)</div>
            </div>

            <div class="form-group">
                <label for="email">Email Address</label>
                <input type="email" id="email" name="email" placeholder="name@example.com" required>
                <i class="fas fa-envelope input-icon"></i>
                <div class="error-message">Please enter a valid email address</div>
            </div>

            <div class="form-group">
                <label for="age">Age</label>
                <input type="number" id="age" name="age" placeholder="18" min="16" max="30" required>
                <i class="fas fa-birthday-cake input-icon"></i>
                <div class="error-message">Age must be between 16 and 30</div>
            </div>
            <button type="submit">
                <i class="fas fa-user-plus"></i> Register Now
            </button>
        </form>
    </div>

    <!-- Success Popup -->
    <div class="overlay" id="overlay"></div>
    <div class="success-popup" id="successPopup">
        <div class="success-icon">
            <i class="fas fa-check-circle"></i>
        </div>
        <h2>Registration Successful!</h2>
        <p>Thank you for registering. Your have been registered successfully.</p>
        <button class="popup-btn" id="closePopup">Continue</button>
    </div>

    <script>
        const form = document.getElementById('studentForm');
        const successPopup = document.getElementById('successPopup');
        const overlay = document.getElementById('overlay');
        const closePopup = document.getElementById('closePopup');

        form.addEventListener('submit', function(e) {
            e.preventDefault();
            
            if (this.checkValidity()) {
                // Show success popup
                successPopup.classList.add('active');
                overlay.classList.add('active');
                
                // Reset form
                this.reset();
            } else {
                // HTML5 validation will show error messages automatically
                console.log('Form validation failed');
            }
        });

        // Close popup when clicking the button or overlay
        closePopup.addEventListener('click', closeSuccessPopup);
        overlay.addEventListener('click', closeSuccessPopup);

        function closeSuccessPopup() {
            successPopup.classList.remove('active');
            overlay.classList.remove('active');
        }
    </script>
</body>
</html>
