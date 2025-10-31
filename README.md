<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Menopause Journal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tenor Sans:ital,wght@0,400..700;1,400..700&family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Calm Transformation (Dusty Rose, Red Wine, Soft Terracotta) -->
    <!-- Application Structure Plan: A tabbed interface provides a clear, non-linear user experience. The structure separates daily tasks, physical wellness, and deeper reflection.
        1. Dashboard: For daily check-ins, now with an added in-line explanation of thought patterns for better user understanding.
        2. Trackers: For visualizing data over time.
        3. Body & Mind: Dedicated section for physical wellness.
        4. Toolkit: Resource library for psychological exercises, now enhanced with a new section on Somatic Exercises.
        5. Reflections: A space for open-ended journaling.
        This updated structure provides a more holistic tool, integrating psychological and somatic (body-based) practices. -->
    <!-- Visualization & Content Choices: 
        - Thought Pattern Explanations (Content) -> Goal: Improve User Understanding -> Method: Added a new content card to the dashboard. -> Interaction: Static text for quick reference. -> Justification: Directly addresses user request and makes the daily check-in more intuitive. -> Library: HTML.
        - Somatic Exercises (Content) -> Goal: Provide Body-Based Healing Tools -> Method: New accordion in the Toolkit section with guided exercises. -> Interaction: User expands accordion to access step-by-step instructions. -> Justification: Fulfills user request for deeper, body-focused exercises to complement the existing psychological tools. -> Library: JS/HTML.
     -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body { font-family: 'Montserrat', serif; background-color: #FFFAF9; }
        h1, h2, h3, h4, h5, h6, button, .font-heading { font-family: 'Tenor sans', sans-serif; }
        .tab-active { border-color: #F2CCB6; color: #77212E; }
        .tab-inactive { border-color: transparent; }
        .accordion-content { max-height: 0; overflow: hidden; transition: max-height 0.3s ease-out; }
        .chart-container { position: relative; width: 100%; max-width: 600px; margin-left: auto; margin-right: auto; height: 300px; max-height: 400px; }
        @media (min-width: 768px) { .chart-container { height: 350px; } }
    </style>
</head>
<body class="text-stone-700">

    <div class="container mx-auto p-4 md:p-8 max-w-5xl">
        <header class="text-center mb-8">
            <h3 class="text-lg font-semibold text-stone-500 font-heading">Presented by Happy In Our Skin</h3>
            <h1 class="text-4xl md:text-5xl font-bold text-stone-800 mt-1">My Menopause Journal</h1>
            <p class="mt-2 text-lg text-stone-600">Become who you really are.</p>
        </header>

        <nav class="flex flex-wrap justify-center border-b border-stone-300 mb-8 space-x-2 md:space-x-4">
            <button data-tab="dashboard" class="py-2 px-4 font-heading border-b-2 tab-active">Dashboard</button>
            <button data-tab="trackers" class="py-2 px-4 font-heading border-b-2 tab-inactive">Trackers</button>
            <button data-tab="body-mind" class="py-2 px-4 font-heading border-b-2 tab-inactive">Body & Mind</button>
            <button data-tab="toolkit" class="py-2 px-4 font-heading border-b-2 tab-inactive">Toolkit</button>
            <button data-tab="reflections" class="py-2 px-4 font-heading border-b-2 tab-inactive">Reflections</button>
        </nav>

        <main>
            <section id="dashboard" class="tab-content">
                <div class="bg-white rounded-lg shadow p-6 mb-8 border-l-4 border-[#F2CCB6]">
                    <h2 class="text-2xl font-bold text-stone-800 mb-2">Daily Check-in</h2>
                    <p>Take a moment to connect with yourself. This space is for capturing a snapshot of your day—your feelings, your thoughts, and your moments of gratitude and joy.</p>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                    <div class="bg-white rounded-lg shadow p-6">
                        <h3 class="text-xl font-bold text-stone-800 mb-4">Today's Data</h3>
                        <div class="space-y-4">
                            <div>
                                <label for="mood-slider" class="block font-semibold mb-1">How is your overall mood today?</label>
                                <div class="flex items-center space-x-2 text-sm text-stone-500">
                                    <span>Heaviness</span>
                                    <input type="range" id="mood-slider" name="mood-slider" min="1" max="5" value="3" class="w-full">
                                    <span>Contentment</span>
                                </div>
                            </div>
                             <div>
                                <label for="thought-select" class="block font-semibold mb-1">Notice any thought patterns today?</label>
                                <select id="thought-select" class="w-full p-2 border rounded-md border-stone-300 bg-stone-50">
                                    <option value="none">No specific pattern noticed</option>
                                    <option value="catastropher">The Catastropher</option>
                                    <option value="perfectionist">The Perfectionist</option>
                                    <option value="comparer">The Comparer</option>
                                    <option value="minimizer">The Minimizer</option>
                                    <option value="fortune-teller">The Fortune Teller</option>
                                    <option value="all-or-nothing">All-or-Nothing</option>
                                    <option value="body-critic">The Body Critic</option>
                                </select>
                            </div>
                            <button id="log-entry-btn" class="w-full bg-[#F2CCB6] text-white font-bold py-2 px-4 rounded-lg hover:bg-[#FFFAF9] transition-colors">Log Data for Today</button>
                        </div>
                    </div>
                     <div class="bg-white rounded-lg shadow p-6">
                        <h3 class="text-xl font-bold text-stone-800 mb-4">Today's Reflections</h3>
                        <div class="space-y-3">
                            <div>
                               <label class="block font-semibold text-sm">Today I am grateful for...</label>
                               <input type="text" class="w-full mt-1 p-2 border rounded-md border-stone-300 bg-stone-50">
                            </div>
                            <div>
                               <label class="block font-semibold text-sm">One thing that brought me joy today was...</label>
                               <input type="text" class="w-full mt-1 p-2 border rounded-md border-stone-300 bg-stone-50">
                            </div>
                             <div>
                               <label class="block font-semibold text-sm">My body feels...</label>
                               <input type="text" class="w-full mt-1 p-2 border rounded-md border-stone-300 bg-stone-50">
                            </div>
                            <div>
                               <label class="block font-semibold text-sm">Today I choose to...</label>
                               <input type="text" class="w-full mt-1 p-2 border rounded-md border-stone-300 bg-stone-50">
                            </div>
                        </div>
                    </div>
                    <div class="bg-white rounded-lg shadow p-6">
                        <h3 class="text-xl font-bold text-stone-800 mb-4">Thought Patterns Explained</h3>
                        <ul class="text-sm space-y-1 text-stone-700">
                            <li><b>The Catastropher:</b> Assumes the worst-case scenario.</li>
                            <li><b>The Perfectionist:</b> Sets impossibly high standards.</li>
                            <li><b>The Comparer:</b> Measures self-worth against others.</li>
                            <li><b>The Minimizer:</b> Downplays one's own feelings or needs.</li>
                            <li><b>The Fortune Teller:</b> Predicts negative outcomes.</li>
                            <li><b>All-or-Nothing:</b> Sees things in black and white terms.</li>
                            <li><b>The Body Critic:</b> Focuses on perceived physical flaws.</li>
                        </ul>
                    </div>
                </div>
            </section>
            
            <section id="trackers" class="tab-content hidden">
                 <div class="bg-white rounded-lg shadow p-6 mb-8 border-l-4 border-[#77212E]">
                    <h2 class="text-2xl font-bold text-stone-800 mb-2">Your Journey Visualized</h2>
                    <p>This section transforms your daily data into visual charts. Use these to gently observe patterns in your moods and thoughts over time. Noticing these rhythms is the first step towards understanding and self-compassion.</p>
                </div>
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                    <div class="bg-white rounded-lg shadow p-6">
                        <h3 class="text-xl font-bold text-stone-800 mb-4">Monthly Mood Tracker</h3>
                        <div class="chart-container">
                            <canvas id="moodChart"></canvas>
                        </div>
                    </div>
                    <div class="bg-white rounded-lg shadow p-6">
                        <h3 class="text-xl font-bold text-stone-800 mb-4">Thought Pattern Frequency</h3>
                        <div class="chart-container">
                            <canvas id="thoughtChart"></canvas>
                        </div>
                    </div>
                </div>
            </section>

            <section id="body-mind" class="tab-content hidden">
                <div class="bg-white rounded-lg shadow p-6 mb-8 border-l-4 border-[#F2CCB6]">
                    <h2 class="text-2xl font-bold text-stone-800 mb-2">Nurturing Your Body</h2>
                    <p>Movement during menopause is more than "staying fit"—it's a powerful way to support your body, mind, and spirit. This section provides guidance and a space to plan your joyful movement.</p>
                </div>
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                    <div class="space-y-4">
                        <div class="accordion-item bg-white rounded-lg shadow">
                            <button class="accordion-header w-full text-left p-4 font-bold text-lg text-stone-800 flex justify-between items-center">
                                <span>✨ Why Movement Matters</span>
                                <span class="transform transition-transform duration-300">▼</span>
                            </button>
                            <div class="accordion-content">
                                <p class="p-4 border-t border-stone-200">Hormonal shifts can affect bone density, muscle mass, mood, and metabolism. Movement helps balance these changes, reducing symptoms and building resilience. It is also a proven way to calm the nervous system and lift emotional well-being.</p>
                            </div>
                        </div>
                         <div class="accordion-item bg-white rounded-lg shadow">
                            <button class="accordion-header w-full text-left p-4 font-bold text-lg text-stone-800 flex justify-between items-center">
                                <span>🌸 Benefits of Exercise</span>
                                <span class="transform transition-transform duration-300">▼</span>
                            </button>
                            <div class="accordion-content">
                                <ul class="p-4 border-t border-stone-200 list-disc list-inside space-y-1">
                                    <li>Maintains bone density & lowers osteoporosis risk.</li>
                                    <li>Preserves muscle strength for daily activities.</li>
                                    <li>Supports heart health.</li>
                                    <li>Helps manage weight and energy levels.</li>
                                    <li>Reduces anxiety, irritability, and mood swings.</li>
                                    <li>Improves sleep quality.</li>
                                    <li>Releases endorphins, your natural “feel good” hormones.</li>
                                </ul>
                            </div>
                        </div>
                        <div class="accordion-item bg-white rounded-lg shadow">
                            <button class="accordion-header w-full text-left p-4 font-bold text-lg text-stone-800 flex justify-between items-center">
                                <span>🧘 Best Types of Exercise</span>
                                <span class="transform transition-transform duration-300">▼</span>
                            </button>
                            <div class="accordion-content">
                                 <div class="p-4 border-t border-stone-200">
                                    <p class="mb-2"><strong>Strength training (2–3x/week):</strong> Protects bones, builds lean muscle.</p>
                                    <p class="mb-2"><strong>Walking or low-impact cardio (30 min most days):</strong> Supports heart health and energy.</p>
                                    <p class="mb-2"><strong>Yoga or Pilates (2–3x/week):</strong> Improves flexibility, balance, and calms the nervous system.</p>
                                    <p><strong>Joyful Movement:</strong> Dancing, swimming, or cycling are great joint-friendly options.</p>
                                </div>
                            </div>
                        </div>
                    </div>
                     <div class="bg-white rounded-lg shadow p-6">
                        <h3 class="text-xl font-bold text-stone-800 mb-4">Workout Planner</h3>
                        <div class="space-y-4">
                             <div>
                               <label class="block font-semibold">Date:</label>
                               <input type="date" class="w-full mt-1 p-2 border rounded-md border-stone-300 bg-stone-50">
                            </div>
                            <div>
                               <label class="block font-semibold">Focus Area / Type of Movement:</label>
                               <input type="text" placeholder="e.g., Strength, Cardio, Yoga" class="w-full mt-1 p-2 border rounded-md border-stone-300 bg-stone-50">
                            </div>
                            <div>
                               <label class="block font-semibold">Duration (minutes):</label>
                               <input type="number" placeholder="e.g., 30" class="w-full mt-1 p-2 border rounded-md border-stone-300 bg-stone-50">
                            </div>
                            <div>
                               <label class="block font-semibold">Notes & Reflections:</label>
                               <textarea placeholder="How did it feel? What did I enjoy?" class="w-full mt-1 p-2 border rounded-md border-stone-300 bg-stone-50" rows="3"></textarea>
                            </div>
                            <button class="w-full bg-[#E0A387] text-white font-bold py-2 px-4 rounded-lg hover:bg-[#D48F71] transition-colors">Log Workout</button>
                        </div>
                    </div>
                </div>
            </section>

            <section id="toolkit" class="tab-content hidden">
                <div class="bg-white rounded-lg shadow p-6 mb-8 border-l-4 border-[#E0A387]">
                    <h2 class="text-2xl font-bold text-stone-800 mb-2">Your Toolkit for Inner Healing</h2>
                    <p>Here you'll find guided exercises to help you understand yourself more deeply. Explore these topics at your own pace. Each tool is designed to help you release old patterns and find a gentler, truer relationship with who you are today.</p>
                </div>
                <div class="space-y-4">
                    <div class="accordion-item bg-white rounded-lg shadow">
                        <button class="accordion-header w-full text-left p-4 font-bold text-lg text-stone-800 flex justify-between items-center">
                            <span>💖 Connecting With Your Inner Child</span>
                            <span class="transform transition-transform duration-300">▼</span>
                        </button>
                        <div class="accordion-content">
                            <div class="p-4 border-t border-stone-200 space-y-6">
                                <div>
                                    <p class="mb-4">Your inner child is the part of you that carries feelings from your younger years—your joy, but also your hurts and unmet needs. When old wounds aren’t healed, this inner child can still feel scared or unworthy. These exercises help you offer her the care she always deserved.</p>
                                    <div class="space-y-4 p-4 bg-stone-50 rounded-lg">
                                        <div>
                                            <label class="font-semibold block">Imagine your younger self. What did she need to hear back then that she missed?</label>
                                            <textarea placeholder="e.g., 'You are safe,' 'It wasn't your fault,' 'You are so loved...'" class="w-full mt-1 p-2 border rounded-md border-stone-300" rows="3"></textarea>
                                        </div>
                                        <div>
                                            <label class="font-semibold block">Write a short letter of reassurance to her now.</label>
                                            <textarea placeholder="Dear Little Me..." class="w-full mt-1 p-2 border rounded-md border-stone-300" rows="5"></textarea>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="accordion-item bg-white rounded-lg shadow">
                        <button class="accordion-header w-full text-left p-4 font-bold text-lg text-stone-800 flex justify-between items-center">
                            <span>🌿 Exploring Your Inner Parts (IFS)</span>
                             <span class="transform transition-transform duration-300">▼</span>
                        </button>
                        <div class="accordion-content">
                            <div class="p-4 border-t border-stone-200 space-y-6">
                                <p class="mb-4">We all have different “parts” inside us—like inner characters—that developed to help us cope. There might be a critic that pushes you, or a worrier that tries to keep you safe. These parts are not "bad"; they formed to protect us. By listening to them, we can help them soften.</p>
                                 <div class="space-y-4 p-4 bg-stone-50 rounded-lg">
                                    <div>
                                        <label class="font-semibold block">Bring a difficult feeling or thought to mind. Which part of you feels this way? (e.g., The Worrier, The Critic, The Scared Child)</label>
                                        <input type="text" placeholder="e.g., My Inner Critic feels this..." class="w-full mt-1 p-2 border rounded-md border-stone-300">
                                    </div>
                                    <div>
                                        <label class="font-semibold block">Ask this part: What are you afraid would happen if you didn't do your job?</label>
                                        <textarea placeholder="e.g., It's afraid I'll be rejected, that I'll fail..." class="w-full mt-1 p-2 border rounded-md border-stone-300" rows="3"></textarea>
                                    </div>
                                    <div>
                                        <label class="font-semibold block">What does this part truly need from you to feel safe and calm?</label>
                                        <textarea placeholder="e.g., It needs reassurance, kindness, to know I'm listening..." class="w-full mt-1 p-2 border rounded-md border-stone-300" rows="3"></textarea>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="accordion-item bg-white rounded-lg shadow">
                        <button class="accordion-header w-full text-left p-4 font-bold text-lg text-stone-800 flex justify-between items-center">
                            <span>🧘‍♀️ Body-Based Somatic Exercises</span>
                             <span class="transform transition-transform duration-300">▼</span>
                        </button>
                        <div class="accordion-content">
                            <div class="p-4 border-t border-stone-200 space-y-6">
                                <p class="mb-4">Our bodies hold emotions and memories. Somatic exercises help us connect with our body's wisdom to release stored tension and find safety in the present moment. Try these gentle practices when you feel overwhelmed or disconnected.</p>
                                 <div class="space-y-4 p-4 bg-stone-50 rounded-lg">
                                    <h4 class="font-bold">1. The Safety Anchor</h4>
                                    <p class="text-sm">This helps ground you when you feel anxious.</p>
                                    <ul class="list-decimal list-inside text-sm space-y-1">
                                        <li>Sit or stand comfortably. Feel your feet on the floor.</li>
                                        <li>Place one hand on your heart and the other on your belly.</li>
                                        <li>Take three slow, deep breaths. Feel the gentle pressure of your hands.</li>
                                        <li>Silently repeat to yourself: "I am safe in this moment. I am right here."</li>
                                    </ul>
                                 </div>
                                  <div class="space-y-4 p-4 bg-stone-50 rounded-lg">
                                    <h4 class="font-bold">2. Self-Compassion Touch</h4>
                                    <p class="text-sm">Offer kindness to a part of you that feels hurt or unloved.</p>
                                    <ul class="list-decimal list-inside text-sm space-y-1">
                                        <li>Identify a place in your body where you feel discomfort or sadness.</li>
                                        <li>Gently place your hand over that area.</li>
                                        <li>Breathe softly into that space. Send it warmth from your hand.</li>
                                        <li>Whisper a kind phrase, such as: "I am here with you. It's okay to feel this way. I will not leave you."</li>
                                    </ul>
                                 </div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
            
            <section id="reflections" class="tab-content hidden">
                <div class="bg-white rounded-lg shadow p-6 mb-8 border-l-4 border-stone-400">
                    <h2 class="text-2xl font-bold text-stone-800 mb-2">Your Reflection Space</h2>
                    <p>Journaling gives your thoughts and feelings a voice. Use this space to write freely. There are no rules. Just a few minutes a day can bring more clarity and self-compassion. Use the prompts below to get started if you feel stuck.</p>
                </div>
                <div class="bg-white rounded-lg shadow p-6">
                    <h3 class="text-xl font-bold text-stone-800 mb-4">Journal Prompts</h3>
                    <ul class="list-disc list-inside mb-6 space-y-2 text-stone-600">
                        <li>In what ways am I different today compared to 10 years ago?</li>
                        <li>What do I want to let go of at this stage of my life?</li>
                        <li>When I feel anxious or irritable, what soothes me best?</li>
                        <li>What dreams or desires am I ready to explore in this new chapter?</li>
                    </ul>
                     <textarea id="journal-entry" class="w-full p-4 border rounded-md border-stone-300 bg-stone-50" rows="15" placeholder="Start writing..."></textarea>
                </div>
            </section>
        </main>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            const tabs = document.querySelectorAll('nav button');
            const tabContents = document.querySelectorAll('.tab-content');
            const accordions = document.querySelectorAll('.accordion-item');

            tabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    tabs.forEach(t => {
                        t.classList.remove('tab-active');
                        t.classList.add('tab-inactive');
                    });
                    tab.classList.remove('tab-inactive');
                    tab.classList.add('tab-active');

                    tabContents.forEach(content => {
                        content.classList.add('hidden');
                    });

                    document.getElementById(tab.dataset.tab).classList.remove('hidden');
                });
            });
            
            accordions.forEach(item => {
                const header = item.querySelector('.accordion-header');
                const content = item.querySelector('.accordion-content');
                const icon = header.querySelector('span:last-child');

                header.addEventListener('click', () => {
                    const isOpen = content.style.maxHeight;
                    
                    accordions.forEach(i => {
                         const i_content = i.querySelector('.accordion-content');
                         if(i_content !== content){
                            i_content.style.maxHeight = null;
                            const otherIcon = i.querySelector('.accordion-header span:last-child');
                            if (otherIcon) otherIcon.style.transform = 'rotate(0deg)';
                         }
                    });

                    if (!isOpen) {
                        content.style.maxHeight = content.scrollHeight + 'px';
                        if (icon) icon.style.transform = 'rotate(180deg)';
                    } else {
                        content.style.maxHeight = null;
                        if(icon) icon.style.transform = 'rotate(0deg)';
                    }
                });
            });

            const moodData = {
                labels: ['Day 1', 'Day 2', 'Day 3', 'Day 4', 'Day 5', 'Day 6', 'Day 7'],
                datasets: [{
                    label: 'Mood Rating (1=Heaviness, 5=Contentment)',
                    data: [3, 4, 2, 3, 5, 4, 3],
                    borderColor: '#E0A387',
                    backgroundColor: 'rgba(224, 163, 135, 0.2)',
                    fill: true,
                    tension: 0.4
                }]
            };

            const thoughtData = {
                labels: ['The Comparer', 'The Perfectionist', 'The Body Critic', 'All-or-Nothing'],
                datasets: [{
                    label: 'Thought Patterns',
                    data: [5, 4, 6, 2],
                    backgroundColor: ['#D8B6A4', '#B2B8A3', '#E0A387', '#BF6A56'],
                    hoverOffset: 4
                }]
            };

            const chartOptions = {
                maintainAspectRatio: false,
                responsive: true,
                plugins: {
                    legend: {
                        position: 'bottom',
                    },
                },
            };

            const moodCtx = document.getElementById('moodChart').getContext('2d');
            const moodChart = new Chart(moodCtx, {
                type: 'line',
                data: moodData,
                options: chartOptions
            });

            const thoughtCtx = document.getElementById('thoughtChart').getContext('2d');
            const thoughtChart = new Chart(thoughtCtx, {
                type: 'doughnut',
                data: thoughtData,
                options: chartOptions
            });
            
            const logEntryBtn = document.getElementById('log-entry-btn');
            logEntryBtn.addEventListener('click', () => {
                const moodValue = document.getElementById('mood-slider').value;
                const thoughtValue = document.getElementById('thought-select').value;
                
                const today = `Day ${moodData.labels.length + 1}`;
                moodData.labels.push(today);
                moodData.datasets[0].data.push(parseInt(moodValue));
                if(moodData.labels.length > 30) {
                    moodData.labels.shift();
                    moodData.datasets[0].data.shift();
                }
                moodChart.update();

                if (thoughtValue !== 'none') {
                    const thoughtLabel = document.querySelector(`#thought-select option[value=${thoughtValue}]`).textContent;
                    const thoughtIndex = thoughtData.labels.indexOf(thoughtLabel);
                    if (thoughtIndex > -1) {
                        thoughtData.datasets[0].data[thoughtIndex]++;
                    } else {
                        thoughtData.labels.push(thoughtLabel);
                        thoughtData.datasets[0].data.push(1);
                        const newColor = `#${(0x1000000+Math.random()*0xffffff).toString(16).substr(1,6)}`;
                        thoughtData.datasets[0].backgroundColor.push(newColor);
                    }
                    thoughtChart.update();
                }
                
                logEntryBtn.textContent = 'Data Logged!';
                logEntryBtn.classList.remove('bg-[#B2B8A3]', 'hover:bg-[#9FA68F]');
                logEntryBtn.classList.add('bg-green-500');
                setTimeout(() => {
                    logEntryBtn.textContent = "Log Data for Today";
                    logEntryBtn.classList.remove('bg-green-500');
                    logEntryBtn.classList.add('bg-[#B2B8A3]', 'hover:bg-[#9FA68F]');
                }, 2000);
            });
        });
    </script>
</body>
</html>

