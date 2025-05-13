# Text To Math Problem Solver & Data Search Assistant

This Streamlit application serves as an intelligent assistant capable of solving mathematical problems, answering logic-based reasoning questions, and searching for information using Wikipedia. It leverages the power of Google's Gemma 2 model via the Groq API and uses Langchain to orchestrate interactions and tools.

## 🧮 Features

*   **Mathematical Problem Solving:** Solves arithmetic and mathematical expressions.
*   **Logical Reasoning:** Provides detailed, step-by-step explanations for logic-based questions.
*   **Wikipedia Search:** Fetches information from Wikipedia on various topics.
*   **Interactive Chat Interface:** User-friendly chat interface built with Streamlit.
*   **Real-time Agent Thoughts:** Displays the agent's reasoning process (if `expand_new_thoughts` is enabled, though currently set to `False`).
*   **API Key Integration:** Securely uses your Groq API key.

## ⚙️ How it Works

The application is built using Python and Streamlit for the front end. The core logic relies on Langchain:

1.  **LLM Integration:** It uses the `Gemma2-9b-It` model hosted on Groq, accessed via the `ChatGroq` Langchain integration.
2.  **Tools:** The assistant is equipped with three specialized tools:
    *   **Calculator Tool:** Utilizes `LLMMathChain` to solve mathematical expressions. It takes a mathematical expression as input and returns the result.
    *   **Wikipedia Tool:** Employs `WikipediaAPIWrapper` to search Wikipedia for information.
    *   **Reasoning Tool:** A custom `LLMChain` with a prompt engineered to guide the LLM in solving logical reasoning questions and providing point-wise explanations.
3.  **Agent:** A `ZERO_SHOT_REACT_DESCRIPTION` agent from Langchain is initialized with these tools. This agent decides which tool to use based on the user's query and the descriptions of the available tools. It can reason about the steps needed to answer a question and use tools sequentially if required.
4.  **User Interface:** Streamlit provides the chat interface where users can input their Groq API key and ask questions. The conversation history is maintained within the session.
5.  **Callbacks:** `StreamlitCallbackHandler` is used to potentially display the agent's internal thought process directly in the Streamlit UI.

## 🛠️ Technologies Used

*   **Python 3.x**
*   **Streamlit:** For the web application interface.
*   **Langchain:** For building LLM applications, managing agents, and tool integrations.
    *   `langchain-groq`: For Groq API integration.
    *   `langchain_community`: For community-provided utilities like `WikipediaAPIWrapper`.
*   **Groq API:** Provides access to fast LLMs like Gemma 2.
*   **Wikipedia API:** For information retrieval.

## 🚀 Setup and Installation

1.  **Clone the repository (if applicable) or save the script:**
    If this script is part of a larger project, clone it. Otherwise, save the Python script (e.g., `app.py`).

2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3.  **Install dependencies:**
    Create a `requirements.txt` file with the following content:
    ```txt
    streamlit
    langchain
    langchain-groq
    langchain-community
    wikipedia
    ```
    Then install them:
    ```bash
    pip install -r requirements.txt
    ```

4.  **Get a Groq API Key:**
    *   Sign up at [GroqCloud](https://console.groq.com/keys) and obtain an API key.

## ▶️ Running the Application

1.  **Set your Groq API Key:**
    The application will prompt you to enter your Groq API Key in the sidebar.

2.  **Run the Streamlit app:**
    Open your terminal, navigate to the directory where you saved the script, and run:
    ```bash
    streamlit run your_script_name.py
    ```
    (Replace `your_script_name.py` with the actual name of your Python file).

3.  **Interact with the Chatbot:**
    Once the app is running, you can enter your questions in the text area and click "Generate Response".

## 📝 Usage

1.  Open the application in your browser.
2.  Enter your Groq API Key in the sidebar input field.
3.  Type your math problem, logical reasoning question, or information query into the main text area.
    *   **Example Math Question:** `What is (5 + 7) * 3 / 2?`
    *   **Example Reasoning Question:** `If all bloops are razzies and some razzies are lazzies, are all bloops lazzies? Explain.`
    *   **Example Wikipedia Query:** `Who was Marie Curie?`
    *   **Default Example:** `I have 5 bananas and 7 grapes. I eat 2 bananas and give away 3 grapes. Then I buy a dozen apples and 2 packs of blueberries. Each pack of blueberries contains 25 berries. How many total pieces of fruit do I have at the end?`
4.  Click the "Generate Response" button.
5.  The assistant's response, including explanations or calculations, will be displayed.

## 🔧 Configuration

*   **Groq API Key:** Must be provided via the sidebar in the application.
*   **LLM Model:** Currently hardcoded to `Gemma2-9b-It`. This can be changed in the script if needed:
