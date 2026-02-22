fertilizer_website/
│
├── app.py
├── model.py
│
├── templates/
│   └── index.html
│
├── static/
│   └── style.css# AI-BASED-FERTILIZER-RECOMMENDATIONS-SYSTEM
from flask import Flask, render_template, request, redirect, url_for, session

app = Flask(__name__)
app.secret_key = "secretkey"   # Needed for login session

# ---------------- LOGIN PAGE ----------------
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        username = request.form['username']
        password = request.form['password']

        # Simple username & password
        if username == "admin" and password == "1234":
            session['user'] = username
            return redirect(url_for('index'))
        else:
            return render_template('login.html', error="Invalid Username or Password")

    return render_template('login.html')


# ---------------- LOGOUT ----------------
@app.route('/logout')
def logout():
    session.pop('user', None)
    return redirect(url_for('login'))


# ---------------- MAIN PAGE (Your Existing Code) ----------------
@app.route('/', methods=['GET', 'POST'])
def index():

    # Check login first
    if 'user' not in session:
        return redirect(url_for('login'))

    result = ""
    if request.method == 'POST':
        n = request.form['nitrogen']
        p = request.form['phosphorus']
        k = request.form['potassium']
        ph = request.form['ph']
        crop = request.form['crop']

        result = "Urea Fertilizer"

    return render_template('index.html', result=result)


if __name__ == "__main__":
    app.run(debug=True)
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
    <link rel="stylesheet" href="/static/style.css">
</head>
<body>

<div class="container">
    <h2>Login Page</h2>

    <form method="POST">
        <input type="text" name="username" placeholder="Username" required>
        <input type="password" name="password" placeholder="Password" required>
        <button type="submit">Login</button>
    </form>

    {% if error %}
        <p style="color:red;">{{ error }}</p>
    {% endif %}
</div>

</body>
</html>
fertilizer_website/
│
├── app.py
├── model.py
│
├── templates/
│   └── index.html
│
├── static/
│   └── style.css
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
<!DOCTYPE html>
<html>
<head>
    <title>Fertilizer Recommendation</title>
    <link rel="stylesheet" href="/static/style.css">
</head>
<body>

<div class="container">
    <h1>🌱 Fertilizer Recommendation System</h1>

    <form method="POST">
        <input type="number" name="nitrogen" placeholder="Nitrogen (N)" required>
        <input type="number" name="phosphorus" placeholder="Phosphorus (P)" required>
        <input type="number" name="potassium" placeholder="Potassium (K)" required>
        <input type="number" step="0.1" name="ph" placeholder="Soil pH" required>

        <select name="crop" required>
            <option value="">Select Crop</option>
            <option>Rice</option>
            <option>Wheat</option>
            <option>Maize</option>
            <option>Pulses</option>
        </select>

        <button type="submit">Get Recommendation</button>
    </form>

    {% if result %}
    <div class="result">
        Recommended Fertilizer: <b>{{ result }}</b>
    </div>
    {% endif %}
</div>

</body>
</html>
body {
    background: #e8f5e9;
    font-family: Arial, sans-serif;
}

.container {
    width: 400px;
    margin: auto;
    background: white;
    padding: 20px;
    margin-top: 50px;
    border-radius: 10px;
}

h1 {
    text-align: center;
    color: green;
}

input, select, button {
    width: 100%;
    padding: 10px;
    margin: 8px 0;
}

button {
    background: green;
    color: white;
    border: none;
}

.result {
    background: #c8e6c9;
    padding: 10px;
    margin-top: 15px;
    text-align: center;
}
