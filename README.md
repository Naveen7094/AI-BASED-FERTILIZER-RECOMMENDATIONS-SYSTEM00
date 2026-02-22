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
