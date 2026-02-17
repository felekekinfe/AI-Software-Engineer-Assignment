
# AI Software Engineer Assignment

This repository contains a simple HTTP client with OAuth2 token handling. 

## Local Setup
1. (Optional) Create a virtual environment:

   python -m venv venv
   source venv/bin/activate  # or venv\Scripts\activate on Windows

2. Install dependencies:

pip install -r requirements.txt


3. Run tests:

python -m pytest -v


## Docker Instructions

To run the tests in a clean, isolated environment:

1. **Build the image:**

docker build -t ai-assignment .

2. **Run the tests:**

docker run --rm ai-assignment


## Project Structure

* `app/`: Contains the core logic (`http_client.py` and `tokens.py`).
* `tests/`: Contains `pytest` suites.
* `Explanation.md`: Detailed breakdown of the bug and fix.

