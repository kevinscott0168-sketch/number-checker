from flask import Flask, render_template, request, jsonify
import requests

app = Flask(__track__)

# Apni Numverify API Key
API_KEY = 'c9b33c8db46002f405198d7b3baf7b35'

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/track', methods=['POST'])
def track_number():
    number = request.form.get('phone_number')
    if not number:
        return jsonify({"error": "Number is required"}), 400

    # API Request
    url = f"http://apilayer.net/api/validate?access_key={API_KEY}&number={number}"
    response = requests.get(url)
    data = response.json()

    return jsonify(data)

if __name__ == '__main__':
    app.run(debug=True)
