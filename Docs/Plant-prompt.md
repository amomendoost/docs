Act as an expert Python developer specializing in creating robust, user-friendly, and asynchronous Telegram bots integrated with AI services.

Your task is to generate a complete, production-ready Python script for a Telegram bot called "Plant Pal" ("گیاه بان"). This bot's purpose is to analyze a plant photo submitted by a user, send it to a multimodal Vision LLM API for analysis, and return a user-friendly, comprehensive analysis in Persian.

**Core Requirements & Technical Specifications:**

1.  **Technology Stack:**
    * **Language:** Python 3.10+
    * **Telegram Bot Framework:** `python-telegram-bot` (version 20.0 or higher, using the modern `asyncio` and `async/await` syntax).
    * **HTTP Requests:** The `requests` library for communicating with the Vision LLM API.

2.  **Configuration:**
    * The script must not contain any hardcoded API keys.
    * It must read the `TELEGRAM_BOT_TOKEN` and a `VISION_API_KEY` from environment variables. Use `os.getenv()` for this.

3.  **Bot Behavior and User Flow:**
    * **/start Command:** When a user first starts the bot, it should reply with a welcoming message in Persian. The message should be friendly and clearly explain the bot's function.
        * **Welcome Message Text (in Persian):**
            ```
            🌿 به «گیاه‌بان» خوش آمدید! 🌿

            من اینجا هستم تا به شما در مراقبت از گیاهان‌تان کمک کنم.

            یک عکس واضح از گیاه خود برای من ارسال کنید تا آن را بررسی کنم و اطلاعات زیر را در اختیارتان قرار دهم:
            - شناسایی نوع گیاه
            - بررسی وضعیت سلامت و تشخیص احتمالی بیماری یا آفت
            - راهنمای کامل مراقبت (آبیاری، نور، خاک)

            منتظر عکس گیاه شما هستم!
            ```

    * **Photo Submission:**
        * The bot should be configured to listen for any message containing a photo.
        * Upon receiving a photo, it must immediately send a "processing" message to the user to manage expectations.
        * **Processing Message Text (in Persian):** `🔍 در حال بررسی تصویر گیاه شما... لطفاً چند لحظه صبر کنید.`

    * **Image Analysis Logic:**
        * The bot needs to download the highest-resolution version of the photo sent by the user.
        * It will then send this image to a placeholder Vision LLM API endpoint: `https://api.visionllm.placeholder/v1/chat/completions`. (You should assume this endpoint accepts a `multipart/form-data` request similar to OpenAI's GPT-4o API).
        * **Crucially, the prompt sent to the Vision LLM API must be structured to elicit a detailed and helpful response.** The internal prompt should be:
            ```
            You are an expert botanist and plant pathologist. Analyze the provided image of a plant and respond in simple, clear, and encouraging Persian. Structure your response with Markdown for readability using bolding and bullet points. Your analysis must include the following sections:

            1.  **تشخیص نوع گیاه:** (Plant Identification) Identify the species of the plant. If you are uncertain, state your best guess and mention the uncertainty.
            2.  **وضعیت سلامت کلی:** (Overall Health Status) Give a general assessment of the plant's health (e.g., healthy, stressed, diseased).
            3.  **بیماری‌ها و آفات احتمالی:** (Potential Diseases and Pests) Based on visual evidence, identify any signs of diseases (like fungal spots, root rot) or pests. If none are visible, state that the plant appears free of common issues.
            4.  **راهنمای مراقبت:** (Care Guide) Provide actionable advice tailored to this specific plant, including:
                * **آبیاری:** (Watering) How often and how much?
                * **نور:** (Light) What kind of sunlight does it need (direct, indirect, low)?
                * **خاک و کود:** (Soil and Fertilizer) What is the ideal soil type and when to fertilize?
            ```

    * **Displaying the Result:** The Persian analysis received from the Vision LLM API should be sent back to the user in a single, well-formatted Telegram message.

4.  **Error Handling:**
    * **Non-Photo Messages:** If the user sends a text message or any other file type that is not a photo, the bot should reply with a helpful error message in Persian.
        * **Error Message Text (in Persian):** `متاسفم، من فقط می‌توانم تصاویر را تحلیل کنم. لطفاً یک عکس از گیاه خود ارسال کنید.`
    * **API or Processing Failures:** If there's an error during the API call or image processing, the bot should send a generic failure message to the user.
        * **Failure Message Text (in Persian):** `خطایی در پردازش تصویر رخ داد. لطفاً کمی بعد دوباره امتحان کنید یا یک عکس دیگر ارسال نمایید.`

**Final Output Structure:**

Please provide the following as your final output:

1.  **The complete Python script named `plant_bot.py`**, fully commented to explain the logic, especially the API interaction part.
2.  **The contents for a `requirements.txt` file**, listing all necessary libraries.
3.  **A Detailed, Beginner-Friendly Setup and Execution Guide.** This guide should be written in clear, simple language, assuming the user may be new to Python. It must include the following sections:
    * **Step 1: Prerequisites:** State that Python 3.10+ must be installed.
    * **Step 2: Project Setup:** Explain how to create a project folder and place the `plant_bot.py` and `requirements.txt` files inside it.
    * **Step 3: Virtual Environment (Best Practice):** Explain why this is recommended. Provide the exact commands to create and activate the virtual environment for both **Windows (`.\venv\Scripts\activate`)** and **macOS/Linux (`source venv/bin/activate`)**.
    * **Step 4: Install Dependencies:** Provide the command `pip install -r requirements.txt`.
    * **Step 5: Set API Keys:** This is the most important step.
        * Explain how to get the `TELEGRAM_BOT_TOKEN` from BotFather and the `VISION_API_KEY` from a vision model provider.
        * Provide the **exact commands** to set these as environment variables for the current terminal session, with clear placeholders. Include examples for:
            * Windows (Command Prompt): `set YOUR_VARIABLE="YOUR_KEY_HERE"`
            * Windows (PowerShell): `$env:YOUR_VARIABLE="YOUR_KEY_HERE"`
            * macOS & Linux: `export YOUR_VARIABLE="YOUR_KEY_HERE"`
        * Strongly emphasize that these keys must be kept private.
    * **Step 6: Run the Bot:** Provide the final `python plant_bot.py` command and explain that the terminal window must be left open for the bot to run.