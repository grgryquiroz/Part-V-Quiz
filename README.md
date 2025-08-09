<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Part V - Vehicles: Requirements & Maintenance</title>
    <style>
        :root {
            --primary-color: #0066cc;
            --secondary-color: #003366;
            --accent-color: #ff9900;
            --light-gray: #f5f5f5;
            --medium-gray: #ddd;
            --dark-gray: #666;
            --success-color: #28a745;
            --danger-color: #dc3545;
            --nav-bg: #0055aa;
            --nav-hover: #004499;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f8f9fa;
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            padding: 20px 0;
            background-color: var(--secondary-color);
            color: white;
            margin-bottom: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            font-size: 1.8rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
        }
        
        .card {
            background-color: white;
            border-radius: 8px;
            padding: 25px;
            margin-bottom: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        
        .intro-text {
            font-size: 1.1rem;
            margin-bottom: 25px;
            text-align: justify;
        }
        
        .btn {
            display: inline-block;
            padding: 12px 24px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
        }
        
        .btn:hover {
            background-color: var(--secondary-color);
            transform: translateY(-2px);
        }
        
        .btn-success {
            background-color: var(--success-color);
        }
        
        .btn-success:hover {
            background-color: #218838;
        }
        
        .btn-danger {
            background-color: var(--danger-color);
        }
        
        .btn-danger:hover {
            background-color: #c82333;
        }
        
        .btn-secondary {
            background-color: var(--medium-gray);
        }
        
        .btn-secondary:hover {
            background-color: #ccc;
        }
        
        .start-btn {
            display: block;
            margin: 0 auto;
            font-size: 1.2rem;
            padding: 15px 30px;
            font-weight: 600;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .start-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
        }
        
        .question-container {
            display: none;
        }
        
        .question-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid var(--medium-gray);
        }
        
        .progress-container {
            flex-grow: 1;
            margin: 0 20px;
        }
        
        .progress-bar {
            height: 10px;
            background-color: var(--light-gray);
            border-radius: 5px;
            overflow: hidden;
        }
        
        .progress {
            height: 100%;
            background-color: var(--primary-color);
            width: 0%;
            transition: width 0.3s ease;
        }
        
        .question-text {
            font-size: 1.2rem;
            margin-bottom: 20px;
            line-height: 1.5;
            font-weight: 500;
        }
        
        .options-container {
            margin-bottom: 30px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            padding: 15px;
            background-color: #f9f9f9;
        }
        
        .option {
            display: block;
            padding: 14px 18px;
            margin-bottom: 12px;
            background-color: white;
            border: 2px solid #e0e0e0;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.2s ease;
            font-size: 1.05rem;
        }
        
        .option:hover {
            background-color: #f0f7ff;
            border-color: var(--primary-color);
        }
        
        .option.selected {
            border-color: var(--primary-color);
            background-color: #e6f2ff;
            box-shadow: 0 2px 4px rgba(0, 102, 204, 0.2);
        }
        
        .option.correct {
            border-color: var(--success-color);
            background-color: #d4edda;
        }
        
        .option.incorrect {
            border-color: var(--danger-color);
            background-color: #f8d7da;
        }
        
        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
        
        /* Enhanced navigation buttons */
        .nav-btn {
            padding: 14px 28px;
            font-size: 1.1rem;
            font-weight: 600;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .prev-btn {
            background-color: #e74c3c;
            color: white;
        }
        
        .prev-btn:hover {
            background-color: #c0392b;
            transform: translateY(-2px);
            box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
        }
        
        .next-btn {
            background-color: #27ae60;
            color: white;
        }
        
        .next-btn:hover {
            background-color: #219653;
            transform: translateY(-2px);
            box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
        }
        
        .submit-btn {
            background-color: #8e44ad;
            color: white;
            padding: 14px 28px;
            font-size: 1.1rem;
            font-weight: 600;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .submit-btn:hover {
            background-color: #7d3c98;
            transform: translateY(-2px);
            box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
        }
        
        .results-container {
            display: none;
            text-align: center;
        }
        
        .score {
            font-size: 3rem;
            font-weight: bold;
            color: var(--primary-color);
            margin: 20px 0;
        }
        
        .percentage {
            font-size: 1.5rem;
            color: #555;
            margin: 10px 0 20px;
        }
        
        .performance {
            font-size: 1.3rem;
            margin-bottom: 25px;
            font-weight: 500;
        }
        
        .feedback {
            margin: 20px 0;
            padding: 15px;
            background-color: var(--light-gray);
            border-radius: 4px;
            text-align: left;
            border-left: 5px solid var(--primary-color);
        }
        
        .review-container {
            display: none;
            margin-top: 20px;
        }
        
        .review-item {
            margin-bottom: 30px;
            padding: 20px;
            background-color: #f9f9f9;
            border-radius: 8px;
            border: 1px solid #e0e0e0;
        }
        
        .review-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--primary-color);
        }
        
        .review-question {
            font-weight: bold;
            margin-bottom: 15px;
            font-size: 1.1rem;
            line-height: 1.4;
        }
        
        .answer-section {
            margin: 15px 0;
            padding: 10px;
            border-radius: 6px;
        }
        
        .user-answer {
            background-color: #e6f2ff;
            border-left: 5px solid var(--primary-color);
            font-weight: 500;
        }
        
        .user-answer.correct {
            background-color: #d4edda;
            border-color: var(--success-color);
            color: var(--success-color);
        }
        
        .user-answer.incorrect {
            background-color: #f8d7da;
            border-color: var(--danger-color);
            color: var(--danger-color);
        }
        
        .correct-answer {
            background-color: #d1ecf1;
            border-left: 5px solid var(--primary-color);
            font-weight: bold;
        }
        
        .explanation {
            background-color: #fff3cd;
            border-left: 5px solid #ffc107;
            font-style: italic;
            padding: 12px;
            margin-top: 15px;
            border-radius: 6px;
        }
        
        .action-buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 30px;
        }
        
        .restart-btn {
            background-color: #28a745;
            color: white;
            padding: 16px 32px;
            font-size: 1.2rem;
            font-weight: 600;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            min-width: 200px;
        }
        
        .restart-btn:hover {
            background-color: #218838;
            transform: translateY(-3px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.25);
        }
        
        .review-btn {
            background-color: var(--primary-color);
            color: white;
            padding: 16px 32px;
            font-size: 1.2rem;
            font-weight: 600;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            min-width: 200px;
        }
        
        .review-btn:hover {
            background-color: var(--secondary-color);
            transform: translateY(-3px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.25);
        }
        
        .hidden {
            display: none;
        }
        
        @media (max-width: 600px) {
            .container {
                padding: 15px;
            }
            
            .card {
                padding: 20px;
            }
            
            h1 {
                font-size: 1.7rem;
            }
            
            .subtitle {
                font-size: 1rem;
            }
            
            .btn {
                padding: 10px 20px;
                font-size: 0.9rem;
            }
            
            .nav-btn {
                padding: 12px 20px;
                font-size: 1rem;
            }
            
            .submit-btn {
                padding: 12px 20px;
                font-size: 1rem;
            }
            
            .question-text {
                font-size: 1.1rem;
            }
            
            .option {
                padding: 12px 15px;
                font-size: 0.95rem;
            }
            
            .score {
                font-size: 2.5rem;
            }
            
            .percentage {
                font-size: 1.2rem;
            }
            
            .restart-btn, .review-btn {
                padding: 14px 24px;
                font-size: 1.1rem;
                min-width: 160px;
            }
            
            .review-item {
                padding: 15px;
            }
            
            .explanation {
                padding: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Part V - Vehicles: Requirements & Maintenance</h1>
            <p class="subtitle">Test your knowledge of TLC vehicle requirements and maintenance regulations</p>
        </header>
        
        <div id="intro-screen" class="card">
            <h2>Welcome to the Vehicle Requirements & Maintenance Quiz</h2>
            <p class="intro-text">
                This practice test is designed to help you prepare for Part V of the TLC regulations exam, focusing on vehicle requirements and maintenance. 
                The quiz contains 30 multiple-choice questions covering various aspects of TLC vehicle regulations, 
                including inspections, technology systems, signage requirements, and proper operation procedures. Take your time to answer 
                each question carefully. After completing the quiz, you'll receive your score and be 
                able to review all questions with explanations.
            </p>
            <p class="intro-text">
                <strong>Instructions:</strong> Click the "Start Quiz" button below to begin. You'll be presented 
                with one question at a time. Select your answer and navigate using the Previous and Next 
                buttons. You can change your answers at any time before submitting the quiz.
            </p>
            <button id="start-btn" class="btn start-btn">Start Quiz</button>
        </div>
        
        <div id="quiz-container">
            <!-- Questions will be dynamically inserted here -->
        </div>
        
        <div id="results-container" class="results-container">
            <div class="card">
                <h2>Quiz Complete!</h2>
                <p>Your score:</p>
                <div id="score" class="score">0/0</div>
                <div id="percentage" class="percentage">0%</div>
                <p id="performance" class="performance"></p>
                
                <div id="feedback" class="feedback"></div>
                
                <div class="action-buttons">
                    <button id="review-btn" class="review-btn">Review Answers</button>
                    <button id="restart-btn" class="restart-btn">Restart Quiz</button>
                </div>
            </div>
        </div>
        
        <div id="review-container" class="review-container">
            <div class="card">
                <h2>Review Your Answers</h2>
                <p class="intro-text">Below is a detailed review of your answers, including the correct answers and explanations for each question.</p>
                <div id="review-content">
                    <!-- Review content will be inserted here -->
                </div>
                <div class="action-buttons">
                    <button id="return-results-btn" class="review-btn">Return to Results</button>
                    <button id="restart-review-btn" class="restart-btn">Restart Quiz</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Quiz questions data from the provided PDF
        const questions = [
            {
                question: "What must a driver inspect BEFORE starting their shift?",
                options: ["Only the taximeter and roof light", "Only the vehicle's cleanliness", "Brakes, wipers, seat belts, tire pressure, hazard lights, etc.", "Only the interior for odors"],
                correct: 2,
                explanation: "§80-22 explicitly lists brakes, wipers, seat belts, tire pressure, hazard lights, etc. as part of the pre-shift inspection to ensure the vehicle is in good condition."
            },
            {
                question: "What must a driver ensure about the vehicle's exterior markings?",
                options: ["They are covered for protection.", "They are clean, unobstructed, and easily visible.", "They match the driver's personal preferences.", "They are only visible at night."],
                correct: 1,
                explanation: "§80-22 mandates that exterior markings required by the commission must be kept clean and unobstructed for easy recognition."
            },
            {
                question: "What is prohibited inside the vehicle regarding technology systems?",
                options: ["Using any electronic device.", "Installing any equipment not approved by the driver.", "Installing unauthorized equipment that could tamper with Taxicab/SHL Tech Systems or Accessible Dispatch Equipment.", "Having more than one GPS device."],
                correct: 2,
                explanation: "§80-22 & §80-26 strictly prohibit unauthorized equipment that could interfere with these systems."
            },
            {
                question: "How many electronic devices with E-Hail Applications can a driver use simultaneously?",
                options: ["As many as they want.", "Two.", "One.", "Three."],
                correct: 2,
                explanation: "§80-22 clearly states: 'The driver must not use more than one electronic device with an E-Hail Application.'"
            },
            {
                question: "What signage is allowed in a taxicab or SHL?",
                options: ["Any signage the driver finds helpful.", "Only signage approved by the passenger.", "No unauthorized signage.", "Only advertisements."],
                correct: 2,
                explanation: "§80-22 prohibits unauthorized signage in taxicabs or SHLs."
            },
            {
                question: "What system MUST be equipped in Taxicabs and SHLs?",
                options: ["A CB radio.", "A rear-seat entertainment system.", "Taxicab Technology System or Street Hail Livery Technology System (or written trip record when permitted).", "A dashcam."],
                correct: 2,
                explanation: "§80-23 states this as a mandatory requirement for Taxicabs and SHLs."
            },
            {
                question: "Where must the driver's TLC license and rate card be displayed in a Yellow or Green taxi?",
                options: ["On the dashboard.", "On the passenger sun visor.", "In a frame behind the driver's seat (illuminated after sunset).", "In the glove compartment."],
                correct: 2,
                explanation: "§80-23 specifies the location and that the frame must be illuminated after sunset."
            },
            {
                question: "What navigation aid must be present in a Taxicab or SHL?",
                options: ["A smartphone with maps.", "A compass.", "An Atlas or GPS.", "Written directions to major landmarks."],
                correct: 2,
                explanation: "§80-23 mandates the presence of an Atlas or GPS in the vehicle."
            },
            {
                question: "Where should the certificate of registration and insurance card be kept in an FHV?",
                options: ["Only in the trunk.", "On the driver's person.", "On the right visor, right dashboard, or glove compartment.", "Under the driver's seat."],
                correct: 2,
                explanation: "§80-24 lists these specific locations for the certificate of registration and insurance card in FHVs."
            },
            {
                question: "How must a Livery driver display their TLC license?",
                options: ["It doesn't need to be displayed.", "In their wallet.", "In a protective holder attached to the back of the driver's seat.", "On the passenger sun visor."],
                correct: 2,
                explanation: "§80-24 specifies this display requirement for Livery drivers' TLC licenses."
            },
            {
                question: "What must be clearly displayed in a Livery vehicle?",
                options: ["The driver's personal information.", "The Passenger's Bill of Rights.", "Advertisements for the base.", "A map of NYC."],
                correct: 1,
                explanation: "§80-24 requires the Livery Passenger's bill of rights to be clearly displayed."
            },
            {
                question: "What must a driver check BEFORE starting their shift? regarding the Taxi/SHL",
                options: ["Only the fuel level.", "That both the Roof Light and Taximeter are working.", "Only the tire tread depth.", "The passenger seat comfort."],
                correct: 1,
                explanation: "§80-26 states the driver must check both BEFORE starting the shift."
            },
            {
                question: "What must a driver do if the roof light or taximeter malfunctions?",
                options: ["Continue working and report it later.", "Take the vehicle to the garage, base, or a licensed authorized repair shop.", "Attempt to fix it themselves.", "Only stop working if the taximeter is broken."],
                correct: 1,
                explanation: "§80-26 requires immediate repair at one of these authorized locations."
            },
            {
                question: "What must a driver do if they suspect the taximeter has been tampered with?",
                options: ["Ignore it if the readings seem correct.", "Report it to TLC by phone immediately and in writing within 24 hours.", "Report it only at the next inspection.", "Report it to the passenger."],
                correct: 1,
                explanation: "§80-26 outlines this specific reporting procedure upon suspicion of taximeter tampering."
            },
            {
                question: "When must the Roof Light be ON?",
                options: ["Only at night.", "Whenever the driver is on duty and the taximeter is not in use (available for hire).", "Only when driving to a pickup.", "Whenever the vehicle is moving."],
                correct: 1,
                explanation: "§80-26 defines when the roof light must be on (available for street hails)."
            },
            {
                question: "When must the Roof Light be OFF?",
                options: ["Only when parked.", "Whenever the taximeter is recording (carrying a passenger), the driver is off-duty, or on a pre-arranged trip.", "Only during heavy rain.", "Only when the driver is logged out."],
                correct: 1,
                explanation: "§80-26 defines when the roof light must be off (not available for street hails)."
            },
            {
                question: "What is the Taxicab Technology System/Street Hail Livery Technology System?",
                options: ["Just the taximeter.", "Just the GPS device.", "A cluster of equipment (Taximeter, GPS, PIM, DIM, Trip Data Collection, etc.) working together.", "Only the credit card payment system."],
                correct: 2,
                explanation: "The 'OVERVIEW' section describes it as a cluster of various interconnected equipment."
            },
            {
                question: "What is the primary purpose of the Taxicab/SHL Technology Systems?",
                options: ["Solely to calculate fares.", "To play music and videos for passengers.", "To allow data collection, monitoring by agencies, and electronically record fares according to TLC rules.", "To track the driver's personal mileage."],
                correct: 2,
                explanation: "The 'INTRODUCTION TO TAXICAB TECHNOLOGY SYSTEM' section describes these as the primary functions."
            },
            {
                question: "What does the Driver Information Monitor (DIM) allow the driver to do?",
                options: ["Watch movies.", "Log in/out, switch rates, check trip history, and receive TLC messages/updates.", "Control the passenger's screen.", "Browse the internet."],
                correct: 1,
                explanation: "The 'DRIVER INFORMATION MONITOR (DIM)' section lists these functions."
            },
            {
                question: "When can the TLC send messages to the driver via the DIM?",
                options: ["Only when the driver is logged in.", "Only when the vehicle is stopped.", "Anytime the vehicle is moving.", "Only during an emergency."],
                correct: 1,
                explanation: "The 'TEXT MESSAGING' section states messages are sent when the vehicle is stopped."
            },
            {
                question: "What is the Passenger Information Monitor (PIM) used for?",
                options: ["For the driver to see the route.", "To display news, sports, events, ads, a map with the taxi's location, and facilitate payment for passengers.", "To control the vehicle's temperature.", "To display the driver's license information."],
                correct: 1,
                explanation: "The 'PASSENGER INFORMATION MONITOR (PIM)' section describes these functions."
            },
            {
                question: "What controls does the PIM have for the passenger?",
                options: ["Volume control only.", "Mute and turn off buttons.", "Channel changing buttons.", "Speed control."],
                correct: 1,
                explanation: "The PIM section states: 'All monitors have buttons to both mute and turn off the PIM.'"
            },
            {
                question: "What must a taxicab or SHL driver provide to the passenger at the end of the trip upon request?",
                options: ["A business card.", "A receipt of fare payment (personally, via PIM, or electronically).", "Directions to their next destination.", "A survey form."],
                correct: 1,
                explanation: "The 'NOTE' at the end explicitly states this requirement upon passenger request."
            },
            {
                question: "What must a driver select on the Technology System when using the taxicab/SHL for personal use?",
                options: ["On Duty Available", "Off-Duty", "PERSONAL USE-OFF DUTY", "Pre-Arranged Trip"],
                correct: 2,
                explanation: "The 'USING TAXICAB TECHNOLOGY SYSTEM/LPEP' section specifies this selection for personal use."
            },
            {
                question: "What must a driver enter on the Technology System when moving to pick up a pre-arranged customer?",
                options: ["Available for Street Hail", "ON DUTY UNAVAILABLE", "Carrying Passenger", "End Shift?"],
                correct: 1,
                explanation: "The 'USING TAXICAB TECHNOLOGY SYSTEM/LPEP' section specifies entering this code when moving to a pre-arranged pickup."
            },
            {
                question: "How soon must a driver report an inoperable Taxicab/SHL Technology System to the service provider?",
                options: ["Within 1 week.", "Within 24 hours.", "Within 1 hour of knowing it.", "At the end of their shift."],
                correct: 2,
                explanation: "The 'USING' section mandates reporting an inoperable system to the provider within 1 hour of the driver knowing about it."
            },
            {
                question: "How long can a driver knowingly operate with a defective Technology System AFTER reporting it?",
                options: ["Up to 1 week.", "Up to 24 hours.", "Up to 48 hours.", "They cannot operate at all until it's fixed."],
                correct: 2,
                explanation: "The 'USING' section states the driver must not knowingly operate with a defective system for more than 48 hours after filing the report."
            },
            {
                question: "What must a driver do while operating with a defective Technology System?",
                options: ["Use a different approved provider's system.", "Maintain a written trip record.", "Only accept cash payments.", "Drive only during daylight hours."],
                correct: 1,
                explanation: "The 'USING' section requires maintaining a written trip record when operating with a defective system."
            },
            {
                question: "Which component allows TLC to send messages to drivers?",
                options: ["The Taximeter.", "The Roof Light.", "The Driver Information Monitor (DIM).", "The Passenger Information Monitor (PIM)."],
                correct: 2,
                explanation: "The 'TEXT MESSAGING' section states the DIM permits TLC to send messages."
            },
            {
                question: "Which component shows passengers a map of the current location and helps with payment?",
                options: ["The Driver Information Monitor (DIM).", "The Taximeter.", "The Passenger Information Monitor (PIM).", "The Roof Light control."],
                correct: 2,
                explanation: "The PIM section states it displays a map with the taxicab's current location and facilitates payment."
            }
        ];

        // DOM elements
        const introScreen = document.getElementById('intro-screen');
        const quizContainer = document.getElementById('quiz-container');
        const resultsContainer = document.getElementById('results-container');
        const reviewContainer = document.getElementById('review-container');
        const startBtn = document.getElementById('start-btn');
        const reviewBtn = document.getElementById('review-btn');
        const returnResultsBtn = document.getElementById('return-results-btn');
        const restartBtn = document.getElementById('restart-btn');
        const restartReviewBtn = document.getElementById('restart-review-btn');
        const percentageElement = document.getElementById('percentage');

        // Quiz state
        let currentQuestion = 0;
        let userAnswers = Array(questions.length).fill(null);
        let quizStarted = false;

        // Initialize the quiz
        function initQuiz() {
            // Create question elements
            questions.forEach((q, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question-container';
                questionDiv.id = `question-${index}`;
                
                let optionsHtml = '';
                q.options.forEach((option, optionIndex) => {
                    optionsHtml += `
                        <div class="option" data-question="${index}" data-option="${optionIndex}">
                            ${String.fromCharCode(65 + optionIndex)}. ${option}
                        </div>
                    `;
                });
                
                const submitButton = index === questions.length - 1 ? 
                    '<button id="submit-btn" class="submit-btn">Submit Quiz</button>' : '';
                
                questionDiv.innerHTML = `
                    <div class="question-header">
                        <button id="prev-btn-${index}" class="nav-btn prev-btn">← Previous</button>
                        <div class="progress-container">
                            <div class="progress-bar">
                                <div class="progress" id="progress-bar"></div>
                            </div>
                            <p>Question ${index + 1} of ${questions.length}</p>
                        </div>
                        <button id="next-btn-${index}" class="nav-btn next-btn">Next →</button>
                    </div>
                    <div class="question-content">
                        <p class="question-text">${q.question}</p>
                        <div class="options-container">
                            ${optionsHtml}
                        </div>
                        ${submitButton}
                    </div>
                `;
                
                quizContainer.appendChild(questionDiv);
            });

            // Add event listeners
            document.querySelectorAll('.option').forEach(option => {
                option.addEventListener('click', function() {
                    const questionIndex = parseInt(this.getAttribute('data-question'));
                    const optionIndex = parseInt(this.getAttribute('data-option'));
                    
                    // Remove selected class from all options for this question
                    document.querySelectorAll(`.option[data-question="${questionIndex}"]`).forEach(opt => {
                        opt.classList.remove('selected');
                    });
                    
                    // Add selected class to clicked option
                    this.classList.add('selected');
                    
                    // Store user answer
                    userAnswers[questionIndex] = optionIndex;
                });
            });

            // Add navigation event listeners
            for (let i = 0; i < questions.length; i++) {
                const nextBtn = document.getElementById(`next-btn-${i}`);
                const prevBtn = document.getElementById(`prev-btn-${i}`);
                
                if (nextBtn) {
                    nextBtn.addEventListener('click', () => {
                        if (currentQuestion < questions.length - 1) {
                            goToQuestion(currentQuestion + 1);
                        }
                    });
                }
                
                if (prevBtn) {
                    prevBtn.addEventListener('click', () => {
                        if (currentQuestion > 0) {
                            goToQuestion(currentQuestion - 1);
                        }
                    });
                }
            }

            // Add submit button event listener
            const submitBtn = document.getElementById('submit-btn');
            if (submitBtn) {
                submitBtn.addEventListener('click', showResults);
            }
        }

        // Start the quiz
        startBtn.addEventListener('click', () => {
            introScreen.style.display = 'none';
            quizContainer.style.display = 'block';
            quizStarted = true;
            goToQuestion(0);
        });

        // Go to a specific question
        function goToQuestion(questionIndex) {
            // Hide all questions
            document.querySelectorAll('.question-container').forEach(q => {
                q.style.display = 'none';
            });
            
            // Show current question
            document.getElementById(`question-${questionIndex}`).style.display = 'block';
            currentQuestion = questionIndex;
            
            // Update progress bar
            updateProgress();
            
            // Update selected option for current question
            updateSelectedOption();
        }

        // Update progress bar
        function updateProgress() {
            const progressPercent = (currentQuestion / (questions.length - 1)) * 100;
            document.getElementById('progress-bar').style.width = `${progressPercent}%`;
        }

        // Update selected option display
        function updateSelectedOption() {
            const selectedOption = userAnswers[currentQuestion];
            if (selectedOption !== null) {
                document.querySelectorAll(`.option[data-question="${currentQuestion}"]`).forEach((opt, index) => {
                    opt.classList.remove('selected');
                    if (index === selectedOption) {
                        opt.classList.add('selected');
                    }
                });
            }
        }

        // Show results
        function showResults() {
            // Calculate score
            let correctAnswers = 0;
            for (let i = 0; i < questions.length; i++) {
                if (userAnswers[i] === questions[i].correct) {
                    correctAnswers++;
                }
            }
            
            // Calculate percentage
            const percentage = Math.round((correctAnswers / questions.length) * 100);
            
            // Display results
            document.getElementById('score').textContent = `${correctAnswers}/${questions.length}`;
            document.getElementById('percentage').textContent = `${percentage}%`;
            
            // Determine performance level
            const percentageValue = (correctAnswers / questions.length) * 100;
            let performanceText, feedbackText;
            
            if (percentageValue >= 90) {
                performanceText = "Excellent!";
                feedbackText = "You have an outstanding understanding of vehicle requirements and maintenance regulations. You're well-prepared for the exam!";
            } else if (percentageValue >= 80) {
                performanceText = "Great Job!";
                feedbackText = "You have a strong grasp of vehicle requirements and maintenance regulations. With a bit more review, you'll be fully prepared.";
            } else if (percentageValue >= 70) {
                performanceText = "Good Work!";
                feedbackText = "You have a solid understanding of vehicle requirements and maintenance regulations, but there are areas that need improvement.";
            } else if (percentageValue >= 60) {
                performanceText = "Passing Score";
                feedbackText = "You've passed, but you should review the material more thoroughly before taking the actual exam.";
            } else {
                performanceText = "Needs Improvement";
                feedbackText = "You need to study vehicle requirements and maintenance regulations more before attempting the exam. Focus on the areas where you had difficulties.";
            }
            
            document.getElementById('performance').textContent = performanceText;
            document.getElementById('feedback').textContent = feedbackText;
            
            // Hide quiz and show results
            quizContainer.style.display = 'none';
            resultsContainer.style.display = 'block';
            
            // Generate review content
            generateReviewContent();
        }

        // Generate review content
        function generateReviewContent() {
            const reviewContent = document.getElementById('review-content');
            reviewContent.innerHTML = '';
            
            questions.forEach((q, index) => {
                const userAnswer = userAnswers[index];
                const isCorrect = userAnswer === q.correct;
                
                const reviewItem = document.createElement('div');
                reviewItem.className = 'review-item';
                
                // Create the answer text
                const userAnswerText = userAnswer !== null ? 
                    `${String.fromCharCode(65 + userAnswer)}. ${q.options[userAnswer]}` : 
                    'No answer selected';
                
                const correctAnswerText = `${String.fromCharCode(65 + q.correct)}. ${q.options[q.correct]}`;
                
                reviewItem.innerHTML = `
                    <div class="review-header">
                        <h3>Question ${index + 1}</h3>
                        <span class="performance ${isCorrect ? 'correct' : 'incorrect'}">
                            ${isCorrect ? '✓ Correct' : '✗ Incorrect'}
                        </span>
                    </div>
                    <p class="review-question">${q.question}</p>
                    <div class="answer-section user-answer ${isCorrect ? 'correct' : 'incorrect'}">
                        <strong>Your Answer:</strong> ${userAnswerText}
                    </div>
                    ${!isCorrect ? `<div class="answer-section correct-answer">
                        <strong>Correct Answer:</strong> ${correctAnswerText}
                    </div>` : ''}
                    <div class="explanation">
                        <strong>Explanation:</strong> ${q.explanation}
                    </div>
                `;
                
                reviewContent.appendChild(reviewItem);
            });
        }

        // Event listeners for navigation buttons
        reviewBtn.addEventListener('click', () => {
            resultsContainer.style.display = 'none';
            reviewContainer.style.display = 'block';
        });

        returnResultsBtn.addEventListener('click', () => {
            reviewContainer.style.display = 'none';
            resultsContainer.style.display = 'block';
        });

        restartBtn.addEventListener('click', restartQuiz);
        restartReviewBtn.addEventListener('click', restartQuiz);

        // Restart the quiz
        function restartQuiz() {
            // Reset state
            currentQuestion = 0;
            userAnswers = Array(questions.length).fill(null);
            quizStarted = false;
            
            // Reset display
            resultsContainer.style.display = 'none';
            reviewContainer.style.display = 'none';
            quizContainer.style.display = 'none';
            introScreen.style.display = 'block';
            
            // Reset all selected options
            document.querySelectorAll('.option').forEach(opt => {
                opt.classList.remove('selected');
            });
        }

        // Initialize the quiz when page loads
        initQuiz();

        // If the quiz was already started, continue from current question
        // Otherwise, show intro screen
        if (!quizStarted) {
            quizContainer.style.display = 'none';
            resultsContainer.style.display = 'none';
            reviewContainer.style.display = 'none';
        }
    </script>
</body>
</html>
