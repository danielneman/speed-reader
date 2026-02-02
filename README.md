# speed-reader[index.html](https://github.com/user-attachments/files/25000632/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Speed Reader - RSVP</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: #000000;
            min-height: 100vh;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            background: #0a0a0a;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(255, 255, 255, 0.05);
            max-width: 900px;
            width: 100%;
            overflow: hidden;
            border: 1px solid #1a1a1a;
        }

        .header {
            background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 100%);
            border-bottom: 1px solid #fff;
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2em;
            margin-bottom: 10px;
            color: #fff;
            font-weight: 300;
            letter-spacing: 2px;
        }

        .header p {
            opacity: 0.6;
            font-size: 0.95em;
            font-weight: 300;
        }

        .content {
            padding: 30px;
        }

        .input-section {
            margin-bottom: 25px;
        }

        .input-section label {
            display: block;
            margin-bottom: 8px;
            font-weight: 400;
            color: #fff;
        }

        .input-section input[type="url"],
        .input-section textarea {
            width: 100%;
            padding: 12px 15px;
            background: #000;
            border: 1px solid #333;
            border-radius: 8px;
            font-size: 1em;
            font-family: inherit;
            transition: all 0.3s;
            color: #fff;
        }

        .input-section input[type="url"]:focus,
        .input-section textarea:focus {
            outline: none;
            border-color: #fff;
        }

        .input-section textarea {
            min-height: 120px;
            resize: vertical;
        }

        .controls {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 15px;
            margin-bottom: 20px;
        }

        .control-group {
            display: flex;
            flex-direction: column;
        }

        .control-group label {
            margin-bottom: 8px;
            font-weight: 400;
            color: #fff;
            font-size: 0.9em;
        }

        .control-group input[type="range"] {
            width: 100%;
        }

        .control-group .value-display {
            text-align: center;
            margin-top: 5px;
            color: #fff;
            font-weight: 300;
        }

        .buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        button {
            flex: 1;
            min-width: 120px;
            padding: 15px 25px;
            border: 1px solid #fff;
            border-radius: 8px;
            font-size: 1em;
            font-weight: 400;
            cursor: pointer;
            transition: all 0.3s;
            background: transparent;
            color: #fff;
        }

        .btn-primary {
            background: transparent;
            color: #fff;
            border: 1px solid #fff;
        }

        .btn-primary:hover {
            background: #fff;
            color: #000;
        }

        .btn-secondary {
            background: transparent;
            color: #fff;
            border: 1px solid #fff;
        }

        .btn-secondary:hover {
            background: #fff;
            color: #000;
        }

        .btn-danger {
            background: transparent;
            color: #fff;
            border: 1px solid #fff;
        }

        .btn-danger:hover {
            background: #fff;
            color: #000;
        }

        button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .reader-display {
            display: none;
            background: #000;
            color: #fff;
            min-height: 500px;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 40px;
            position: relative;
        }

        .reader-display.active {
            display: flex;
        }

        .word-display {
            font-size: 3em;
            font-weight: 700;
            min-height: 120px;
            display: flex;
            align-items: center;
            justify-content: center;
            letter-spacing: 2px;
            text-align: center;
            width: 100%;
        }

        .word-display .highlight {
            color: #f87171;
        }

        .progress-bar {
            width: 100%;
            height: 4px;
            background: #333;
            margin-top: 30px;
            border-radius: 2px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: #fff;
            transition: width 0.1s linear;
        }

        .reader-controls {
            margin-top: 30px;
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }

        .reader-info {
            margin-top: 20px;
            opacity: 0.7;
            font-size: 0.9em;
        }

        .url-fetch-info {
            margin-top: 10px;
            padding: 10px;
            background: #f0f7ff;
            border-radius: 8px;
            font-size: 0.85em;
            color: #1e40af;
        }

        .error-message {
            background: #fee;
            color: #c00;
            padding: 12px;
            border-radius: 8px;
            margin-top: 10px;
        }

        .info-box {
            background: #000;
            border-left: 2px solid #fff;
            padding: 15px;
            margin-top: 20px;
            border-radius: 0;
            font-size: 0.9em;
            color: #999;
        }

        .info-box h3 {
            margin-bottom: 8px;
            color: #fff;
            font-weight: 300;
        }

        .info-box ul {
            margin-left: 20px;
        }

        .info-box li {
            margin: 5px 0;
        }

        /* Custom slider styling */
        input[type="range"] {
            -webkit-appearance: none;
            appearance: none;
            width: 100%;
            height: 6px;
            background: #333;
            outline: none;
            border-radius: 3px;
        }

        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 18px;
            height: 18px;
            background: #fff;
            cursor: pointer;
            border-radius: 50%;
            border: 2px solid #000;
        }

        input[type="range"]::-moz-range-thumb {
            width: 18px;
            height: 18px;
            background: #fff;
            cursor: pointer;
            border-radius: 50%;
            border: 2px solid #000;
        }

        input[type="range"]::-webkit-slider-runnable-track {
            background: #333;
            border-radius: 3px;
            height: 6px;
        }

        input[type="range"]::-moz-range-track {
            background: #333;
            border-radius: 3px;
            height: 6px;
        }

        @media (max-width: 768px) {
            .controls {
                grid-template-columns: 1fr;
            }

            .word-display {
                font-size: 2em;
            }

            .header h1 {
                font-size: 1.5em;
            }

            .buttons {
                flex-direction: column;
            }

            button {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>SPEED READER</h1>
            <p>Read faster with RSVP technology - one word at a time</p>
        </div>

        <div class="content" id="inputSection">
            <div class="input-section">
                <label>🔗 Paste Article URL</label>
                <input type="url" id="urlInput" placeholder="https://example.com/article">
                <button class="btn-secondary" id="fetchBtn" style="margin-top: 10px; width: 100%;">📥 Fetch Article</button>
            </div>

            <div style="text-align: center; margin: 15px 0; color: #999; font-weight: 600;">OR</div>

            <div class="input-section">
                <label>📝 Paste Text Directly</label>
                <textarea id="textInput" placeholder="Paste any article, document, or text you want to read faster..."></textarea>
            </div>

            <div class="controls">
                <div class="control-group">
                    <label>📊 Reading Speed (WPM)</label>
                    <input type="range" id="wpmSlider" min="100" max="1000" value="300" step="50">
                    <div class="value-display" id="wpmDisplay">300 WPM</div>
                </div>

                <div class="control-group">
                    <label>🔤 Font Size</label>
                    <input type="range" id="fontSlider" min="2" max="6" value="3" step="0.5">
                    <div class="value-display" id="fontDisplay">3em</div>
                </div>

                <div class="control-group">
                    <label>⏸️ Sentence Pause Multiplier</label>
                    <input type="range" id="pauseSlider" min="1" max="5" value="3" step="0.5">
                    <div class="value-display" id="pauseDisplay">3x</div>
                </div>
            </div>

            <div id="errorMessage" class="error-message" style="display: none;"></div>

            <div class="buttons">
                <button class="btn-primary" id="startBtn">▶ Start Reading</button>
                <button class="btn-secondary" id="loadSampleBtn">📖 Load Sample Text</button>
            </div>

            <div class="info-box">
                <h3>💡 How to Use:</h3>
                <ul>
                    <li><strong>Paste URL:</strong> Enter an article URL and click "Fetch Article" to auto-extract the content</li>
                    <li><strong>Copy & Paste:</strong> Or copy text from any article or document and paste it directly</li>
                    <li><strong>Adjust Speed:</strong> Start at 300 WPM and increase as you get comfortable</li>
                    <li><strong>Keyboard Shortcuts:</strong> Space = Play/Pause, R = Restart, ← = Back One Sentence, Esc = Exit</li>
                    <li><strong>ORP Highlighting:</strong> The red letter shows where your eyes should focus</li>
                </ul>
            </div>
        </div>

        <div class="reader-display" id="readerDisplay">
            <div class="word-display" id="wordDisplay">Ready</div>
            <div class="progress-bar">
                <div class="progress-fill" id="progressFill"></div>
            </div>
            
            <div style="width: 100%; max-width: 600px; margin-top: 20px;">
                <div class="control-group">
                    <label style="color: white;">📊 Reading Speed (WPM)</label>
                    <input type="range" id="readerWpmSlider" min="100" max="1000" value="300" step="50">
                    <div class="value-display" id="readerWpmDisplay" style="color: white;">300 WPM</div>
                </div>
            </div>

            <div class="reader-controls">
                <button class="btn-primary" id="playPauseBtn">⏸ Pause</button>
                <button class="btn-secondary" id="restartBtn">↺ Restart</button>
                <button class="btn-danger" id="exitBtn">✕ Exit</button>
            </div>
            <div class="reader-info" id="readerInfo">Word 0 / 0</div>
        </div>
    </div>

    <script>
        // State
        let words = [];
        let currentIndex = 0;
        let isPlaying = false;
        let interval = null;
        let wpm = 300;
        let fontSize = 3;
        let sentencePauseMultiplier = 3;

        // Elements
        const urlInput = document.getElementById('urlInput');
        const fetchBtn = document.getElementById('fetchBtn');
        const textInput = document.getElementById('textInput');
        const wpmSlider = document.getElementById('wpmSlider');
        const fontSlider = document.getElementById('fontSlider');
        const pauseSlider = document.getElementById('pauseSlider');
        const readerWpmSlider = document.getElementById('readerWpmSlider');
        const wpmDisplay = document.getElementById('wpmDisplay');
        const fontDisplay = document.getElementById('fontDisplay');
        const pauseDisplay = document.getElementById('pauseDisplay');
        const readerWpmDisplay = document.getElementById('readerWpmDisplay');
        const startBtn = document.getElementById('startBtn');
        const loadSampleBtn = document.getElementById('loadSampleBtn');
        const inputSection = document.getElementById('inputSection');
        const readerDisplay = document.getElementById('readerDisplay');
        const wordDisplay = document.getElementById('wordDisplay');
        const progressFill = document.getElementById('progressFill');
        const playPauseBtn = document.getElementById('playPauseBtn');
        const restartBtn = document.getElementById('restartBtn');
        const exitBtn = document.getElementById('exitBtn');
        const readerInfo = document.getElementById('readerInfo');
        const errorMessage = document.getElementById('errorMessage');

        // Slider updates
        wpmSlider.addEventListener('input', (e) => {
            wpm = parseInt(e.target.value);
            wpmDisplay.textContent = `${wpm} WPM`;
            if (isPlaying) {
                stopReading();
                startReading();
            }
        });

        fontSlider.addEventListener('input', (e) => {
            fontSize = parseFloat(e.target.value);
            fontDisplay.textContent = `${fontSize}em`;
            wordDisplay.style.fontSize = `${fontSize}em`;
        });

        pauseSlider.addEventListener('input', (e) => {
            sentencePauseMultiplier = parseFloat(e.target.value);
            pauseDisplay.textContent = `${sentencePauseMultiplier}x`;
            if (isPlaying) {
                stopReading();
                startReading();
            }
        });

        // Sync reader WPM slider with main WPM slider
        readerWpmSlider.addEventListener('input', (e) => {
            wpm = parseInt(e.target.value);
            readerWpmDisplay.textContent = `${wpm} WPM`;
            wpmSlider.value = wpm;
            wpmDisplay.textContent = `${wpm} WPM`;
            
            // If currently playing, restart with new speed
            if (isPlaying) {
                stopReading();
                startReading();
            }
        });

        function showError(message) {
            if (message) {
                errorMessage.textContent = message;
                errorMessage.style.display = 'block';
            } else {
                errorMessage.style.display = 'none';
            }
        }

        // Fetch and extract article content from URL
        async function fetchArticle(url) {
            try {
                showError('');
                fetchBtn.disabled = true;
                fetchBtn.textContent = '⏳ Fetching article...';

                // Use a CORS proxy to fetch the article
                const proxyUrl = 'https://api.allorigins.win/raw?url=';
                const response = await fetch(proxyUrl + encodeURIComponent(url));
                
                if (!response.ok) {
                    throw new Error('Failed to fetch article');
                }

                const html = await response.text();
                
                // Create a temporary DOM to parse the HTML
                const parser = new DOMParser();
                const doc = parser.parseFromString(html, 'text/html');
                
                // Extract article content using simple heuristics
                let articleText = extractArticleContent(doc);
                
                if (!articleText || articleText.length < 100) {
                    throw new Error('Could not extract article content. Try copying the text directly.');
                }

                textInput.value = articleText;
                fetchBtn.textContent = '✓ Article loaded!';
                setTimeout(() => {
                    fetchBtn.textContent = '📥 Fetch Article';
                    fetchBtn.disabled = false;
                }, 2000);

                return articleText;
            } catch (error) {
                console.error('Error fetching article:', error);
                showError('Failed to fetch article. Please copy and paste the text directly.');
                fetchBtn.textContent = '📥 Fetch Article';
                fetchBtn.disabled = false;
                return null;
            }
        }

        // Extract main article content from parsed HTML
        function extractArticleContent(doc) {
            // Remove unwanted elements
            const unwantedSelectors = [
                'script', 'style', 'nav', 'header', 'footer', 
                'aside', 'iframe', 'noscript', '.ad', '.advertisement',
                '.social-share', '.related-articles', '.comments',
                '[role="navigation"]', '[role="complementary"]'
            ];
            
            unwantedSelectors.forEach(selector => {
                doc.querySelectorAll(selector).forEach(el => el.remove());
            });

            // Try to find the main article content
            let article = doc.querySelector('article') || 
                         doc.querySelector('[role="main"]') ||
                         doc.querySelector('main') ||
                         doc.querySelector('.post-content') ||
                         doc.querySelector('.article-content') ||
                         doc.querySelector('.entry-content') ||
                         doc.querySelector('.content');

            if (!article) {
                // Fallback: find the element with the most <p> tags
                const allDivs = doc.querySelectorAll('div');
                let maxParagraphs = 0;
                let bestDiv = null;

                allDivs.forEach(div => {
                    const pCount = div.querySelectorAll('p').length;
                    if (pCount > maxParagraphs) {
                        maxParagraphs = pCount;
                        bestDiv = div;
                    }
                });

                article = bestDiv || doc.body;
            }

            // Extract text from paragraphs
            const paragraphs = article.querySelectorAll('p');
            let text = Array.from(paragraphs)
                .map(p => p.textContent.trim())
                .filter(t => t.length > 20) // Filter out very short paragraphs
                .join('\n\n');

            return text;
        }

        // Fetch button click handler
        fetchBtn.addEventListener('click', async () => {
            const url = urlInput.value.trim();
            if (!url) {
                showError('Please enter a URL');
                return;
            }

            if (!url.startsWith('http://') && !url.startsWith('https://')) {
                showError('Please enter a valid URL starting with http:// or https://');
                return;
            }

            await fetchArticle(url);
        });

        // Process text into words
        function processText(text) {
            return text
                .trim()
                .split(/\s+/)
                .filter(word => word.length > 0);
        }

        // Highlight ORP (Optimal Recognition Point)
        // The ORP is typically around 30% into the word
        function highlightORP(word) {
            const orpIndex = Math.floor(word.length * 0.3);
            if (word.length <= 2) {
                return `<span class="highlight">${word}</span>`;
            }
            return word.substring(0, orpIndex) +
                   `<span class="highlight">${word[orpIndex]}</span>` +
                   word.substring(orpIndex + 1);
        }

        // Calculate pause duration based on punctuation
        function getPauseDuration(word, baseDelay) {
            if (word.match(/[.!?]$/)) {
                return baseDelay * sentencePauseMultiplier; // Use slider value for sentence endings
            }
            if (word.match(/[,;:]$/)) {
                return baseDelay * 1.5; // Medium pause for commas
            }
            return baseDelay;
        }

        // Display word
        function displayWord(index) {
            if (index >= words.length) {
                stopReading();
                wordDisplay.innerHTML = '✓ Finished!';
                return;
            }

            const word = words[index];
            wordDisplay.innerHTML = highlightORP(word);
            
            // Update progress
            const progress = ((index + 1) / words.length) * 100;
            progressFill.style.width = `${progress}%`;
            readerInfo.textContent = `Word ${index + 1} / ${words.length}`;
        }

        // Start reading
        function startReading() {
            if (words.length === 0) return;
            
            isPlaying = true;
            playPauseBtn.textContent = '⏸ Pause';
            
            function showNextWord() {
                if (!isPlaying || currentIndex >= words.length) {
                    stopReading();
                    return;
                }

                displayWord(currentIndex);
                const baseDelay = 60000 / wpm; // milliseconds per word
                const delay = getPauseDuration(words[currentIndex], baseDelay);
                currentIndex++;
                
                interval = setTimeout(showNextWord, delay);
            }

            showNextWord();
        }

        // Stop reading
        function stopReading() {
            isPlaying = false;
            playPauseBtn.textContent = '▶ Play';
            if (interval) {
                clearTimeout(interval);
                interval = null;
            }
        }

        // Toggle play/pause
        playPauseBtn.addEventListener('click', () => {
            if (isPlaying) {
                stopReading();
            } else {
                startReading();
            }
        });

        // Restart
        restartBtn.addEventListener('click', () => {
            stopReading();
            currentIndex = 0;
            displayWord(0);
        });

        // Exit reader
        exitBtn.addEventListener('click', () => {
            stopReading();
            readerDisplay.classList.remove('active');
            inputSection.style.display = 'block';
        });

        // Start button
        startBtn.addEventListener('click', () => {
            showError('');
            
            const text = textInput.value.trim();
            
            if (!text) {
                showError('Please paste some text to read');
                return;
            }

            words = processText(text);
            if (words.length === 0) {
                showError('No valid text found');
                return;
            }

            currentIndex = 0;
            inputSection.style.display = 'none';
            readerDisplay.classList.add('active');
            wordDisplay.style.fontSize = `${fontSize}em`;
            readerWpmSlider.value = wpm;
            readerWpmDisplay.textContent = `${wpm} WPM`;
            displayWord(0);
            startReading();
        });

        // Load sample text
        loadSampleBtn.addEventListener('click', () => {
            const sampleText = `Speed reading is a collection of techniques that aim to increase reading speed without greatly reducing comprehension or retention. The human brain can process information much faster than we typically read. RSVP, or Rapid Serial Visual Presentation, is one of the most effective speed reading methods. It works by displaying words one at a time in the same location, eliminating the need for eye movement. This technique can help you read significantly faster while maintaining good comprehension. Studies have shown that people can comfortably read at 300 to 500 words per minute using RSVP, with some achieving speeds of over 1000 words per minute with practice. The key is finding your optimal speed where you can still understand and retain the information you're reading. Start slow and gradually increase your speed as you become more comfortable with the technique. Remember, the goal is not just to read faster, but to read faster with understanding.`;
            
            textInput.value = sampleText;
            showError('');
        });

        // Find the start of the current sentence
        function findSentenceStart(fromIndex) {
            // First, check if we're within the first few words of a sentence
            // If so, we want to go to the previous sentence instead
            let foundCurrentSentenceStart = false;
            let wordsFromStart = 0;
            
            // Count how many words we are from the current sentence start
            for (let i = fromIndex - 1; i >= 0; i--) {
                const word = words[i];
                if (word.match(/[.!?]$/)) {
                    foundCurrentSentenceStart = true;
                    break;
                }
                wordsFromStart++;
            }
            
            // If we're within the first 3 words of a sentence, go to previous sentence
            if (wordsFromStart <= 3) {
                // Look for the previous sentence
                let sentenceEndCount = 0;
                for (let i = fromIndex - 1; i >= 0; i--) {
                    const word = words[i];
                    if (word.match(/[.!?]$/)) {
                        sentenceEndCount++;
                        if (sentenceEndCount === 2) {
                            return i + 1; // Return start of previous sentence
                        }
                    }
                }
            }
            
            // Otherwise, go to start of current sentence
            for (let i = fromIndex - 1; i >= 0; i--) {
                const word = words[i];
                if (word.match(/[.!?]$/)) {
                    return i + 1;
                }
            }
            
            return 0; // If no sentence ending found, go to start
        }

        // Go back one sentence
        function goBackOneSentence() {
            const wasPlaying = isPlaying;
            if (wasPlaying) {
                stopReading();
            }
            
            // Find the start of the current sentence
            const sentenceStart = findSentenceStart(currentIndex);
            currentIndex = sentenceStart;
            displayWord(currentIndex);
            
            if (wasPlaying) {
                startReading();
            }
        }

        // Keyboard shortcuts
        document.addEventListener('keydown', (e) => {
            if (readerDisplay.classList.contains('active')) {
                if (e.code === 'Space') {
                    e.preventDefault();
                    playPauseBtn.click();
                } else if (e.code === 'Escape') {
                    exitBtn.click();
                } else if (e.code === 'KeyR') {
                    restartBtn.click();
                } else if (e.code === 'ArrowLeft') {
                    e.preventDefault();
                    goBackOneSentence();
                }
            }
        });

        // Auto-focus text input on load
        window.addEventListener('load', () => {
            textInput.focus();
        });
    </script>
</body>
</html>
