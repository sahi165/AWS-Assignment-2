from flask import Flask, render_template, request, redirect, url_for, session

app = Flask(__name__)
app.secret_key = 'your_secret_key'  


users_database = {}


@app.route('/')
def registration_page():
    return render_template('registration.html')


@app.route('/submit', methods=['POST'])
def submit_registration():
    username = request.form['username']
    password = request.form['password']
    first_name = request.form['firstName']
    last_name = request.form['lastName']
    email = request.form['email']

    users_database[username] = {
        'password': password,
        'first_name': first_name,
        'last_name': last_name,
        'email': email
    }

    return redirect(url_for('login_page'))


@app.route('/login')
def login_page():
    return render_template('login.html')


@app.route('/login_submit', methods=['POST'])
def login_submit():
    entered_username = request.form['username']
    entered_password = request.form['password']


    if entered_username in users_database and users_database[entered_username]['password'] == entered_password:
        session['username'] = entered_username
        return redirect(url_for('display_info'))
    else:
        return "Invalid credentials"


@app.route('/display_info')
def display_info():
    if 'username' in session:
        username = session['username']
        user_info = users_database.get(username, {})
        return render_template('display_info.html', user_info=user_info)
    else:
        return redirect(url_for('login_page'))


if __name__ == '__main__':
    app.run(debug=True)
