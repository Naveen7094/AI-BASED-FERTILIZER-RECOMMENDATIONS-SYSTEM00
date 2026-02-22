# AI-BASED-FERTILIZER-RECOMMENDATIONS-SYSTEM
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Login - Fertilizer Recommendation</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background: linear-gradient(to right, #2e7d32, #66bb6a);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .login-box {
            background: white;
            padding: 30px;
            width: 350px;
            border-radius: 10px;
            box-shadow: 0px 5px 15px rgba(0,0,0,0.2);
        }

        .login-box h2 {
            text-align: center;
            margin-bottom: 20px;
            color: #2e7d32;
        }

        .input-box {
            margin-bottom: 15px;
        }

        .input-box input {
            width: 100%;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
            outline: none;
        }

        .input-box input:focus {
            border-color: #2e7d32;
        }

        .btn {
            width: 100%;
            padding: 10px;
            background: #2e7d32;
            border: none;
            color: white;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
        }

        .btn:hover {
            background: #1b5e20;
        }

        .footer-text {
            text-align: center;
            margin-top: 15px;
            font-size: 14px;
        }

        .footer-text a {
            color: #2e7d32;
            text-decoration: none;
        }
    </style>
</head>
<body>

<div class="login-box">
    <h2>🌱 Login</h2>

    <form action="/" method="POST">
        <div class="input-box">
            <input type="text" name="username" placeholder="Enter Username" required>
        </div>

        <div class="input-box">
            <input type="password" name="password" placeholder="Enter Password" required>
        </div>

        <button type="submit" class="btn">Login</button>
    </form>

    <div class="footer-text">
        <p>AI Fertilizer Recommendation System</p>
    </div>
</div>

</body>
</html>
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/', methods=['GET', 'POST'])
def index():
    result = ""
    if request.method == 'POST':
        n = request.form['nitrogen']
        p = request.form['phosphorus']
        k = request.form['potassium']
        ph = request.form['ph']
        crop = request.form['crop']

        # Temporary logic (replace with ML later)
        result = "Urea Fertilizer"

    return render_template('index.html', result=result)

if __name__ == "__main__":
    app.run(debug=True)
