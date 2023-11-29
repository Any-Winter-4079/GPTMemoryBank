# GPTMemoryBank


![Group 290](https://github.com/Any-Winter-4079/GPTMemoryBank/assets/50542132/59f9db07-886f-4397-b10e-35e44d5553b8)


GPTMemoryBank is a (free and personal) project that aims to augment GPT models with a local memory bank stored in a vector database, allowing for persistent context and improved memory management. Inspired by [MemGPT](https://github.com/cpacker/MemGPT) (paper [here](https://arxiv.org/pdf/2310.08560.pdf))  but interacting with the Web Interface of GPT (Plus) (via GPT Actions) instead of the API, as the API can get costly quickly.

## Quick Start

### 1. Clone the Repository
```bash
git clone https://github.com/Any-Winter-4079/GPTMemoryBank.git
```

### 2. Navigate to the Project Directory
```bash
cd GPTMemoryBank
```


### 3. (Optional) Create and activate a Virtual Environment
```bash
python -m venv GPTMemoryBankEnv
source GPTMemoryBankEnv/bin/activate  # On Windows, use `GPTMemoryBankEnv\Scripts\activate`
```

### 4. Install Depedencies
```bash
pip install -r requirements.txt
```

### 5. Configure ngrok

![Group 294](https://github.com/Any-Winter-4079/GPTMemoryBank/assets/50542132/e306cdc5-4d47-450f-a310-94dfb827747a)



[ngrok](https://ngrok.com/) is used to make the local Flask app available on the internet (vs. having it on localhost which GPT-4 can't access).
The Flask app remains on your local machine to make use of LanceDB (vector database) without memory limits (other than your computer's disk, which is likely much larger than what a free-tier hosting or vector database service can offer). Feel free to host the Flask app on the Cloud or use a different tunneling service if you'd like. Here, ngrok is used to make the Flask app (with the GET, POST, PUT, DELETE endpoints for GPT-4 to call) available on a public domain. An intermediate proxy server (in Node.js) is used to set 'ngrok-skip-browser-warning': 'true' (as ngrok suggests) to bypass ngrock's user confirmation screen before reaching the endpoint, which would break GPT-4's access to the endpoint.

```bash
brew install ngrok/ngrok/ngrok # On macOS. Or download from https://ngrok.com/download
```
Sign up at ngrok.com to get an auth token
```bash
ngrok config add-authtoken {AUTH_TOKEN}  # Replace {AUTH_TOKEN} with your actual auth token
```
Create a custom API key in a .env file for security
```bash
echo "API_KEY=your_custom_api_key_here" > .env  # Replace with your actual API key
```
Get a free domain from ngrok's cloud-edge domains.

### 6. Save your schema in GPT-4 Actions
Go to Configure, Create new action, Paste schema
In Authentication:
* Select ```API Key```
* Choose ```API Key``` as Authentication Type
* Paste your API Key on ```<HIDDEN>```
* Select ```Basic``` as Auth Type


